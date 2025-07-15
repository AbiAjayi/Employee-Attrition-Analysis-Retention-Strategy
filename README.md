# Employee-Attrition-Analysis-Retention-Strategy
## Table of Contents
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Tools & Techniques](#tools--techniques)
- [Dataset Summary](#dataset-summary)
- [Dashboard Features](#dashboard-features)
- [Key Insights from SQL Analysis](#key-insights-from-sql-analysis)
- [Sample SQL Queries](#sample-sql-queries)
- [Business Recommendations](#business-recommendations)
- [Skills Demonstrated](#skills-demonstrated)
- [Dashboard Preview](#dashboard-preview)
## Project Overview
I completed this project in a real-world business setting as part of an initiative to analyze employee attrition and develop an employee retention strategy. Over 4 weeks, I led the data analysis and dashboard development, collaborating with HR and leadership teams to provide actionable insights.

The goal was to answer:

Why are employees leaving?

Which groups are most at risk?

What strategies can reduce attrition and improve retention?
## Objectives
- Analyze workforce data using SQL for in-depth EDA
- Identify factors driving employee attrition
- Develop a Power BI dashboard to monitor attrition trends
- Recommend data-driven retention strategies
## Tools & Techniques

| Tools                   | Purpose                                |
| ---------------------- | -------------------------------------- |
| **SQL Server (MYSQL)** | Data extraction & exploratory analysis |
| **Power BI**           | Dashboard creation & visualization     |
| **DAX**                | Custom KPIs & calculations             |
| **Excel**              | Minor data cleaning                    |

## Dataset Summary
Source: Internal HR database (anonymized for confidentiality)

Records: 5,000+ employees

Key Fields: Age, Gender, Department, Job Role, Job Level, Education, Satisfaction Scores, Monthly Income, Tenure, Attrition

## Dashboard Features
The Power BI dashboard provides:
- Key KPIs: Attrition Rate, Retention Rate, Total Employees
- Attrition Analysis by Department, Job Role, Job Level
- Demographic Insights: Age, Gender, Marital Status
- Tenure-based Attrition & Career Progression
- Engagement Metrics: Job Satisfaction, Environment Satisfaction, Manager Relationship
- Overtime & Distance Impact
- Compensation Analysis: Stock Options, Salary, Hike

## Key Insights from SQL Analysis
1.  Overall Workforce Metrics
   
- Attrition Rate: 16%

- Retention Rate: 83%

2. Department & Job Role
- Sales and HR departments have the highest attrition rates (20% and 19%).

- Sales Representatives face the highest attrition at 39%, followed by Lab Technicians (~23%).

3. Tenure
- Employees with <1 year tenure have the highest attrition rate.

- 1–5 years tenure accounts for most exits (146 employees).

4. Demographics
Age:

- 18–24 years: 39% attrition

- 25–34 years: 20%

Marital Status:

- Single employees: 25% attrition

5. Job Level & Compensation
- Job Level 1: 26% attrition (entry-level risk)

- No stock options: 24% attrition (highest)

6. Engagement & Work Conditions
- Low satisfaction correlates strongly with attrition:

  - Environment Satisfaction = 1 → 25% attrition

  - Job Satisfaction (low) → 22%

- Overtime workers have 30% attrition

- Distance 15–29 km correlates with higher attrition

## Sample SQL Queries
### Overall Attrition & Retention Rate

```sql
SELECT 
COUNT(CASE WHEN Attrition = 1 THEN 1 END)*100/ COUNT(*) AS Attrition_rate,
COUNT(CASE WHEN Attrition = 0 THEN 0 END)*100/ COUNT(*) AS Retention_rate
FROM dbo.Employee_data
```
### Attrition by Department 
```sql
SELECT Department,
COUNT(CASE WHEN Attrition=1 THEN 1 END) * 100/ COUNT(*) AS Attrition_rate,
COUNT(CASE WHEN Attrition=1 THEN 1 END) AS Resigned
FROM dbo.Employee_data
GROUP BY Department;
```
### Attrition by Tenure
```sql
WITH CTE AS (
SELECT *,
CASE
	WHEN YearsAtCompany < 1 THEN '<1'
	WHEN YearsAtCompany BETWEEN 1 AND 5 THEN '1-5'
	WHEN YearsAtCompany BETWEEN 6 AND 10 THEN '6-10'
	WHEN YearsAtCompany BETWEEN 11 AND 15 THEN '11-15'
	WHEN YearsAtCompany BETWEEN 16 AND 20 THEN '16-20'
	WHEN YearsAtCompany BETWEEN 21 AND 25 THEN '21-25'
	ELSE '>25'
	END AS Tenure
FROM dbo.Employee_data )
SELECT Tenure, 
COUNT(CASE WHEN Attrition=1 THEN 1 END) * 100/ COUNT(*) AS Attrition_rate,
COUNT(CASE WHEN Attrition=1 THEN 1 END) AS Resigned
FROM CTE 
GROUP BY Tenure;
```
### Attrition by Age
```sql
SELECT
  CASE
    WHEN Age BETWEEN 18 AND 24 THEN '18–24'
    WHEN Age BETWEEN 25 AND 34 THEN '25–34'
    WHEN Age BETWEEN 35 AND 44 THEN '35–44'
    WHEN Age BETWEEN 45 AND 54 THEN '45–54'
    ELSE '55–60'
  END AS AgeGroup,
COUNT(CASE WHEN Attrition = 1 THEN 1 END)*100/ COUNT(*) AS Attrition_rate
FROM Employee_data
GROUP BY 
CASE
    WHEN Age BETWEEN 18 AND 24 THEN '18–24'
    WHEN Age BETWEEN 25 AND 34 THEN '25–34'
    WHEN Age BETWEEN 35 AND 44 THEN '35–44'
    WHEN Age BETWEEN 45 AND 54 THEN '45–54'
    ELSE '55–60'
  END;
``` 


## Business Recommendations
- Strengthen Onboarding: Reduce early-tenure exits with structured programs
- Career Development Plans: For employees in 1–5 year range
- Engage Younger Workforce: Flexible policies, mentorship
- Improve Work-Life Balance: Reduce mandatory overtime
- Compensation Strategy: Offer stock options for retention
- Department-Specific Interventions: Focus on Sales & R&D

## Skills Demonstrated
- SQL EDA: Joins, aggregations, CASE statements, KPI calculations

- Power BI: Dashboard design, DAX for custom measures

- Data Storytelling: Translating analysis into actionable insights

- Stakeholder Collaboration: Working with HR to inform strategy

## Dashboard Preview



