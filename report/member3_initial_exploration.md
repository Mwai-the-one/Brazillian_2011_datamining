# Member 3: Initial Data Exploration – Online Retail Dataset

## Objective
The goal of this task is to perform **initial data exploration** and **understand the variables** in the Online Retail dataset used by our group for the Data Mining project.

---

## Dataset Overview
- **File name:** Online Retail.xlsx  
- **Rows:** 541,909  
- **Columns:** 8  
- **Domain:** E-commerce  
- **Description:** Contains all transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based online retail store.

---

## Variables and Their Meanings

| Column | Description | Example |
|---------|--------------|----------|
| **InvoiceNo** | Unique identifier for each invoice (transaction). | 536365 |
| **StockCode** | Unique product/item code. | 85123A |
| **Description** | Product description/name. | WHITE HANGING HEART T-LIGHT HOLDER |
| **Quantity** | Number of units of the product purchased. | 6 |
| **InvoiceDate** | Date and time the invoice was generated. | 12/1/2010 8:26 |
| **UnitPrice** | Price per item (in pounds sterling). | 2.55 |
| **CustomerID** | Unique identifier assigned to each customer. | 17850 |
| **Country** | Country where the customer resides. | United Kingdom |

---

## Key Insights from Initial Exploration
1. There are **missing values** in the `CustomerID` and `Description` columns.  
2. Most transactions come from the **United Kingdom**, with some from other countries.  
3. The dataset covers transactions between **2010 and 2011**.  
4. The **`Quantity`** and **`UnitPrice`** columns can be used to calculate the **total revenue** for each transaction.  
5. Data can later be used for **customer segmentation, sales trends**, and **product analysis**.

---

## Next Steps
- Clean missing values and handle duplicates.  
- Create new variable `TotalPrice = Quantity × UnitPrice`.  
- Prepare the dataset for further analysis (Member 4 and 5 will build upon this).
