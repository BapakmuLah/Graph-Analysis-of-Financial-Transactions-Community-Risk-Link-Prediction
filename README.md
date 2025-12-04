# 🌐 Project Overview

This project explores multiple analytical and machine-learning approaches to detect suspicious transactions and fraudulent account behaviors.
It combines unsupervised anomaly detection, graph network analysis, and link prediction to identify hidden, non-obvious fraud patterns.

## 📂 Repository Structure

    Fraud Detection/
    │
    ├── data/                              # transaction and account profile datasets
    │   ├── bank_accounts.parquet
    │   ├── credit_cards.parquet
    │   ├── devices.parquet
    │   └── transactions.parquet
    │
    ├── Notebook 
    │   ├── EDA_IsolationForest.ipynb          # anomaly analysis + Isolation Forest
    │   ├── Local-Outlier-Factor.ipynb         # LOF anomaly detection modeling
    │   ├── graph-analysis.ipynb               # graph construction & centrality analysis
    │   ├── link_prediction.ipynb              # predict suspicious transactions with GraphSAGE
    │   └── money_laundry_pattern.ipynb        # pattern discovery of laundering chains

---

## 📚 Framework & Library Used

- Pytorch Geometric
- Scikit-Learn
- Networkx
- Pandas 
- Numpy
- Seaborn & Matplotlib

## 🎯 Project Goals / Main Objectives

1. **Detect Suspicious User & Abnormal Pattern**
2. **Predict Missing or Future Links (Link Prediction)**
3. **Detect Suspicious or Abnormal Transactions (Edge-Level Anomaly Detection)**
4. **Recommend Potential New Connections (Link Recommendation)**

## 🚀 Project Highlights

- Built multiple anomaly detection models (Isolation Forest, LOF)
- Constructed transaction graph networks to detect fraud clusters
- Performed link prediction using GraphSAGE to estimate suspicious Transactions
- Analyzed potential money-laundering chains and circular transaction loops
- Delivered interpretable insights backed by visualizations

## 📒 Summary 

- The anomaly user receives 10–100 times more transactions and significantly larger amounts of money compared to the normal user.
- The anomaly user made an average of 5-6 transfers with total 318k dollar, whereas the normal user made 1-2 transfers totaling 82k dollar.
- The anomaly user owns an average of 5-8 bank accounts and 11.8 devices, while the normal user has 1-2 bank accounts and 3.34 devices.
- The anomaly user’s total transaction volume is 8.5 million, compared to the normal user’s average of around 123 thousand.

## 👤 Top Suspicious Customer

| user_id     | Suspicious Reason |
|-------------|------------------|
| **C187679100** | Performed **74 outgoing transactions** to **48 different recipients**. far above normal behavior (90% of users make ≤3 transactions).  |
| **C63997352** | Performed **67 outgoing transactions** to **29 different users**. large number of transfers is highly abnormal for typical users. |
| **C87169706** | Performed **63 outgoing transactions** to **29 different users**, showing an excessively high and abnormal transaction volume for a single account. |
| **C102234504** | Received **3,478 incoming transactions** from around **3,272 different senders**, with **zero outgoing transactions**. a massive number of incoming transfers is extremely unusual (most users receive only 1–2 transfers). |
| **C22371544** | Received **2,736 incoming transactions** from thousands of senders (and made no outgoing transactions). This pattern is far beyond typical user behavior. |
| **C39287026** | Received **2,206 incoming transactions** from many different senders. Receiving thousands of transfers into one account is highly abnormal. |
| **C8158386** | Accessed the account using **582 different devices** (median users use only 2). This extreme number indicates abnormal activity (e.g., account sharing with many people or automated/bot access). |
| **C16111126** | Used **521 devices** to access the account and received **192 incoming transactions** without sending any out.  |
| **C192932592** | Shares the **same device identifier with 35 other users** (36 accounts using one device). This suggests possible mass account creation or coordinated unauthorized activities. |
| **C8767344** | Linked **39 bank accounts** (typical users link only 1) and received **490 incoming transactions**. Using dozens of bank accounts to receive hundreds of transfers  |
| **C2019758** | Has **29 different bank accounts** linked and received **540 incoming transactions**. The volume of accounts and transfers is far outside normal behavior. |
| **C109749590** | Shares a **bank account number (934222000)** with **88 other users**. One bank account being used by dozens of different identities  |
| **C2264618** | Has **19 registered credit cards** (normal users have only 1) and was involved in **100 transactions (91 as the recipient)** |
| **C24294346** | Has **20 registered credit cards**, an extremely abnormal number for any legitimate user. Even though transaction activity is low |

## 😈 Suspicious Account Criteria (Based on my analysis)

A `user_id` is considered **suspicious** if it meets one or more of the following conditions:

