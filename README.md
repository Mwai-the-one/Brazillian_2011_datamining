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

#### 🌟 Member 3: Whitney Gituara
### 📊 Statistical Analysis & Correlation Studies

As Member 3, I was responsible for leading the statistical analysis and correlation assessment phase of the Exploratory Data Analysis (EDA). My role focused on extracting meaningful numerical insights from the cleaned dataset and quantifying relationships between key customer behavior variables to support informed decision-making and the upcoming data mining phase.

## 📈 Summary Statistics & Distribution Analysis

I computed descriptive statistics for core numerical variables such as Quantity and TotalPrice using summary measures (mean, standard deviation, minimum, maximum, and quartiles). This provided a clear overview of:
✅ Purchase behavior
✅ Spending patterns
✅ The overall spread of transaction values

To further understand the data, I:
🔹 Generated distribution plots to examine how purchases are spread across different countries.
🔹 Identified the number of unique values in key categorical variables such as Country and Description to evaluate product diversity and market coverage.

## 🌍 Country-Level Statistical Insights

I analyzed the average purchase values per country, which allowed us to:
📌 Identify regions with the highest average customer spending
📌 Support geographic market performance analysis
📌 Help prioritize high-value customer regions

## 🔗 Correlation & Relationship Analysis (RFM Metrics)

To support customer segmentation and behavioral analysis, I conducted a detailed correlation study using RFM (Recency, Frequency, Monetary) metrics:

✅ Computed the Pearson correlation between Recency and Monetary value to understand how recent customer activity relates to spending behavior.
✅ Generated a full correlation matrix for Recency, Frequency, and Monetary values to quantify inter-variable relationships.
✅ Visualized these relationships using a correlation heatmap, providing an intuitive interpretation of customer behavior dynamics.

These results were crucial in validating assumptions for RFM-based customer segmentation and guiding feature selection for the mining phase.

## ✅ Key Impact on the Project

My contributions ensured that:

✔️ The dataset was statistically explored and validated beyond basic visualization
✔️ Hidden relationships between customer behavior variables were uncovered and quantified
✔️ The team gained a solid numerical foundation for
  • Segmentation
  • Predictive modeling
  • Business interpretation
✔️ The RFM structure was statistically justified before being used in further clustering and mining tasks

## 🗓️ Importance of Week 3 to the Overall Project

Week 3 serves as the analytical backbone of the project, bridging the gap between:
📍 Data Cleaning (Week 2) and
📍 Data Mining & Modeling (Subsequent Weeks)

The statistical and correlation analyses carried out during this week ensure that:

✅ The dataset is well-understood, reliable, and analytically sound
✅ Features selected for mining are justified by statistical evidence
✅ All predictive, clustering, and rule-mining models are built on a validated exploratory foundation rather than assumptions
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

## A. RFM Cluster Profiles and Strategic Recommendations

The K-Means Clustering resulted in four distinct customer segments based on their average RFM scores (where scores are on a 1-5 scale, with 5 being the best in each category). Analyzing these scores is the key step in naming the segments and defining their specific marketing strategies.

## 👥 RFM Cluster Profiles and Strategic Recommendations

The K-Means clustering yielded four distinct customer segments based on their average RFM scores (1-5 scale, with 5 being the highest/best).

| Cluster | Avg. R Score | Avg. F Score | Avg. M Score | Segment Name | Rationale & Recommended Action |
| :---: | :---: | :---: | :---: | :---: | :--- |
| **1** | 4.2 (Highest) | 3.6 (High) | 3.6 (High) | **VIP / Champions** | Highest scores across all metrics. **Action:** Implement exclusive **loyalty rewards** and high-touch service to maintain retention. |
| **3** | 2.5 (Medium) | 2.7 (Medium) | 2.9 (Medium-High) | **Average Value** | Solid customers, but with room for growth. **Action:** Focus on **upselling** and personalized offers to move them into the VIP category. |
| **2** | 1.5 (Low) | 2.3 (Low-Medium) | 2.3 (Low-Medium) | **Needs Attention** | Low Recency (1.5) and moderate F/M. Could be New Customers or Hibernating. **Action:** **Onboarding** or reactivation campaigns to encourage repeat purchases. |
| **0** | 1.0 (Lowest) | 1.8 (Low) | 1.8 (Low) | **Churn Risk / Lost** | Very low Recency indicates they haven't bought recently. **Action:** Launch aggressive **win-back campaigns** and discounts to reactivate them. |

Key Takeaways

    Cluster 2 (VIP/Champions) is the most valuable segment and should be prioritized for retention efforts.

    Cluster 1 (Churn Risk/Lost) represents the most immediate challenge and requires urgent, incentive-based intervention.

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

## 📅 Week 5: Insights, Storytelling & Dashboard- Peter Kidiga

### 🎯 Overview
In this final phase (Week 5), we synthesized the findings from our ETL pipeline, Exploratory Data Analysis (EDA), and Data Mining models (Clustering & Apriori/FP-Growth) into actionable business intelligence. The goal was to translate raw data into a visual story that informs strategic decision-making.

