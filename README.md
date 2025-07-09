# 🏭 Palmoria Workforce Equity Dashboard

A Power BI HR Analytics project to uncover gender-related disparities in performance, pay, and compliance at Palmoria Group, a manufacturing company based in Nigeria.

📊 **Tool**: Power BI (no Excel used)  
🧩 **Data**: Employee details + Bonus rules (merged via Power Query)

---

## 🎯 Business Background

After media backlash for gender inequality, Palmoria’s CHRO initiated an internal audit of their workforce to:
- Examine gender fairness across departments and regions
- Check salary compliance with ₦90k legal minimum
- Assess bonus allocations based on ratings

---

## 📈 Dashboard Overview

![Dashboard](./DSA%20Palmoria.PNG)

---

## 📊 Key Metrics

| Metric | Value |
|--------|-------|
| 👥 Total Employees | 874 |
| 💰 Total Salary | ₦65M |
| 🎁 Total Bonus Payout | ₦323K |
| ⚠️ % Earning Below ₦90k | 69% |

---

## 🧠 Insights

### 1. **Gender Representation**
- Males make up **49%**, females **46%**, unspecified **5%**
- Male dominance is strongest in **Kaduna** and **Lagos**
- **Equal gender spread** only in **Abuja**

### 2. **Performance Ratings**
- **Females received more positive ratings**: “Very Good”, “Good”
- **Males** were more likely rated “Average”, “Poor”, “Very Poor”
- Suggests **female performance is rated more favorably**

### 3. **Departmental Gender Spread**
- **6 departments**: Male-dominated  
- **4 departments**: Female-dominated  
- **2 departments**: Equal

### 4. **Gender Pay Gap**
- Males earn **more on average in 8 departments**
- Even when females perform well, they **earn less on average** than males
- **Slight exception**: In “Good” ratings, female average salary is slightly higher

### 5. **Salary Compliance**
- **69% of employees earn less than ₦90k**
- Non-compliance is equal by gender
- But **males dominate among compliant earners**: 51% vs 44%

### 6. **Salary Bands**
- **Males dominate** upper bands (₦100k–₦120k)
- **Females concentrated** in ₦70k–₦90k

---

## 🔧 Power BI Process

✔️ All transformations done in **Power BI (Power Query)**  
✔️ **Bonus Rules** unpivoted and merged with Employee Table  
✔️ No modeling required — merged tables were cleaned and deduplicated  
✔️ DAX measures calculated:

```dax
-- Bonus % from merged table
Bonus % = [from bonus rules]

-- Bonus Amount
Bonus Amount = 'Palmoria merge'[Salary] * 'Palmoria merge'[Bonus %]

-- Total Pay
Total Pay = 'Palmoria merge'[Salary] + 'Palmoria merge'[Bonus Amount]

-- Salary Band
Salary Band = 
SWITCH(TRUE(),
    [Salary] <= 20000, "₦10k–₦20k",
    [Salary] <= 30000, "₦20k–₦30k",
    ...
    [Salary] <= 120000, "₦110k–₦120k",
    "₦120k+"
)

-- % Below ₦90k
% Below ₦90k = 
DIVIDE(CALCULATE(COUNTROWS('Palmoria merge'), 'Palmoria merge'[Salary] < 90000), COUNTROWS('Palmoria merge'))
```

## ✅ Recommendations
📌 Review salary structures to ensure equity across gender and performance

📌 Promote females in underrepresented, higher-paying departments

📌 Investigate rating systems for potential unconscious bias

📌 Raise sub-₦90k salaries to meet legal compliance (69% currently underpaid)

📌 Track performance and pay equity continuously across gender and region

🙋‍♀️ Author
Assumpta-Mary Chidimma Chianakwana
📊 Data Analyst | Power BI | HR Insights
📫 chianakwanachidimma@gmail.com
