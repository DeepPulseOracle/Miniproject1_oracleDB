# ICU Clinical Time-Series Analysis Project 🏥

이 프로젝트는 ICU(중환자실) 환자의 임상 데이터를 기반으로 사망률 및 예후를 예측하는 AI 모델 개발 파이프라인입니다. **MIMIC-IV** 데이터를 활용하여 코호트를 구축하고, 시계열 Deep Learning 모델(Main Model)과 머신러닝 Boosting 모델 간의 성능을 비교 분석합니다.

## 📋 Project Pipeline

전체 프로젝트는 데이터 추출부터 모델 검증까지 아래와 같은 흐름으로 진행됩니다.

1.  **Cohort Generation**: Raw Data(MIMIC-IV)에서 필요한 환자군 및 변수 추출
2.  **Data EDA**: 데이터 분포, 결측치, Time-step 간격 확인
3.  **Main Model Training**: 제안하는 시계열 딥러닝 모델 학습 및 평가
4.  **Comparison Model**: Boosting 계열(XGBoost 등) 모델과 성능 비교
5.  **Validation & XAI**: 최종 모델 검증 및 중요 변수 해석(SHAP)

![Model Overview](image_51f269.png)
*(프로젝트의 주요 아키텍처 또는 결과 그래프)*

---

## 📂 File Description

각 파일은 파이프라인의 특정 단계를 담당합니다.

### 1. Data Processing
- **`Cohort_build.ipynb`**
  - SQL 쿼리를 활용하여 원본 데이터베이스에서 타겟 환자군(Cohort)을 정의하고 추출합니다.
  - 환자별 시계열 데이터(Vital Sign, Lab test 등)를 전처리하여 학습용 데이터셋(CSV)으로 변환합니다.

- **`Dataset_EDA.ipynb`**
  - 구축된 데이터셋의 기초 통계량을 분석합니다.
  - 관측 기간(Window hours), 측정 간격(Delta time) 분포 시각화 및 결측치 패턴을 확인합니다.

### 2. Deep Learning (Proposed Approach)
- **`MainModel.ipynb`**
  - 본 프로젝트의 핵심인 **시계열 딥러닝 모델**의 학습 및 추론 코드가 포함되어 있습니다.
  - Time-series 데이터의 불규칙성을 처리하고, 사망/생존 환자의 임상 특징을 학습하여 예측을 수행합니다.
  - 모델의 Loss 추이 및 실제 관측값 대비 예측 결과를 시각화합니다.

### 3. Comparison & Baseline
- **`Comparison_model.ipynb`**
  - Main Model과의 성능 비교를 위한 머신러닝 모델(XGBoost, Random Forest 등)을 학습합니다.
  - Permutation Importance 등을 통해 ML 모델 관점에서의 주요 변수를 확인합니다.
  
- **`Comparison(Boosting)_EDA.ipynb`**
  - Boosting 모델 학습을 위한 전용 데이터 분석 및 Feature Engineering 과정을 담고 있습니다.

### 4. Evaluation
- **`Validation_pipeline.ipynb`**
  - 학습된 모델들의 최종 검증 파이프라인입니다.
  - **SHAP (SHapley Additive exPlanations)** 값을 계산하여 모델이 예측에 중요하게 활용한 임상 변수(Feature Importance)를 해석하고 시각화합니다.

---

## 🛠 Tech Stack & Requirements

- **Language**: Python 3.x
- **Data Source**: MIMIC-IV Database
- **Libraries**:
  - Data: `pandas`, `numpy`, `scipy`
  - DL/ML: `PyTorch` (or `TensorFlow`), `scikit-learn`, `xgboost`
  - Visualization: `matplotlib`, `seaborn`, `shap`

## 🚀 How to Run

1. `Cohort_build.ipynb`를 실행하여 데이터셋을 생성합니다. (사전 DB 접근 권한 필요)
2. `MainModel.ipynb`를 실행하여 딥러닝 모델을 학습합니다.
3. `Comparison_model.ipynb`를 통해 베이스라인 모델 성능을 측정합니다.
4. `Validation_pipeline.ipynb`에서 결과를 시각화하고 해석합니다.

---
