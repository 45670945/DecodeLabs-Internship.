# 🧹 DecodeLabs — Data Analytics Project 1
### Data Cleaning & Preparation | Industrial Training Kit | Batch 2026

<br>

> **"Before you build a single predictive model or dashboard, you must master the art of scrubbing raw, messy datasets into reliable sources of truth."**
> — DecodeLabs

<br>

---

## 📋 Project Overview

This project demonstrates the **Data Cleaning & Preparation** phase of the data analytics pipeline. Using Python (Pandas) in Google Colab, raw e-commerce order data was inspected, cleaned, validated, and exported as a production-ready dataset.

| Detail | Info |
|--------|------|
| 🏢 **Organization** | DecodeLabs |
| 📦 **Project** | Project 1 — Data Cleaning & Preparation |
| 🐍 **Tool** | Python (Pandas) — Google Colab |
| 📊 **Raw Dataset** | `Dataset_for_Data_Analytics.xlsx` — 1,200 rows, 14 columns |
| ✅ **Cleaned Output** | `Cleaned_Dataset.xlsx` — 1,200 rows, 0 nulls, 0 duplicates |
| 📅 **Batch** | 2026 |

---

## 📁 Repository Structure

```
decodelabs-data-analytics-project1/
│
├── 📄 README.md                          ← You are here
├── 📓 Decodelabs_project.ipynb           ← Python cleaning notebook (Google Colab)
├── 📊 Dataset_for_Data_Analytics.xlsx    ← Raw original dataset
└── ✅ Cleaned_Dataset.xlsx               ← Final cleaned output
```

---

## 🗂️ Dataset Overview

**Raw File:** `Dataset_for_Data_Analytics.xlsx` — **1,200 rows × 14 columns**

| Column | Data Type | Description |
|--------|-----------|-------------|
| `OrderID` | object | Unique order identifier (e.g. ORD200000) |
| `Date` | datetime64 | Order date — verified as YYYY-MM-DD format |
| `CustomerID` | object | Unique customer identifier |
| `Product` | object | Laptop, Phone, Tablet, Monitor, Printer, Desk, Chair |
| `Quantity` | int64 | Units ordered (1–5) |
| `UnitPrice` | float64 | Price per unit (11.39 – 699.93) |
| `ShippingAddress` | object | Delivery street address |
| `PaymentMethod` | object | Cash, Credit Card, Debit Card, Gift Card, Online |
| `OrderStatus` | object | Delivered, Shipped, Pending, Cancelled, Returned |
| `TrackingNumber` | object | Unique shipment tracking code |
| `ItemsInCart` | int64 | Total items in cart at checkout (1–10) |
| `CouponCode` | object | SAVE10, FREESHIP, WINTER15 — **had 309 nulls** |
| `ReferralSource` | object | Google, Facebook, Instagram, Email, Referral |
| `TotalPrice` | float64 | Final order value |

---

## 🔍 Issues Found in Raw Data

| Issue | Column | Count | Action Taken |
|-------|--------|-------|--------------|
| Missing values | `CouponCode` | 309 nulls | Filled with `'No Coupon'` |
| Duplicate rows | All columns | 0 found | No action needed |
| Duplicate Order IDs | `OrderID` | 0 found | Verified unique ✅ |
| Incorrect date format | `Date` | Verified | Converted to `datetime64` ✅ |

---

## 🧪 Cleaning Steps Performed

### Step 1 — Load the Dataset
```python
import pandas as pd

df = pd.read_excel("/content/Dataset for Data Analytics.xlsx")
df.head()
```

### Step 2 — Explore the Dataset
```python
df.shape      # (1200, 14)
df.columns    # All 14 column names
```

### Step 3 — Check Missing Values
```python
df.isnull().sum()
# Result: CouponCode had 309 missing values
# All other columns: 0 nulls
```

### Step 4 — Handle Missing Values
```python
# Fill missing CouponCode with 'No Coupon'
df['CouponCode'] = df['CouponCode'].fillna('No Coupon')

# Verify fix
df.isnull().sum()
# Result: All columns now show 0 nulls ✅
```

### Step 5 — Check for Duplicate Records
```python
df.duplicated().sum()
# Result: 0 duplicate rows ✅

df['OrderID'].duplicated().sum()
# Result: 0 duplicate Order IDs ✅
```

### Step 6 — Verify & Fix Date Format
```python
df.dtypes
# Date column: datetime64[ns] ✅

df['Date'] = pd.to_datetime(df['Date'])
df['Date'].head()
# All dates in YYYY-MM-DD format ✅
```

