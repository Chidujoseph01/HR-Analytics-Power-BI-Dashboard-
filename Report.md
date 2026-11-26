# 2026 Employment Attrition Analysis

A multi-tool data analytics project using **Microsoft Excel, SQL Server Management Studio (SSMS), Power BI, and Microsoft PowerPoint** to analyse employee attrition and identify patterns that can inform employee-retention strategies.

## Table of Contents

- [Executive Summary](#executive-summary)
- [Background and Objectives](#background-and-objectives)
- [Tools Used](#tools-used)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [SQL and DAX Examples](#sql-and-dax-examples)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

## Executive Summary

Employees in the **Research and Development** department recorded a reported attrition rate of **56%**, compared with **39%** in Sales and **5%** in Human Resources. Employees who left came from different job categories, with laboratory technicians, sales executives, and research scientists among the leading roles.

The overall attrition rate was **16.1%**. Of the employees who left, **127 worked overtime**, compared with **110 who did not work overtime**. Employees aged **25–34** accounted for **112 of the 237 departures**.

The analysis recommends reviewing overtime policies and expanding career-development opportunities, particularly for employees aged 25–34.

## Background and Objectives

Employee attrition can reduce organisational efficiency, increase recruitment costs, and affect organisational structure through the loss of experienced workers.

This project analyses employee attrition using a Power BI dashboard. The dashboard is intended to provide insights into:

- Total number of employees.
- Overall employee attrition rate.
- Attrition across departments and job roles.
- Average monthly income of employees who stayed and those who left.
- Patterns in attrition across relevant employee groups.

The overall objective is to identify who is leaving, where attrition is occurring, and factors associated with employee exits, in order to support retention efforts.

## Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data cleaning and transformation |
| SQL Server Management Studio (SSMS) | Data querying and analysis |
| Power BI | Data modelling, DAX measures, and dashboard development |
| Microsoft PowerPoint | Presentation of project findings |

## Dataset

**Source:** IBM HR Analytics Employee Attrition & Performance dataset (Kaggle).

**File:** `WA_Fn-UseC_-HR Employee-Attrition`

## Methodology

### 1. Data Cleaning

The following data-cleaning steps were carried out:

- Checked for duplicate Employee Number values and blank values.
- Removed the `Employee Count`, `Over 18`, and `Standard Hours` columns because they contained the same values across the rows.
- Decoded numeric scales for Education, Environment Satisfaction, Job Satisfaction, Relationship Satisfaction, and Job Involvement into descriptive labels using lookup tables.
- Created `Age_Group`, `Income_Band`, and `Tenure_Band` columns to group employees by age, income, and length of service.
- Created an `Attrition_Flag` column to convert attrition status into a consistent numeric value.

### 2. Data Transformation and Analysis

**Excel**
- Used `Ctrl + T` to convert the data range into an Excel table.
- Used lookup tables to translate numeric scale values into descriptive labels.

**SQL**
- Used SQL queries to calculate the overall attrition rate and analyse job roles by average years since last promotion.

**Power BI**
- Created DAX measures for employee metrics, including total employees and average monthly income.
- Developed a dashboard to present attrition patterns and workforce metrics.

## SQL and DAX Examples

### SQL: Total Employees and Overall Attrition Rate

```sql
SELECT
    COUNT(*) AS Total_Employees,
    100.0 * SUM(CAST(Attrition_Flag AS INT)) / COUNT(*) AS Total_Attrition_Rate
FROM Attrition_Project;
```

### SQL: Top 5 Job Roles by Average Years Since Last Promotion

```sql
SELECT TOP 5
    Job_Role,
    ROUND(
        AVG(CAST(Years_Since_Last_Promotion AS FLOAT)),
        2
    ) AS Average_Years_Since_Promotion
FROM Attrition_Project
GROUP BY Job_Role
ORDER BY Average_Years_Since_Promotion DESC;
```

### DAX: Total Employees

```dax
Total Employees = COUNTROWS(Clean)
```

### DAX: Average Monthly Income

```dax
Average Monthly Income = AVERAGE(Clean[Monthly Income])
```

## Key Findings

### 1. Attrition by Department

The Research and Development department recorded the highest attrition in the analysis. It had **133 employee departures**: 43 females and 90 males. Sales followed with **92 departures**, while Human Resources recorded **12 departures**.

The report gives the Research and Development attrition rate as **56%** in the Executive Summary and **58%** in the Findings section; this figure should be checked against the final dashboard before publication.

### 2. Overtime and Attrition

A total of **410 employees** worked overtime, compared with **1,060 employees** who did not.

- 127 of the 410 employees who worked overtime left (**31%**).
- 110 of the 1,060 employees who did not work overtime left (**10%**).

This indicates a higher attrition rate among employees who worked overtime.

### 3. Job Satisfaction and Attrition

Employee departures occurred across all four job-satisfaction categories: low, medium, high, and very high.

- 72 employees who left had high job satisfaction.
- 66 employees who left had low job satisfaction.
- The highest attrition rate was among employees with low job satisfaction (**23%**).
- Attrition rates for medium, high, and very high satisfaction were **17%**, **16%**, and **11%**, respectively.

### 4. Age Group and Attrition

Employees aged **25–34** accounted for about half of the employees who left the organisation.

The under-25 age group had an attrition rate of **16%**, while the 55+ age group had the lowest reported attrition rate of **5%**.

### 5. Monthly Income and Attrition

The source report states that average monthly income was **6.8k** and **4.7k** for the two employee groups, but its sentence repeats “those who left” and does not clearly identify which figure belongs to employees who stayed. Confirm the group labels against the dashboard before publishing this comparison.

## Recommendations

1. **Strengthen departmental management:** Review management practices in departments with higher employee attrition.
2. **Review overtime policies:** Assess overtime expectations and their relationship with employee retention.
3. **Review compensation benefits:** Evaluate whether compensation and benefits support employee retention.
4. **Provide career-development opportunities:** Expand career progression and development opportunities, especially for employees aged 25–34.

## Limitations

The analysis was based on the information available in the dataset. Some potentially relevant factors were not captured, including:

- External employment opportunities.
- Organisational culture.
- Individual circumstances.
- Employee preferences.

These limitations mean that the analysis identifies patterns and associations in the available data; it does not establish every cause of employee attrition.

## Appendix

Additional dashboard visuals, queries, and supporting project materials can be added to this section.
