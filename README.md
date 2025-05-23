# 2024_POSTECH_OIBC_CHALLENGE

### 제6회 BIG DATA CHALLENGE 🏆

---

## 📌 프로젝트 소개
이 프로젝트는 2024 POSTECH × OIBC CHALLENGE에서 전력 가격 예측을 위해 개발된 솔루션입니다.  
Jeju Power Market의 날씨 데이터와 시장 데이터를 활용해 RandomForest 및 SVR 앙상블 모델을 기반으로 하루 전(day-ahead) 전기 가격을 예측하였습니다.

---

## 👥 팀 구성

- 윤명세 (동의대학교 인공지능학과 3학년)  
- 황언종 (부산대학교 의생명융합공학부 데이터사이언스전공 3학년)  

*모든 작업은 팀원 모두가 공동으로 수행하였습니다.*

---

## ⚙️ 기술 스택 및 사용 라이브러리

| 구분           | 도구 및 라이브러리                                                                             |
|----------------|----------------------------------------------------------------------------------------------|
| 프로그래밍 언어 | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) Python |
| 데이터 처리    | ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white) ![Numpy](https://img.shields.io/badge/Numpy-013243?style=flat&logo=numpy&logoColor=white) pandas, numpy |
| 시각화         | ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat&logo=matplotlib&logoColor=white) ![Seaborn](https://img.shields.io/badge/Seaborn-1A2F40?style=flat&logo=seaborn&logoColor=white) matplotlib, seaborn |
| 머신러닝       | ![Scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white) RandomForest Regressor, SVR |
| 하이퍼파라미터 | ![Optuna](https://img.shields.io/badge/Optuna-6F32BE?style=flat&logo=optuna&logoColor=white) Optuna |

---

## 🔍 데이터 설명

- 기상 실측 데이터, 기상 예측 데이터, 시장 전기 가격 데이터, 시장 현황 데이터 통합  
- 시계열 특성을 반영하여 1시간 단위로 데이터 통합 및 결측치 보간  
- 날짜, 시간, 요일, 공휴일, 계절성 등의 파생 변수 생성

---

## 📂 데이터 전처리 및 통합

1. **데이터 수집 및 적재**  
Jeju Power Market의 시장 가격(하루 전 SMP), 기상 실측/예측 데이터(2개 지점 × 2종) 등 다양한 소스에서 데이터를 수집하였습니다.  
REST API를 활용해 최신 데이터(2024-10~11월)를 자동으로 추가 수집하였고, csv 파일과 병합하여 데이터셋을 최신화하였습니다.

2. **데이터 정제 및 통합**  
- 타임스탬프(ts) 통일: 모든 데이터의 시간 정보를 UNIX timestamp(Int64)로 통일하여 병합의 기준으로 삼았습니다.  
- 결측치 처리: ts(시간) 정보가 없는 행 삭제, 주요 변수 결측치는 전·후 시점의 값으로 보간하거나 필요시 삭제  
- 불필요하거나 결측치가 많은 변수(예: appr_temp, pressure 등) 제거  
- 중복 및 이상치 처리: 동일 시점(ts)에 중복 데이터는 평균값으로 통합, ts 기준 정렬 및 중복 제거

3. **데이터 리샘플링 및 병합**  
- 시간 단위 통일: 기상 데이터(5분/15분 단위)를 1시간 단위 평균 리샘플링, SMP 데이터도 1시간 단위 변환  
- 지점별 데이터 병합: 두 개 지점(1, 2)의 기상 실측/예측 데이터를 ts 기준 outer merge, 동일 변수는 평균값으로 대표값 생성  
- 최종 통합: SMP, 기상 실측, 기상 예측 데이터를 ts 기준 left join, 필요 없는 변수(ice, snow_prob 등) 제거

4. **파생 변수 생성 및 Feature Engineering**  
- 날짜/시간 특성: ts → datetime 변환(Asia/Seoul), hour, month, day, weekday 추출  
- 시간 주기성 반영: hour_sin = sin(2π × hour/24)  
- 요일/공휴일/주말 변수: 요일, 평일/주말, 공휴일(법정 공휴일 리스트 기반) 더미 변수 생성  
- 결측치 추가 보간: 남은 결측치(예: precip_prob)는 전/후일 값으로 보간  
- 최종 불필요 컬럼 제거: temp_max, datetime 등 제거

---

## 🧪 모델 학습 및 평가

- 앙상블 모델 적용: RandomForest로 기본 예측 후 SVR로 잔차 보정  
- 하이퍼파라미터 최적화: Optuna 베이지안 최적화 활용  
- 시간 분할 검증 및 커스텀 평가 지표 적용  

---

## 📊 프로젝트 워크플로우

[데이터 수집 및 적재] --> [데이터 정제 및 통합]
[리샘플링 및 병합]
[파생 변수 생성 및 Feature Engineering]
[모델 학습 및 앙상블 적용]
[모델 평가 및 검증]
[결과 분석 및 개선]

---
🏆 수상 내역
- **200**여 팀이 참가한 대회에서 **14등**을 기록하며 **참가상**을 수상하였습니다. 
- 상금: 200,000원
상위 17팀만 수상하였으며, 참가상은 10위~17위 팀에게 수여되었습니다.
---

## 📖 결론

이번 대회에서는 약 **200개 팀**이 참가한 가운데 **14등**이라는 성과를 기록하며, 상위 **10%에 근접한 성과**를 이루었습니다. 이를 통해 참가상(200,000 KRW)을 수상하며, 대회 목표였던 **제주 전력시장의 하루 전 전기가격 예측**에 대한 이해와 모델링 경험을 성공적으로 쌓았습니다.

### 주요 학습 및 경험
- **시계열 데이터의 특성 이해**:  
  주기성과 계절성을 반영하기 위한 분석 및 모델링 기법을 처음으로 학습하며, 시계열 데이터의 복잡성을 다룰 수 있는 방법을 배웠습니다.  
- **전처리 및 하이퍼파라미터 튜닝**:  
  데이터 정제 및 극단값 처리, 모델 최적화를 통한 성능 개선 경험을 쌓으며, 머신러닝과 데이터 분석에 대한 이해도를 높였습니다.  
- **Pretrained Model 활용의 한계**:  
  사전학습된 모델(Pretrained Model)의 성능 향상을 실험하려 했으나, **Fine-Tuning**에 대한 경험 부족으로 실제 적용하지 못한 점은 아쉬움으로 남았습니다. 이 부분은 향후 학습을 통해 보완할 계획입니다.  

### 성능 및 개선점
- 예측 모델은 전체적인 가격 추세를 잘 따라갔으나, **극단적인 이상치 구간**에서는 한계를 보였습니다.  
  - 이는 데이터를 더욱 심층적으로 분석하고 극단값 처리를 보완해야 함을 시사합니다.  
얹
### 향후 계획
이번 대회는 단순히 예측 성능에 초점을 맞추는 것을 넘어, **시계열 데이터의 특성을 이해하고 분석 및 모델링에 효과적으로 적용하는 방법**을 학습할 수 있는 귀중한 기회였습니다.  
앞으로는:
1. **복잡한 데이터와 문제**를 다룰 수 있는 역량 강화.  
2. **Pretrained Model 활용** 및 **Fine-Tuning** 기술 학습.  
3. 다양한 모델링 기법과 고도화된 접근 방식을 실험적으로 적용하여 데이터 분석의 깊이를 더해나갈 계획입니다.  
---
🤝Contribution

이 프로젝트는 팀 단위로 진행되었으며, 모든 팀원이 함께 작업하였습니다.

---
### 📬 Contact

프로젝트에 대한 질문은 아래 이메일 또는 GitHub 링크로 연락해주세요.  
</br>
- **Email**: djswhd1234@naver.com
- **GitHub**: [https://github.com/eonjong0218](https://github.com/eonjong0218)
