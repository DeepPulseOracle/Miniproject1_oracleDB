# 🏥 Medical FTR Risk Prediction & Real-time Monitoring System

> **MIMIC-IV 데이터를 활용한 중환자실(ICU) 내 FTR 리스크 예측 및 실시간 모니터링 파이프라인**

본 프로젝트는 환자의 급격한 상태 악화(Failure To Rescue, FTR)를 방지하기 위해, 시계열 데이터의 결측치를 Diffusion 모델로 보정하고 RNN 기반으로 리스크를 예측하여 의료진에게 실시간 알람과 해석(XAI)을 제공하는 엔드 투 엔드 시스템입니다.

---

## 🏗 System Architecture Pipeline
![System Architecture](Source/pipeline.png)


---

## 📋 Pipeline Steps

### 1. 코호트 정의 및 데이터 수집 (Cohort & Data)
* **Dataset:** MIMIC-IV (ICU 입실 에피소드 기준)
* **Criteria:** 연령, 입원 기간, 데이터 결측률 등 Inclusion/Exclusion 적용
* **Extraction:** Vital signs, Lab, 인구학 정보, 중재(Intervention) 정보 테이블 조인 및 시계열 구조화

### 2. 전처리 및 동적 임퓨테이션 (Preprocessing & Imputation)
* **Sampling:** 5분/1시간 단위 리샘플링 및 이상치(Outlier) 제거
* **Method:** Forward filling 대비 **Diffusion 기반 Generative Dynamic Imputation** 성능 검증
* **Feature:** 마스킹 벡터(Masking Vector)를 생성하여 결측 패턴 학습 반영

### 3. 피처 엔지니어링 및 베이스라인 (Feature & ML)
* **Statistics:** 초기 24시간 요약 통계 및 최근 윈도우 기반 트렌드 피처 생성
* **Scores:** APACHE II, SOFA, NEWS 등 기존 의료 스코어 계산
* **Baseline:** XGBoost, LightGBM, Random Forest를 통한 임상적 유의성 평가 (AUROC/AUPRC)

### 4. End-to-End RNN 및 디퓨전 모델 (Modeling)
* **Architecture:** LSTM/GRU 기반 시계열 모델 설계
* **Optimization:** 임퓨테이션 모델과 예측 모델의 **Joint Optimization** 수행
* **Target:** FTR 리스크(환자 악화) 발생 예측

### 5. XAI 모델 해석 (Explainable AI)
* **Global/Local:** SHAP을 활용한 모델의 의사결정 근거 분석
* **Temporal SHAP:** 시간 흐름에 따라 어떤 변수가 리스크 상승에 기여했는지 시각화
* **Validation:** 의료진이 신뢰할 수 있는 해석 가능성(Interpretability) 검증

### 6. 실시간 파이프라인 및 API (Real-time Backend)
* **Tech:** FastAPI + SQLAlchemy (DAO Pattern)
* **Engine:** 5초 단위 데이터 스트리밍 시뮬레이션 파이프라인
* **Interface:** 실시간 리스크 스코어 및 XAI 데이터 제공 REST API

### 7. 웹 UI 및 스마트 트리아지 (Frontend & Dashboard)
* **Tech:** TypeScript, React, Tailwind CSS, Vite
* **Features:** * 환자별 실시간 리스크 트렌드 차트
  * 고위험군 우선순위 자동 정렬(Smart Triage)
  * 위험 징후 포착 시 Push 알람 및 처치 권고 UI

---

## 🛠 Tech Stack

| Category | Details |
| :--- | :--- |
| **Language** | Python 3.10+, TypeScript |
| **Data/ML** | PyTorch, Pandas, Scikit-learn, SHAP |
| **Backend** | FastAPI, PostgreSQL/SQLite |
| **Frontend** | React, Recharts, Tailwind CSS |
| **Environment** | Docker, Git |

---

## 📅 Project Roadmap (WBS)

1. [ ] Phase 1: Data ETL & Cohort Study
2. [ ] Phase 2: Diffusion Imputation Model Development
3. [ ] Phase 3: Risk Prediction Model & XAI Integration
4. [ ] Phase 4: Real-time API & Dashboard Prototype
5. [ ] Phase 5: System Evaluation & Performance Optimization
