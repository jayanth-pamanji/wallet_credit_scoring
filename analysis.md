

# 📊 Score Analysis of Wallets

This analysis highlights the behavior of wallets based on their assigned **credit scores (1–1000)** after unsupervised clustering using PCA and KMeans/DBSCAN.

---
<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/c6b16472-3b08-49e3-b821-f04e26e5e477" />

<img width="1989" height="590" alt="image" src="https://github.com/user-attachments/assets/35112b66-bce2-4ec7-8694-df5609e2874b" />

<img width="850" height="547" alt="image" src="https://github.com/user-attachments/assets/d9241978-8be0-417a-ae7f-39f10b0e997a" />


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
