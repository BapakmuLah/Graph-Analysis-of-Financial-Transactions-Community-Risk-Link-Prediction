# 📁 Financial Transaction Dataset

This folder contains the **core datasets** used in the Fraud Detection project.  

## 📂 Files Overview

| File                    | Deskripsi singkat                                      |
|-------------------------|--------------------------------------------------------|
| `bank_accounts.parquet` | Contains bank account–related information such as user IDs, account numbers, account types, and financial attributes.                     |
| `credit_cards.parquet`  | Holds credit-card information, likely including user IDs, masked card numbers, card types, limits, or status details.    |
| `devices.parquet`       | Includes data about user devices, such as device type, operating system, model, or unique device identifiers.  |
| `transactions.parquet`  | Stores transaction records, typically including timestamps, amounts, categories, payment methods, and user identifiers.    |

## 🏦 `bank_accounts`

| Feature        | Description |
|----------------|-------------|
| `user_id`      | Unique identifier representing the customer who owns the bank account |
| `bank_account` | Bank account number  |
<br>

**Shape:** `350,841 rows × 2 columns`

| user_id     | bank_account |
|-------------|--------------|
| C419128     | 0            |
| C19901940   | 0            |
| C21407120   | 0            |
| C54966514   | 0            |
| C80507942   | 0000039209   |

## 💳 `credit_cards`

| Feature        | Description |
|----------------|-------------|
| `user_id`      | Unique ID of the user who owns the credit card |
| `credit_card`  | Credit Card Number |
<br>

**Shape:** `38,708 rows × 2 columns`

| user_id     | credit_card      |
|-------------|------------------|
| C63177098   | 30024x08-2020    |
| C18468478   | 30024x08-2021    |
| C22163518   | 30024x12-2020    |
| C5845542    | 30134x02-2021    |
| C31447074   | 30134x10-2017    |

## 📱 `devices`

| Feature    | Description |
|------------|-------------|
| `user_id`  | Identifier linking a device to a specific user |
| `device`   | Device fingerprint |

<br>

| user_id     | device                                                    |
|-------------|-----------------------------------------------------------|
| C10146534   | +++3s/8YvFLP/ePRr1RQw27UpSq8iJAdybTVjPiHUc8=              |
| C123913948  | +++GW0vx4xLjxTNHKWO+kWDS+w45sJZz//ZUlST6TCg=              |
| C147271198  | +++b/gSDahdOss9vZHx/0qorN1zrvnT0DJ6vttl/YBE=              |
| C16126238   | +++hbM5PFzSOZglwP8ORRbmr40UrvzEgCMq6ZtuJjMu=              |
| C102164030  | +++ivFTF+M/DxnA21MRSxuqZO/KUheIu0RXva/O41sq=              |

## 💸 `transactions`

| Feature        | Description |
|----------------|-------------|
| `transid`      | Unique transaction identifier. |
| `org_user_id`  | The sender / origin user in the transaction. |
| `dest_user_id` | The receiving user in the transaction. |
| `amount`       | Transaction amount . |
<br>

**Shape:** `620,947 rows × 4 columns`

| transid     | org_user_id | dest_user_id | amount |
|-------------|-------------|---------------|--------|
| 1953278092  | C47388162   | C20822974     | 99094  |
| 1953295120  | C26855196   | C16416890     | 52714  |
| 1953306402  | C121296714  | C28477978     | 43888  |
| 1953314712  | C131221930  | C72837912     | 45771  |
| 1953381964  | C183398314  | C28423332     | 96840  |
