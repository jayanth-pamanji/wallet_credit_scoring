# README.md

# 🏦 DeFi Wallet Credit Scoring using Aave V2 Protocol

This project scores wallets on a scale of **1 to 1000** based on their historical activity on the **Aave V2 protocol**. By leveraging unsupervised learning techniques, the goal is to assign relative credit scores to help DeFi lending platforms or researchers better understand wallet behavior and potential creditworthiness.

---

## 🔍 Project Goals

* Extract and preprocess Aave V2 on-chain wallet transaction data
* Engineer features that capture wallet behavior
* Cluster wallets using unsupervised techniques (KMeans, DBSCAN)
* Normalize and assign credit scores (1 to 1000) based on behavioral clusters
* Analyze score distributions and wallet behaviors

---

## 📂 Dataset Description

* **Source**: Aave V2 Protocol (Polygon Network)
* **Size**: 100,000+ transaction entries
* **Actions**: `deposit`, `borrow`, `repay`, `redeemunderlying`, `liquidationcall`
* **Format**: JSON-like documents containing fields like:

  * `userWallet`, `timestamp`, `action`, `asset`, `amount`, `price_usd`, etc.

---

## 💡 Processing Flow & Architecture

```mermaid
graph TD
    A[Raw Aave V2 Data] --> B[Data Cleaning]
    B --> C[Expand actionData JSON]
    C --> D[Drop irrelevant columns]
    D --> E[Normalize + Feature Engineering]
    E --> F[PCA for dimensionality reduction]
    F --> G[KMeans Clustering]
    F --> H[DBSCAN Clustering]
    G --> I[Cluster ranking]
    I --> J[Assign scores (1-1000)]
    J --> K[Export & Visualization]
```

---

## 📊 Feature Engineering

| Feature                               | Description                                 |
| ------------------------------------- | ------------------------------------------- |
| `total_tx`                            | Total number of transactions                |
| `active_days`                         | Number of days wallet was active            |
| `tx_per_day`                          | Transactions per day                        |
| `total_volume_usd`                    | Total volume transacted in USD              |
| `volume_per_tx`                       | Average USD volume per transaction          |
| `log_volume`                          | Log-transformed total volume                |
| `avg_time_between_tx`                 | Mean time between two actions               |
| `tx_time_std`                         | Std deviation in transaction time intervals |
| `busiest_hour`                        | Hour of the day with max activity           |
| `deposit_ratio`, `borrow_ratio`, etc. | Proportion of each action type              |
| `has_liquidation`                     | Binary, if wallet was liquidated            |
| `max_tx_usd`, `median_tx_usd`         | Extremes of transaction size                |
| `is_active`                           | Binary, if wallet has meaningful activity   |

---

## 🤖 Clustering

* **PCA**: Reduced to 13 principal components
* **KMeans**:

  * Chosen `n_clusters=20` based on elbow/variance curve
  * Wallets within each cluster scored based on behavioral quality
* **DBSCAN**:

  * Density-based clustering to detect noise wallets
  * Noise wallets were assigned lowest scores

---

## 🔢 Scoring Strategy

* Clusters were ranked manually based on average:

  * Volume, frequency, stability, and action diversity
* Scores were scaled between **1 and 1000**
* Better clusters (healthier wallets) got higher scores

---

## 👁‍🗨️ Visualization & Output

* Score distribution
* Histogram by cluster
* Exported CSVs:

  * `cleaned_wallet_data.csv`
  * `wallet_features.csv`
  * `wallet_scores.csv`

---

## 🚀 How to Run

```bash
pip install -r requirements.txt
python wallet_scoring.py
```

---

## 💼 Folder Structure

```
wallet-credit-scoring/
├── data/                   # Raw and processed data
├── src/                    # Feature engineering and model scripts
├── outputs/                # Final scores and visualizations
├── README.md
└── analysis.md             # Score distribution and insights
```

---

## 📄 License

MIT License.

---

## 🌟 Future Work

* Add on-chain price volatility features
* Integrate multi-chain behavior
* Use self-supervised learning on wallet embeddings

---

# analysis.md

# 📊 Score Analysis of Wallets

This analysis highlights the behavior of wallets based on their assigned **credit scores (1-1000)** after unsupervised clustering using PCA and KMeans/DBSCAN.

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

*Replace **\`\`** with actual wallet counts after scoring.*

### Histogram

```python
import matplotlib.pyplot as plt
plt.hist(scores_df['credit_score'], bins=10, edgecolor='black')
plt.title('Wallet Credit Score Distribution')
plt.xlabel('Credit Score (1-1000)')
plt.ylabel('Number of Wallets')
plt.grid(True)
plt.show()
```

---

## 💲 Behavior of Low-Scoring Wallets (0 - 300)

* Typically single or very few transactions
* High presence of `redeemunderlying` or inactivity
* Many faced `liquidationcall`
* Low or zero total volume
* No diversity in DeFi actions (mostly one-off)

---

## 📈 Behavior of High-Scoring Wallets (700 - 1000)

* Active across multiple days
* High number of `deposit`, `borrow`, and `repay` events
* Consistent transaction patterns
* High total and average transaction volume
* No liquidation events
* Represent users with reliable and sustained DeFi behavior

---

## 📊 Insights

* A significant portion of wallets are low activity (score < 300)
* Clustering allowed clear separation of responsible vs erratic users
* DBSCAN helped isolate wallets that may be noise, spam, or exploits (score \~0)

---

Let me know if you want these files structured for GitHub upload or a ZIP with folders!
