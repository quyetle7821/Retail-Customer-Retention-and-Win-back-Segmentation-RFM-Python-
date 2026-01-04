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

### 🛠 Step 1. Imports (setup library)

<img width="1737" height="230" alt="image" src="https://github.com/user-attachments/assets/95e0b5e1-f73c-4255-9536-767e5986b515" />

### 🛠 Step 2. Load + clean + revenue

[In 2]:

<img width="1742" height="470" alt="image" src="https://github.com/user-attachments/assets/02d61fa8-8877-4a20-8726-0b29cc9a3db3" />


[Out 2] :

<img width="1768" height="279" alt="image" src="https://github.com/user-attachments/assets/dbb24e70-7d2f-4990-8e77-72b33e6da564" />

### 🔎 Observations
From the raw transaction data, a few quality issues can affect RFM results:

- **Missing values** may appear in key fields (especially `CustomerID`), which prevents customer-level aggregation.
- **Invalid transactions** can exist (e.g., `Quantity <= 0` or `UnitPrice <= 0`), often related to cancellations/returns or data entry errors.
- The dataset is **transaction line-item level**, meaning one invoice can have multiple rows → requires aggregation later for Frequency/Monetary.

### 🧠 Why these cleaning rules?
To build a reliable RFM dataset, I applied minimal but essential rules:

- **Convert data types** (`InvoiceDate` to datetime, `UnitPrice/Quantity` to numeric)  
  → ensures calculations (Recency, Revenue) are accurate and consistent.
- **Drop rows missing required fields** (`CustomerID`, `InvoiceDate`, `UnitPrice`, `Quantity`)  
  → RFM is computed per customer and requires valid timestamps and transaction values.
- **Keep only `UnitPrice > 0` and `Quantity > 0`**  
  → removes cancellations/returns and invalid records so Monetary isn’t distorted.
- **Create `Revenue = UnitPrice × Quantity`**  
  → provides the Monetary metric at line-item level for later customer aggregation.

### ✅ Output of this section
After preprocessing, the dataset is ready for the RFM model:

- All remaining records have valid `CustomerID` and `InvoiceDate`
- Invalid or non-positive transactions are excluded
- A new `Revenue` column is created for Monetary calculation

➡️ The cleaned transaction table will be aggregated at customer level in the next step to compute **Recency, Frequency, and Monetary**.

## 4. 🧮 Apply RFM Model

### 🛠 Step 1. Build RFM Metrics (Customer-level)

[In 3]:

<img width="1756" height="526" alt="image" src="https://github.com/user-attachments/assets/a171fae4-a7f9-449e-b969-1dfbff8eafaf" />

[Out 3]:

<img width="512" height="240" alt="image" src="https://github.com/user-attachments/assets/b112eba9-dcb5-4c8c-b490-4d6396c55545" />

### 🛠 Step 2. Score RFM & Create RFM Code

[In 4]:

<img width="1769" height="261" alt="image" src="https://github.com/user-attachments/assets/00b82163-7312-4c8a-81b3-2792b5c000e4" />

[Out 4]:

<img width="699" height="210" alt="image" src="https://github.com/user-attachments/assets/37b258c0-b624-46c2-aab9-78b8f0d13a89" />


### 🛠 Step 3 — Map RFM Code to Business Segments

[In 5]

<img width="1493" height="650" alt="image" src="https://github.com/user-attachments/assets/534f7154-f17d-4ae2-a92a-9f492ade8a04" />

[Out 5] 

<img width="1006" height="264" alt="image" src="https://github.com/user-attachments/assets/1ef4601b-2700-4229-a48d-6e76e895d8da" />

[In 6]

<img width="883" height="611" alt="image" src="https://github.com/user-attachments/assets/177d2881-2b86-4e54-a2b6-daddcb98af68" />

[Out 6] : 

<img width="1082" height="220" alt="image" src="https://github.com/user-attachments/assets/fa8dc70d-f627-4ede-93ed-65fc652c4e85" />


### 🔎 Observations
- The workflow successfully transforms transaction data into a **customer-level RFM dataset**:
  - **Recency** = days since the most recent purchase (relative to `REF_DATE`)
  - **Frequency** = number of unique invoices per customer
  - **Monetary** = total revenue per customer
- RFM metrics are then standardized into **R/F/M scores (1–5)** using quintiles and combined into a 3-digit **RFM_Code** (e.g., 555).
- Finally, customers are assigned to **business segments** (e.g., Champions, At Risk, Lost Customers) by mapping `RFM_Code` to segment labels from the `Segmentation` sheet.
- A small issue can appear when cells are run multiple times: duplicate segment columns like `Segment_x / Segment_y` may show up due to repeated merges.

