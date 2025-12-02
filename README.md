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

### Week 4 member 4 Dennis
## 1. Customer Segmentation (K-Means & RFM) 🧑‍🤝‍🧑

This part of the project aimed to group customers into distinct segments based on their purchasing behavior (RFM metrics).
Implementation Steps

    Data Preparation: The first step was filtering the rfm_df to exclude unknown customers (CustomerID != '-1'). This cleaned dataset was then MinMax scaled to normalize the Recency, Frequency, and Monetary values between 0 and 1. This scaling is crucial for K-Means, which relies on distance calculations.

    Optimal K Determination (Silhouette Score):

        You iterated K-Means from K=2 to K=10.

        The Silhouette Score was calculated for each K to measure how similar an object is to its own cluster compared to other clusters.

        Result Analysis (Silhouette Plot): The printed scores and the plot show that K=2 (Score: 0.7397) yielded the highest Silhouette Score. This result statistically suggested that two clusters were the most well-defined and separated groups.

    Final Clustering: Although K=2 was optimal, you chose K=4 for the final segmentation to introduce more variety and potentially discover more granular customer segments, acknowledging that the higher K would result in slightly less distinct clusters (Score: 0.6132).

    Cluster Assignment and Visualization: The Cluster ID was assigned to each customer. The Frequency vs. Monetary scatter plots were generated, with the second, "Zoomed In" plot, effectively mitigating the visual distortion caused by extreme outliers (very high Frequency/Monetary customers) to show the main cluster distribution more clearly.

## Results and Analysis of K=4 Clusters

The validation focused on analyzing the average RFM scores and the size of each of the four clusters.
A. Cluster Characteristics (Average RFM Score)

The bar chart of average RFM scores per cluster (where R=5 is most recent, F/M=5 is highest value) is the key to naming the segments. | Cluster | Avg. R Score (Recency) | Avg. F Score (Frequency) | Avg. M Score (Monetary) | Segmentation Name | Business Insight (Based on your notes) | | :------ | :--------------------- | :----------------------- | :----------------------- | :------------------ | :------------------------------------- | | 0 | 2.5 (Medium) | 2.7 (Medium) | 2.9 (Medium-High) | Average/Medium | Medium customers → upselling strategies | | 1 | 1.0 (Lowest) | 1.8 (Low) | 1.8 (Low) | Churn Risk/Lost | Low value, inactive customers → offer discounts | | 2 | 4.2 (Highest) | 3.6 (High) | 3.6 (High) | VIP/Champions | High value VIP customers → loyalty rewards | | 3 | 1.5 (Low) | 2.3 (Low-Medium) | 2.3 (Low-Medium) | New/Infrequent | New customers → onboarding campaigns |

Note on your notes: Your business insights seem to have mixed the cluster meanings, especially Cluster 1 and Cluster 3 are typically defined differently in standard RFM. Based purely on the data:

    Cluster 2 (VIP/Champions): Highest scores across all metrics. These are your best customers.

    Cluster 1 (Churn Risk/Lost): Lowest Recency score (1.0) means they haven't purchased in the longest time. They are the most inactive.

## B. Cluster Sizes

The bar chart for customer counts provides context on the size of each segment. * Cluster 2 (VIP/Champions) is the largest segment (over 2000 customers), which is highly positive for the business.

    Cluster 0 (Average/Medium) is the next largest (approx. 1000 customers).

    Cluster 1 (Churn Risk/Lost) is the smallest (approx. 500 customers).

## C. Snake Plot

The Snake Plot visualizes the average scaled RFM values (actual Recency/Frequency/Monetary values, not the 1-5 scores). It clearly shows the profile of each cluster: * Cluster 2 (Green Line - VIP/Champions): Stands out dramatically with the highest scaled Frequency and Monetary values, confirming they are the highest value group. They also have the highest scaled Recency (most recent purchases).

    Cluster 0 (Purple Line - Average/Medium): Has moderately high values, especially in Monetary.

    Clusters 1 and 3 (Yellow and Blue Lines): Show generally low scaled values across all metrics compared to Cluster 2.

## 2. Market Basket Analysis (FP-Growth/Apriori) 🛒

This part aimed to find relationships between products purchased together to derive Association Rules, which are useful for cross-selling and product placement.
Implementation Steps

    Data Preparation: Twelve monthly product encoding dataframes were concatenated into a single basket_df. This dataframe, which represents transactions (rows) and products (columns with 0/1 for presence/absence), was then optimized by converting it to a boolean type, which is a key step for memory efficiency in association rule mining.

    Frequent Itemset Generation:

        Combined Data (FP-Growth): The FP-Growth algorithm (an optimized alternative to Apriori) was applied to the entire combined dataset. A minimum support of 0.02 was used.

        Monthly Data (Apriori): The Apriori algorithm was applied separately to each of the 12 monthly datasets, also with a minimum support of 0.02.

    Association Rule Generation:

        Rules were generated from the frequent itemsets using a minimum confidence of 0.3 for both the combined (FP-Growth) and monthly (Apriori) results.

    Rule Validation & Export: The top rules were printed, sorted by Lift, which is the most critical metric for valuable rules (Lift > 1 indicates a positive association). Rules with a lift greater than 1 were exported for future use.

Results and Analysis of Association Rules
# A. Combined Data Analysis (FP-Growth)

The frequent itemsets and association rules derived from the full year provide the most robust, generalizable patterns. The generated visualisations, such as the top itemsets, show which combinations of products are bought together most frequently (high Support).

    Interpretation of Top Rules (sorted by Lift): Rules with a high Lift indicate a strong relationship between the antecedent (product bought) and the consequent (product also bought), beyond random chance. These are the most valuable for recommendations.

        Example: If a top rule is {Item A} → {Item B} (Lift=5.0), it means customers who buy Item A are 5 times more likely to buy Item B than an average customer.

# B. Monthly Analysis (Apriori)

Running Apriori month-by-month allows you to identify seasonal or short-term trends in product associations that might be masked in the annual data.

    Example: A specific combination of products might have a very high support in December (Christmas items) but low support the rest of the year. This helps tailor monthly promotions.

The monthly plots of the Top 15 Frequent Itemsets (Combinations Only) are crucial for visually inspecting the consistency and changes in popular product bundles throughout the year.

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