1. Unusually high number of outgoing transactions
2. Unusually high number of incoming transactions
3. Many unique counterparties
4. Too many devices used
5. Device shared by many users
6. Bank account shared by many users
7. Too many credit cards linked
8. Credit card shared by many users
9. Circular Transactions that could indicate money laundring
10. Multiple small accounts transferring to a single large account (Smurfing)
11. A single account sending funds to multiple smaller accounts (Layering/Distribution)

## 📊 Key Findings & Insights

The dataset and resulting graph are fairly large:
- **486,277+ nodes (users)**  
- **620,947+ edges (transactions)**  
- **23 features per node**

<br>
The graph is constructed from multiple tables:

- Devices  
- Bank accounts  
- Credit cards  
- Transactions  

Data cleaning steps remove hundreds of duplicates in some tables, which:

- Reduces bias in aggregated features (e.g., number of devices per user).
- Prevents artificial inflation of user connectivity.

### 🔍 Isolation Forest Results
---------------------------

- Identified **1% of transactions** as highly abnormal.  
- These anomalies showed:
  - Unusually large amounts  
  - Sudden spikes in activity 
  - Transaction frequency inconsistent with account history

<img width="1012" height="470" alt="iso" src="https://github.com/user-attachments/assets/1add66fa-2515-4897-b985-7b43c41647d3" />
<img width="1781" height="691" alt="iso1" src="https://github.com/user-attachments/assets/896b7841-0050-4c49-a93e-587cadb52209" />

### 🔍 Local Outlier Factor (LOF) Results
----------------------------
- Detected behaviors abnormal **relative to similar users**
- Flagged accounts connected to high-risk neighbors.  
- Highlighted density anomalies not visible in global methods.

<img width="1012" height="470" alt="lof" src="https://github.com/user-attachments/assets/d973e2b4-edc5-40c4-9135-2b5aa7f5d61e" />
<img width="1781" height="691" alt="lof1" src="https://github.com/user-attachments/assets/6cb14c7d-8329-4a2b-8e53-86ba62a9d5e9" />


**Interpretation:**  
Both models consistently flagged overlapping anomalies, strengthening the confidence of detected suspicious behavior.

### 🧩 **Link Prediction**
------------------------

This project builds a **Graph Neural Network (GraphSAGE)** model to:

1. **Link Prediction**: predict the likelihood of a transaction between two users. (to detect suspicious transactions)
2. **Edge-level Anomaly Detection**: detect transactions that are structurally unusual in the graph.
3. **Link Recommendation**: recommend pairs of users that are likely to be connected in the future.

<br>

**Model architecture:**

The goal is to predict whether two edges (transactions) are normal or abnormal (anomalies).

1. **Encoder** 
   - Two `SAGEConv` Hidden layers with non-linearity ReLU Activation Function
2. **Classification Layer**
   - Two Hidden Layer MLP with non-linearity ReLU Activation Function
3. **Data Split**
   - **Inductive node split** (train/val/test defined at node level, not random edges).
4. **Training**
   - Uses **negative sampling** (non-existent edges as negative class).

Key evaluation results:
- **Train ROC-AUC ≈ 0.9739**
- **Val ROC-AUC   ≈ 0.9753**
- **Test ROC-AUC  ≈ 0.9604**
- **Train Average Precision (AP) ≈ 0.9614**
- **Val Average Precision (AP)   ≈ 0.9604**
- **Test Average Precision (AP)  ≈ 0.9612**

Train, validation, and test sets all exhibit high and consistent ROC-AUC and AP values.

### Edge-Level Anomaly Detection

The model is repurposed as an **unsupervised edge-level anomaly detector**:

- For every existing edge, the model computes its probability of existence.
- Edges with **very low predicted probabilities** are treated as anomaly candidates.
- Observations:
  - “Normal” edges often have probabilities around **0.998–0.999**.
  - “Anomalous” edges can drop to **~0.06–0.37**.

<img width="500" height="400" alt="output" src="https://github.com/user-attachments/assets/b799d420-8e65-4593-b822-f742463ad8b3" />
<img width="500" height="400" alt="output1" src="https://github.com/user-attachments/assets/85b846d0-ad67-4fc9-987a-8d5f95d439c6" />

### Link Recommendation

Beyond anomaly detection, the model is also used for link recommendation:

- For a target node (user), the model computes the probability of forming an edge with all other nodes that are **not currently connected**.
- The top-K highest scores are interpreted as **candidate future links**.

### Main Takeaways

1. **Graph-based modeling with GraphSAGE** effective for learning patterns in large-scale user–transaction networks.
2. **Feature engineering based on shared items and network structure** provides strong signals for both anomaly detection and link prediction.
3. The **inductive node split** leads to a more realistic evaluation setup. generalization to unseen users and edges.
4. The model achieves **strong performance (ROC-AUC ~0.97, AP ~0.96)**. it a solid foundation for link prediction and anomaly detection in production-like environments.
5. Combining **link prediction, anomaly scoring, and link recommendation** in a single GNN framework offers substantial flexibility for various real-world applications in the transaction/financial domain.
