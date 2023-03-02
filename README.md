# Project_Customer-Segement
⚽"등급별 프로모션 대상자 세분화 및 경기 참여 촉진"⚽

# 01. 프로젝트 개요


## 1 - 1. 프로젝트 목표
- 등급별 프로모션 대상자 세분화 및 경기 참여 촉진
  - 고객 예매 기록과 특성에 따라 고객 세분화 진행
  - 고객 그룹별로 차등화된 가격과 프로모션 
  
## 1 - 2. 프로젝트 절차
- 지난 경기 관람 여부, 순위, 경기 결과의 영향을 받아 **경기 예매 수와 금액 예측**
- 예매 유도에 반응하는 고객 그룹 세분화
- 차등화된 프로모션을 도입하여 고급좌석 이용 예측

## 1 - 3. 분석결과 소개
```
✅ 인기 있는 상대팀과 경기시에 더 많은 홍보를 하여 고객 호응 유도

✅  당일예약 비중이 높은 것으로 보아 당일 예약 고객을 유입하기 위해 할인 프로모션 진행함 ⇒ 
     취소고객으로 인한 손해를 방지

✅ 예매권북 이용단위를 3개월 단위로 조정하여 재방문율을 높인다. 

✅ 회사와 제휴를 맺어 티켓 판매를 높인다. 

✅ 회사 및 동반 할인 이벤트 진행

✅ 구단 홈페이지와 SNS를 이용하여 홍보 진행, Platinum등급의 경우 구단 문자메시지 이용

```
---
# 02. 데이터 소개

📌 분석 데이터
- 분석 데이터 : 더스포츠커뮤니케이션
- 분석 기  간 : 2022.01.30 ~ 2022.02.15

**Data Description** `Survey_DataFrame` `Final_DataFrame`

<img width="1169" alt="화면 캡처 2023-02-21 171126" src="https://user-images.githubusercontent.com/109959349/220286079-92d7f5dc-b922-43bb-b4ec-600e64ea0c9b.png">

---
# 03. 프로젝트 수행 절차
#### 3 - 1) RFM
#### 3 - 2) Cohort
#### 3 - 3) 재구매 모델링
#### 3 - 4) 차등화된 프로모션

## 3 - 1. RFM
💡 목적 :
> RFM

`Recency` `Frequency` `Monetary`

고객 세분화를 통해 마케팅 전략 제시
> Clustering

`KMeans(n_clusters=3)`

새로운 고객의 정보를 얻은 경우 기존 고객의 특성을 기반으로 어느 집단에 속하는지 분류 가능

- green
  - 구매비용, 최근성, 빈도 낮은 고객
- blue
  - 구매비용, 빈도는 낮지만 최근성이 높은 고객
- gray
  - 구매비용, 최근성, 빈도 높은 고객

### ✔️ 분석결과
- **BAD**등급
  - 전체 고객의 35% 차지하는 반면에 총 매출 11% 차지
- **Platinum**등급
  - 전체 고객의 9.7% 차지하는 반면에 총 매출 37% 차지
<img width="680" alt="제목을-입력해주세요_-002" src="https://user-images.githubusercontent.com/109959349/220497943-ca7a0e53-ab5a-42f6-8059-7771973f7405.png">  


## 3 - 2. Cohort
💡 목적 :
- 시간 경과에 따른 고객 유지율 파악

### ✔️ 분석결과

- 2022년 기준 새롭게 유입 고객이 제일 많은 달
  - **2** 월 **8** 월 **10** 월 **4** 월 **5** 월
<img width="680" alt="제목을-입력해주세요_-001" src="https://user-images.githubusercontent.com/109959349/220493443-64ee14af-38b7-4b5a-930d-910f058ac6ab.jpg" height = "300">

💡 목적 :
- `요일` `상대팀` `경기시간`에 따른 `관객수` 변화
  - 관중수를 기준으로 하여 **인기 있는 상대팀** 기준설립
- New Aquisition User 바탕으로 **새롭게 유입 고객에 영향을 미친 feature 파악**

### ✔️ 분석결과
- 관객 유입에 영향을 많이 주는 변수는 **주말**이 가장 큰 요인
- 평일에 시간대가 늦더라도 관객 유입에 효과 없음
- **주말에 인기 있는 상대팀과 경기 진행**은 관객 유입 효과는 배로 증가 될 것이라 판단  
  
<img width="500" alt="Untitled (3)" src="https://user-images.githubusercontent.com/109959349/220295604-d044410e-84ce-4fc9-911b-40cd48d8224b.png" height = "400">


## 3- 3. 재구매 모델
💡 목적 : 
재구매한 고객들을 파악해서 재구매율 예측 모델 생성

