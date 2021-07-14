---
layout: post
title: "FASTA 압축기 만들기"
date:   2018-06-20 12:00:00 +0900
author: "Sihyung Park"
categories: [bioinformatics]
locale: ko_KR
---



DNA 시퀀스를 다루는 사람들에겐 FASTA/FASTQ라는 이름만큼 익숙한 포맷이 또 없을 것이다. 시퀀싱된 염기서열을 저장하는, 가히 표준이라 할 수 있을만큼 널리 사용되는 포맷이다. FASTA 포맷은 샘플 이름과 샘플 시퀀스로 이루어져있다. 예를 들어 “sample1”, “sample2″이라는 이름의 샘플이 각각 “ATGCATGC”, “TTTTTTTTT”라는 시퀀스로 시퀀싱되었다면 아래와 같은 FASTA 포맷의 파일로 표현할 수 있다.

```
>sample1
ATGCATGC
>sample2
TTTTTTTTT
```

FASTA 포맷의 가장 큰 장점은 굳이 포맷이라고 이름붙이는 것이 어색해 보일 정도의 간결성과 직관성에 있다. Parsing 작업이 굳이 필요하지 않으며, 필요하더라도 아주 쉽게 코딩할 수 있다 (물론 Biopython등 상용화된 패키지를 이용하는 것이 제일 편하다).

굳이 단점을 꼽자면 용량 측면에서의 비효율성이 있을 것이다. 각 베이스를 베이스 그대로 표기하여 직관성을 얻은 대신 하나의 베이스마다 8비트(1바이트)의 메모리를 할당해야하는 것이다.

비록 그렇게 큰 용량은 아니지만, 빠르고 원활한 시퀀스 파일 공유를 위해 FASTA 압축 알고리즘을 짜보면 어떨까 싶어 재미삼아 몇 가지 코딩을 해봤다.

이 글은 “새로운”(?) FASTA용 무손실 압축 알고리즘을 짜보고 싶다는 생각으로 시작했지만 결국 상용화된 프로그램이 짱이라는 결론에 이르는, 컴퓨터 비전공자의 분투를 담은 글이다.

- TOC
{:toc}
<br> 

## 1. Look-and-Say 수열을 이용한 압축 알고리즘 ("`.said`" format)

Look-and-say 수열은 현재 항 숫자의 종류와 갯수를 읽고, 읽은 내용으로 다음 항을 결정하는 수열이다. 수열의 첫 항이 1일 때, “1이 한 개 있다”고 읽을 수 있다. “1이 한 개(1)”이므로 이 수열의 둘째 항은 11이된다. 둘째 항은 11이므로 “1이 두 개 있다”고 읽을 수 있다. “1이 두 개(2)”이므로 셋째 항은 12가 된다. 이 과정을 계속해서 반복하면 다음과 같은 수열이 만들어진다.

```
[1]: 1
[2]: 11
[3]: 12
[4]: 1121
[5]: 122111
...
```

베르베르의 소설 ‘개미’에도 등장하여 우리나라에선 ‘개미 수열’이라는 이름으로도 알려져 있다. 바로 이 수열을 시퀀스 데이터 압축에 사용하면 어떨까 싶었다.

* 1바이트(8비트) 중 3비트는 베이스 종류를 나타내는 데에 사용한다.
    * 000은 A, 001은 T, 010은 G, 011은 G, 100은 N, 101은 U
    * 110과 111은 비워두었다.
* 나머지 5바이트는 반복수를 나타내는 데에 사용한다.
    * 00000 ~ 11111, 즉 1부터 32까지의 반복수를 표현할 수 있다.
    * 32번 이상 반복되는 베이스는 1바이트로 표현할 수 없다. 두 개 이상의 바이트를 써야한다.

예를 들어 AAAAAAATGGGGGGGGG라는 시퀀스는 이 방법으로 3 바이트로 표현할 수 있다.

```
[-1 byte-] [-2 byte-] [-3 byte-]
[00000110] [00100000] [01001000]
```

같은 시퀀스를 FASTA로 저장하려면 17바이트가 필요하다.

FASTA 포맷에 비교한 `.said` 포맷은 장점은 다음 두 가지로 요약할 수 있다.

1. Homopolymer가 많은 시퀀스일수록 압축 효율이 높아진다. poly A region과 같은 시퀀스에서는 비교도 안될 정도로 작은 용량의 파일을 만드는 것을 확인할 수 있다.
2. 반복이 거의 없더라도 같은 시퀀스가 저장된 FASTA보다는 작은(<=) 파일을 만든다. 이는 한 베이스가 반복되지 않는 경우에도 FASTA에서와 같이 1바이트 용량만을 차지하기 때문이다.
    반복수를 (대체로) 늘려주는 Burrows-Wheeler transformation을 사용한 후 `.said` 압축을 하면 좀 더 좋은 압축률을 얻을 수 있지 않을까? 했는데 생각만큼 크게 개선되진 않았다.

