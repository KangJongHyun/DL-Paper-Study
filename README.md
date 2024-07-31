# DL-Paper-Study

# ${\textsf{\color{blue}Attention is All You Need}}$

**Author**   
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin  

지배적으로 많이 사용하고 있는 Sequence 변환 모델은 인코더와 디코더를 포함한 RNN 혹은 CNN에 기반하고 있다. 현재(2017년) 좋은 성능을 보이는 모델은 **Attention** 메커니즘을 통해 **인코더와 디코더**를 연결한다. 본 Paper에서는 recuurence와 convolution을 없애고, Attention 메커니즘만 사용하여 간단한 transformer 아키텍쳐 모델을 제안한다. 
**Model Architecture**  
<img src="https://github.com/user-attachments/assets/e6953b5e-696c-47ee-b4be-af844c1ec5ec" width="300" height="500"/>

기존 neural sequence 모델은 Encode-Decoder 구조를 가지고 있다. 보통 인코터는 입력 시퀀스 $(x_1, ... x_n)$에서 연속적인 표현 시퀀스 $z=z_1, ... , z_n$으로 매핑한다. 이후 디코더는 출력 시퀀스 $(y_1, ... , y_m)&을 생성한다. 각 단계에서 모델은 Auto regressive 하며 Transformer에서는 인토더와 디코더 모두 self-attention 메커니즘과 Point wise Fully connection 을 사용하여 아키텍쳐를 구성한다.   


**Incoder** : 구성 자체는, $N=6$ 개의 동일한 레이어로 구성된 스택형태. 각 레이어에는 두 개의 서브 레이어가 있는데, 위의 그림에서 확인할 수 있다. Multi-Head self Attention 메커니즘과 단순한 Position wise fully connected feed forward 네트워크이다. 각 서브 레이어 주위에는 Residual Connection(TCN 참고)를 사용하고, 뒤에서는 Normalization을 통해 레이어를 정규화한다. 이로써 각 서브 레이어의 Output은 $LayerNorm(x+Sublayer(x))$이며, $Sublayer(x)$는 서브 레이어의 자체 함수다. 이러한 Residual 연결을 용이하게 하기 위해 모델의 모든 서브 레이어와 임베딩 레이어는 $d_model = 512$의 차원을 갖는 출력을 생성한다.   
**Decoder** : Incoder와 마찬가지로 동일한 스펙의 스택으로 이루어져 있다. 다만 인코더와는 조금 다르게, 인코더의 두 서브 레이어 외에도 디코더는 인코더 스택의 Output을 통해 Multi-head Attention메커니즘을 우행하는 세번째 레이어를 추가한다. 

🤑 **인코더와 디코더, Attention 메커니즘이란?** 🤑  
참고 : https://glee1228.tistory.com/3  
Attention Mechanism : 