### 📂 Final Deliverables
| File Name | Description |
|-----------|-------------|
| `notebooks/4_insights_dashboard.ipynb` | A Jupyter Notebook containing the "Mini Dashboard" code. It visualizes seasonality, customer clusters (Snake Plots/Scatter), and top association rules. |
| `report/executive_summary.pdf` | A 2-page executive report summarizing the methodology, 4 key findings, and 3 strategic business recommendations. |
| `report/presentation.pptx` | The final slide deck presenting the end-to-end data pipeline and business story. |

### 📊 Dashboard Features
The **Strategic Dashboard** in Notebook 4 visualizes:
1.  **Seasonal Revenue Trends:** Identifies peak sales months (specifically November) for inventory planning.
2.  **Customer Segmentation:** Visualizes the 4 K-Means clusters (VIPs, At-Risk, New, Big Spenders) based on Frequency vs. Monetary value.
3.  **Market Basket Opportunities:** Displays the top product associations with the highest "Lift," identifying candidates for product bundling.
4.  **Geographic Performance:** Highlights the top revenue-generating countries.

### 🚀 How to Run the Dashboard
To generate the dashboard and insights, follow these steps:

1.  **Prerequisites:** Ensure the Week 4 mining results are saved. The dashboard depends on:
    * `data/transformed/rfm_results.csv` (From Notebook 3)
    * `data/transformed/market_basket_rules.csv` (From Notebook 3)
2.  **Launch the Notebook:**
    ```bash
    jupyter notebook notebooks/4_insights_dashboard.ipynb
    ```
3.  **View Output:** Run all cells to generate the 5-panel Matplotlib/Seaborn visualization grid.

### 💡 Key Findings
* **Segmentation:** The "VIP" cluster drives the highest revenue despite not being the largest group; retention efforts should focus here.
* **Associations:** High-lift rules (>1.0) exist between Tea Sets and Saucers, validating a cross-selling strategy.
* **Seasonality:** Revenue drops significantly post-December; marketing campaigns are required in Q1 to maintain cash flow.

This project showcases how **data science turns raw transactions into strategic intelligence** — helping businesses grow smarter, faster, and stronger! 💪📊  

---

Ultimately, this project demonstrates how data science transforms raw transactions into strategic intelligence — one dataset at a time. 🔥

Daisy Yano- Member 5, week 5
Week 5: Insights Dashboard & Storytelling
Overview

This project presents a consolidated Mini Dashboard that transforms raw e-commerce data into actionable business insights. It combines exploratory data analysis, customer segmentation, market basket analysis, and geographic revenue insights to support strategic decision-making.

The goal is to provide a clear, visual narrative that helps executives and managers make informed decisions based on customer behavior, product associations, and seasonal trends.

Key Insights
Seasonal Revenue Trends

Highlights monthly revenue patterns to identify seasonality.

Helps businesses anticipate peak periods and plan inventory accordingly.

Customer Segmentation

Identifies clusters of customers based on purchase frequency and spending.

Supports targeted marketing strategies for high-value customers and retention campaigns for lower-frequency segments.

Segment Distribution

Illustrates the size and proportion of each customer segment.

Guides resource allocation and marketing focus for maximum impact.

Top Product Associations

Reveals product bundles that frequently occur together.

Supports cross-selling, upselling, and the creation of promotional bundle offers.

Geographic Revenue

Shows which countries or regions contribute most to revenue.

Informs market expansion strategies and localized marketing campaigns.

Actionable Recommendations

Targeted Marketing

Offer loyalty programs for high-value clusters.

Reactivate low-frequency customers with engagement initiatives.

Product Bundling

Promote frequently bought-together products as bundles.

Increase overall basket size and revenue per customer.

Inventory Planning

Adjust stock levels to match seasonal sales peaks.

Ensure popular items are well-stocked ahead of peak months.

Geographic Focus

Prioritize marketing and stock planning in top-performing markets.

Explore opportunities in secondary markets for growth.

Project Structure
Brazillian_2011_datamining/
│
├─ data/                   # Raw, transformed, and final datasets
│
├─ notebooks/              # Jupyter notebooks for analysis
│
├─ report/                 # Executive summary and documentation
│
└─ README.md               # Project overview and insights

Full Project Summary

This repository represents a comprehensive e-commerce analytics workflow. It covers the entire process from raw data collection to actionable insights:

Data Cleaning & Transformation

Handling missing values, correcting inconsistencies, and preparing datasets for analysis.

Exploratory Data Analysis (EDA)

Understanding overall trends, distributions, and correlations within the data.

Customer Segmentation

Using RFM analysis and clustering to identify high-value, medium, and low-value customers.

Market Basket Analysis

Applying Apriori algorithm to uncover product associations and bundle opportunities.

Insights Dashboard & Storytelling (this part)

Synthesizing findings into a visual and textual dashboard for decision-makers.

Reporting

Delivering an executive summary with actionable recommendations for marketing, sales, and inventory planning.

Overall, this project demonstrates end-to-end data science in an e-commerce context, combining analytics, visualization, and business storytelling to guide strategic decisions and optimize revenue.
