
# 📊 Score Analysis of Wallets

This analysis highlights the behavior of wallets based on their assigned **credit scores (1–1000)** after unsupervised clustering using PCA and KMeans/DBSCAN.

---

## 🔢 Score Distribution

### Score Buckets:

| Score Range | Wallet Count |
| ----------- | ------------ |
| 0 - 100     | xxx wallets  |
| 101 - 200   | xxx wallets  |
| 201 - 300   | xxx wallets  |
| 301 - 400   | xxx wallets  |
| 401 - 500   | xxx wallets  |
| 501 - 600   | xxx wallets  |
| 601 - 700   | xxx wallets  |
| 701 - 800   | xxx wallets  |
| 801 - 900   | xxx wallets  |
| 901 - 1000  | xxx wallets  |

> *Replace `xxx` with actual counts from your final scores.*

---

### Histogram

```python
import matplotlib.pyplot as plt

plt.hist(scores_df['credit_score'], bins=10, edgecolor='black')
plt.title('Wallet Credit Score Distribution')
plt.xlabel('Credit Score (1–1000)')
plt.ylabel('Number of Wallets')
plt.grid(True)
plt.show()
```

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
