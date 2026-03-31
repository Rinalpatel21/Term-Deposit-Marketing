# 📊 Term Deposit Marketing Campaign Success Prediction

## 🚀 Project Overview

This project focuses on developing a **robust machine learning system** to improve the success rate of direct marketing campaigns for a European banking institution.

The primary goal is to **predict whether a customer will subscribe to a term deposit** using demographic, financial, and campaign-related attributes. Beyond prediction, this project emphasizes **business impact** by enabling data-driven decision-making, optimizing marketing strategies, and identifying high-potential customers.

---

## 📁 Data Description

The dataset contains customer information collected through direct marketing campaigns, primarily via phone calls.

### Key Features

- **age** – Age of the customer (numeric)  
- **job** – Type of job (categorical)  
- **marital** – Marital status (categorical)  
- **education** – Educational background (categorical)  
- **default** – Has credit in default? (binary)  
- **balance** – Average yearly balance in euros (numeric)  
- **housing** – Has a housing loan? (binary)  
- **loan** – Has a personal loan? (binary)  
- **contact** – Contact communication type (categorical)  
- **day** – Last contact day of the month (numeric)  
- **month** – Last contact month of the year (categorical)  
- **duration** – Last contact duration in seconds (numeric)  
- **campaign** – Number of contacts performed during this campaign (numeric)  
- **y** – Target variable: subscription to term deposit (Yes/No)  

---

## 🎯 Business Objective

The core objective of this project goes beyond prediction and focuses on **business optimization**.

### Goals

- Predict whether a customer will subscribe to a term deposit  
- Identify **high-conversion customer segments**  
- Reduce unnecessary marketing efforts by targeting **high-value leads**  
- Improve overall **campaign efficiency and ROI**  
- Provide **actionable insights** for stakeholders  

### Business Problem

> **How can we maximize conversions while minimizing cost and effort?**

---

## 🔄 Project Workflow

### 1️⃣ Data Understanding & Exploration

The initial phase focused on exploring the dataset to understand its structure and patterns.

#### Key Findings

- Strong class imbalance:
  - **92.76% → No subscription**
  - **7.24% → Subscription**
- Right-skewed distributions in:
  - `balance`
  - `duration`
  - `campaign`
- Presence of outliers in financial and interaction features  
- Diverse categorical distributions across:
  - Job  
  - Education  
  - Marital status  

This step helped form **initial hypotheses** about customer behavior and guided further analysis.

---

### 2️⃣ Data Preprocessing

To prepare the data for modeling, several preprocessing steps were applied:

- Handled missing values and **‘unknown’ categories**  
- Encoded categorical variables using appropriate techniques  
- Scaled/normalized numerical features where necessary  
- Addressed class imbalance using:
  - Oversampling  
  - Undersampling  
- Created derived features such as:
  - **Age groups** for better interpretability  

These steps ensured the dataset was **clean, structured, and ready for modeling**.

---

### 3️⃣ Exploratory Data Analysis (EDA)

EDA was conducted to uncover relationships between features and the target variable.

#### Key Insights

- Customers with **higher balances** are more likely to subscribe  
- **Call duration** strongly correlates with subscription  
  - ⚠️ Not usable for pre-call prediction  
- Customers contacted **fewer times** show higher conversion rates  
- Certain months (e.g., **March, October**) yield better campaign outcomes  
- Features such as:
  - Job  
  - Education  
  - Marital status  
  - Loan status  
  significantly influence customer behavior  

EDA provided both **statistical and visual insights**, forming the foundation for modeling and business recommendations.

---

## 📌 Summary

This project demonstrates how machine learning can transform traditional marketing campaigns into **targeted, efficient, and data-driven systems**.

By leveraging customer data effectively, businesses can:
- Improve conversion rates  
- Reduce unnecessary outreach  
- Optimize resource allocation  
- Make better strategic decisions  

---

## 👨‍💻 Author

**Rinal Patel**  
📍 Houston, TX  

- 🔗 LinkedIn: https://www.linkedin.com/in/rinalpatel-datascientist  
- 💻 GitHub: https://github.com/Rinalpatel21  

---

## ⭐ Final Note

This project highlights the ability to:
- Translate business problems into machine learning solutions  
- Perform end-to-end data analysis and modeling  
- Generate actionable business insights  
- Build practical, real-world deployable models  