### 🧠 Explanation
- RFM is designed to measure customer value at the **customer level**, so the transaction-level table must be aggregated by `CustomerID`.
- A fixed reference date (`REF_DATE`) ensures Recency is measured consistently across all customers.
- Quintile scoring converts raw metrics with different ranges into a comparable **ranking-based scale**, making segmentation easier and more interpretable.
  - Recency is scored inversely because **more recent buyers are more valuable** for retention and reactivation.
- `RFM_Code` acts as a compact key for segmentation, and the mapping sheet provides a **business-friendly interpretation layer** so results can be used directly by Marketing/Sales.
- Safe-merge practices (dropping old segment columns, ensuring one segment per code, and tracking “Unmapped”) are used to keep segmentation stable and avoid downstream errors.

### ✅ Conclusion
- The section outputs a finalized customer-level table that includes:
  - **Recency, Frequency, Monetary**
  - **R_Score, F_Score, M_Score**
  - **RFM_Code**
  - **Segment**
- This dataset is the core deliverable for the next section (**EDA & Recommendations**), where segment size and value contribution will be visualized and translated into actionable marketing strategies.


## 5. 💡 Exploratory Data Analysis (EDA) & Recommendations.

[In 7] : 

<img width="822" height="325" alt="image" src="https://github.com/user-attachments/assets/ffa7811a-01a8-4aa0-a720-02b88b2b496a" />

[Out 7]:

<img width="1703" height="455" alt="image" src="https://github.com/user-attachments/assets/52a5a35a-7edc-4adb-be77-ea36fe8e78fe" />

<img width="1673" height="452" alt="image" src="https://github.com/user-attachments/assets/1f2b21e1-dc0d-495a-a4d7-48154c1a9acf" />

[In 8]

<img width="845" height="321" alt="image" src="https://github.com/user-attachments/assets/c33a9622-107f-4cd0-ba30-d40a9768f2ae" />

[Out 8]

<img width="800" height="241" alt="image" src="https://github.com/user-attachments/assets/8e7951b7-489f-434a-ac66-735576c147a2" />

[In 9] : 

<img width="778" height="87" alt="image" src="https://github.com/user-attachments/assets/2cbdffcb-35ae-4580-a852-ad082deb5cd6" />

[Out 9] : 

<img width="702" height="72" alt="image" src="https://github.com/user-attachments/assets/aafeda09-6b84-4abf-bc45-a3e9b1b2b4d4" />


### 🔎 Observations
- The EDA focuses on understanding **segment performance** from two key angles:
  1) **Customer distribution** (Customers by Segment)
  2) **Revenue contribution** (Total Monetary by Segment)
- The charts show that segment size and segment value are **not always aligned**:
  - Some segments contain many customers but contribute less total monetary value.
  - High-value segments may represent a smaller portion of customers but drive a large share of revenue.
- The quick summary table calculates each segment’s **customer share**, then identifies:
  - The **largest segment by customer count**
  - The **highest-value segment by Monetary**
- Based on the segment insights, the notebook outputs brief marketing directions such as:
  - Protecting high-value segments (VIP/loyalty benefits)
  - Upsell/cross-sell focus for large segments
  - Win-back campaigns for low-recency groups
- The final cell proposes a clear business prioritization for growth:
  - **Frequency (F)** first → then **Recency (R)** → then **Monetary (M)**

### 🧠 Explanation
- Segment-level analysis is the most actionable way to translate RFM results into business decisions:
  - **Customers by Segment** highlights where most customers sit (operational scale).
  - **Total Monetary by Segment** highlights which segments matter most for revenue (business impact).
- Comparing size vs value helps avoid misleading decisions:
  - Targeting only the largest segment may not maximize revenue.
  - Ignoring smaller high-value segments can increase churn risk and revenue loss.
- The quick summary provides a “decision-ready” view:
  - Customer share → indicates where campaigns can reach the most people.
  - Monetary leader → indicates where retention protection has the highest ROI.
- The priority order (F → R → M) reflects a practical growth strategy:
  - **Increase Frequency** to build repeat purchase behavior and stabilize long-term value (LTV).
  - Use **Recency** to identify churn risk and time win-back campaigns effectively.
  - Improve **Monetary** via bundles/cross-sell after engagement is stabilized (F & R improved).

### ✅ Conclusion
- This section validates the segmentation by showing **who the customers are (distribution)** and **where the revenue comes from (value contribution)**.
- The analysis produces actionable outcomes:
  - Clear targeting focus by segment (retain high-value, scale large segments, win back inactive customers).
  - A prioritized RFM roadmap (F → R → M) that can guide campaign planning and KPI tracking.
- These insights can directly support Marketing/Sales in designing personalized retention, reactivation, and upsell strategies for each customer group.

## 6. 💡 Insight & Recommendation

### A. Customer Segmentation Strategy

Based on the segment distribution and revenue contribution, we recommend focusing on 3 strategic customer groups:

---

