# 🚗 Craigslist Cars & Trucks — Exploratory Data Analysis

## 📌 Project Overview

This project performs a comprehensive **Exploratory Data Analysis (EDA)** on the Craigslist Cars & Trucks dataset available on Kaggle.

The objective is to understand the structure and quality of the dataset, identify important patterns and relationships, analyze vehicle pricing, investigate missing values and outliers, and derive meaningful insights that could support future machine-learning or vehicle-price prediction tasks.

The analysis was completed as part of an **EDA assessment** and includes:

* Data quality assessment
* Missing-value analysis
* Data cleaning
* Feature engineering
* Univariate analysis
* Bivariate analysis
* Multivariate analysis
* Vehicle price analysis
* Mileage and vehicle-age analysis
* Manufacturer and model analysis
* Vehicle-type analysis
* Geographic analysis
* Correlation analysis
* Outlier investigation
* Assumptions and observations
* Limitations
* Recommendations for further analysis

---

## 📊 Dataset

**Dataset:** Craigslist Cars & Trucks

**Source:** Kaggle — Austin Reese

[Craigslist Cars & Trucks Dataset](https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data)

The original dataset contains approximately:

* **426,880 vehicle listings**
* **26 attributes**

The dataset contains information such as:

| Category            | Examples                                   |
| ------------------- | ------------------------------------------ |
| Vehicle Information | Manufacturer, Model, Year, Type            |
| Pricing             | Price                                      |
| Usage               | Odometer                                   |
| Vehicle Condition   | Condition, Title Status                    |
| Specifications      | Cylinders, Fuel, Transmission, Drive, Size |
| Appearance          | Paint Color                                |
| Location            | Region, State, Latitude, Longitude         |
| Listing Information | URL, Description, Posting Date             |
| Identification      | VIN                                        |

---

# 🎯 Objectives

The main objectives of this analysis are:

1. Understand the structure and characteristics of the dataset.
2. Assess the quality and completeness of the available data.
3. Identify missing values and potential data-quality issues.
4. Clean invalid numerical and categorical values.
5. Analyze the distribution of vehicle prices.
6. Investigate the relationship between price, mileage, and vehicle age.
7. Compare prices across vehicle types and manufacturers.
8. Analyze geographic patterns in listings.
9. Identify potential outliers and anomalies.
10. Generate actionable insights from the dataset.
11. Document assumptions and limitations.
12. Prepare the dataset for potential future machine-learning applications.

---

# 🔍 Analysis Workflow

The analysis follows the workflow below:

```text
Raw Dataset
     │
     ▼
Data Loading
     │
     ▼
Initial Data Inspection
     │
     ▼
Data Quality Assessment
     │
     ├── Missing Values
     ├── Duplicate Records
     ├── Invalid Values
     └── Data Types
     │
     ▼
Data Cleaning
     │
     ├── Numerical Cleaning
     ├── Categorical Cleaning
     └── Invalid Record Handling
     │
     ▼
Feature Engineering
     │
     ├── Vehicle Age
     ├── Age Groups
     ├── Mileage Groups
     ├── Price Groups
     ├── Price per Mile
     └── Log Transformations
     │
     ▼
Exploratory Data Analysis
     │
     ├── Univariate Analysis
     ├── Bivariate Analysis
     ├── Multivariate Analysis
     └── Geographic Analysis
     │
     ▼
Insights & Observations
     │
     ▼
Assumptions & Limitations
     │
     ▼
Conclusion & Recommendations
```

---

# 🧹 Data Cleaning

The following cleaning steps were performed:

### Duplicate Handling

Exact duplicate records were checked.

```text
Duplicate Rows: 0
```

No rows were removed because of exact duplication.

### Price Cleaning

Records with non-positive prices were removed because they are not suitable for normal vehicle-price analysis.

```text
price > 0
```

### Year Cleaning

Vehicle years outside the analytical range of **1900–2026** were treated as invalid and converted to missing values.

### Odometer Cleaning

Non-positive odometer values were treated as invalid and converted to missing values.

### Missing Values

Missing values were **not universally removed**.

This is important because several fields have significant missingness, and deleting every incomplete row would result in substantial information loss.

Instead, missing values were retained where appropriate and handled according to the analytical requirement.

---

# ⚙️ Feature Engineering

Several additional features were created to support deeper analysis.

### Vehicle Age

```text
Vehicle Age = 2026 - Vehicle Year
```

### Age Groups

Vehicles were grouped into:

```text
0–3 years
4–5 years
6–10 years
11–15 years
16–20 years
20+ years
```

### Mileage Groups

```text
<25K
25K–50K
50K–75K
75K–100K
100K–150K
150K+
```

### Price per Mile

```text
Price per Mile = Price / Odometer
```

This was used as an exploratory normalized metric.

