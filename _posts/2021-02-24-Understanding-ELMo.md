---
layout: post
title: "Understanding ELMo"
date:   2021-02-24 16:01:00 +0900
author: "Sihyung Park"
categories: [machine learning, natural language processing]

---

Word2Vec and FastText paved the way to quality word embedding by utilizing context information, either word-level or character-level. ELMo (**e**mbeddings from **l**anguage **mo**del) improved upon those with not only single context, but with both character and word-level contexts by dedicated architecture for the tasks.

ELMo is composed of two structures: bidirectional language model (biLM) and the task-specific layer. Pretrained on large data, BiLM provides enough context to task-specific layer that facilitates hi-quality embedding.



- TOC
{:toc}
<br> 

## The architecture

### Bidirectional language model

#### Character-level CNN

character-level tokens goes through convolutional layers with different kernel sizes. The original "small" ELMo model uses kernels of size 1, 2, 3, 4, 5, 6, 7 with 32, 32, 64, 128, 256, 512, 1024 channels, respectively. Outputs from each convolutional layers are then max-pooled and concatenated to yield $32+32+64+128+256+512+1024=2048$-length vector. This concatenated vector can be used as a word embedding. Since convolutional layer is well known for its feature-extracting property, this can be regarded as a character-level context extraction process.

#### Bidirectional LSTM

$L$-layer bi-LSTM is used to account for word/sentence-level information. Originally $L=2$ is used for ELMo. By using bidirectional LSTM, we can efficiently train the language model to encode contexts from the full sentence to embeddings.

According to the authors of ELMo, output from the first layer is reported to produce better result when used for POS tagging (Belinkov et al., 2017), while output from the top most layer (here, the second layer) was known for learning word-sense representations (Melamud et al., 2016).

![ELMo-architecture](/assets/fig/210224_elmo-architecture.png)

<br>

### Task specific layer

Task specific layer is a mere weighted sum and scaling of biLM outputs. All intermediate outputs from pretrained biLM, from character-level CNN and each layer of bi-LSTM, is used to train task specific layer.

Output from this layer can be further passed to other layers for downstream task such as classification. We train the whole model after freezing the pretrained biLM weights.

<br>



## Pytorch implementation

Here I pretrained the biLM using IMDB data in order to further use the pretrained model to sentiment analysis, which is positive/negative binary classification in this case.

### Character-level CNN

```python
class CharConv(nn.Module):
    """
    character-level convolutional network
    """
    def __init__(self):
        super(CharConv, self).__init__()
        
        # Embedding layer
        self.char_embedding = nn.Embedding(CHAR_VOCAB_SIZE, CHAR_EMBED_DIM)
        
        # Conv layers
        self.conv1 = nn.Conv2d(CHAR_EMBED_DIM, 2, 1)
        self.conv2 = nn.Conv2d(CHAR_EMBED_DIM, 2, (1, 2))
        self.conv3 = nn.Conv2d(CHAR_EMBED_DIM, 4, (1, 3))
        self.conv4 = nn.Conv2d(CHAR_EMBED_DIM, 8, (1, 4))
        self.conv5 = nn.Conv2d(CHAR_EMBED_DIM, 16, (1, 5))
        self.conv6 = nn.Conv2d(CHAR_EMBED_DIM, 32, (1, 6))
        self.conv7 = nn.Conv2d(CHAR_EMBED_DIM, 64, (1, 7))
        self.convs = [
            self.conv1, self.conv2, 
            self.conv3, self.conv4, 
            self.conv5, self.conv6, 
            self.conv7
        ]
        
    
    def forward(self, x):
        x = self.char_embedding(x).permute(0,3,1,2)
        x = [conv(x) for conv in self.convs]
        x = [F.max_pool2d(x_c, kernel_size=(1, x_c.shape[3])) for x_c in x]
        x = [torch.squeeze(x_p, dim=3) for x_p in x]
        x = torch.hstack(x)
        
        return x
```

I used smaller numbers of channels, even compared to the "small" model. So final output from `CharConv` will be only 128-length vector per sample.

### Bidirectional LSTM

```python
class BiLSTM(nn.Module):
    def __init__(self):
        super(BiLSTM, self).__init__()
        # Bi-LSTM
        self.lstm1 = nn.LSTM(128, 1024, bidirectional=True)
        self.dropout = nn.Dropout(0.1)
        self.proj = nn.Linear(2*1024, 2*128, bias=False)
        self.lstm2 = nn.LSTM(2*128, 1024, bidirectional=True)
    
    def forward(self, x):
        # 1st LSTM layer
        o, (h1, __) = self.lstm1(x)
        o = self.dropout(o)
        
        # main connection
        p = self.proj(o)
        
        # skip connection
        x2 = x.repeat(1,1,2)
        x3 = x2 + p
        
        # 2nd LSTM layer
        _, (h2, __) = self.lstm2(x3)
        
        return h1, h2
```

Return both outputs from the first and the second layer for later use.

### Bidirectional language model

Stack `CharConv` on top of `BiLM` to build a biLM module.

```python
class BiLangModel(nn.Module):
    """
    Bidirectional language model (will be pretrained)
    """
    def __init__(self, char_cnn, bi_lstm):
        super(BiLangModel, self).__init__()
        
        # Highway connection
        CHAR_EMBEDDING_DIM = 16
        self.highway = nn.Linear(128, 128)
        self.transform = nn.Linear(128, 128)
        self.char_cnn = char_cnn
        self.bi_lstm = bi_lstm
        
    def forward(self, x):
        # Character-level convolution
        x = self.char_cnn(x)
        x = x.permute(2, 0, 1)
        
        # highway
        h = self.highway(x)
        t_gate = torch.sigmoid(self.transform(x))
        c_gate = 1 - t_gate
        x = h * t_gate + x * c_gate
        
        # Bi-LSTM
        x1, x2 = self.bi_lstm(x)
        
        return x1, x2
```

Note there is a highway connection between character-level CNN and bi-LSTM.

<br>

### Intermediate results

<TBD>



<TBD: task specific layer>

<br>



Python code for the algorithm is in the last part of [this notebook (GitHub)](https://github.com/naturale0/NLP-Do-It-Yourself/blob/main/NLP_with_PyTorch/3_document-embedding/3-2.%20ELMo.ipynb).

<br>



***References***

* Peters et al. 2018. **Deep contextualized word representations**. https://arxiv.org/abs/1802.05365