---
layout: post
title: "요인분석으로 내게 맞는 스마트폰 카메라 찾기"
date:   2017-12-29 12:00:00 +0900
author: "Sihyung Park"
categories: [applied, exploratory analysis, multivariate]
locale: ko_KR
---



해를 거듭하면서 스마트폰 성능이 눈에 띄게 향상되고 있다. 특히나 아이폰에 탑재되는 A-시리즈 APU의 성능은 작년부터 PC를 위협해오더니 급기야 [13인치 맥북 프로를 벤치마크 상에서 앞지르기에 이르렀다](https://www.macrumors.com/2017/09/13/a11-bionic-chip-geekbench-scores/). 일정 가격 이상의 대부분의 스마트폰 성능이 상향 평준화 되어버린 지금, [Kantar가 2014년 수행한 북미 시장에서의 설문조사](https://www.google.co.kr/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwin_5iBmq7YAhUHabwKHZSdDKIQFggrMAA&url=https%3A%2F%2Fwww.kantarworldpanel.com%2Fdwl.php%3Fsn%3Dnews_downloads%26id%3D593&usg=AOvVaw3_-kGyaLVbfZQXSlZqniaG)를 보면 스마트폰 구매 선택은 성능 외적인 부분에서 주로 결정되는 것으로 보인다.

특히 카메라 성능은 고가의 스마트폰을 구입하는 데에 있어서 결정적인 역할을 하는 요인으로 생각된다. 2016년 이전에는 코빼기도 보이지 않던 [DxOMark](https://www.dxomark.com/category/mobile-reviews/) 카메라 벤치마크가 이제는 많은 리뷰에서 빠짐없이 등장하는 현상이 이를 뒷받침한다. 비록 DxOMark에서 다양한 성능 카테고리에 대해서 카메라를 테스트하기는 하지만, 벤치마크와 실제 사용자 경험은 차이가 있을 수 있다. 테스트 점수가 높다고해서 내게 만족스러운 카메라가 되는 것은 아니라는 의미이다.

어떤 카메라가 내게 맞는 카메라인지에 대해 대략의 답을 제공하기 위해 DxOMark 벤치마크 데이터에 대해 탐색적 요인 분석(exploratory factor analysis; EFA)을 해보았다.

분석을 시작하면서 답을 찾고자 한 질문들은 이렇다.

1. 각 브랜드는 스마트폰 카메라를 제작할 때 어떤 성능요인(색감, 선명도, …)에 중점을 두는가
2. 각 브랜드의 스마트폰 카메라는 시간에 따라 어떤 방향으로 발전해왔는가
3. 어떤 스마트폰 브랜드끼리 서로 비슷한 사진을 찍어내는가

주로 애플과 삼성을 중점으로 분석을 진행했다. 이 외의 브랜드의 스마트폰 카메라 분석을 원한다면 다음 gist를 참조하시길. 분석과 코드를 정리해 두었다 [[벤치마크 크롤러](https://gist.github.com/naturale0/46054738f4f61916d6399058c58fafdc#file-dxocrawler-py)][[노트북](https://gist.github.com/naturale0/46054738f4f61916d6399058c58fafdc#file-dxomark_efa-ipynb)].

- TOC
{:toc}
<br> 

## 최근 데이터들의 3-factor EFA 결과

DxOMark는 2017년 9월에 새로운 테스트 프로토콜을 제시한 바 있다. 테스트 프로토콜에 따른 테스트 점수 변동이 있을 수 있으므로, 이전 프로토콜에서 만들어진 데이터(이 글에서는 “과거” 데이터라 호칭한다)와 새로운 프로토콜(“최근”)에서 만들어진 데이터를 따로 분석하기로 했다.

Varimax 방법으로 새 프로토콜에서 얻은 데이터들을 회전시킨 EFA 결과, 다음과 같은 factor loading을 얻을 수 있었다.

![output_39_0](/assets/fig/171229_output_39_0.png)

각 요인에 크게 연관되어 있는 manifest variable에 따라 요인을 해석해서 이름을 붙였다.

* FA1: AF, texture, exposure&contrast 등에 강한 음의 상관관계가 있으므로 **“Bad Focus”**.
* FA2: artifacts, noise 등에 강한 양의 상관관계가 있으므로 **“Sharp, Clear”**.
* FA3: flash, texture 등에 강한 양의 상관관계가 있으므로 **“High Detail”**.

즉, FA1 값이 클수록 포커스가 잘 안잡히는 카메라, FA2가 클 수록 선명하고 또렷한 카메라다.

현재 시점 (2017/12/29)에 DxOMark에 올라온 모든 최근 스마트폰 카메라의 점수를 요인 점수로 변환해서 그래프로 나타내 보았다.

![output_43_0](/assets/fig/171229_output_43_0.png?)

같은 색 포인트는 같은 회사에서 제작된 스마트폰이다. 이 그래프에서 각 브랜드의 장단점을 파악할 수 있다. 예를들어 구글의 경우 Sharp, Clear 점수가 조금 떨어지지만 포커싱과 디테일이 매우 우수하다. 반면 애플은 포커싱이 비교적 안좋은 반면 Sharp, Clear과 디테일이 우수한 것을 볼 수 있다. 삼성과 구글의 지향점이 서로 비슷한 듯하다.

각 브랜드의 최근 카메라 제작 트렌드를 좀 더 자세히 들여다보기 위해 삼성과 애플 제품만 따로 나타내보았다.

![output_42_0](/assets/fig/171229_output_42_0.png)

애플 아이폰 모델이 최신형에 이르면서 포커싱보다는 Sharp, Clear과 디테일에 중점을 두고 발전하는 것을 확인할 수 있다. 삼성 또한 갤럭시 S6 엣지에서 갤럭시 노트 8에 이르면서 Sharp, Clear보다는 포커싱과 디테일에 중점을 두는 모양새를 볼 수 있다.

<br>

## 과거 데이터들의 3-factor EFA 결과

최근 데이터와 동일한 방법으로 분석을 진행했다. Varimax rotated factor loading은 아래와 같다.

![output_51_0](/assets/fig/171229_output_51_0.png)

최신 데이터와는 조금 다른 해석을 사용해서 요인에 이름을 붙였다.

* FA1: AF, texture, noise 등에 강한 음의 상관관계가 있으므로 **“Bad Focus”**.
* FA2: color, exposure&contrast 등에 강한 양의 상관관계가 있으므로 **“Colorful”.**
* FA3: noise, flash, exposure&contrast 등에 강한 양의 상관관계가 있으므로 **“Clear”**.

즉, FA1 값이 클수록 포커스가 잘 안잡히는 카메라, FA2가 클 수록 선명하고 또렷한 카메라다.

DxOMark에서 테스트한 과거 모든 스마트폰 카메라를 스캐터플롯으로 나타내어 보았다.

![output_54_0](/assets/fig/171229_output_54_0.png)

삼성과 애플 제품들만 모아보았다.

![output_55_0](/assets/fig/171229_output_55_0.png)

삼성 제품들과 애플 제품들이 서로 다른 클러스터로 구별된다.
삼성은 포커스와 색감, 선명성에서 개선을 이뤄낸 것이 보인다. 최신 기종에 이를수록 개선 폭은 작아지는 것이 확인된다.
애플은 반면에 과거 기종부터 우수한 색감을 보인다. 주로 선명성과, 특히 포커싱 개선에 노력을 들인 것으로 보인다.

<br>



## 나에게 맞는 스마트폰 카메라 찾기

[Moment](https://www.shopmoment.com/)라는 스마트폰 카메라 전문 렌즈 제작 스타트업은 “항상 휴대하는 카메라가 가장 좋은 카메라”라고 한 바 있다. 스마트폰 카메라의 우수한 휴대성을 강조한 말이다. “이왕 항상 휴대하는 거, 수치상으로 가장 좋은 카메라 대신, 내가 지향하는 사진을 찍을 수 있게 하는 카메라를 선택하는게 어떨까?”라는 생각에서 시작해서 벤치마크 숫자만으로는 파악할 수 없는 잠재적인 요인들을 요인분석으로 파악해 보았다.

색감을 중요시하는 사람은 전통적으로 우수한 색감을 자랑해온 애플 아이폰, 또는 세대가 거듭함에 따라 비약적인 색감 개선을 이뤄낸 삼성 제품을 선택할 수 있을 것이다. 또, 디테일을 중요하게 생각하는 사람은 디테일(FA1) 1위 제품을 만들어낸 구글 제품을 선택할 수 있을 것이다.

단순 벤치마크보다는 누군가의 스마트폰 선택에 도움이 되는 정보이기를 바란다.