### Log Transformations

The following transformations were created:

```text
log_price
log_odometer
```

These help reduce the influence of extreme values and are useful for future statistical or machine-learning analysis.

---

# 📈 Exploratory Analysis

The notebook covers the following major analytical areas.

## 1. Data Quality

* Dataset dimensions
* Data types
* Missing-value percentages
* Duplicate records
* Invalid numerical values

## 2. Price Analysis

* Price distribution
* Median and average price
* Price outliers
* Log-transformed price
* Price by vehicle type
* Price by manufacturer
* Price by condition

## 3. Vehicle Analysis

* Vehicle year distribution
* Vehicle age
* Mileage distribution
* Mileage groups
* Vehicle types
* Fuel types
* Transmission
* Condition

## 4. Manufacturer & Model Analysis

* Most frequently listed manufacturers
* Most frequently listed models
* Manufacturer-level pricing
* Manufacturer-level mileage
* Manufacturer vs condition

## 5. Relationship Analysis

* Price vs mileage
* Price vs vehicle age
* Price vs vehicle type
* Price vs manufacturer
* Age vs price
* Mileage vs price
* Numerical correlation analysis

## 6. Geographic Analysis

* Listings by state
* State-level pricing
* Geographic distribution of listings

---

# 📌 Key Findings

### 1. Dataset Size

The original dataset contains approximately **426,880 listings and 26 attributes**.

After basic data-quality cleaning, approximately **393,985 records** remained.

---

### 2. Significant Missing Values

Several important fields contain substantial missing data.

Examples include:

| Column        | Approx. Missing |
| ------------- | --------------: |
| `county`      |            100% |
| `size`        |            ~72% |
| `cylinders`   |            ~42% |
| `condition`   |            ~41% |
| `VIN`         |            ~38% |
| `drive`       |            ~31% |
| `paint_color` |            ~31% |
| `type`        |            ~22% |

This indicates that missing data is one of the major data-quality considerations in the dataset.

---

### 3. Price Distribution Is Highly Skewed

Vehicle prices contain extreme values.

The original maximum price is approximately:

```text
$3.74 Billion
```

while the median price is approximately:

```text
$13,950
```

This large difference indicates significant right-skew and the presence of extreme observations.

For visualization, the analysis uses the **99th percentile price (~$68,747)** to prevent extreme values from dominating charts.

Importantly, this percentile filtering is primarily a **visualization strategy**, not an assumption that every value above the threshold is invalid.

---

### 4. Mileage Contains Extreme Values

The dataset contains vehicles with very high odometer readings.

The original data has approximately:

```text
Median:      85,548 miles
75th Percentile: 133,543 miles
Maximum:     10,000,000 miles
```

This demonstrates the importance of checking outliers before performing statistical analysis.

---

### 5. Vehicle Type Has a Strong Relationship With Price

Examples from the analysis:

| Vehicle Type | Listings | Median Price |
| ------------ | -------: | -----------: |
| Sedan        |   80,322 |      $10,995 |
| SUV          |   70,599 |      $14,900 |
| Pickup       |   41,373 |      $27,999 |
| Truck        |   30,634 |      $24,995 |
| Coupe        |   18,214 |      $19,990 |
| Hatchback    |   15,917 |      $14,590 |
| Convertible  |    7,439 |      $15,900 |

Pickup and truck listings have substantially higher median prices than sedans.

---

### 6. Median Is More Reliable Than Mean for Many Comparisons

Several categories have large differences between their mean and median prices because of extreme listings.

For example, pickup vehicles have a median price of approximately:

```text
$27,999
```

while their average price is approximately:

```text
$152,228
```

This demonstrates how strongly extreme observations can influence the mean.

Therefore, **median price is generally preferred for descriptive comparisons in this dataset**.

---

### 7. Model Is a High-Cardinality Feature

The processed dataset contains approximately:

```text
28,281 unique model values
```

This creates challenges for machine-learning applications because seller-entered model names can contain:

* Spelling variations
* Trim variations
* Naming inconsistencies
* Rare categories

Model normalization would therefore be important before predictive modeling.

---

# 💡 Assumptions

The following assumptions were made during the analysis.

### Price

The `price` field is assumed to represent the **advertised listing price**, not the final transaction price.

### Missing Values

Missing information is not automatically treated as an error or negative category.

For example:

```text
Missing condition ≠ Poor condition
```

### Outliers

Extreme values are not automatically deleted.

An unusual price could represent a luxury, collector, commercial, or specialty vehicle—or a data-entry error.

### Vehicle Age

Vehicle age is calculated using:

```text
2026 - vehicle_year
```

This is a convenient analytical reference but does not necessarily represent the vehicle's age at the time the Craigslist listing was created.

### Correlation

Correlation is interpreted as an association rather than evidence of causation.

