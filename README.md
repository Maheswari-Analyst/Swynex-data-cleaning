# Swynex-data-cleaning
# E-Commerce Transaction Data Cleaning Pipeline 

## Project Overview
This repository contains the data cleaning pipeline built for **Task 1** of the Data Analyst experience with **Swynex Technologies** (in collaboration with Internship Studio). 

The goal of this project was to take a messy, raw e-commerce dataset spanning 36 months of promotional and transaction history in India and transform it into a high-fidelity, structurally sound asset optimized for downstream business intelligence (BI) dashboards and predictive financial modeling.

## The Raw Data Challenge
The baseline raw dataset (`indian_ecommerce_pricing_revenue_growth_36_months.csv`) contained several structural anomalies commonly found in real-world production pipelines:
* **Incorrect Data Types:** Quantitative metrics such as prices, discount metrics, and age parameters were stored as unparsed text strings.
* **Temporal Inconsistencies:** Order dates were locked in mixed object types rather than true datetime scales.
* **Data Fragmentation:** Text categories contained stray leading/trailing spaces and random string casing variations.
* **Duplicate Records:** Potential duplicates across primary transactional identifiers.

---

## Technical Cleaning Workflow (Python & Pandas)

The programmatic script executes an end-to-end data sanitization process across the following structural milestones:

### 1. Chronological Type Conversion
Converted the raw text `order_date` using explicit string formatting constraints to transform text streams into verified, queryable datetimes.
```python
df['order_date'] = pd.to_datetime(df['order_date'], format='%d-%m-%Y', errors='coerce')
```

### 2. Quantitative Type Enforcement
Safely mapped categorical numeric object arrays (`base_price`, `discount_percent`, `final_price`, `units_sold`, and `revenue`) into unified floating-point numbers and integer schemas.

### 3. Deduplication & Null Imputation
* Enforced structural uniqueness by executing deep drop protocols based on the primary key identifier (`order_id`).
* Mapped missing string parameters to standardized fallback default states (`"Unknown"`) to preserve structural query indexing blocks.

### 4. Categorical Normalization
Standardized and streamlined dynamic string arrays across e-commerce categories and geographic zones using strict whitespace stripping and capitalization methods to eliminate structural analysis fragmentation.

### 5. Mathematical Sanity Audits & Constraints
Programmed explicit multi-field domain constraints to assert operational truth across transaction rows:
* Evaluated that `discount_percent` fell logically within bound thresholds \([0, 100]\).
* Verified that customer purchasing ages fit real-world transaction paradigms (10 to 100 years old).
* Enforced decimal accuracy across all row-level calculations by asserting:  
  \[\text{Revenue} = \text{Final Price} \times \text{Units Sold}\]

---

## Repository Structure

```text
├── indian_ecommerce_pricing_revenue_growth_36_months.csv  # Raw baseline dataset
├── cleaned_ecommerce_data.csv                              # Math-sanitized target asset
├── data_cleaning_pipeline.py                               # Operational cleaning script
└── README.md                                               # Technical documentation
```

---

## Getting Started

### Prerequisites
To run the programmatic cleaning pipeline script locally, you will need python installed along with the following libraries:
```bash
pip install pandas numpy
```

### Execution
Clone the repository and run the operational pipeline script to reproduce the target clean output file:
```bash
python data_cleaning_pipeline.py
```

## Next Milestone
With **Task 1** completed and the transaction parameters formally sanitized, this validated analytical dataset is prepared for **Task 2**: designing an interactive business performance dashboard to track category revenue velocity over the 36-month timeline.
