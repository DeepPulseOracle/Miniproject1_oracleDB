# ICU Clinical Time-Series Analysis Project 🏥

**MIMIC-IV** 데이터를 활용하여 ICU 환자의 예후(사망률)를 예측하는 AI 파이프라인입니다.
불규칙한 시계열 데이터를 처리하는 **Deep Learning 모델**을 제안하며, Boosting 계열(XGBoost) 모델과 성능을 비교합니다.

![Model Architecture](gpraph_1.png)

## 📂 Code Structure

전체 파이프라인은 **데이터 구축 → 모델 학습 → 검증 및 해석** 순서로 구성됩니다.

| Step | File Name | Description |
| :--- | :--- | :--- |
| **1. Data** | **`Cohort_build.ipynb`** | SQL을 통한 환자군(Cohort) 정의 및 Raw Data 전처리 (CSV 생성) |
| | **`Dataset_EDA.ipynb`** | 데이터 기초 통계, 관측 간격(Time-step) 및 결측치 패턴 분석 |
| **2. DL** | **`MainModel.ipynb`** | **[핵심]** 시계열 딥러닝 모델 학습, Loss 추이 및 생존/사망 패턴 예측 |
| **3. ML** | **`Comparison_model.ipynb`** | Baseline 모델(XGBoost, RF) 학습 및 성능 비교 (Permutation Importance) |
| | `Comparison(Boosting)_EDA.ipynb` | ML 모델 학습을 위한 추가 Feature Engineering 및 분석 |
| **4. Val** | **`Validation_pipeline.ipynb`** | 최종 모델 검증 및 **SHAP** 기반 변수 중요도(Feature Importance) 해석 |

## 🛠 Environments
* **Data**: MIMIC-IV Database (Access Required)
* **Stack**: Python, PyTorch, XGBoost, SHAP, Pandas

## 🚀 How to Run
1.  `Cohort_build.ipynb` 실행 (Dataset 생성)
2.  `MainModel.ipynb` 실행 (제안 모델 학습)
3.  `Validation_pipeline.ipynb` 실행 (결과 해석 및 시각화)
