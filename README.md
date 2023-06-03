# PV-power-generation-forecast

<br>

## 전라남도 영암군의 태양광 발전량을 분석 및 예측하자
<br>

### 데이터셋
- 공공데이터포털에서 제공하는 2013~2022년 영암1차 PV 발전량 데이터
- 발전지역과 인근 위치의 기상 데이터 수집
  - ASOS 데이터
- 미세먼지와의 관계 분석을 위해 전남 영암군의 미세먼지 데이터 수집
  - 영암군 대불에 위치한 관측소 데이터 크롤링
- 엘니냐와 라니냐의 영향을 파악하기위해 NINO3.4 데이터 수집

<br>

### 데이터 병합 및 전처리과정
- 결측값 채우기
  - 일조,일사량은 결측값으로 된 부분이 모두 0이 들어가야함
  - 적설량 4-11월은 0으로 처리, 이외의 기간은 보간
  - 결측치의 분포를 확인하여 보간 및 지수가중이동평균으로 결측치처리
- 데이터 범위 제한
  - 태양광 발전이 가능한 06-20시로 제한 

<br>

## EDA
#### 상관관계 시각화
<img src= "https://github.com/smart0515/PV-genertation-analysis/assets/48974564/17b32a22-4e65-456d-80f5-ddc9be7f4650" height="700px" width="750px">

<br>

#### 다중공선성 확인
다중공선성이 10이 넘어가지 않게 상관관계가 높고 비슷한 분포를 가지는 피처를 드롭함 <br>

<img src= "https://github.com/smart0515/PV-genertation-analysis/assets/48974564/25fe707a-dbb4-44ff-96aa-eb166980bf72" height="320px" width="250px">

<br>

#### PCA 및 클러스트링
Elbow 및 Silhouette Score에 기반하여 클러스터수는 3으로 결정
<img src= "https://github.com/smart0515/PV-genertation-analysis/assets/48974564/1f119b01-1847-4ed6-a92a-9cd854f4e6d9" height="300px" width="750px">
- pca 결과를 보면 일사/일조그룹, 습도/운량그룹, 미세먼지/온실가스/기압그룹으로 나누어지는 것을 볼 수 있음
   - 일사와 습도/운량은 같은 PC1의 반대를 나타내고 미세먼지/온실가스/기압그룹은 PC1과 수직에 가까운 분포를 가짐
   
<br>

#### 엘니뇨/라니냐와 발전량과의 관계
연도별 일사량의 추세를 확인했을때 알수없는 추이가 보여서 이를 확인하기 위하여 추가적인 데이터를 수집
<img src= "https://github.com/smart0515/PV-genertation-analysis/assets/48974564/a89072ad-b778-4f38-ad32-d14c6c0756fd" height="300px" width="750px">
- 엘니뇨/라니냐는 주로 겨울철 한국에 영향을 끼침으로 데이터를 12-2월로 제한하여 비교
  - 비교 결과 10년의 기간이라 확정지을 수는 없지만 엘니뇨시기와 라니냐시기 겨울철에 유의미한 차이가 나타남 
