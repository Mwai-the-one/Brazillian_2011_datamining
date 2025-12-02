# 🛍️ DSA2040A_DataMining_EcomAnalytics  
### *Uncovering Hidden Patterns in Brazil’s E-Commerce World* 🇧🇷  

---

## 🌟 Project Overview

Welcome to our **end-to-end data mining adventure!**  
In this project, we dive deep into the **Brazilian E-Commerce Public Dataset by Olist**, exploring how real customers shop, how sellers perform, and what drives customer satisfaction in Brazil’s growing online marketplace.  

Our mission is to transform messy, real-world data into **actionable insights** — moving through every stage of the pipeline:  
**ETL → EDA → Data Mining → Insights & Storytelling.**

We aim to answer *real business questions*, build machine learning models, and visualize insights that help e-commerce platforms like Olist **make smarter, data-driven decisions.** 💡

---

## 🎯 Objectives & Research Questions

Our analysis focuses on solving key business problems through data-driven insights:

### 👩‍💻 Customer Insights
- Who are Olist’s most valuable customers?  
- Which **regions** in Brazil drive the most sales and revenue?  
- Can we segment customers based on purchase frequency or spending?

### 📦 Product & Sales Analysis
- Which **product categories** are top performers?  
- How does **seasonality** affect order volume?  
- What are the most preferred **payment methods** and how do they affect purchase value?

### ⭐ Customer Experience
- What factors influence **review scores**?  
- Do **late deliveries** lower satisfaction levels?  
- Are there **correlations** between order value, payment type, and ratings?

### 🧠 Predictive & Pattern Discovery
- Can we **predict** customer satisfaction levels?  
- Which products are **frequently bought together** (Market Basket Analysis)?  

---


### Members contribution
## Week 2 member 2 Gachunga Gift
Detailed Week 2 Contribution Summary

During Week 2, significant progress was made in building a full data preparation pipeline, starting from raw Excel data to clean, structured, encoded datasets ready for mining tasks. The work involved ETL development, data cleaning, missing value handling, outlier detection, feature engineering, scaling, and monthly one-hot encoding.

The process began with the creation of an ETL pipeline that loaded the raw Excel dataset, standardized column names, and converted key fields such as InvoiceDate into the proper datetime format. Invalid rows containing zero or negative Quantity or UnitPrice were removed, eliminating 11,699 faulty transactions. The pipeline provided clear validation feedback by printing the dataset’s initial and final shapes (from 547,328 rows down to 514,256) and returned a cleaned DataFrame that served as the foundation for the rest of the processing.

Further cleaning included removing 8,065 duplicate records to ensure data consistency. Missing values were carefully handled: missing country names were replaced with "Unknown", rows missing critical identifiers such as InvoiceDate, InvoiceNo, or StockCode were removed entirely, and missing CustomerID fields were filled with -1 so those transactions could still be used analytically. Negative quantities were preserved but flagged using a new IsReturn column to distinguish returned items. Country naming inconsistencies (like “RSA”, “EIRE”, “European Community”) were standardized to more accurate and uniform names. Additional analytical features were engineered, including TotalPrice and date-based fields such as Year, Month, and Day derived from InvoiceDate. The cleaned dataset was then exported to cleaned_data.csv.

Outlier detection was performed using the Interquartile Range (IQR) method. Outliers in Quantity and UnitPrice were identified, with clear upper and lower bounds calculated for each numeric variable. Sample outlier records were displayed to provide context on the data points that fell outside acceptable thresholds. Multiple strategies for handling these outliers were implemented: removing extreme values entirely, applying Winsorization to cap values within IQR limits, and eliminating records with zero or negative prices. These different approaches resulted in several alternative cleaned datasets (df_clean, df_capped, df_no_zero_price), offering flexibility for subsequent analysis and model selection.

To prepare the data for market basket mining, scaling was applied to Quantity and UnitPrice using MinMaxScaler to ensure consistent ranges for algorithms sensitive to value magnitude. The dataset was then segmented by month to allow month-specific transaction pattern analysis. For each month, transactions were reconstructed by grouping products under each invoice, creating realistic item lists per transaction. The TransactionEncoder was used to convert these item lists into one-hot encoded matrices, with sparse matrix handling implemented to preserve memory efficiency. The encoded datasets for each month were saved separately, such as encoded_products_Month_11.csv for November and encoded_products_Month_12.csv for December, providing ready-to-use inputs for Apriori and association rule mining in later stages.

Overall, the Week 2 work produced a comprehensive, well-cleaned, validated, and fully encoded dataset pipeline that transforms raw retail data into structured, analysis-ready inputs suitable for advanced data mining processes.

### Member 3: Whitney Gituara.
### Statistical Analysis & Correlation Studies

