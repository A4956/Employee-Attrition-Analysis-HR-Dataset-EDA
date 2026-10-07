Employee Attrition Analysis: HR Dataset EDA

Exploratory data analysis (univariate and bivariate) of an HR dataset to understand why employees are leaving and which factors influence that decision. Built with Python (pandas, matplotlib, seaborn) in Untitled4.ipynb.

Problem Statement

A company is experiencing increasing employee attrition. The HR team wants to understand why employees are leaving and what factors influence their decision. As the Data Analyst, the task is to explore the HR dataset and provide actionable insights.

Objective

Use Exploratory Data Analysis to:

Understand employee distribution
Identify key factors affecting attrition
Discover patterns and relationships
Provide data-driven recommendations
Dataset
File: HRdataset (1).csv
Size: 311 employee records, 36 columns
Contents: demographics, department and position, manager, salary, recruitment source, performance score, engagement and satisfaction scores, absences, hire and termination dates, termination reason, employment status
Missing values: only DateofTermination (207 nulls, i.e. active employees) and ManagerID (8 nulls)
Approach
Technique	Analysis	Columns
Univariate	Overall attrition rate	EmploymentStatus
Univariate	Employee distribution across departments (bar chart)	Department
Univariate	Salary distribution (histograms)	Salary
Bivariate	Average salary by employment status	Salary x EmploymentStatus
Bivariate	Attrition rate by department (normalized crosstab)	Department x EmploymentStatus
Bivariate	Age vs. salary (scatter plot)	Age (derived from DOB) x Salary
Bivariate	Average salary by department	Department x Salary

Data preparation: inspection (head, info, describe, null counts), missing-value handling, and conversion of DOB to datetime to derive Age.

Key Findings
Question	Result
Overall attrition	33.4% have left: 28.3% voluntary, 5.1% terminated for cause. 66.6% are active.
Employee distribution	Production is the largest department (209 of 311, about 67%), followed by IT/IS (50) and Sales (31).
Salary distribution	Most employees earn low to mid-range salaries. A small number earn very high salaries.
Salary vs. attrition	Voluntary leavers have the lowest average salary (~$63.9K) vs. active employees (~$70.7K).
Department attrition	Production has the highest voluntary attrition (~36%), then Software Engineering (~27%). Sales (~10%) and IT/IS (~12%) are lowest among the larger departments.
Department pay	Production has the lowest average salary (~$60K). IT/IS (~$97K) and Software Engineering (~$95K) pay the most.
Age vs. salary	No clear relationship in the scatter plot.
Insights
Voluntary attrition is the main driver of turnover, at roughly 5x the rate of terminations for cause.
Attrition is concentrated in Production, which is both the largest and lowest-paid department. It alone accounts for 75 of the 88 voluntary exits.
Employees who leave voluntarily earn less on average than those who stay, which suggests pay may be one contributing factor. This is an association, not proof of cause.
Age does not explain pay differences, so compensation looks tied more to department and role than to seniority by age.
Recommendations
Benchmark Production pay against market rates and review compensation, since this is the department with the highest attrition and lowest average salary.
Run a targeted retention plan for Production: stay interviews, career-path clarity, and recognition programs.
Monitor Software Engineering: the headcount is small (11), but 27% voluntary attrition is high for a high-paying department, so non-pay factors are likely at play.
Investigate non-pay drivers (manager, engagement, satisfaction, recruitment source, termination reason) before committing to pay increases alone.
Track attrition monthly by department so HR can spot problems early.
Known Limitations
Date bug in Age: two-digit birth years were parsed into the wrong century (e.g. 2075 instead of 1975), producing negative ages. Fix by correcting the century when parsing DOB, or by specifying an explicit date format.
Missing-value handling: fillna("0") turns the date column DateofTermination and numeric ManagerID into strings. Leaving them as null is cleaner.
Small groups: Executive Office has 1 employee and Terminated for Cause has 16, so averages for these groups are unreliable.
Scope: the "why" is only partly answered so far. Factors such as TermReason, EngagementSurvey, EmpSatisfaction, ManagerName, RecruitmentSource, PerformanceScore, and Absences are in the data but not yet analyzed.
Next Steps
Fix the DOB century issue and recompute Age, adding a correlation coefficient for age vs. salary
Analyze attrition by manager, recruitment source, performance score, engagement, and satisfaction
Break down TermReason to see the stated reasons for leaving
Analyze tenure using DateofHire and DateofTermination
Build a dashboard from the cleaned data