# 2026 Employment Attrition Analysis

**Prepared by:** Nwachukwu Joseph C.  
**Date:** 26 November 2026

A multi-tool data analytics project using **Microsoft Excel, SQL Server Management Studio (SSMS), Power BI, and Microsoft PowerPoint** to analyse employee attrition and identify patterns that can guide employee-retention efforts.

## Table of Contents

- [Executive Summary](#executive-summary)
- [Background and Objectives](#background-and-objectives)
- [Tools Used](#tools-used)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Data Transformation and Analysis](#data-transformation-and-analysis)
- [Key Findings](#key-findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)

## Executive Summary

Employees in the **Research and Development** department recorded the highest reported attrition rate at **56%**, compared with **39%** in Sales and **5%** in Human Resources. Departures occurred across job categories, with laboratory technicians, sales executives, and research scientists leading.

Although the overall attrition rate was **16.1%**, the report found that **127 employees who left worked overtime**, compared with **110 who did not work overtime**. Employees aged **25–34** accounted for **112 of the 237 employees who left**.

The project recommends reviewing overtime policies and expanding career-development opportunities, particularly for employees aged 25–34.

## Background and Objectives

Employee attrition remains a concern for organisations because losing experienced workers can reduce efficiency, increase recruitment costs, and affect organisational structure.

This project analyses employee attrition using Power BI. The dashboard presents information including the total number of employees (**1,470**), overall attrition rate, attrition across job roles and departments, and average income of employees who stayed and those who left.

The objective is to provide insights into who is leaving the organisation, where attrition is occurring, and factors associated with employee exits, ultimately supporting employee-retention efforts.

## Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data cleaning and transformation |
| SQL Server Management Studio (SSMS) | Data querying and analysis |
| Power BI | Data modelling, DAX measures, and dashboard development |
| Microsoft PowerPoint | Presentation of project findings |

## Dataset

**Source:** IBM HR Analytics Employee Attrition & Performance (Kaggle)  
**File:** `WA_Fn-UseC_-HR Employee-Attrition`

The dataset contains **1,470 rows and 35 columns**, covering employee information such as age, department, job role, income, overtime, satisfaction scores, years at company, and attrition status (Yes/No).

## Methodology

### 1. Data Cleaning

The following steps were carried out:

- Checked for duplicate Employee Number values and blank values.
- Removed the `Employee Count`, `Over 18`, and `Standard Hours` columns because they contained the same values across the rows.
- Decoded numeric scales for Education, Environment Satisfaction, Job Satisfaction, Relationship Satisfaction, and Job Involvement into descriptive labels using lookup tables.
- Created `Age_Group`, `Income_Band`, and `Tenure_Band` columns to group employees by age, income, and length of service.
- Created an `Attrition_Flag` column to convert attrition status into a consistent numeric value.

## Data Transformation and Analysis

### Excel

- Used `Ctrl + T` to convert the data range into an Excel table.
- Used lookup tables to translate numeric scale values into descriptive labels.

### SQL

SQL queries were used to calculate the overall attrition rate and identify job roles by average years since last promotion.

**Overall employee count and attrition rate:**

```sql
SELECT
    COUNT(*) AS Total_Employees,
    100 * SUM(CAST(Attrition_Flag AS INT)) / COUNT(*) AS Total_Attrition_Rate
FROM Attrition_Project;
```

**Top 5 job roles by average years since last promotion:**

```sql
SELECT TOP 5
    Job_Role,
    ROUND(
        AVG(CAST(Years_Since_Last_Promotion AS FLOAT)),
        2
    ) AS Average_Years_Since_Promotion
FROM Attrition_Project
GROUP BY Job_Role
ORDER BY Average_Years_Since_Promotion;
```

### Power BI

DAX measures were used to calculate key workforce metrics.

**Total Employees:**

```dax
Total Employees = COUNTROWS(Clean)
```

**Average Monthly Income:**

```dax
Average Monthly Income = AVERAGE(Clean[Monthly Income])
```

## Key Findings

### 1. Attrition by Department

The Research and Development department recorded the highest attrition rate at **56%**, with **133 employee departures**. Among these employees, 43 were females and 90 were males. Sales recorded 92 departures, while Human Resources recorded 12.

| Department | Number of Employees Who Left | Attrition Rate |
|---|---:|---:|
| Research and Development | 133 | 56% |
| Sales | 92 | 39% |
| Human Resources | 12 | 5% |

### 2. Overtime and Attrition

The report states that 410 employees worked overtime, while 1,060 did not.

| Overtime | Employees Who Stayed | Employees Who Left |
|---|---:|---:|
| No | 944 | 110 |
| Yes | 289 | 127 |

Of the employees who worked overtime, **31%** left the organisation. In comparison, **10%** of employees who did not work overtime left.

### 3. Job Satisfaction and Attrition

Employee exits occurred across all four job-satisfaction categories: low, medium, high, and very high.

- 72 employees who left had high job satisfaction.
- 66 employees who left had low job satisfaction.
- The highest attrition rate (**23%**) was among employees with low job satisfaction.
- Attrition rates for medium, high, and very high satisfaction were **17%**, **16%**, and **11%**, respectively.

### 4. Age Group and Attrition

Employees aged **25–34** recorded the highest number of departures, accounting for 112 of the 237 employees who left.

| Age Group | Number of Employees Who Left |
|---|---:|
| 25–34 | 112 |
| 35–44 | 51 |
| Under 25 | 38 |
| 45–54 | 25 |
| 55+ | 11 |

The under-25 age group had the third-highest attrition rate at **16%**, while the 55+ age group had the lowest attrition rate at **5%**.

### 5. Average Monthly Income: Employees Who Stayed vs. Left

Employees who stayed had a higher average monthly income (**6.8k**) compared with employees who left (**4.7k**). This raises questions about possible dissatisfaction with compensation among employees who left.

## Recommendations

1. **Strengthen Departmental Management:** Review management practices in departments with higher employee attrition.
2. **Review Overtime Policies:** Assess overtime expectations and their relationship with employee retention.
3. **Review Compensation Benefits:** Evaluate compensation and benefits to support employee retention.
4. **Provide Career Development Opportunities:** Expand career progression and development opportunities, particularly for employees aged 25–34.

## Limitations

The analysis was based on the available dataset. Some factors were not captured in the original data, including:

- External employment opportunities.
- Organisational culture.
- Individual circumstances.
- Employee preferences.

## Appendix

Additional dashboard visuals, SQL queries, and supporting project materials can be added to this section.
