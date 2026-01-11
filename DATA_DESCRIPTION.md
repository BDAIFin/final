Due to GitHub file size limits, the full dataset **is not included** in this repository.

You can download the dataset from Kaggle:

👉 https://www.kaggle.com/datasets/computingvictor/transactions-fraud-datasets

---

# 📊 Dataset Overview

| 항목      | 내용                                        |
| ------- | ----------------------------------------- |
| 프로젝트 성격 | 금융 결제 **Fraud Detection**                 |
| 분석 단위   | Transaction (거래 단위)                       |
| 핵심 난이도  | **극심한 클래스 불균형 + 시간 누수(Temporal Leakage)** |
| 실무 적합성  | 높음                                        |
| 재사용성    | 데이터 구조 유지 시 재활용 가능                        |

---

## 📁 Data Structure

```text
├── users_data.csv              # 고객 단위 정보
├── cards_data.csv              # 카드 단위 메타데이터
├── transactions_data.csv       # 거래 단위 로그
├── mcc_codes.json              # 가맹점 업종 코드북
└── train_fraud_labels.json     # 거래 단위 사기 라벨
```

---

## 🧑 users_data.csv

> 고객(사용자) 단위의 인구통계·소득·부채·신용 정보를 담은 테이블
> 카드 및 거래 데이터의 기준 테이블

| 컬럼명                 | 타입     | 설명                      |
| ------------------- | ------ | ----------------------- |
| `id`                | int    | 고객 고유 식별자 (Primary Key) |
| `current_age`       | int    | 현재 나이                   |
| `retirement_age`    | int    | 은퇴 예정 나이                |
| `birth_year`        | int    | 출생 연도                   |
| `birth_month`       | int    | 출생 월 (1–12)             |
| `gender`            | object | 성별 (Female / Male)      |
| `address`           | object | 주소 문자열                  |
| `latitude`          | float  | 거주지 위도                  |
| `longitude`         | float  | 거주지 경도                  |
| `per_capita_income` | object | 1인당 소득 (`$` 포함 문자열)     |
| `yearly_income`     | object | 연 소득 (`$` 포함 문자열)       |
| `total_debt`        | object | 총 부채 (`$` 포함 문자열)       |
| `credit_score`      | int    | 신용 점수                   |
| `num_credit_cards`  | int    | 보유 신용카드 수               |

---

## 💳 cards_data.csv

> 카드 단위 메타데이터
> **한 명의 고객(`client_id`)은 여러 장의 카드를 보유 가능**

| 컬럼명                     | 타입     | 설명                                |
| ----------------------- | ------ | --------------------------------- |
| `id`                    | int    | 카드 고유 식별자 (Primary Key)           |
| `client_id`             | int    | 카드 소유 고객 ID (`users_data.csv.id`) |
| `card_brand`            | object | 카드 브랜드 (Visa, Mastercard, Amex 등) |
| `card_type`             | object | 카드 유형 (Debit, Credit, Prepaid)    |
| `card_number`           | int    | 카드 번호 (16자리)                      |
| `expires`               | object | 카드 만료일 (MM/YYYY)                  |
| `cvv`                   | int    | 카드 보안 코드                          |
| `has_chip`              | object | IC 칩 탑재 여부 (YES / NO)             |
| `num_cards_issued`      | int    | 해당 계좌에서 발급된 카드 수                  |
| `credit_limit`          | object | 카드 한도 금액 (`$` 포함 문자열)             |
| `acct_open_date`        | object | 계좌 개설일 (MM/YYYY)                  |
| `year_pin_last_changed` | int    | PIN 마지막 변경 연도                     |
| `card_on_dark_web`      | object | 다크웹 유출 여부 (Yes / No)              |

---

## 🧾 transactions_data.csv

> 카드 결제 및 승인 시도 단위의 **핵심 거래 로그 테이블**
> 시간·금액·결제 방식·가맹점·에러 정보 포함

| 컬럼명              | 타입     | 설명                             |
| ---------------- | ------ | ------------------------------ |
| `id`             | int    | 거래 고유 식별자 (Transaction ID)     |
| `date`           | object | 거래 시각 (YYYY-MM-DD HH:MM:SS)    |
| `client_id`      | int    | 거래 고객 ID                       |
| `card_id`        | int    | 사용 카드 ID (`cards_data.csv.id`) |
| `amount`         | object | 거래 금액 (`$` 포함, 음수는 환불/취소)      |
| `use_chip`       | object | 결제 방식 (Swipe / Chip / Online)  |
| `merchant_id`    | int    | 가맹점 ID                         |
| `merchant_city`  | object | 가맹점 도시                         |
| `merchant_state` | object | 가맹점 주 / 국가 코드                  |
| `zip`            | float  | 가맹점 우편번호                       |
| `mcc`            | int    | 가맹점 업종 코드 (MCC)                |
| `errors`         | object | 거래 실패 또는 승인 거절 사유              |

---

## 🏪 mcc_codes.json

> `transactions_data.csv.mcc`를 **업종명(Category)** 으로 매핑하는 코드북

* **Key**: MCC 코드 (문자열)
* **Value**: 업종 설명 (영문)

| 항목       | 타입     | 예시                                | 설명    |
| -------- | ------ | --------------------------------- | ----- |
| MCC Code | string | `"5812"`                          | 업종 코드 |
| Category | string | `"Eating Places and Restaurants"` | 업종명   |

```json
{
  "5812": "Eating Places and Restaurants",
  "5541": "Service Stations",
  "7996": "Amusement Parks, Carnivals, Circuses"
}
```

---

## 🚨 train_fraud_labels.json

> 거래 단위 **Fraud 정답 라벨**
> 학습 시 `transactions_data.csv.id`와 매칭하여 사용

* **Key**: Transaction ID
* **Value**: `"Yes"` / `"No"`

```json
{
  "14794212": "No",
  "13803632": "Yes"
}
```

### ⚠️ Target Imbalance

| Label | Count     |
| ----- | --------- |
| No    | 8,901,631 |
| Yes   | 13,332    |

👉 **극심한 불균형 데이터**로,
Resampling / Cost-sensitive learning / PR-AUC 중심 평가 필요

---
