# F1 Race Retirement Prediction – Pre-Race Machine Learning Model

This project builds a machine learning model to predict whether a Formula 1 car will **finish** or **retire (DNF)** *before the race starts*, using only **pre-race features** such as grid position, driver age, constructor, circuit and historical retirement rate.

---

## 🎯 Problem Statement

Can we estimate the likelihood of a driver **not finishing (DNF)** a race *before* the lights go out?

Accurate pre-race risk prediction can help teams:

- Optimise race strategy  
- Identify high-risk scenarios  
- Allocate engineering resources  
- Improve driver safety and reliability  

---

## 🧵 Data Overview  

This project uses multiple relational F1 tables:

- `results` – race outcome and status ID  
- `races` – race date, year, round, circuit ID  
- `drivers` – driver details and date of birth  
- `constructors` – team/constructor information  
- `status` – textual description of finish/retirement reason  
- `circuits` – circuit metadata  

These tables are merged using keys such as:

- `raceId`
- `driverId`
- `constructorId`
- `statusId`
- `circuitId`

---

## 🧮 Feature Engineering  

Key engineered pre-race features:

- **Driver age on race day**  
- **Grid position**  
- **Constructor (one-hot encoded)**  
- **Circuit (one-hot encoded)**  
- **Historical retirement rate** per driver up to that race  

### Additional Features (Model 2 Only – Exploratory)
Used **in-race data** such as:

- Pit stop count  
- Fastest lap  
- Lap times  

These were removed for the deployment-ready model.

---

## 🧠 Models

### **Model 1 – Naive Baseline**
- Predicts the most common class (“Finish”)
- High accuracy but **no real predictive value**

---

### **Model 2 – Initial Decision Tree (Post-Race Analysis)**

Uses both pre-race and in-race data.  
Useful for **insights**, not deployment.

Key findings:

- Cars with **0 pit stops** often retire early  
- **Grid position** influences collision/retirement risk  
- **Constructor reliability** matters  
- Retirement rates fell sharply over decades due to safety improvements  

---

### **Model 3 – True Pre-Race Decision Tree (Deployment-Ready)**

Uses **only pre-race features**:

- Grid position  
- Constructor  
- Circuit  
- Driver age  
- Historical retirement rate  

**Train/Test Strategy:**

- Train → past seasons  
- Test → most recent season  
- Simulates real deployment scenario  

**Performance:**

- Accuracy: ~0.87  
- Recall for DNFs: low (DNFs are rare → class imbalance)  

Shows the challenges of predicting **rare but important events**.

---

## 📂 Repository Structure

```
f1_retirement_prediction.ipynb
README.md
```


- Notebook includes data wrangling, feature engineering, model building and evaluation.  
- Raw datasets are not included to keep the repository lightweight.

---

## 🛠️ Tech Stack

- Python  
- Pandas, NumPy  
- Scikit-learn  
- Matplotlib, Seaborn  
- Decision Trees  
- Feature Engineering on Relational Data  

---

## 📌 Key Learnings

- How to merge **multiple relational tables** using composite keys  
- Pre-race vs post-race model design and leakage prevention  
- Handling **class imbalance** in real-world prediction  
- Interpreting model importance for race engineering insights  

---

## 🚀 Future Improvements

- Apply **SMOTE**, undersampling or class weights  
- Try ensembles: **Random Forest, XGBoost, Gradient Boosting**  
- Add **weather**, driver form, constructor reliability history  
- Evaluate **precision/recall** specifically for DNFs  

---

## 👤 Author

**Cheong Wei En**  
Data Science Student @ Ngee Ann Polytechnic  
LinkedIn: https://www.linkedin.com/in/cheong-wei-en-222911303  
