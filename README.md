# Fitness-data
# 📊 Exercise & Calories Burned SQL Analysis

## 🚀 Portfolio Overview
This project is part of my portfolio during my Data Analysis training with **Incubator**. It applies real-world SQL analysis to an exercise dataset, offering valuable insights into physical activity, calorie burn, and heart rate monitoring. 

The purpose of this project is to demonstrate the practical use of SQL in analyzing exercise patterns for health optimization.

> **"Without data, you're just another person with an opinion."** – W. Edwards Deming

---

## 📁 Project Title
**Exercise and Calories Burn Analysis Using SQL**

---

## 🗂 Data Source
- **Format:** CSV (.csv)
- **Access:** Open-source sample dataset

### 🔧 Tools Used
- **MySQL** – for querying and analysis
- **Power BI** – for visualization
- **Microsoft Excel** – for initial data inspection and cleaning

---

## 🧼 Data Cleaning and Preparation
1. **Loaded** CSV into MySQL
2. **Handled** missing or null values
3. **Formatted** numeric and string fields
4. **Inspected** distributions and outliers

---

## 🔍 Exploratory Data Analysis (EDA)
The data was analyzed to uncover:
- Most efficient activity
- Heart rate trends
- Calorie burn per time
- Fitness zones by age

---

## 🧠 Key SQL Analysis & Insights

### 📌 Efficiency of Exercises (Calories Burned per Minute)
```sql
SELECT type, calories/minutes AS calories_by_minutes
FROM exercise_logs
ORDER BY calories_by_minutes DESC
LIMIT 1;
```
> ✅ **Dancing** was the most efficient with **13.33 cal/min**

### 💓 Highest Average Heart Rate by Activity
```sql
SELECT type, AVG(heart_rate) AS Avg_heart_rate
FROM exercise_logs
GROUP BY type
ORDER BY Avg_heart_rate DESC;
```
> ✅ **Dancing** also had the **highest average heart rate (120 BPM)**

### 🔥 Average Calories Burned in 30 Minutes
```sql
SELECT type, AVG(calories) AS avg_calories
FROM exercise_logs
WHERE minutes = 30
GROUP BY type;
```
> ✅ On average, a person burns **80 calories in 30 minutes** of exercise

### ❤️ Moderate Heart Rate Activities (85–110 BPM)
```sql
SELECT type, AVG(heart_rate)
FROM exercise_logs
WHERE heart_rate BETWEEN 85 AND 110
GROUP BY type;
```
> ✅ Best for moderate HR: **Biking**, **Tree Climbing**, **Rowing**, **Hiking**

### 🧬 Heart Rate Zones Based on Age (29 yrs)
```sql
/* Research showed that the maximum heart rate is 220 minus your age. 
Since, my age is 29 years old. Then, my maximum heart rate is 220-29. */

SELECT COUNT(*) FROM exercise_logs WHERE heart_rate > (220-29);
-- the total number of heart_rate  greater than the normal BPM is 0
SELECT COUNT(*) FROM exercise_logs WHERE heart_rate < (220-29);
-- the total number of heart_rate  less than the normal BPM is 16

/* 50-90% of max */ 
 SELECT COUNT(*) FROM exercise_logs 
		WHERE heart_rate <= ROUND(0.90 *(220-29))
	AND 
		heart_rate >= ROUND(0.50 *(220-30));
-- Based on the AND condition, the total number of heart_rate ranging from 50 to 90% of maximum is 8        
 SELECT COUNT(*) FROM exercise_logs 
		WHERE heart_rate <= ROUND(0.90 *(220-29))
	OR
		heart_rate >= ROUND(0.50 *(220-29));      
-- Based on the OR condition, the total number of heart_rate ranging from 50 to 90% of maximum is 16
/* CASE */ 
SELECT type, heart_rate,
		CASE 
        WHEN heart_rate > 220-30 THEN "above max"
		WHEN heart_rate > ROUND(0.90 *(220-29)) THEN "above target"
        WHEN heart_rate > ROUND(0.50 *(220-29)) THEN "within target"
        ELSE "below target"
        END "hr_zone"
FROM exercise_logs;
SELECT COUNT(*),
  CASE 
    WHEN heart_rate > 191 THEN "Above Max"
    WHEN heart_rate > 171 THEN "Above Target"
    WHEN heart_rate >= 95 THEN "Within Target"
    ELSE "Below Target"
  END AS hr_zone
FROM exercise_logs
GROUP BY hr_zone;
```
> ✅ **8** within target zone, **8** below target zone

---

## 📊 Visualization





---

## 📌 Conclusion
This project illustrates how SQL can be used to gain health and fitness insights from structured data. From identifying the most effective exercises to classifying heart rate zones, this analysis has shown the power of **data-driven fitness tracking**.

---

## 📚 Key Learnings
- Writing complex SQL queries
- CASE and aggregation logic
- Applying SQL in real-world datasets
- Health analytics through data


---

**#DataAnalysis #SQL #PortfolioProject #HealthAnalytics**
