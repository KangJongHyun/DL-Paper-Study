# DL-Paper-Study

# ${\textsf{\color{purple}Attention is All You Need}}$

**Author**   
Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin  

지배적으로 많이 사용하고 있는 Sequence 변환 모델은 인코더와 디코더를 포함한 RNN 혹은 CNN에 기반하고 있다. 현재(2017년) 좋은 성능을 보이는 모델은 **Attention** 메커니즘을 통해 **인코더와 디코더**를 연결한다. 본 Paper에서는 recuurence와 convolution을 없애고, Attention 메커니즘만 사용하여 간단한 transformer 아키텍쳐 모델을 제안한다. 
**Model Architecture**  
<img src="https://github.com/user-attachments/assets/e6953b5e-696c-47ee-b4be-af844c1ec5ec" width="300" height="500"/>

기존 neural sequence 모델은 Encode-Decoder 구조를 가지고 있다. 보통 인코터는 입력 시퀀스 $(x_1, ... x_n)$에서 연속적인 표현 시퀀스 $z=z_1, ... , z_n$으로 매핑한다. 이후 디코더는 출력 시퀀스 $(y_1, ... , y_m)&을 생성한다. 각 단계에서 모델은 Auto regressive 하며 Transformer에서는 인토더와 디코더 모두 self-attention 메커니즘과 Point wise Fully connection 을 사용하여 아키텍쳐를 구성한다.  

🤑 **인코더와 디코더, Attention 메커니즘이란?** 🤑  
참고 : https://glee1228.tistory.com/3  
Attention Mechanism : 

