# Salifort-Motors_retention
Google Advanced Data Analytics Capstone: Analyzing customer retention at Salifort Motors.

## Overview 
This project aims to help the HR department at Salifort Motors improve employee retention by predicting which employees are likely to leave the company. The HR team has     collected data from employees, and the objective is to analyze this data to identify key factors contributing to employee turnover.

By building a predictive model, this project aims to provide data-driven insights to the HR department, enabling them to take proactive measures to improve employee satisfaction and reduce attrition. The goal is to develop a model that accurately predicts the likelihood of an employee leaving, helping the company retain valuable talent and reduce the costs associated with recruitment and onboarding.

## Business Understanding 
 Employee retention is a critical challenge for Salifort Motors. The company has been experiencing higher-than-expected turnover, which leads to increased hiring and training costs.  One significant concern is the company's average monthly working hours. While the standard 40-hour workweek typically corresponds to 166.66 hours per month, Salifort Motors has an average of 201 monthly hours. This increase in working hours could lead to employee burnout, dissatisfaction, and ultimately, higher turnover rates.

Employees who work extended hours without sufficient breaks or work-life balance are more likely to experience stress, fatigue, and disengagement, which can contribute to them leaving the company.

## Data Understanding

*   Variable______________________________Description
*   satisfaction_level_____________________Employee-reported job satisfaction level [0–1]
*   last_evaluation_______________________Score of employee's last performance review [0–1]
*   number_project_______________________Number of projects employee contributes to
*   average_monthly_hours________________Average number of hours employee worked per month
*   time_spend_company__________________How long the employee has been with the company (years)
*   Work_accident_________________________Whether or not the employee experienced an accident while at work
*   left____________________________________Whether or not the employee left the company
*   promotion_last_5years_________________Whether or not the employee was promoted in the last 5 years
*   Department____________________________The employee's department
*   salary_________________________________The employee's salary (U.S. dollars)

We will analyze how different variables behave in relation to the "left" variable, which indicates whether an employee left the company. However, there are certain limitations in the data:
* Unclear Split on Departure Reason: We do not know whether employees left voluntarily or were let go by the company. This lack of clarity is important, as it may affect the average_monthly_hours and other variables. For instance, an employee who learns they will be let off at the end of the month might reduce their working hours or drop off projects, which could impact the analysis.
* Lack of Job Role Data: We do not have information about the employee’s job role, which could be valuable in analyzing whether employees in lower or higher positions are more likely to leave the company. We hypothesize that the promotion_last_5years variable might provide some insight into this.

<img src="https://github.com/user-attachments/assets/e73272f6-24be-47cb-8aa4-ef7f482bd5a5" width="300" height="200">
<img src="https://github.com/user-attachments/assets/8ed455ca-1344-4db0-9979-b9eddd168faa" width="300 " height="200">

Based on our analysis, we identified three distinct groups of employees who left the company:

*Underutilized Employees:* These employees worked fewer hours, contributed to fewer projects, received lower evaluation scores, and reported moderate satisfaction levels. Their departure may stem from feeling undervalued or underutilized within the company.

*Overworked Employees:* This group worked 240 to 310 hours per month (44% to 85% more than the typical workload), contributed to numerous projects, and had good performance evaluations. Despite their positive evaluations, these employees reported the lowest satisfaction levels, suggesting that overwork and potential burnout could have played significant roles in their decision to leave.

*High-Performing Employees:* This group worked 215-280 hours per month, received high performance evaluations, and reported high satisfaction levels. However, further investigation shows that these employees were likely to leave after 5-6 years with the company, potentially due to the lack of career progression or the influence of promotions within the last five years.

## Modeling and Evaluation
Since the variable we want to predict (whether an employee leaves the company) is categorical, we  build a Logistic Regression model and Tree-based Machine Learning models. We implement both solutions and compare the results

| Model                | Precision | Recall  | F1      | Accuracy | AUC    |
|----------------------|-----------|---------|---------|----------|--------|
| Logistic             | 0.500     | 0.098   | 0.164   | 0.830    | 0.539  |
| Decision Tree Test   | 0.793     | 0.876   | 0.832   | 0.941    | 0.915  |
| Random Forest1 Test  | 0.878     | 0.880   | 0.879   | 0.960    | 0.928  |


| Model          | True Positive | True Negative | False Positive | False Negative |
|----------------|---------------|---------------|----------------|----------------|
| Logistic       | 49            | 2381          | 49             | 449            |
| Decision Tree  | 436           | 2386          | 114            | 62             |
| Random Forest  | 438           | 2439          | 61             | 60             |

*   The logistic regression model demonstrated the lowest performance across all evaluation metrics, primarily predicting true negatives.
*   Among the two tree-based models:
*    The random forest model outperformed the decision tree model in most metrics, with only a slight difference of 0.01 in recall.
*    The random forest model also exhibited the best predictive accuracy for true positives, true negatives, and false negatives.
*    The random forest model slightly underperformed compared to the logistic regression model in accurately predicting employees who did not leave (false positives).
*    Given the company's goal of predicting employee attrition, the random forest model's slightly lower accuracy in predicting false positives is acceptable.
  
**The random forest model's superior performance in other metrics, particularly its ability to identify true positives (employees who are likely to leave), makes it the most suitable choice for this application.**

##Conclusion, Recommendations, Next Steps
The machine learning models and feature importances derived from the random forest model suggest that employee departures are strongly linked to workload, particularly excessive working hours and a high number of projects. To mitigate these factors and improve employee retention, we recommend the following actions:

*  Set a maximum limit on the number of concurrent projects assigned to each employee to prevent overload and potential burnout.
*  Accelerate the promotion process by reducing the time to promotion (e.g., to 4 years) and increasing the number of employees eligible for advancement.
*  Implement measures to recognize and reward employees who consistently work longer hours, such as financial incentives, additional time off, or other forms of recognition. Alternatively, consider setting a maximum limit on monthly working hours (e.g., 200 hours) to prevent overwork.
*  If implementing rewards or maximum hour limits is not feasible, ensure that potential employees are fully informed about the company's work culture during the hiring process. This will allow candidates to make informed decisions about their suitability for the role and the company's expectations.
*  Re-evaluate the performance evaluation process to ensure fairness and consistency. The current system seems to favor employees working over 200 hours per month, which may create feelings of inequity among those working standard hours.
*  Removing hours and projects from burnout employees could shift the workload to employees with fewer hours and projects, who may feel underappreciated and undervalued. It's important to balance the workload to avoid creating new dissatisfaction or burnout in other employees.
