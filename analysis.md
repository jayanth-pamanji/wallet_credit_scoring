
# 📊 Score Analysis of Wallets

This analysis highlights the behavior of wallets based on their assigned **credit scores (1–1000)** after unsupervised clustering using PCA and KMeans/DBSCAN.

---

## 🔢 Score Distribution

### Score Buckets:
| Score Range | Wallet Count |
| ----------- | ------------- |
| 1 - 100     |           757 |
| 101 - 200   |           471 |
| 201 - 300   |           467 |
| 301 - 400   |           396 |
| 401 - 500   |           305 |
| 501 - 600   |           304 |
| 601 - 700   |           297 |
| 701 - 800   |           286 |
| 801 - 900   |           138 |
| 901 - 1000  |            76 |

---

## 💲 Behavior of Low-Scoring Wallets (0–300)

- Minimal or no activity
- Mostly `redeemunderlying`, occasional `liquidationcall`
- Very low transaction volume
- No signs of consistent engagement with Aave
- Often considered noisy or one-off wallets

---

## 📈 Behavior of High-Scoring Wallets (700–1000)

- Active on multiple days
- Consistent use of `deposit`, `borrow`, `repay`
- Strong behavioral consistency in volume and timing
- No liquidation events
- Likely long-term users of the protocol

---

## 📊 Insights

- Majority of wallets fall in lower score buckets (due to inactivity)
- Higher scoring wallets demonstrate deeper integration with Aave
- DBSCAN detected 300+ wallets as noise (score ~0)
- Scores help filter trustworthy vs inactive wallets for further DeFi analysis
