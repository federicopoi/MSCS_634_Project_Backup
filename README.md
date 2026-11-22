# Telco Customer Churn

**Residency Day 3 · Project Deliverable 4 · Final Insights, Recommendations, and Presentation**

MSCS-634-M50 · Advanced Big Data and Data Mining

Group project · Federico Poi and Umama Azhar

## Dataset and goals

We used the [IBM Telco Customer Churn sample](https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv). It contains 7,043 customers and 21 original columns covering account details, services, charges, and whether the customer left. About 26.5% of customers churned. The dataset let us estimate monthly bills, predict churn, group customers, and look for common account patterns using the same records.

## Project steps and findings

1. **Cleaning and exploration.** We converted 11 whitespace-only cumulative totals to missing values. All 11 customers had zero tenure. We found no duplicate customer records and kept all 7,043 customers. The 342 bills flagged in the no-internet group all belonged to customers with multiple phone lines. Churn was 42.7% for month-to-month contracts, 11.3% for one-year contracts, and 2.8% for two-year contracts.
2. **Feature engineering and regression.** We compared Multiple Linear Regression and Ridge on the same five validation folds. The internet add-on count and fiber interaction made little difference. Nine original service fields did about as well as all 17 original predictors. With those nine inputs, Multiple Linear Regression had a held-out RMSE of **$1.0504** and Ridge had **$1.0506**. Both had an R² of **0.9988**.
3. **Churn classification.** We compared k-NN with 21 neighbors against a tuned Decision Tree. Five-fold grid search chose depth 7 and a minimum of 50 customers per leaf. Tuning raised the tree's mean validation F1 from 0.4987 to 0.6226. On the test set, the tree had higher churn F1 (**0.6254 vs. 0.5887**) and ROC AUC (**0.8370 vs. 0.8240**). It caught **293 vs. 219** churned customers. k-NN had higher overall accuracy (**78.28% vs. 75.09%**).
4. **Customer groups.** We used K-Means on tenure, monthly charges, contract, and internet service. We used churn to describe the groups after fitting. The short-tenure cluster had 3,006 customers, a median tenure of 11 months, and **46.9% observed churn**.
5. **Association rules.** Apriori retained 10 churn rules after filtering. The highest-lift rule paired a month-to-month contract with fiber service. The pair and churn occurred together in **16.5%** of records. Among customers with both traits, **54.6%** churned, about **2.06 times** the overall rate.

## Recommendations and limitations

Start with the nine service fields for billing estimates and recheck performance if pricing changes. For retention, test a service check-in with a randomly selected group of month-to-month fiber customers and compare their churn with customers receiving usual support. The tree detects more churn at the tested cutoff and also creates more false alarms, so the cutoff should reflect the team's outreach capacity.

We used a public sample, excluded customer IDs from the predictive inputs, and presented aggregate results. The data comes from one snapshot, and the observed patterns do not establish cause and effect. Before real-world use, check performance on newer customer data and compare missed churn and false alerts across demographic groups.

## Recorded presentation

[Watch the Telco Customer Churn presentation on SharePoint](https://cumber-my.sharepoint.com/:v:/g/personal/fpoi51581_ucumberlands_edu/IQAZH-Kj0DQtQYTSLQJAK038AZjtIpy2cPuRVYaXoKcDxs0?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=AEf2FK)
