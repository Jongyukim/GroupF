# Seongbuk-gu Rent Prediction (성북구 월세 및 보증금 예측 모델)

서울특별시 성북구 지역의 전월세 실거래 데이터를 기반으로 월세 및 보증금을 예측하는 머신러닝 회귀 모델을 구축하였습니다. 서울시 공공 데이터를 활용하여 실제 주택 임대 시장의 예측 가능성과 확장 가능성을 검증합니다.

## 프로젝트 구조

```
Seongbukgu_Rent_Prediction/
├── data/       # 전월세 실거래가, 기준금리, CPI 등 원본 데이터
├── results/    # 전처리 및 분석 결과 데이터
├── notebooks/  # 실험 코드 (rent_prediction_final.ipynb)
└── README.md   # 프로젝트 설명
```

## 사용 데이터

| 데이터명 | 기간 | 설명 | 출처 |
|----------|------|------|------|
| Seoul_Rent_Data_2022.csv, Seoul_Rent_Data_2023.csv, Seoul_Rent_Data_2024.csv | 2022~2024 | 서울시 전월세 실거래가 데이터| [바로가기](https://data.seoul.go.kr/dataList/OA-21276/S/1/datasetView.do) |
| Korea_Base_Interest_Rate_Trend.csv | 1999-05-06~ 2025-05-09 | 한국은행 기준금리 변동 이력 | [바로가기](https://www.bok.or.kr/portal/singl/baseRate/list.do?dataSeCd=01&menuNo=200643) |
| Consumer_Living_Price_Index.csv | 2022-01~ 2024-12   | 통계청 월별 생활물가지수(cpi) | [바로가기](https://data.seoul.go.kr/dataList/10611/S/2/datasetView.do) |

## 주요 전처리 및 모델링 과정

- 데이터 통합 및 중복 제거  
  (연말/연초 중복 제거, 성북구 + 월세 필터링, 컬럼 영문화)
- 계약일 기준 기준금리 및 CPI 매핑
- 결측치 처리 (층 NaN → 1, 건축년도 → KNN Imputer, 연식 생성)
- 이상치 제거 (IQR 클리핑, Isolation Forest)
- Smooth Target Encoding (법정동코드 + 건물용도)
- 계약월 주기성 반영 (Month_sin, Month_cos)
- StandardScaler 정규화 적용
- 모델 학습 및 평가 (XGBoost + GridSearchCV)
- 대화형 예측 UI (ipywidgets 기반)
- Linear Regression / Random Forest 비교 실험 포함

## 예측 성능 (2024년 테스트셋 기준, XGBoost + GridSearch)

- MAE  : 1778.20  
- RMSE : 3512.22  
- R²   : 0.4871

## 코드 실행 환경

- Python: 3.13.0  
- numpy: 2.1.3  
- pandas: 2.2.3  
- scikit-learn: 1.6.1  
- xgboost: 3.0.0  
- matplotlib: 3.10.1  
- ipywidgets: 8.1.7  

## 실행 예시

```bash
# Jupyter 환경에서 실행 권장
# 또는 ipynb를 .py로 변환하여 실행

jupyter notebook rent_prediction_final.ipynb
```