📌 분류모델 :

사용모델 : `LogisticRegression`

재구매한 고객들에게 가장 영향을 준 변수 파악하여 분석

### 변수 소개 
<img width="500" alt="1c1ce941-473c-4e37-abea-bd13eadc8226" src="https://user-images.githubusercontent.com/109959349/220510604-5aa5223f-5bd5-4294-906a-cafb65ab36c8.png" height = "500">

#### Feature Importace
|Weight|Feature|Explain|
|------|---|---|
|0.1551 ± 0.0112|customer_type|Bad/ Bronze/ Silver/Gold / Platinum|
|0.0040 ± 0.0030|audience|청중수|
|0.0027 ± 0.0020|MB_AGE|고객 나이|
|0.0024 ± 0.0036|month|달|
|0.0019 ± 0.0013|sale|혜택 받은 유무|
|0.0018 ± 0.0030|weather|날씨|
|0.0017 ± 0.0013|day|요일|
|0.0015 ± 0.0013|game_time|경기 시간|
|0.0008 ± 0.0008|rank|경기 기록|
|0.0007 ± 0.0022|match_info|상대팀|
|0.0005 ± 0.0019|product_grade_name|좌석|
|-0.0007 ± 0.0056|new_price|티켓에 사용한 금액|
|-0.0021 ± 0.0022|reserve_diff|(경기일 - 예약시간)|
|-0.0077 ± 0.0038|survey_y|설문조사 유무|

### ✔️ 분석결과
- 예약요일
  - **4일 전** 예약과 **당일 예약**고객이 많음

- 나이대별 관중
  - 30대, 40대 고객이 가장 많음
  - **직장인과 가족단위** 관람 비중이 높음
  
- 상대팀
  - 상대팀의 인기도에 따라 관객수가 달라짐
  
- 날씨
  - 관객수에 날씨는 큰 영향을 미치지 못함
<img width="650" alt="제목을-입력해주세요_-003" src="https://user-images.githubusercontent.com/109959349/220514619-c3cb3564-97bf-4ab5-879d-a63c5c7f584f.png" height = "400">

---
### Upgrade 🆚 Stay 고객으로 분류
<img width="877" alt="Untitled (9)" src="https://user-images.githubusercontent.com/109959349/220522965-ab5256b3-9660-4df3-9f25-951c9eff9c25.png">

- [분류]재구매 진행하는 고객 vs 진행하지 않은 고객
    - RFM기반 5등급[Platinum/ Gold/ Silver/ Bronze/ Bad]으로 고객 세분화
        - 승급 가능성 있는 고객등급 파악하여 **등급별 프로모션 진행**
        - `상위 25%` 고객 : Upgrade 고객으로 분류

## 3 - 4. 설문조사 기반 키워드 추출
### ✔️ 분석결과
- 현재 멤버십 제도에서 가장 만족하는 점❓
  - **선예매 혜택**
  
- 어떤 점을 개선해 나아가면 좋을까요❓
  - 자가용 이용하는 고객이 많음
    ➡ 주차문제를 해결하면 고객들의 경기장 이용 만족도 높일 수 있음
<img width="550" alt="제목을-입력해주세요_-004" src="https://user-images.githubusercontent.com/109959349/220525152-5de5e98e-feb4-44d7-8483-ae5922df2e0e.png" height = "400">

# 04. 분석 결과

### 프로모션 전략
```
✅ 인기 있는 상대팀과 경기시에 더 많은 홍보를 하여 고객 호응 유도

✅  당일예약 비중이 높은 것으로 보아 당일 예약 고객을 유입하기 위해 할인 프로모션 진행함 ⇒ 
     취소고객으로 인한 손해를 방지

✅ 예매권북 이용단위를 3개월 단위로 조정하여 재방문율을 높인다. 

✅ 회사와 제휴를 맺어 티켓 판매를 높인다. 

✅ 회사 및 동반 할인 이벤트 진행

✅ 구단 홈페이지와 SNS를 이용하여 홍보 진행, Platinum등급의 경우 구단 문자메시지 이용
```

## 🚩 고객 등급별 맞춤 프로모션 제안
> 🌟 재구매 진행한 Upgrade 등급

# 05. 프로젝트 회고
- 데이터가 2022년만 제공되었기 때문에 연도별 추가 분석 진행이 어려웠음
  - 세부 가설에서 5,000원 혜택을 7,000원 혜택으로 비중을 늘린다면 이에 대한 가설이 경제적 손실을 채울 수 있을 만큼의 이득을 얻을 수 있는지에 대한 추가 분석을 진행이 필요함
