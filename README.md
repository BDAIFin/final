# 💳 BDAI-Fin  
### Financial Transaction Fraud Detection

본 프로젝트는 **금융 결제(Transaction) 데이터**를 기반으로  
**사기 거래(Fraud Transaction)를 탐지하는 데이터 사이언스 프로젝트**입니다.

극심한 클래스 불균형과 시간 누수(Temporal Leakage) 문제를 핵심 난제로 삼아,  
**실무 환경에 가까운 EDA · Feature Engineering · Modeling 파이프라인 구축**을 목표로 합니다.

---

## 📌 Project Overview

| 항목 | 내용 |
|---|---|
| 프로젝트 성격 | 금융 결제 Fraud Detection |
| 분석 단위 | Transaction (거래 단위) |
| 핵심 난이도 | 극심한 클래스 불균형, 시간 누수 |
| 활용 분야 | 금융 데이터 분석, 이상 거래 탐지 |
| 프로젝트 목적 | 실무형 데이터 사이언스 역량 강화 |

---

## 📂 Repository Structure

```text
bdai-fin/
├── README.md                   # 프로젝트 전체 설명
│
├── data/
│   └── DATA_DESCRIPTION.md     # 데이터 구조 및 컬럼 설명
│
├── notebooks/
│   ├── EDA/                    # 탐색적 데이터 분석 노트북
│   └── modeling/               # 모델링 및 평가 노트북
│
├── src/                        # 전처리 / 피처 엔지니어링 / 모델 코드
└── reports/                    # 분석 결과, 시각화, 정리 문서
````

---

## 📊 Dataset

본 프로젝트는 Kaggle에서 제공하는 **실제 금융 거래 기반 Fraud Detection 데이터셋**을 사용합니다.

### 🔗 Original Dataset (Kaggle)

[https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets](https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets)

⚠️ **GitHub 파일 크기 제한(25MB)**으로 인해
원본 데이터(CSV/JSON)는 본 레포지토리에 포함되어 있지 않습니다.

데이터 구조 및 컬럼 설명은 아래 문서에 정리되어 있습니다.

📘 **Data Description**
→ `data/DATA_DESCRIPTION.md`

---

## 📥 Data Setup

1. Kaggle 링크에서 데이터셋 다운로드
2. 로컬 환경에서 데이터 로드
3. 노트북 실행 시 로컬 경로에 맞게 불러오기

> 데이터 파일명 및 컬럼 구조는
> `data/DATA_DESCRIPTION.md`를 기준으로 합니다.

---

## 🧠 Key Challenges

### 1️⃣ Extreme Class Imbalance

* Fraud 거래 비율이 극히 낮음
* Accuracy 중심 평가는 부적절
* **Recall / Precision / PR-AUC 중심 평가 필요**

### 2️⃣ Temporal Leakage

* 거래 시점 이후 정보 사용 금지
* 시간 순서를 고려한 Split 및 Feature 설계 필수

---

## 🔍 Analysis & Modeling Flow

1. **EDA**

   * 거래 금액, 빈도, 시간 패턴 분석
   * Fraud vs Non-Fraud 비교 분석

2. **Feature Engineering**

   * 고객 / 카드 / 거래 단위 파생 변수 생성
   * 시간 기반 Feature (Recency, Frequency 등)

3. **Modeling**

   * Baseline: Logistic Regression
   * Tree-based Models (RandomForest, XGBoost 등)

4. **Evaluation**

   * PR-AUC, Recall 중심 성능 비교
   * Threshold 기반 해석

---

## 🛠️ Tech Stack

* **Language**: Python
* **Libraries**: pandas, numpy, scikit-learn
* **Environment**: Jupyter Notebook

---

## 👥 Team Members

* 김나경
* 김채현
* 김형준
* 정준우

각 팀원의 개별 실험 및 분석 내용은
각자 이름의 repository에서 관리합니다.

---

## 📌 Notes

* 본 프로젝트는 **교육 및 학습 목적**으로 진행됩니다.
* 데이터의 출처 및 라이선스는 Kaggle 원본을 따릅니다.

---

## 🚀 Future Work

* 클래스 불균형 처리 고도화
* 거래 시퀀스 기반 Feature 확장
* 실시간 Fraud Detection 시뮬레이션

```