As Member 3, I was responsible for leading the statistical analysis and correlation assessment phase of the Exploratory Data Analysis (EDA). My role focused on extracting meaningful numerical insights from the cleaned dataset and quantifying relationships between key customer behavior variables to support informed decision-making and the upcoming data mining phase.

 Summary Statistics & Distribution Analysis

I computed descriptive statistics for core numerical variables such as Quantity and TotalPrice using summary measures (mean, standard deviation, min, max, and quartiles). This provided a clear overview of purchase behavior, spending patterns, and the overall spread of transaction values. To further understand the data, I:

Generated distribution plots to examine how purchases are spread across different countries.

Identified the number of unique values in key categorical variables such as Country and Description to evaluate product diversity and market coverage.

Country-Level Statistical Insights

I analyzed average purchase values per country, allowing us to identify regions with the highest average customer spending. This supports geographic market performance analysis and helps prioritize high-value customer regions.

Correlation & Relationship Analysis (RFM Metrics)

To support customer segmentation and behavioral analysis, I conducted a detailed correlation study using the RFM (Recency, Frequency, Monetary) metrics:

Computed the Pearson correlation between Recency and Monetary value to understand how recent customer activity relates to spending behavior.

Generated a full correlation matrix for Recency, Frequency, and Monetary values to quantify inter-variable relationships.

Visualized these relationships using a correlation heatmap, providing an intuitive interpretation of customer behavior dynamics.

These results were crucial in validating assumptions for RFM-based customer segmentation and guiding feature selection for the mining phase.

✅ Key Impact on the Project

My contributions ensured that:

The dataset was statistically explored and validated beyond basic visualization.

Hidden relationships between customer behavior variables were uncovered and quantified.

The team gained a solid numerical foundation for segmentation, predictive modeling, and business interpretation.

The RFM structure was statistically justified before being used in further clustering and mining tasks.
✅ Importance of Week 3 to the Overall Project

Week 3 serves as the analytical backbone of the project, bridging the gap between data cleaning (Week 2) and data mining/modeling (subsequent weeks). The statistical and correlation analyses carried out during this week ensure that:

The dataset is well-understood, reliable, and analytically sound.

Features selected for mining are justified by statistical evidence.

All predictive, clustering, and rule-mining models are built on a validated exploratory foundation rather than assumptions.

## 🧾 Dataset Description

**📚 Source:** [Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)  
**📊 Data Period:** 2016–2018  

**📦 Files Included:**

| File | Description |
|------|--------------|
| `olist_orders_dataset.csv` | Order details and delivery statuses |
| `olist_order_items_dataset.csv` | Products sold per order |
| `olist_products_dataset.csv` | Product category metadata |
| `olist_cu_
```
DSA2040A_DataMining_EcomAnalytics/
├── data/
│ ├── raw/ # Original Olist CSV files
│ ├── transformed/ # Cleaned and merged datasets
│ └── final/ # Ready-to-analyze datasets
├── notebooks/
│ ├── 1_extract_transform.ipynb
│ ├── 2_exploratory_analysis.ipynb
│ ├── 3_data_mining.ipynb
│ └── 4_insights_dashboard.ipynb
├── report/
│ ├── executive_summary.pdf
│ └── presentation.pptx
├── requirements.txt
├── .gitignore
└── README.md

```
---

## 👥 Team Members & Roles

| 🧑‍💻 Name | 🎓 Role | 🔍 Responsibilities |
|------------|----------|---------------------|
| *[Member 1]* | **ETL Lead** | Data extraction, cleaning, and transformation |
| *[Member 2]* | **Data Analyst** | EDA, visualization, and summary statistics |
| *[Member 3]* | **Data Miner / Modeler** | Clustering, classification, and association rules |
| *[Member 4]* | **Reporter / Presenter** | Dashboard creation, executive summary, presentation |
| *All Members* | **Collaborators** | Each makes ≥3 commits and documents their notebook sections |

---

## 🧰 Tools & Technologies

🖥️ **Programming:** Python (Pandas, NumPy, scikit-learn)  
📊 **Visualization:** Seaborn, Matplotlib, Plotly, Power BI  
🤖 **Machine Learning:** K-Means, Logistic Regression, Decision Tree, Apriori  
📁 **Version Control:** Git & GitHub (team collaboration)  
🧾 **Reporting:** Jupyter Notebooks, PDF Summary, PowerPoint Slides  

---

## 🚀 Expected Outcomes

By the end of this project, we will have:  
✅ A **clean and enriched dataset** ready for analysis  
📈 A **detailed exploratory analysis** with visual insights  
🤖 **Machine learning models** for prediction and clustering  
🛍️ **Actionable business insights** for e-commerce strategy  
🎨 A **mini dashboard** for storytelling and presentation  

This project showcases how **data science turns raw transactions into strategic intelligence** — helping businesses grow smarter, faster, and stronger! 💪📊  

---

Ultimately, this project demonstrates how data science transforms raw transactions into strategic intelligence — one dataset at a time. 🔥
