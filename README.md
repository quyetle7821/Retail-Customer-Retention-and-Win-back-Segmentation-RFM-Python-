# 🧩 RFM Customer Segmentation for Retention | Retail Marketing | Python (Pandas)

<img width="1363" height="907" alt="image" src="https://github.com/user-attachments/assets/9d429a37-b57d-4b9a-a675-705b5a8fa604" />

Author: Lê Trường Quyết

Date: 2025-09-07

Tools Used: Python (Pandas)

## 📑 Table of Contents  
1. [📌 Background & Overview](#-background--overview)
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
3. [🧹 Data Cleaning & Preprocessing](#-data-cleaning--preprocessing)

## 1. 📌 Background & Overview  

### Objective

### 📖 What is this project about? 

- **SuperStore (Global Retail)** wants to run targeted marketing programs to **retain high-value customers**, **reactivate inactive customers**, and **nurture potential loyalists** based on purchasing behavior.
- Because the transaction dataset is large (hundreds of thousands of rows), **manual segmentation in Excel is no longer feasible**.
- To solve this, I applied the **RFM model (Recency–Frequency–Monetary)** using **Python (Pandas/Colab)** to:
  + Clean and prepare transaction data
  + Calculate **RFM metrics & scores** for each customer
  + Assign customers into meaningful **segments** (e.g., Champions, Loyal, At Risk, Hibernating, etc.)
  + Visualize segment distribution and value contribution
  + Provide **actionable recommendations** for Marketing to design appropriate campaigns per segment.

### 👥 Who is this project for?

✅ Marketing team (Customer retention & campaign planning)

✅ Sales/CRM team (prioritizing customers and offers)

✅ Decision-makers & stakeholders (understanding customer value structure)

### ❓ Business Questions

✅ How can we segment customers effectively using the **RFM model?**

✅ Which customer segments contribute the most to **revenue** and should be prioritized?

✅ Which customer groups show signs of churn risk **(inactive / at-risk)** and need re-engagement?

✅ What marketing actions should be applied to each segment to improve **retention and lifetime value?**

## 2. 📂 Dataset Description & Data Structure 

### 📌 Data Source

- **Source**: Provided dataset for E-commerce / Retail transaction analysis (SuperStore – Global retail context)
- **File**: xlsx (Excel file with two sheets
- **Size**: 541,909 rows × 8 columns (Sheet 1: ecommerce retail) + 11 rows × 2 columns (Sheet 2: Segmentation)

### 📊 Data Structure & Relationships  

### 1️⃣ Tables Used

- **Sheet 1**: ecommerce retail — Transaction-level data (invoice line items), including product details, customer IDs, timestamps, and country.
- **Sheet 2**: Segmentation — A mapping table that links **RFM score codes** (e.g., 555, 544, …) to **customer segments** (e.g., Champions, Loyal, At Risk, etc.).

### 2️⃣ Table Schema & Data Snapshot

#### 📌 Sheet 1: E-commerce Retail

#### 🧾 Table Schema: `ecommerce retail`

<details>
  <summary>📁 <b>Dataset Schema</b> (Click to expand)</summary>

  | Column | Data Type | Description |
|---|---|---|
| `InvoiceNo` | object (string) | Invoice number (one invoice can contain multiple line items). |
| `StockCode` | object (string) | Product/item identifier. |
| `Description` | object (string) | Product name/description. |
| `Quantity` | int | Quantity per line item (**can be ≤ 0** for cancellations/returns). |
| `InvoiceDate` | datetime | Invoice timestamp (date + time). |
| `UnitPrice` | float | Unit price (**can be ≤ 0** due to adjustments/data issues). |
| `CustomerID` | float | Customer identifier (**missing values exist**). |
| `Country` | object (string) | Customer country. |

</details>

#### 📌 Sheet 2: Segmentation

#### 📊 Customer Segmentation & RFM Scores
<details>
  <summary>📈 <b>RFM Segmentation Mapping</b> (Click to expand)</summary>
  

| Segment | RFM Score |
|---|---|
| Champions | 555, 554, 544, 545, 454, 455, 445 |
| Loyal | 543, 444, 435, 355, 354, 345, 344, 335 |
| Potential Loyalist | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323 |
| New Customers | 512, 511, 422, 421, 412, 411, 311 |
| Promising | 525, 524, 523, 522, 521, 515, 514, 513, 425,424, 413,414,415, 315, 314, 313 |
| Need Attention | 535, 534, 443, 434, 343, 334, 325, 324 |
| About To Sleep | 331, 321, 312, 221, 213, 231, 241, 251 |
| At Risk | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124 |
| Cannot Lose Them | 155, 154, 144, 214,215,115, 114, 113 |
| Hibernating customers | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211 |
| Lost customers | 111, 112, 121, 131,141,151 |

</details>

## 3. 🧹 Data Cleaning & Preprocessing