### Step 7 — Final Validation
```python
df.isnull().sum().sum()     # 0 — no missing values ✅
df.duplicated().sum()        # 0 — no duplicate rows ✅
df['OrderID'].duplicated().sum()  # 0 — all IDs unique ✅
```

### Step 8 — Save Cleaned Dataset
```python
df.to_excel("Cleaned_Dataset.xlsx", index=False)
```

---

## ✅ Before vs After Cleaning

| Metric | Before Cleaning | After Cleaning |
|--------|----------------|----------------|
| Total Rows | 1,200 | 1,200 |
| Total Columns | 14 | 14 |
| Missing Values | 309 (CouponCode) | **0** ✅ |
| Duplicate Rows | 0 | **0** ✅ |
| Duplicate Order IDs | 0 | **0** ✅ |
| Date Format | datetime64 | **datetime64** ✅ |
| Data Quality Score | ⚠️ Incomplete | **✅ Production Ready** |

---

## 🚀 How to Run This Notebook

### Option A — Google Colab (Recommended)

1. Go to [colab.research.google.com](https://colab.research.google.com)
2. Click **File → Upload notebook** → select `Decodelabs_project.ipynb`
3. Upload the dataset:
   - Click the 📁 **Files** icon on the left panel
   - Click **Upload** → select `Dataset_for_Data_Analytics.xlsx`
4. Click **Runtime → Run all** (`Ctrl + F9`)
5. The cleaned file `Cleaned_Dataset.xlsx` will appear in the Files panel — right-click to download

### Option B — Jupyter Notebook (Local)

```bash
# Install required library
pip install pandas openpyxl

# Open notebook
jupyter notebook Decodelabs_project.ipynb
```

> Update the file path in the load step:
> ```python
> df = pd.read_excel("Dataset_for_Data_Analytics.xlsx")
> ```

---

## 🧠 Key Concepts Used

| Concept | Python Code | Purpose |
|---------|-------------|---------|
| Load Excel | `pd.read_excel()` | Import raw data |
| Preview data | `df.head()` | Check first 5 rows |
| Dataset shape | `df.shape` | Rows × Columns count |
| Column names | `df.columns` | List all fields |
| Find nulls | `df.isnull().sum()` | Count missing values per column |
| Fill nulls | `df.fillna('No Coupon')` | Replace NaN with a value |
| Find duplicates | `df.duplicated().sum()` | Check for duplicate rows |
| Unique IDs | `df['OrderID'].duplicated().sum()` | Verify no duplicate IDs |
| Check types | `df.dtypes` | Verify data types |
| Fix dates | `pd.to_datetime()` | Standardize date format |
| Export data | `df.to_excel()` | Save cleaned output |

---

## 🏆 DecodeLabs Verification Gate

As required by Project 1 standards:

| Requirement | Status |
|-------------|--------|
| 0% Error Rate on Unique Identifiers | ✅ Passed — `OrderID` duplicates = 0 |
| 0% Error Rate on Date Formats | ✅ Passed — All dates in `datetime64` |
| Zero missing values remaining | ✅ Passed — Total nulls = 0 |
| Cleaned dataset exported | ✅ `Cleaned_Dataset.xlsx` saved |

---

## ✅ Project Checklist

- [x] Raw dataset loaded and explored
- [x] Dataset shape confirmed — 1,200 rows × 14 columns
- [x] Missing values identified — 309 nulls in `CouponCode`
- [x] Missing values handled — filled with `'No Coupon'`
- [x] Duplicate rows checked — 0 found
- [x] Duplicate Order IDs verified — 0 found
- [x] Data types reviewed and date column validated
- [x] Date format standardized to `datetime64`
- [x] Final validation passed — 0 nulls, 0 duplicates
- [x] Cleaned dataset exported as `Cleaned_Dataset.xlsx`
- [x] Project published to GitHub

---

## 🛠️ Tools Used

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 👨‍💻 Author

| | |
|--|--|
| 👤 **Name** | Thilani Senarath |
| 💼 **Role** | Data Analytics Intern |
| 🏢 **Organization** | DecodeLabs |
| 📅 **Batch** | 2026 |

---

## 📜 License

This project is created for **educational and learning purposes only**.

All code, analysis, and documentation in this repository are part of the DecodeLabs Industrial Training Program and are intended solely for skill development and portfolio building.

---

## 📞 About DecodeLabs

| | |
|--|--|
| 🌐 Website | [www.decodelabs.tech](https://www.decodelabs.tech) |
| 📧 Email | decodelabs.tech@gmail.com |
| 📞 Phone | +91 89330 06408 |
| 📍 Location | Greater Lucknow, India |

---

<div align="center">

**DecodeLabs Industrial Training Kit — Batch 2026**

*"Your analysis is only as good as your data. Make it count."*

</div>