이 스크립트를 사용하면 `.said` 포맷으로 FASTA 변환할 수 있다: [[압축](https://github.com/naturale0/SeqCompressor/blob/master/fa2said.py), [압축해제](https://github.com/naturale0/SeqCompressor/blob/master/said2fa.py)]

```shell
# COMPRESS
python fa2said.py input.fa
# DECOMPRESS
python said2fa.py input.said
```

<br>



## 2. 한 베이스를 2 비트만으로 표현하기 ("`.two`" format)

Genome / CDS 시퀀스는 생각보다 반복이 그리 많지 않았다. `.said` format으로는 높은 압축률을 얻기 어려운 상황이다. 그래서 아예 반복수를 기록하지 않고 **한 베이스가 차지하는 용량을 극도로 줄이면** 어떨까 싶었다.

압축 할 시퀀스에 A, T, G, C 네 종류의 베이스밖에 없다고 가정하면 (2^2개 이므로) 2비트만 사용하면 한 베이스를 인코딩할 수 있다. 한 베이스를 표현하는 데에 8비트를 사용해야 했던 FASTA 포맷에 비해 용량을 무려 **1/4**로 줄일 수 있는 것이다. 이렇게 압축한 파일 포맷을 `.two` 포맷이라고 부르도록 하자.

ATGCAATC의 경우 `.two` 포맷으론 2바이트(16비트)로 인코딩할 수 있다.

```
A T G C    A A T C
[00011011] [00000111]
```

이 스크립트를 사용하면 FASTA파일을 `.two` 포맷으로 압축할 수 있다: [[압축](https://github.com/naturale0/SeqCompressor/blob/master/fa2two.py), [압축해제](https://github.com/naturale0/SeqCompressor/blob/master/two2fa.py)]

```shell
# COMPRESS
python fa2two.py input.fa
# DECOMPRESS
python two2fa.py input.say
```

<br>



## 맺으며

이 기회에 야매로 압축 알고리즘을 공부하면서 첫 번째 시도(`.said`)가 run-length encoding이라 불리는 가장 원시적인 압축 알고리즘이라는 것을 알았다.

두 번째 시도 (`.two`)는 Huffman coding과 상당히 닮은 구석이 있다. 차이점은 DNA/RNA의 경우 인코딩하려는 데이터의 종류(A, T, U, G 또는 C, 추가로 N)가 이미 알려져있다는 것이다. DNA의 경우 데이터의 종류가 4개(A, T, G, C) 뿐이기 때문에 사람이 직접 2비트만으로 모든 데이터를 인코딩할 수 있었다.

두 번째 시도는 생물정보학계의 영웅 Jim Kent가 과거에 이미 `.2bit`라는 이름으로 상용화해서 쓰이고 있는 포맷이었다 [[Jim Kent’s Repo](https://github.com/ENCODE-DCC/kentUtils/tree/master/src/utils/faToTwoBit)]. C로 짜인 코드여서 내 것보다 훨씬 빠르게 압축할 수 있다. `.2bit` 포맷은 원하는 샘플의 시퀀스만 가져올 수도 있도록 각 샘플의 해시 딕셔너리도 함께 저장한다.

DNA 시퀀스와 달리 데이터 종류가 알려져 있지 않은 경우엔 Huffman coding을 사용할 수 있다. Huffman coding은 binary tree를 사용해서 자동으로 최적의 인코딩을 찾아준다. `.two`는 binary tree를 사용하지 않고 사람이 직접 인코딩 딕셔너리를 정해주는 특수한 변형이라고 할 수 있겠다.

`.zip` 압축에 사용되는 Lempel-Ziv 알고리즘은 인코딩 딕셔너리가 Huffman coding과 같이 고정되어 있지 않고 *현재까지 압축한 데이터에 따라* 유동적으로 변한다. 비슷한 패턴이 반복해서 나타나는 파일에 있어서 효율적인 압축을 가능케 한다. 압축을 풀기 위해서는 데이터 인코딩에 사용한 binary tree의 정보를 어떤 형태로든 압축된 결과 파일과 함께 저장해야하는 Huffman coding과 달리, 압축된 데이터 그 자체에 인코딩 딕셔너리가 포함된 것과 마찬가지이기 때문에 별도의 정보를 저장할 필요도 없다.

코딩한 결과물 자체는 성능 면에서나 속도 면에서나 무쓸모하지만 그 과정에서 많이 배웠다.

<br>



## 참고

* [SeqCompressor repo.](https://github.com/naturale0/SeqCompressor): 이 글에 사용된 전체 코드를 확인할 수 있다.