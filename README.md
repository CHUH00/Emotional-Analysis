<div align="center">

# 😊 한국어 텍스트 감정 분석 (Word2Vec + BiLSTM)
### 🧠 자연어 처리 파이프라인: 분산 표현 임베딩과 양방향 순환 신경망

![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

</div>

## 📌 프로젝트 개요
**Emotional Analysis** 프로젝트는 AI Hub의 "한국어 단발성 대화 데이터셋"을 기반으로 입력된 문장의 감정(기쁨, 슬픔, 분노 등)을 예측하는 자연어 처리(NLP) 파이프라인입니다. 

단어의 의미적 유사성을 벡터 공간에 맵핑하는 **Gensim Word2Vec** 알고리즘으로 임베딩 층을 구성하였고, 문장의 전후 형태소 문맥을 모두 파악할 수 있는 **양방향 장단기 메모리(BiLSTM)** 신경망 구조를 결합하여 뛰어난 한국어 감정 분류 정확도를 구현했습니다.

## ✨ 데이터 처리 파이프라인 흐름
1. **데이터 로드 및 전처리**
   - `Sentence`: 형태소 분석기 등으로 분리된 토큰 리스트.
   - `Emotion`: 정수형으로 인코딩된 범주형 라벨.
   - 데이터 정제 과정에서 결측치를 제거하고 시퀀스 길이에 따른 패딩을 맞춥니다 (권장: `padding='post'`, 95~99분위 길이 적용).
2. **Word2Vec 임베딩 학습**
   - `gensim.models.Word2Vec`을 활용하여 분산 표현 벡터 매트릭스를 추출합니다. (`vector_size=200`, `window=5`)
3. **BiLSTM 모델 아키텍처 및 학습**
   - `Embedding Layer`: 사전 학습된 Word2Vec 가중치를 동결(`trainable=False`)하여 전이학습 적용.
   - `Bidirectional(LSTM(128))`: 양방향 시퀀스 컨텍스트 정보 추출.
   - `Dense Layers`: 추론용 완전 연결 계층 및 `softmax` 출력을 통한 다중 클래스 분류.

## 📺 각 파이프라인 단계별 구현 화면

### 🔹 1. 데이터 로드 및 전처리
<div align="center">
  <img src="images/데이터로드.png" alt="데이터 로드" width="45%" style="margin:5px;" />
  <img src="images/데이터전처리.png" alt="데이터 전처리" width="45%" style="margin:5px;" />
</div>

### 🔹 2. 모델 정의 및 구조 생성
<div align="center">
  <img src="images/모델정의및생성.png" alt="모델 정의 및 생성" width="70%" />
</div>

### 🔹 3. 다중 에폭(Epoch) 모델 학습 및 평가
Early Stopping과 Best Weights 콜백을 적용해 과적합을 방지하고 손실을 최소화합니다.
<div align="center">
  <img src="images/모델학습.png" alt="모델 학습" width="70%" />
</div>

### 🔹 4. 실시간 문장 감정 추론 테스트
입력된 토큰 리스트에 대해 가장 높은 Confidence 확률을 가진 감정을 도출해 냅니다.
<div align="center">
  <img src="images/추론1.png" alt="추론1" width="70%" style="margin-bottom:10px;" />
  <br>
  <img src="images/추론2.png" alt="추론2" width="70%" style="margin-bottom:10px;" />
  <br>
  <img src="images/추론3.png" alt="추론3" width="70%" />
</div>

---
*본 프로젝트는 인공지능, 딥러닝 및 자연어 처리(NLP) 알고리즘 분야에 대한 끊임없는 탐구의 일환으로 [우진(Woojin Choi)](https://github.com/CHUH00)에 의해 개발되었습니다.*
