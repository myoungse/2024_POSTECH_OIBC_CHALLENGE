# 2024_POSTECH_OIBC_CHALLENGE

### 제6회 BIG DATA CHALLENGE 🏆

<img src="https://github.com/user-attachments/assets/44e6f3e8-b715-46b8-9193-3a21c51ce0f7" alt="2024OIBC-poster-before" width="600" height = "800">

---

![Python](https://img.shields.io/badge/Python-3.8-blue)
![XGBoost](https://img.shields.io/badge/XGBoost-v1.6.1-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![NumPy](https://img.shields.io/badge/NumPy-v1.23.5-blue)
![Pandas](https://img.shields.io/badge/Pandas-v1.5.2-yellow)
![Matplotlib](https://img.shields.io/badge/Matplotlib-v3.6.2-red)
![Challenge](https://img.shields.io/badge/Challenge-POSTECH%20X%20OIBC-orange)
![Goal](https://img.shields.io/badge/Goal-Day--Ahead%20Price%20Forecasting-blue)
---

## 📌 프로젝트 소개
이 프로젝트는 2024 POSTECH X OIBC CHALLENGE에서 전력 가격 예측을 위해 개발된 솔루션입니다.
Jeju Power Market의 날씨 데이터와 시장 데이터를 활용해 XGBoost Regressor 모델을 기반으로 하루 전(day-ahead) 전기 가격을 예측하였습니다.

---

👥 팀 구성

- 팀장: 윤명세
  - 동의대학교 인공지능학과 3학년
- 팀원: 황언종
  - 부산대학교 의생명융합공학부 데이터사이언스전공 3학년

---

⚙️ 기술 스택 및 사용 라이브러리

- 프로그래밍 언어: Python
- 머신러닝 모델: XGBoost Regressor
- 라이브러리:
	- pandas, numpy: 데이터 전처리
	- matplotlib, seaborn: 데이터 시각화
	- sktime: 시계열 데이터 분리 및 평가
	- xgboost: 모델 개발
	- scikit-learn: 평가 지표 계산=
---
🔍 데이터 설명

대회에서 제공된 데이터는 다음과 같습니다:
	1. 기상 실측 데이터: 과거 날씨 데이터
	2. 기상 예측 데이터: 미래 날씨 예측 정보
	3. 시장 전기 가격 데이터: 실시간 가격 및 하루 전 가격
	4. 시장 현황 데이터: 발전량, 수요량, 기타 현황 지표

전처리를 통해 추가적으로 날짜와 시간 기반의 피처를 생성하였습니다.
---

🧪 모델 학습 및 평가

📂 데이터 전처리

1. 스케일링
- Min-Max Scaler를 사용하여 데이터의 값 범위를 정규화하였습니다.
- 정규화는 모델 학습 과정에서 특정 값이 지나치게 큰 영향을 미치지 않도록 하며, 데이터의 본질적인 패턴을 유지한 채 변동성을 학습할 수 있도록 도와줍니다.
2. 시간 단위 조정
- 서로 다른 데이터셋의 시간 단위를 1시간 간격으로 통합.
- 날씨 데이터: 5분 단위 → 1시간 단위 평균.
- SMP 데이터: 15분 단위 → 1시간 단위 평균.
- 이를 통해 데이터셋 간의 일관성을 확보하고 모델 학습에 적합한 형태로 변환하였습니다.
3. 파생 변수 생성
- 시간적 특성: 시간 및 월 데이터를 삼각함수(sin, cos)로 변환하여 주기성을 반영.
- 시계열 특성: 과거 1~3일의 SMP 데이터를 추가하여 시간 의존성을 학습.
- 통계 특성: 특정 시간대의 평균값과 표준편차를 계산하여 변동성을 반영.
- 주말 효과: 주말 여부를 나타내는 더미 변수를 생성하여 주말과 평일의 전력 수요 차이를 반영.
📈 모델 선정 및 설명

  - 최종 모델: XGBoost Regressor
  - 과거 유사 시계열 예측 대회에서 우수한 성능을 보인 사례를 바탕으로 선정.
  - 장점:
	• 시계열 데이터에서 강점을 발휘하며, 결측값 처리와 Feature Importance 제공으로 해석 가능성이 높음.
	• 상대적으로 데이터 요구량이 적고, 소규모 데이터에서도 안정적인 성능을 제공.
	• 비교 모델: LSTM (딥러닝 기반 시계열 모델)
	• 실험적으로 적용하였으나, 데이터 크기가 충분하지 않아 XGBoost에 비해 학습 결과가 저조함.
	• 복잡한 모델 구조로 인해 학습 시간과 자원이 더 소요됨.

이러한 분석 결과를 바탕으로, 성능의 안정성과 구현의 효율성을 고려하여 XGBoost Regressor를 최종 예측 모델로 채택하였습니다.
---
📊 결과 및 시각화
</br>
<img width="500" alt="image" src="https://github.com/user-attachments/assets/3fdb81a8-65ae-4472-b7c5-042d8121a01d" />

---
🏆 수상 내역
- **200**여 팀이 참가한 대회에서 **17등**을 기록하며 **참가상**을 수상하였습니다. 
- 상금: 200,000원
상위 17팀만 수상하였으며, 참가상은 10위~17위 팀에게 수여되었습니다.
---

## 📖 결론

이번 대회에서는 약 **200개 팀**이 참가한 가운데 **17등**이라는 성과를 기록하며, 상위 **10%에 근접한 성과**를 이루었습니다. 이를 통해 참가상(200,000 KRW)을 수상하며, 대회 목표였던 **제주 전력시장의 하루 전 전기가격 예측**에 대한 이해와 모델링 경험을 성공적으로 쌓았습니다.

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
