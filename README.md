# Term Deposit Marketing Campaign Success Prediction

## Project Overview

This project focuses on developing a **robust machine learning system** to improve the success rate of direct marketing campaigns for a European banking institution.

The primary goal is to **predict whether a customer will subscribe to a term deposit** using demographic, financial, and campaign-related attributes. Beyond prediction, this project emphasizes **business impact** by enabling data-driven decision-making, optimizing marketing strategies, and identifying high-potential customers.

---

## Data Description

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

## Business Objective

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

## Project Workflow

### Data Understanding & Exploration

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
---

### Data Preprocessing

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

### Exploratory Data Analysis (EDA)

EDA was conducted to uncover relationships between features and the target variable.

#### Key Insights

- Customers with **higher balances** are more likely to subscribe  
- **Call duration** strongly correlates with subscription  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/ec2e2fa5-8f26-4047-ac62-3ff505ea3108" />
- Customers contacted **fewer times** show higher conversion rates  
- Certain months (e.g., **March, October**) yield better campaign outcomes  
- Features such as:
  - Job  
  - Education  
  - Marital status  
  - Loan status  
  significantly influence customer behavior
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/ec2e2fa5-8f26-4047-ac62-3ff505ea3108" />


---
## Project Approaches

### Approach 1: Full Feature Model

**Goal:** To establish a benchmark by building a model using all available features to understand overall feature importance. This model aims to identify the strongest predictors of term deposit subscription.

**Methodology:**
- Initial data exploration and preprocessing (handling categorical variables, checking for missing values, outlier analysis).
- Training and evaluating various classification models (Bagging, Random Forest, GBM, AdaBoost, Decision Tree, XGBoost) with and without class weighting, using undersampled data, oversampled data to address class imbalance.
- Hyperparameter tuning for top-performing models (Random Forest, GBM, XGBoost) using `RandomizedSearchCV` with `recall` as the primary scoring metric.

**Key Outcomes:**
- The full-feature model achieved the highest predictive performance, with XGBoost and Random Forest (tuned) emerging as the best-performing models.
- Random Forest delivered slightly higher recall (identifying more actual subscribers), while XGBoost provided significantly better precision (fewer false positives).
- The "duration" of the last contact was identified as the most important feature, but its post-call nature made this model impractical for pre-call prediction.
- Best XGBoost model achieved an average recall of 78.05% with a standard deviation of 2.15% on the training set using 10-fold cross validation.

### Approach 2: Pre-Call Prediction Model (without 'Duration')

**Goal:** To build a practical model that can predict term deposit subscriptions before any customer contact, by excluding the 'duration' feature. This model uses features known prior to contacting the customer (demographic, financial, and some campaign-related variables like contact type and month) enabling more efficient targeting, seasonality and better allocation of marketing resources.

**Methodology:**
- Removed the `duration` feature from the dataset.
- Retrained and re-tuned top-performing models (XGBoost, LightGBM, CatBoost) on the modified dataset.
- Evaluated performance using recall and precision metrics on training and validation sets.
- Performed Gain and Lift analysis to assess the model's business impact in targeting potential subscribers.

**Key Outcomes:**
- LightGBM and CatBoost achieved higher recall, capturing more potential subscribers, while XGBoost offered higher precision.
- Gain curve analysis demonstrated that targeting the top 20% of customers, as identified by LightGBM, could capture approximately 49% of all actual subscribers.
- Lift curve analysis demonstrated that a lift of 5 at the 'top 10% of targeted population' means finding 5 times more actual subscribers than random selection, significantly reducing wasted marketing efforts.
- Important features for pre-call prediction included 'balance', 'age', 'job', 'marital', 'education', 'contact_type', 'month', and 'day'.
- Campaigns during high-performing months (e.g., March, April, October) significantly increased effectiveness.

### Approach 3: Demographic-Only Model (without Campaign Data)

**Goal:** To build a simplified model focusing solely on inherent customer characteristics (demographic and financial attributes), excluding all campaign-related features. The aim is to understand customer predispositions to subscribe independent of marketing efforts, supporting early-stage customer segmentation and strategic planning.

**Methodology:**
- Dropped all campaign-related features ('day', 'month', 'duration', 'campaign', 'contact'). Also removed the original 'age' and introduced 'age_group' for broader insights.
- Trained and tuned XGBoost, LightGBM, and CatBoost models on this reduced feature set.
- Evaluated models based on Precision-Recall curves and Gain Curves.
- Analyzed feature importances to identify key demographic and financial drivers.

**Key Outcomes:**
- LightGBM and CatBoost showed the highest recall performance, demonstrating their ability to identify a larger proportion of potential subscribers even without campaign-specific data.
- Targeting the top 20% of customers identified by this model could capture approximately 36% of all actual subscribers.
- Key features for predicting subscription in this context were 'balance', 'age_group', 'job', 'marital status', 'education', 'housing loan', and 'personal loan'.
- The model highlights the importance of financial stability and certain demographic profiles in identifying high-potential customers for term deposits.