### Listings vs Sales

A Craigslist listing does not necessarily represent a completed vehicle sale.

Therefore:

```text
Number of Listings ≠ Number of Vehicles Sold
```

---

# ⚠️ Limitations

The analysis has several limitations.

### 1. Missing Data

Important attributes such as condition, size, cylinders, VIN, drive, and paint color contain significant missing values.

### 2. Outliers

Some price and mileage values appear extreme and may represent data-entry errors or unusual vehicles.

### 3. Seller-Entered Information

Several attributes are entered by sellers and may contain inconsistent or subjective information.

### 4. Listing Price

The dataset contains advertised prices rather than verified transaction prices.

### 5. Geographic Bias

Craigslist usage varies across regions, so listing counts may not accurately represent the complete U.S. vehicle market.

### 6. Historical Age Calculation

Using 2026 as the reference year creates a temporal mismatch for historical listings.

A better approach would be:

```text
Vehicle Age = Posting Year - Vehicle Year
```

### 7. No Causal Analysis

The EDA identifies relationships and patterns but does not establish causal relationships.

---

# 🚀 Future Improvements

The dataset can support several interesting extensions.

## Vehicle Price Prediction

Build a machine-learning model using:

* Random Forest
* XGBoost
* LightGBM
* CatBoost
* Linear Regression

Potential target:

```text
Vehicle Price
```

---

## Depreciation Analysis

Analyze the relationship between:

```text
Vehicle Age
       +
Mileage
       +
Manufacturer
       +
Model
       ↓
Vehicle Price
```

---

## Geographic Pricing

Investigate differences in median vehicle prices by:

* State
* Region
* City
* Latitude/Longitude clusters

---

## NLP Analysis

The `description` field could be processed using NLP to extract information about:

* Accident history
* Vehicle condition
* Features
* Maintenance
* Seller claims
* Premium features

---

## Anomaly Detection

Develop rules or ML models to detect:

* Unrealistic prices
* Suspicious mileage
* Incorrect vehicle years
* Unusual price/mileage combinations
* Duplicate or near-duplicate listings

---

# 📁 Project Structure

```text
eda_Craigslist/
│
├── data/
│   └── vehicles.csv
│ 
├── notebook/
│   └── vehicle_eda.ipynb
│
├── visualizations/
│
├── reports/
│      └── 01_Dataset_and_Methodology.docx
│      └── 02_EDA_Findings_and_Observations.docx
│      └── 03_Assumptions_Limitations_and_Conclusion.docx
│
├── requirements.txt
│
├── .gitignore
│
└── README.md
```

---

# 🛠️ Technologies Used

| Technology       | Purpose                   |
| ---------------- | ------------------------- |
| Python           | Data analysis             |
| Pandas           | Data manipulation         |
| NumPy            | Numerical operations      |
| Matplotlib       | Visualization             |
| Seaborn          | Statistical visualization |
| Jupyter Notebook | Interactive analysis      |
| Git/GitHub       | Version control           |

---

# ▶️ How to Run the Project

### 1. Clone the repository

```bash
git clone https://github.com/VarunChouhan2425/eda_Craigslist.git
cd eda_Craigslist
```

### 2. Create a virtual environment

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Download the dataset

Download the dataset from Kaggle:

https://www.kaggle.com/datasets/austinreese/craigslist-carstrucks-data

Place the CSV at:

```text
data/raw/vehicles.csv
```

### 5. Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
notebook/vehicle_eda.ipynb
```

and execute the cells sequentially.

---

# 📓 Main Deliverable

The primary analysis is available in:

```text
notebook/vehicle_eda.ipynb
```

The notebook contains the complete:

```text
Data Loading
      ↓
Data Cleaning
      ↓
Feature Engineering
      ↓
EDA
      ↓
Visualizations
      ↓
Insights
      ↓
Assumptions
      ↓
Limitations
      ↓
Conclusion
```

---

# 📄 Assessment Report

The detailed written report covers:

* Dataset overview
* Methodology
* Data-quality assessment
* EDA findings
* Key observations
* Assumptions
* Limitations
* Recommendations
* Conclusion

---

# 👤 Author

**Varun Chouhan**

GitHub:
https://github.com/VarunChouhan2425

---

# 📌 Final Conclusion

This EDA provides a structured understanding of the Craigslist Cars & Trucks dataset and highlights the major challenges associated with real-world vehicle listing data.

The most important findings are the **strong price skew, extreme numerical outliers, substantial missingness, differences between vehicle categories, and high-cardinality model information**.

The analysis also demonstrates that careful treatment of missing values and outliers is essential before using the dataset for predictive modeling.

The resulting cleaned and explored dataset provides a strong foundation for future work in **vehicle price prediction, depreciation analysis, market segmentation, geographic pricing, and anomaly detection**.
