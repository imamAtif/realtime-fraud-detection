# 🚀 Real-Time Fraud Detection System
### 1.  How we will detect Fraud?
> Rule Based Approach

### 🛡️ Fraud Rules
| Rule | Example Fraud Scenario |
|------|------------------------|
| **High Amount Rule** | 🚨 If a transaction is ₹1,00,000+, flag it. |
| **Multiple Transactions Rule** | 🚨 If 3+ transactions happen in 1 minute, flag it. |
| **Different Locations Rule** | 🚨 If a user makes two transactions from two different countries in 10 min, flag it. |
| **Unusual Device Rule** | 🚨 If a transaction happens from a new device, flag it. |
| **Velocity Rule** | 🚨 If multiple failed login attempts occur, flag it. |



---

## 🏗️ System Architecture
```
                         ┌──────────────────────────┐
                         │    🏦User Transaction   │
                         │    (Credit/Debit Card)   │
                         └──────────┬────────────── ┘
                                    │  
                                    ▼  
                        ┌──────────────────────────┐
                        │    Kafka Transactions    │
                        │    (transactions-topic)  │
                        └──────────┬──────────────┘
                                    │  
                                    ▼  
                        ┌──────────────────────────┐
                        │  Fraud Detection Engine  │
                        │  (Faust Kafka Streams)   │
                        └──────────┬──────────────┘
                                    │  
                        ┌───────────┴────────────┐
                        ▼                        ▼
         ┌──────────────────────┐    ┌──────────────────────┐
         │  ✅ Normal Txn (Pass) │    │  🚨 Fraud Txn (Flag) │
         │   (Ignored)           │    │   (fraud-alerts-topic)│
         └──────────────────────┘    └──────────┬───────────┘
                                               ▼  
                         ┌──────────────────────────┐
                         │    PostgreSQL Database   │
                         │ (Store flagged fraud Txn)│
                         └──────────┬──────────────┘
                                    ▼  
                      ┌────────────────────────────┐
                      │  🖥️ Fraud Monitoring API   │
                      │  (FastAPI / Streamlit)     │
                      └────────────────────────────┘
```