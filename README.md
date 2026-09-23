# AI-Powered Retail Analytics & Intelligent Customer Churn Predictor

## 1. Project Overview

This project combines retail analytics with machine learning to understand customer purchasing behavior and identify customers who are likely to churn.

The project performs:

- Transaction data cleaning
- Revenue and order analytics
- Monthly sales trend analysis
- Country and product analysis
- RFM (Recency, Frequency, Monetary) customer segmentation
- Time-based customer churn labeling
- Random Forest churn prediction
- Model evaluation using Accuracy, Precision, Recall, F1-score and ROC-AUC
- Feature importance analysis
- Customer-level churn probability and risk bands

## 2. Dataset

**Dataset:** UCI Online Retail

**Official dataset page:**  
https://archive.ics.uci.edu/dataset/352/online+retail

**Dataset DOI:** 10.24432/C5BW33

The UCI description states that the dataset contains transactions from 01/12/2010 to 09/12/2011 for a UK-based non-store online retailer. The dataset has 541,909 transaction records and includes invoice, product, quantity, date, price, customer and country information.

### Dataset loading

The notebook first uses the `ucimlrepo` Python package:

```python
from ucimlrepo import fetch_ucirepo
online_retail = fetch_ucirepo(id=352)
raw = online_retail.data.features.copy()
```

If that method is unavailable, download `Online Retail.xlsx` from the UCI page and place it in the same folder as the notebook.

## 3. Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- UCI ML Repository / `ucimlrepo`
- Excel/XLSX data source

## 4. Project Structure

```text
AI_Retail_Analytics_Churn_Project/
│
├── Anubhav_Chaurasiya_AI_Retail_Analytics_Churn_Predictor.ipynb
├── requirements.txt
├── README.md
└── Anubhav_Chaurasiya_ProjectReport.docx
```

After execution, the notebook can also create:

```text
customer_churn_risk_output.csv
model_metrics.csv
```

## 5. Setup Instructions

### Step 1 — Install Python

Install Python 3.10 or newer.

### Step 2 — Create a virtual environment (recommended)

Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

macOS/Linux:

```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4 — Start Jupyter

```bash
jupyter notebook
```

Open:

```text
Anubhav_Chaurasiya_AI_Retail_Analytics_Churn_Predictor.ipynb
```

### Step 5 — Run all cells

Use:

**Kernel → Restart Kernel and Run All**

The notebook downloads/loads the dataset, cleans it, performs analytics, builds customer features, trains the model and generates outputs.

## 6. Churn Definition

The model uses a time-based approach.

1. Find the last transaction date in the dataset.
2. Reserve the final 90 days as the future/prediction period.
3. Build customer features using only transactions before that 90-day period.
4. Label a customer as:
   - `1 = Churned`: no purchase during the following 90 days.
   - `0 = Not Churned`: at least one purchase during the following 90 days.

This reduces target leakage compared with calculating churn directly from the same period as the input features.

## 7. Machine Learning Model

The main model is a **Random Forest Classifier** with:

- Class balancing
- Numerical imputation
- Standardization
- One-hot encoding for country
- 80/20 stratified train/test split

Evaluation metrics:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix
- ROC curve

## 8. Key Features

| Feature | Meaning |
|---|---|
| Recency | Days since customer's last purchase |
| Frequency | Number of unique invoices |
| Monetary | Total customer revenue |
| TotalItems | Total purchased quantity |
| UniqueProducts | Number of unique products |
| AvgQuantity | Average quantity per transaction line |
| ActiveDays | Number of distinct purchase days |
| AvgOrderValue | Revenue divided by number of orders |
| CancellationCount | Number of cancellation lines before cutoff |
| Country | Customer's most common country |

## 9. Risk Bands

The notebook provides example operational bands:

- Low Risk: churn probability < 0.40
- Medium Risk: 0.40–0.69
- High Risk: >= 0.70

These thresholds are configurable and should be validated against actual campaign costs and business objectives.

## 10. Expected Outputs

The notebook produces:

- Retail KPI table
- Monthly revenue chart
- Top-country revenue chart
- Top-product revenue table
- RFM segment summary
- Customer churn distribution
- Model performance metrics
- Classification report
- Confusion matrix
- ROC curve
- Feature importance chart
- Customer risk table
- `customer_churn_risk_output.csv`
- `model_metrics.csv`

## 11. Academic / Business Use

This project demonstrates how historical transaction data can be transformed into actionable customer intelligence. It can be extended into a web dashboard using Streamlit, Flask or Django, or connected to Power BI/Tableau for visualization.

## 12. Limitations

The model is based on historical transaction data from one retailer. Churn is defined using a 90-day inactivity window, which is an operational definition rather than a universal definition of churn. Model predictions are probabilistic associations and should be monitored and validated before being used for automated customer actions.

## 13. Dataset Citation

Chen, D. (2015). **Online Retail**. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
