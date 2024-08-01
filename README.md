# DL-Paper-Study

# ${\textsf{\color{blue}Attention is All You Need-Transformer}}$

**Author**   
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin  

지배적으로 많이 사용하고 있는 Sequence 변환 모델은 인코더와 디코더를 포함한 RNN 혹은 CNN에 기반하고 있다. 현재(2017년) 좋은 성능을 보이는 모델은 **Attention** 메커니즘을 통해 **인코더와 디코더**를 연결한다. 본 Paper에서는 recuurence와 convolution을 없애고, Attention 메커니즘만 사용하여 간단한 transformer 아키텍쳐 모델을 제안한다. 
**Model Architecture**  
<img src="https://github.com/user-attachments/assets/e6953b5e-696c-47ee-b4be-af844c1ec5ec" width="300" height="500"/>

기존 neural sequence 모델은 Encode-Decoder 구조를 가지고 있다. 보통 인코터는 입력 시퀀스 $(x_1, ... x_n)$에서 연속적인 표현 시퀀스 $z=z_1, ... , z_n$으로 매핑한다. 이후 디코더는 출력 시퀀스 $(y_1, ... , y_m)$을 생성한다. 각 단계에서 모델은 Auto regressive 하며 Transformer에서는 인토더와 디코더 모두 self-attention 메커니즘과 Point wise Fully connection 을 사용하여 아키텍쳐를 구성한다.   


**Incoder** : 구성 자체는, $N=6$ 개의 동일한 레이어로 구성된 스택형태. 각 레이어에는 두 개의 서브 레이어가 있는데, 위의 그림에서 확인할 수 있다. Multi-Head self Attention 메커니즘과 단순한 Position wise fully connected feed forward 네트워크이다. 각 서브 레이어 주위에는 Residual Connection(TCN 참고)를 사용하고, 뒤에서는 Normalization을 통해 레이어를 정규화한다. 이로써 각 서브 레이어의 Output은 $LayerNorm(x+Sublayer(x))$이며, $Sublayer(x)$는 서브 레이어의 자체 함수다. 이러한 Residual 연결을 용이하게 하기 위해 모델의 모든 서브 레이어와 임베딩 레이어는 $d_model = 512$의 차원을 갖는 출력을 생성한다.   
**Decoder** : Incoder와 마찬가지로 동일한 스펙의 스택으로 이루어져 있다. 다만 인코더와는 조금 다르게, 인코더의 두 서브 레이어 외에도 디코더는 인코더 스택의 Output을 통해 Multi-head Attention메커니즘을 우행하는 세번째 레이어를 추가한다.  


사용되는 attention 메커니즘은 Query, Key-value 쌍을 출력으로 mapping하는 것으로 설명할 수 있다.  
본 논문에서는 사용하는 Attention 메커니즘을 Scaled Dot-Product Attention 이라고 부른다. 
<img src="https://github.com/user-attachments/assets/8ae380ac-e6e8-41b7-8d0d-bae0447cb763" width="600" height="300"/>   
input으로는 차원 $d_k$의 Query 와 Key, 그리고 차원 $d_v$를 준다. 이를 이용해서 가중치를 구할 수 있다. 

🤑 **인코더와 디코더, Attention 메커니즘이란?** 🤑  
참고 : https://glee1228.tistory.com/3  
**Attention Mechanism** : 기존의 seq2seq 모델에서는 각 seq를 임베딩(RNN을 거치면서) 하고 Context 벡터로 내놓을 때 고정된 크기로 내놓게 되면서 병목현상이 발생한다. 이는 모델의 딜레이를 초래하게 되고 단점으로써 작용한다. 또한 하나의 seq가 소스 문장의 모든 정보를 가지고 있어야 한다. 이를 해결하기 위해서 기존 Hidden레이어로 작용하는 출력값들을 모두 입력으로서 받는다는 발상이 나온다. Attention메커니즘의 기본 아이디어다.   
- Hidden State를 모두 별도의 배열 &W& 에 저장함으로써, Output seq를 생성할 때 마다 $w$ 를 모두 참고한다.
- 이때, 단어별로 가중치를 두고 참고한다.  
**Decoder 계산 방식** : 디코더에서 $s_n$을 만드는 방식은 이전의 $s_{n-1}$ 의 값과 sorce seq의 hidden state 값들을 이용하여 계산한다.   
Energy : seq기준으로, 단어를 출력하기 위해서 $W$에서 어떤 값에 초점을 둘지 수치화. 이후  SOFTMAX를 씌워 가중치를 계산한다. 
$e_{ij}=a(s_{i-1},h_j)$, 가중치 $\alpha_{ij} = softmax(e_{ij})$  

<img src="https://github.com/user-attachments/assets/b010e26b-abfd-40e4-abd1-133506a12f7a" width="600" height="300"/>  

다시, 정리해서 말하면. 디코딩 과정 중에서 어떠한 단어 $s_n$ 을 출력할 때, 이전 state와 Hidden Layer 각각의 energy를 구하여 최종 디코더 input $c_n$을 구한 후 출력값을 구해내는 일련의 과정이다.  

🤑 **Embedding** 🤑  






