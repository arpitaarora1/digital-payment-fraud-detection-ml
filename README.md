# Digital Payment Fraud Detection using Machine Learning

An end-to-end **Machine Learning fraud detection system for digital payments**, developed using a synthetic transaction dataset and modelled around a PhonePe-inspired digital payment risk environment.

The project demonstrates how transaction-level behavioural and risk signals can be processed through a supervised Machine Learning pipeline to identify potentially fraudulent transactions and convert model predictions into actionable risk categories.

> **Disclaimer:** This is an academic project using a synthetic, programmatically generated dataset. It is not affiliated with, endorsed by, or based on proprietary PhonePe data and does not represent PhonePe's actual fraud detection system.

---

## Overview

Digital payment platforms operate at high transaction volumes, creating the need for automated systems capable of identifying suspicious activity while minimizing unnecessary friction for genuine customers.

This project addresses the following business problem:

**How can Machine Learning help identify potentially fraudulent digital payment transactions while allowing legitimate transactions to proceed smoothly?**

The solution uses transaction characteristics such as transaction amount, account age, device changes, recipient changes, failed attempts, location changes, and transaction frequency to classify transactions as genuine or potentially fraudulent.

---

## Solution Architecture

```text
Synthetic Transaction Data
          ↓
Data Quality & Exploration
          ↓
Feature Preparation
          ↓
Train / Test Split
          ↓
Random Forest Classifier
          ↓
Fraud Probability
          ↓
Model Evaluation
          ↓
Risk Classification
          ↓
Approve / Verify / Block
```

---

## Machine Learning Model

### Random Forest Classifier

A **Random Forest Classifier** was selected for the project because it can model non-linear relationships and provides feature-importance information that can help explain model behaviour.

### Configuration

| Parameter            |                    Value |
| -------------------- | -----------------------: |
| Model                | Random Forest Classifier |
| Number of Estimators |                      150 |
| Maximum Depth        |                       12 |
| Class Weight         |                 Balanced |
| Random State         |                       42 |

The dataset was divided into **80% training and 20% testing data**, with stratified sampling used to preserve the class distribution.

---

## Dataset

The project uses a **synthetic dataset containing 10,000 transactions**.

### Key Features

| Feature                  | Description                               |
| ------------------------ | ----------------------------------------- |
| `transaction_amount`     | Transaction value                         |
| `transactions_last_24h`  | Number of recent transactions             |
| `account_age_days`       | Age of the account                        |
| `new_device`             | Whether a new device was used             |
| `new_recipient`          | Whether the recipient is unfamiliar       |
| `location_change`        | Whether the transaction location changed  |
| `failed_attempts`        | Previous failed attempts                  |
| `night_transaction`      | Whether the transaction occurred at night |
| `previous_fraud_reports` | Previous fraud reports                    |
| `is_fraud`               | Target variable                           |

The dataset contains **7,436 genuine transactions and 2,564 fraudulent transactions**, with no missing values or duplicate records reported in the project.

---

## Model Performance

The model was evaluated on an unseen test set of 2,000 transactions.

| Metric          | Result |
| --------------- | -----: |
| Accuracy        | 80.05% |
| ROC-AUC         | 0.8101 |
| Fraud Precision |    62% |
| Fraud Recall    |    57% |
| Fraud F1-Score  |    59% |

The confusion matrix recorded 1,308 correctly identified genuine transactions, 293 correctly identified fraudulent transactions, 179 false positives, and 220 false negatives.

---

## Feature Importance

The trained model identified the following relative feature importance:

| Rank | Feature                  | Importance |
| ---: | ------------------------ | ---------: |
|    1 | Transaction Amount       |      46.9% |
|    2 | Account Age              |      17.0% |
|    3 | Transactions in Last 24h |       8.7% |
|    4 | Failed Attempts          |       8.2% |
|    5 | Previous Fraud Reports   |       5.2% |
|    6 | New Recipient            |       4.0% |
|    7 | Location Change          |       3.8% |
|    8 | New Device               |       3.7% |
|    9 | Night Transaction        |       2.5% |

Transaction amount and account age were the two most influential features in this synthetic dataset.

---

## Risk Decision Framework

The model's predicted fraud probability is translated into a three-level operational framework:

```text
Fraud Probability
       │
       ├── < 30% ─────── LOW RISK
       │                    ↓
       │                 APPROVE
       │
       ├── 30–70% ───── MEDIUM RISK
       │                    ↓
       │                 VERIFY
       │
       └── > 70% ────── HIGH RISK
                            ↓
                     BLOCK / INVESTIGATE
```

The thresholds are **illustrative academic thresholds** and do not represent PhonePe's proprietary decisioning logic.

---

## Example Predictions

The model was tested using contrasting synthetic transaction scenarios.

### High-Risk Scenario

A transaction involving:

* High transaction amount
* New device
* New recipient
* Location change
* Multiple failed attempts
* Night-time transaction
* Newly created account
* High transaction frequency

