# image_captioning_with_attention

바다나우 어텐션을 활용한 이미지 캡셔닝 모델

* 모델

![캡처d](https://user-images.githubusercontent.com/42109314/116006659-2810a380-a647-11eb-9ff2-558acc02f48b.PNG)


사전훈련된 inceptionV3 CNN를 사용하여 이미지에서 뽑아낸 커널갯수 64개의 특징벡터를 추출했다.  어텐션 매커니즘을 활용해 8X8 사이즈의 Filter와 2048개의 Filter 갯수를 가진 이미지 특징벡터와 LSTM의 hidden_state 사이의 관련도를 함축한 context_vector를 뽑아내고 이를 Decoder LSTM의 Output과 행렬합해 단어사전크기의 노드개수를 가진 Full connection network를 통과해 다음 단어를 예측하였다.

* Attention 메카니즘

  기존 Seq2Seq 모델에서 Encoder에서 출력된 Output들 중, Decoder에서 출력된 Output와 더 연관이 있는 Output를 Decoder Output에 반영해주는 메카니즘

* Show and tell

  Seq2Seq 모델에서 영감을 받아 사전 훈련된 CNN을 Encoder로 사용한다.  Seq2Seq 모델의 ContextVector는 CNN의 마지막 출력층의 Output를 사용한다.

* Merge Model

  show and tell 모델에서 영감을 받은 모델, 사전 훈련된 CNN의 Image Feature를  RNN의 아웃풋과 행렬합해 반영해준다.

* with Attention 메카니즘

  사전 훈련된 CNN의 마지막 출력층 대신 Filter들이 보존된 출력층을 사용한다. 그리고 decoder의 Output과 Filter들 중 가장 관련있는 Filter(Image Feature)를 더 많이 반영한다.



* Requirements

  python3, tensorflow 2.0, NLTK, matplotblib, PIL, h5py, pickle

* 성능

  Greedy 

  BLEU-1: 0.6021306502922246 

  BLEU-2: 0.4124893795271643 

  BLEU-3: 0.31311506016570884 

  BLEU-4: 0.1850805389556838 

  k=3 beam 

  BLEU-1: 0.6458849456814152 

  BLEU-2: 0.45004543862095364 

  BLEU-3: 0.3448907193458137 

  BLEU-4: 0.20824690025701065
