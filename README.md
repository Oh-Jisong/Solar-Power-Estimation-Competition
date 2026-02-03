<p align="center">
  <img src="assets/banner.png" width="900">
</p>

<h1 align="center">Solar Irradiance Prediction Model</h1>

<p align="center">
  기상 데이터 기반 일사량 예측 머신러닝 모델 개발 프로젝트 (TAVE 데이터분석 심화)
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue.svg">
  <img src="https://img.shields.io/badge/XGBoost-ML-orange.svg">
  <img src="https://img.shields.io/badge/Optuna-HPO-purple.svg">
  <img src="https://img.shields.io/badge/Status-Completed-success.svg">
</p>

---

## Project Overview

본 프로젝트는 **기상 관측 시계열 데이터를 활용하여 태양광 발전에 핵심적인 일사량(Solar Irradiance)을 예측하는 머신러닝 모델을 개발**하는 것을 목표로 진행되었습니다.

기존 통계 기반 접근 방식의 한계를 극복하기 위해,  
**데이터 전처리 → 특징 공학 → 모델링 → 하이퍼파라미터 최적화 → 앙상블 전략**까지 포함한 실무형 분석 파이프라인을 구축하였습니다.

센서가 설치되지 않은 발전소 환경에서도 **기상 데이터만으로 안정적인 일사량 추정이 가능하도록 설계**한 것이 핵심 방향입니다.

---

## Core Features

### 데이터 처리 파이프라인

- 5분 단위 기상 시계열 데이터 활용
- 결측치 보간 (Linear Interpolation + 평균 대체)
- 물리 기반 이상치 클리핑 처리
- Datetime 기반 시간 파생 변수 생성

---

### Feature Engineering

- 시간 파생 변수  
  - hour, day of week, day of year
- 주기성 인코딩  
  - sin / cos 변환 (hour, day 기반)
- 기상 파생 변수  
  - 강수 여부 Binary Encoding  
  - 구름량/UV/안개 지표 생성

---

### 모델링 전략

- Baseline Regression 모델 구축
- XGBoost 기반 주 모델 학습
- TabMLP Attention 구조 실험 적용
- Residual Learning 기반 하이브리드 구조 설계

---

### 성능 최적화

- Optuna 기반 하이퍼파라미터 자동 탐색
- Early Stopping 적용
- Validation MAE 기준 최적 모델 선정
- Soft Blending Ensemble 전략 적용

---

## UI Preview (Screenshots)

<table>
  <tr>
    <td align="center"><b>Pipeline Overview</b></td>
    <td align="center"><b>Feature Importance</b></td>
    <td align="center"><b>Model Architecture</b></td>
    <td align="center"><b>Prediction Result</b></td>
  </tr>
  <tr>
    <td>
      <img src="screenshots/pipeline.png" width="100%">
    </td>
    <td>
      <img src="screenshots/feature_importance.png" width="100%">
    </td>
    <td>
      <img src="screenshots/architecture.png" width="100%">
    </td>
    <td>
      <img src="screenshots/result.png" width="100%">
    </td>
  </tr>
</table>

---

## Tech Stack

| Category | Technology |
---------|------------
Language | Python
ML Model | XGBoost, TabMLP
Optimization | Optuna
Data Processing | Pandas, NumPy
Visualization | Matplotlib, Seaborn
Metric | MAE, RMSE

---

## Project Structure

```bash
solar_irradiance_project/
┣ README.md
┣ data/
┃ ┣ raw_data.csv
┃ ┣ processed_data.csv
┣ notebooks/
┃ ┣ eda.ipynb
┃ ┣ feature_engineering.ipynb
┃ ┣ modeling.ipynb
┣ models/
┃ ┣ xgboost_model.pkl
┃ ┣ tabmlp_model.pt
┣ screenshots/
┃ ┣ banner.png
┃ ┣ pipeline.png
┃ ┣ feature_importance.png
┃ ┣ architecture.png
┃ ┣ result.png
┣ train.py
┣ inference.py
┗ requirements.txt
```

---

## Dataset Description
### Input Features

1. 기온 (Temperature)
2. 습도 (Humidity)
3. 풍속 (Wind Speed)
4. 운량 (Cloud Cover)
5. 강수 여부 (Rain)
6. 시간 정보 (Hour, Day, Month)
7. 위치 정보 (좌표 기반)

### Target
1. Solar Irradiance (일사량)

---

## Execution Method

### Environment Setup
```
pip install -r requirements.txt
```

### Model Training
```
python train.py
```

### Inference
```
python inference.py
```

---

## Model Performance

* Evaluation Metric: MAE / RMSE
* Validation 기준 최종 모델:

|Model	|Validation MAE|
|-|-|
|XGBoost|	~41|
|LightGBM|	~43|
|Blending Ensemble	|~42|

※ Validation 기준 성능 안정성과 일반화 성능을 고려하여 XGBoost 기반 모델을 최종 채택

---

## What I Learned

본 프로젝트를 통해 다음 역량을 집중적으로 학습했습니다.

1. 시계열 기상 데이터 전처리 및 품질 관리
2. 시간 기반 Feature Engineering 실전 적용
3. XGBoost 하이퍼파라미터 튜닝 전략
4. Optuna 자동 최적화 파이프라인 구축
5. Ensemble 모델 설계 및 성능 비교
6. 머신러닝 실험 관리 및 Validation 전략 설계

---

# Future Improvements

- [ ] 실시간 기상 API 연동
- [ ] 지역 확장 학습 (Multi-region Generalization)
- [ ] Transformer 기반 시계열 모델 실험
- [ ] 실시간 예측 Dashboard 구축
- [ ] AutoML 파이프라인 적용

---

⚠ Note

상용 서비스 목적이 아닌 에너지 데이터 분석 및 머신러닝 모델링 역량 향상을 목표로 제작되었습니다.