### 1) Core Value Group (Champions + Loyal) — **32.8%**
**Key insights**
- This group forms the **most valuable customer base**, with **strong engagement** and **high revenue impact** (Champions typically lead the **Monetary contribution**).
- They show **lower Recency** and/or **higher Frequency**, indicating **high retention potential** and a stronger buying habit.
- They are ideal targets for **premium offers**, **loyalty benefits**, and **referral programs**.

🔷 **Recommendations**
- **Protect core revenue** with **VIP/loyalty perks** (exclusive deals, early access, member-only rewards).
- Test **upsell & bundling** to increase **AOV** without relying on deep discounts.
- Encourage **reviews & referrals** to turn loyal customers into **organic growth channels**.

---

### 2) High-Risk Customers (At Risk) — **6.7%**
**Key insights**
- This group shows clear **churn-risk signals**: **higher Recency** and weaker ongoing engagement.
- Although smaller in size, losing them can cause **revenue leakage**, especially if they previously had meaningful **Monetary value**.
- **Timing is critical**: the longer they stay inactive, the harder (and more expensive) **reactivation** becomes.

🔷 **Recommendations**
- Launch **win-back campaigns** with **personalized incentives** (e.g., tailored vouchers based on past value).
- Prioritize **high past-Monetary customers** with stronger offers; use lighter incentives for others to control **CAC**.
- Set **churn triggers** (30/60/90-day inactivity) to automatically send **reactivation messages** and offers.

---

### 3) Growth Potential Group (Others + Potential Loyalist + Big Spenders) — **60.4%**
**Key insights**
- This is the **largest opportunity pool** by customer count, but **value varies widely** across sub-segments.
- **Potential Loyalists** are trending upward but still **unstable**, while **Big Spenders** have high value but need **repeat behavior**.
- Because **Others** is the biggest segment (**38.4%**), even small improvements in **Frequency** can create **large-scale impact**.

🔷 **Recommendations**
- Build repeat habits via **nurturing campaigns** (welcome flows, personalized recommendations, “2nd purchase” incentives).
- Use **cross-sell/upsell** for scale segments (Others) to lift **Monetary** while keeping cost efficiency.
- For Big Spenders, push **premium bundles** and tailored suggestions to increase **repeat purchases**, not just one-time high orders.

---

### B. Business Recommendation (Overall Strategy)

In SuperStore’s retail model, the most practical RFM roadmap is to prioritize **Frequency (F)** first, then **Recency (R)**, and finally **Monetary (M)**.

✅ **Why focus on Frequency (F) first?**
- Increasing **purchase frequency** builds a sustainable **repeat-buying habit** and stabilizes long-term revenue (**LTV**).
- Improving Frequency reduces dependence on acquisition and can lower effective **Customer Acquisition Cost (CAC)** over time.

✅ **How this aligns with the segment results**
- The largest pool (**60.4%**) needs **Frequency-building** to move from casual buyers to repeat customers.
- The high-value base (**32.8%**) must be **protected** to prevent revenue loss.
- The churn-risk group (**6.7%**) needs **timely reactivation** to avoid drop-off.

✅ **Execution roadmap**
1) **Boost Frequency (top priority):** loyalty tiers, repeat-purchase vouchers, reorder reminders, bundles.  
2) **Manage Recency:** automated reactivation triggers for churn-risk customers.  
3) **Lift Monetary:** upsell/cross-sell after engagement stabilizes (**F & R improved**).

**Final takeaway:** Protect **Core Value (32.8%)**, prevent churn in **At Risk (6.7%)**, and scale growth by upgrading the **Growth Potential pool (60.4%)** into **repeat buyers**.


### C. Recommended Actions by Segment (Quick Playbook)

| Segment | Share | Key signal | Primary goal | Suggested actions |
|---|---:|---|---|---|
| **Champions** | **21.8%** | Recent + frequent + high value | **Protect & grow value** | VIP perks, early access, premium bundles, referral rewards, review incentives |
| **Loyal** | **11.0%** | High frequency, stable value | **Maintain loyalty** | Tiered loyalty program, personalized offers, subscription/re-order nudges, member-only deals |
| **Potential Loyalist** | **13.7%** | Improving frequency, not stable yet | **Convert to Loyal** | “2nd/3rd purchase” vouchers, onboarding series, product recommendations, retargeting ads |
| **Big Spenders** | **8.3%** | High monetary but inconsistent | **Increase repeat rate** | Premium bundles, tailored cross-sell, replenishment reminders, concierge-style support |
| **Others** | **38.4%** | Largest pool, mixed behavior | **Scale frequency uplift** | Mass personalization (top categories), low-cost incentives, seasonal campaigns, bundle deals |
| **At Risk** | **6.7%** | High recency (inactive), churn risk | **Win-back & prevent churn** | Win-back within 7–14 days, personalized discount, churn triggers (30/60/90 days), feedback outreach |