### Approach 4: Customer Segmentation (for Subscribers Only)

**Goal:** To segment existing subscribers ('y=1') into distinct groups based on their characteristics. This approach aims to uncover nuanced profiles of successful conversions, allowing for highly targeted marketing strategies for future campaigns.

**Methodology:**
- Filtered the dataset to include only customers who subscribed (y=1).
- Applied K-Means clustering to identify natural groupings within this segment.
- Used the Elbow Method to determine the optimal number of clusters (k=3).
- Employed Principal Component Analysis (PCA) for visualizing clusters in a reduced dimension.
- Analyzed and profiled each cluster based on their feature distributions.

**Key Outcomes:**
- Three distinct customer segments were identified among subscribers:
    - **Cluster 0: The Engaged & Deliberate Considerers** (Middle-aged, moderate to higher balances, diverse job roles, requires longer engagement).
    - **Cluster 1: The Young, Responsive, and Efficient Subscribers** (Youngest, good balances for their age, professional roles, quick decision-makers).
    - **Cluster 2: The Mature, Affluent, and Confident Investors** (Oldest and wealthiest, often retired/senior management, high balances, low loan burden, convert easily).
- These segment profiles enable the development of tailored messaging, channel strategies, and timing for future marketing efforts.
  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/79fa5eb7-2bce-45e7-995d-41b34be8cb11" />
  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/d40a8ec2-3d79-4014-a21e-500173fc1083" />
  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/300facbe-4773-4b27-83e9-914c7a8ba02b" />
  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/2aba0576-5cba-4281-a5a0-508f0cc62f75" />
  <img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/b533d5d5-3611-4f86-8955-21cf33b0b9bb" />






## Model Evaluation Metrics

- Precision → Minimize false positives  
- Recall → Capture maximum subscribers  
- Gain Curve → % of subscribers captured  
- Lift Curve → Improvement over random targeting  

## Business Insights

- Customers with **higher account balances** show significantly higher subscription rates, indicating strong purchasing power and investment readiness  

- **Middle-aged and older customers (30+)** are more likely to invest, reflecting stable financial behavior and long-term planning  

- Certain professions such as **management, technicians, and retirees** have higher conversion rates, likely due to financial stability  

- Customers with **tertiary education** are more likely to subscribe, suggesting that financial awareness influences decision-making  

- Customers with **no housing or personal loans** have a higher probability of subscribing due to fewer financial obligations  

- **Cellular communication** is the most effective contact method, driving higher engagement and conversions  

- **Campaign timing plays a critical role** — months like **March, April, and October** consistently show higher success rates  

- Customers who convert are typically contacted **fewer times**, while excessive contact reduces success rates  

- Machine learning models (**LightGBM**) show that targeting the **top 20% of customers** can capture up to **~50% of total subscribers**, significantly improving efficiency  

- Customer segmentation reveals **distinct behavioral patterns**:
  - Some customers require **multiple interactions and trust-building**
  - Some are **fast decision-makers** with minimal engagement
  - High-value customers respond well to **personalized and premium communication**

---

## Business Recommendations

### Target High-Value Customer Segments
Focus marketing efforts on **older customers, financially stable professions, and low-debt individuals** to maximize conversion probability and campaign ROI.

---

### Optimize Campaign Timing
Strategically launch campaigns during **high-performing months (March, April, October)** to leverage seasonal trends and improve response rates.

---

### Implement Predictive Targeting (LightGBM)
Deploy a **LightGBM model** to score and rank customers based on conversion probability, enabling **data-driven prioritization of high-value leads before outreach**.

---

### Combine Customer Profiling + Campaign Timing
Integrate **customer segmentation insights with seasonal trends** to maximize conversions instead of relying on broad, untargeted campaigns.

---

### Develop Segment-Specific Messaging
Create **data-driven communication strategies**:
- Use **trust-building, detailed messaging** for customers needing longer engagement  
- Use **fast, digital-first messaging** for younger, quick-converting segments  
- Use **premium, personalized messaging** for high-value and affluent customers  

---

### Optimize Outreach Strategy
- Prioritize **cellular communication channels** for higher engagement  
- Avoid excessive contact attempts to prevent reduced conversion rates  
- Focus on **quality over quantity in outreach efforts**  

---

### Continuous Model Monitoring & Improvement
- Monitor model performance using key metrics  
- Retrain models with new data  
- Adapt to evolving customer behavior and market trends  



## Summary

This project demonstrates how machine learning can transform traditional marketing campaigns into **targeted, efficient, and data-driven systems**.

By leveraging customer data effectively, businesses can:
- **50–80% reduction in outreach efforts** while still capturing a large portion of conversions  
- Significant **cost savings in call center operations, marketing spend, and human resources**  
- Improved **ROI by prioritizing high-value leads instead of mass targeting**  
- More effective use of **time, workforce, and campaign budgets**  

---

## Author

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
