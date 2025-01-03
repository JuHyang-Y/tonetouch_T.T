# 📘 ToneTouch 프로젝트 소개
## 📢 주제 및 목표
+ 주제 : **청각 장애인을 위한 주변 소리 인식 위험 상황 알리미**
+ 목표
	+ 청각장애인의 안전한 일상을 위한 주변소리 인식 웹페이지 개발
  + 비문해자 청각장애인도 위급 상황에서 한눈에 파악할 수 있는 **간결한  UI**를 목표
  + 생활 소음 및 주변 소리 분석하여 주변 상황 알림 기능 제공
  + 인식한 소리에 따라 라즈베리에서 화면으로, 진동으로 사용자에게 알림
       
## 📆 프로젝트 기간 
+ 24.06.26 - 24.08.02

## ⛰️ 결과
+ 인공지능사관학교 핵심 역량 프로젝트 성과물 발표회 최우수상
  
→ **전체 프로젝트에 대한 설명 github 주소** : [ToneTouch](https://github.com/heehjjaee/AZZ)  

    
# 📄 Modeling part 정리  
## 📚 사용 기술
<div> 
  <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white">
	<img src="https://img.shields.io/badge/jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
</div>

## 📌 개발환경
+ **GPU**
  + Tensorflow 2.4.1(Python 3.8.6, CUDA 11.0, cuDNN 8.0.5)

## 🗃️ DataSet
### 1. Urbansound8k
+ 뉴욕대학교 MARL(Music and Audio Research Lab)에서 공개한 데이터셋
+ 10개의 클래스
+ 데이터셋 링크 : [Urbansound8k dataset](https://urbansounddataset.weebly.com/urbansound8k.html)
### 2. Infant cry audio corpus
+ Kaggle 데이터  
+ 데이터셋 링크 : [Infant cry audio corpus](https://www.kaggle.com/datasets/warcoder/infant-cry-audio-corpus)

→ 이 중 **청각장애인이 소리를 듣지 못해 위험한 상황에 직면했던 소리** 에 해당하는 클래스를 따로 추출    
출처 : 청각장애인의 위험 판단을 위한 소리 정보, 인지 조건과 행동 반응에 관한 연구
   
### class list  
| 번호 | 클래스이름 | 개수 |
|------|-----------|-------|
| 0 | car_horn | 429 |
| 1 | jackhammer | 1,000 | 
| 2 | siren | 929 | 
| 3 | baby_cry | 457 |
| | | 2,815 |


## 🔪 데이터 전처리
### 1. 데이터의 크기 통일
+ 데이터의 길이를 4초 단위로 비슷하게 맞춤
### 2. Librosa 라이브러리
+ 음악 및 오디오 신호처리를 위한 파이썬 라이브러리
+ 원천 데이터 .wav 형식을 **Mel spectrogram**으로 변환
+ Mel Spectrogram은 주파수가 Mel Scale로 변환되는 Spectrogram
+ 사람들은 음성신호를 인식할 때 주파수를 linear scale로 인식하지 못함, Mel Scale은 이러한 특성을 고려한 음조의 지각 척도
![그림01](https://github.com/user-attachments/assets/1d93f3cc-ce2e-42f0-9e46-d485ce9666e2)

## 🥇 모델
### CNN(Convolutional Neural Network, 합성곱 신경망)
+ Random Forest
  + 앙상블의 한 종류
  + 여러개의 Decision Tree를 이용해 최종 예측을 내는 방법
  + 과적합 문제 효과적으로 방지
+ SVM
  + 자료분석을 위한 지도 학습 모델
  + 클래스를 분류할 수 있는 최적의 경계를 찾는 방식
+ CNN
  + 이미지를 인식하기 위한 패턴을 찾는데 유용
  + 이미지를 학습시키는 과정에서 **이미지 공간 정보를 유지한 상태로 학습** 가능
  
+ 모델 비교
  
| 모델 | 정확도 | 정밀도 | 재현율 | F1-Score |
|------|--------|--------|--------|----------|
| Random Forest | 0.77 | 0.77 | 0.77 | 0.76 |
| SVM | 0.78 | 0.79 | 0.78 | 0.76 |
| CNN | 0.90 | 0.90 | 0.90 | 0.90 |

### 학습 및 파라미터 튜닝
+ 과적합 방지를 위해 **Dropout 레이어**를 추가
+ **Earlystopping 함수**를 사용하여 검증 데이터의 오차가 증가하면 학습을 중단
![acc](https://github.com/user-attachments/assets/c4acecc7-9d5c-41a3-a63a-48b05b9ebdd2)
→ 정확도 **0.90**


## 📝 참고사항
+ 코드를 데이터 다운부터 cnn모델 학습, 교차검증까지 한 파일에 진행해서 알아보기 힘듦
+ Urbansound8k 데이터 코드 상에서 다운받아 진행
+ baby_cry를 포함한 모델과 포함하지 않은 모델 2가지가 있음


## 👷 주요 업무
+ **아이디어 기획**
+ **데이터 전처리**
  + librosa 라이브러리를 활용하여 .wav 형식의 소리 데이터를 mel-spectrogram으로 변환
+ **모델링**
  + 전처리한 데이터를 딥러닝 모델(CNN)에 학습 및 가중치 출력
+ **발표**