produced a fraud probability of **81.33%** and was classified as **High Risk — Block / Investigate**.

### Low-Risk Scenario

A transaction involving an established device and recipient, no location change, no failed attempts, an older account, and low transaction frequency produced a fraud probability of **9.68%** and was classified as **Low Risk — Approve**.

---

## AI-Assisted Research

The project also includes a **Prompt Portfolio & AI-Assisted Research** component.

Generative AI tools were used for different stages of the research workflow:

* **ChatGPT** — ML concept understanding
* **Claude** — Research structuring and synthesis
* **Perplexity** — Source discovery and cross-referencing
* **Gemini** — Research-question refinement

The research process emphasizes using AI as an assistant rather than treating generated information as automatically reliable.

---

## Prompt Engineering

The project documents the improvement of a basic research prompt into a more structured prompt.

### Basic

```text
Tell me about AI in PhonePe.
```

### Improved

The refined approach specified:

* A fintech analyst role
* Specific AI/ML use cases
* Business benefits
* Risks and regulatory concerns
* Named sources
* Clear distinction between confirmed information and inference

This produced more targeted and verifiable research output.

---

## Verification & Fact-Checking

Fast-changing business information was treated as provisional until verified.

The project documents verification of AI-generated claims using dated public sources and company leadership statements. It also identifies an example where AI presented changing valuation and UPI market-share figures without sufficient time context.

The improved research process required:

1. Dating every time-sensitive figure.
2. Naming the source.
3. Using ranges where appropriate.
4. Manually checking important claims against external sources.
5. Avoiding unsupported, undated statistics.

---

## Repository Structure

```text
digital-payment-fraud-detection-ml/
│
├── Copy_of_PhonePe_AI_Fraud_Detection_Model.ipynb
├── PhonePe_Fraud_Detection_Dataset.csv
├── PhonePe_Fraud_Detection_Case_Study.docx
├── PhonePe_Part_B_Prompt_Portfolio.docx
└── README.md
```

### Project Files

**`Copy_of_PhonePe_AI_Fraud_Detection_Model.ipynb`**
Machine Learning notebook containing the fraud detection workflow.

**`PhonePe_Fraud_Detection_Dataset.csv`**
Synthetic transaction dataset used to train and evaluate the model.

**`PhonePe_Fraud_Detection_Case_Study.docx`**
Detailed business case study covering the problem, methodology, results, recommendations, and limitations.

**`PhonePe_Part_B_Prompt_Portfolio.docx`**
AI-assisted research documentation containing prompts, prompt improvement, AI tools, verification, and critical evaluation.

---

## Technology Stack

```text
Python
│
├── Pandas
├── NumPy
├── Scikit-learn
└── Matplotlib

Development Environment
└── Google Colab

AI Research
├── ChatGPT
├── Claude
├── Perplexity
└── Gemini
```

---

## Key Takeaways

* Machine Learning can be applied to transaction-level fraud classification.
* Behavioural and transaction signals can contribute to fraud-risk assessment.
* Random Forest provides both classification output and feature-importance information.
* Fraud detection requires balancing false positives against false negatives.
* Model predictions can be translated into operational risk categories.
* AI-generated business research requires source verification and time-context checks.
* Synthetic-data performance should not be interpreted as production performance.

---

## Limitations

This project is an academic demonstration and should not be considered a production fraud-detection system.

Key limitations include:

* Synthetic rather than real transaction data
* Illustrative risk thresholds
* Limited feature set
* No production-scale infrastructure
* No real-time transaction stream
* No direct integration with payment infrastructure
* Synthetic-data performance cannot guarantee equivalent performance on real-world data

Real-world fraud prevention can involve multiple layers such as Machine Learning, rule engines, device intelligence, graph analysis, and human review.

---

## Future Enhancements

Potential future development areas include:

* Real-time transaction scoring
* Device fingerprinting
* IP and geolocation velocity features
* Merchant-category analysis
* Transaction-network graph features
* Model calibration
* Continuous retraining
* Rule-based + ML hybrid detection
* Human-in-the-loop investigation workflows
* Advanced fraud detection algorithms

These improvements are aligned with the recommendations documented in the project case study.

---

## Academic Context

**Program:** BBA FinTech & AI
**Project:** AI-Powered Fraud Detection for Digital Payments
**Focus Company:** PhonePe
**Industry:** FinTech / Digital Payments
**Project Team:** Ayushi, Angel, Arshita, Arpita, Ankita, Aniketa & Anchit

---

## Conclusion

This project demonstrates an end-to-end Machine Learning workflow for digital payment fraud detection — from synthetic data preparation and preprocessing to model training, evaluation, prediction, and risk-based decisioning.

It combines **Machine Learning, business problem solving, risk analysis, and AI-assisted research** into a single academic project while highlighting the importance of explainability, verification, and responsible interpretation of AI-generated information.
