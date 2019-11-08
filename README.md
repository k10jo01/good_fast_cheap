---

# Predicting Wage Level from US Census Data Using Random Forest Machine Learning Model

This repository is for a group project I worked on as a Data Science Immersive student at General Assembly. I worked together with my classmates Eddie Reed and Alaa Senjab.

---

## Executive Summary

- [Problem Statement](Problem_Statement)
- [Description of Data](Description_of_Data)
- [EDA](EDA)
- [Feature Engineering](Feature_Engineering)
- [Modeling](Modeling)
- [Conclusions & Recommendations](Conclusions_&_Recommendations)
- [Next Steps](Next_Steps)
- [Sources](Sources)

---

## Problem Statement

Bank of America’s marketing department wants to target potential customers who earn over $50,000 annually with specific loan products. The department will identify those targets using U.S Census data and build a predictive model using the Random Forest algorithm.

---

## Description of Data

The data included in the model is based on information extracted from the 1994 census database. The specific datapoint identified as being valuable to determine an individual's income are included in the data dictionary below. 

|**Name**|**Type**|**Description**|**Key**|
|---|---|---|---|
|wage|binary|wage is greater than $50K or less than or equal to $50K|>50K, <=50K|
|age|continuous|age of individual in years||
|workclass|categorical|employment status|Private, Self-emp-not-inc, Self-emp-inc, Federal-gov, Local-gov, State-gov, Without-pay, Never-worked|
|fnlwgt|continuous|the number of people the census believes an entry represents||
|education|categorical|highest level of education achieved by an individual|Bachelors, Some-college, 11th, HS-grad, Prof-school, Assoc-acdm, Assoc-voc, 9th, 7th-8th, 12th, Masters, 1st-4th, 10th, Doctorate, 5th-6th, Preschool|
|education-num|continuous|highest level of education achieved in numerical form||
|marital-status|categorical|marital status of an individual|Married-civ-spouse, Divorced, Never-married, Separated, Widowed, Married-spouse-absent, Married-AF-spouse|
|occupation|categorical|general type of occupation|Tech-support, Craft-repair, Other-service, Sales, Exec-managerial, Prof-specialty, Handlers-cleaners, Machine-op-inspct, Adm-clerical, Farming-fishing, Transport-moving, Priv-house-serv, Protective-serv, Armed-Forces|
|relationship|categorical|what this individual is relative to others|Wife, Own-child, Husband, Not-in-family, Other-relative, Unmarried|
|sex|binary|biological sex of individual|Female, Male|
|capital-gain|continuous|capital gains for an individual||
|capital-loss|continuous|capital loss for an individual||
|hours-per-week|continuous|hours an individual has reported to work per week||
|native-country|categorical|country of origin for an individual|United-States, Cambodia, England, Puerto-Rico, Canada, Germany, Outlying-US(Guam-USVI-etc), India, Japan, Greece, South, China, Cuba, Iran, Honduras, Philippines, Italy, Poland, Jamaica, Vietnam, Mexico, Portugal, Ireland, France, Dominican-Republic, Laos, Ecuador, Taiwan, Haiti, Columbia, Hungary, Guatemala, Nicaragua, Scotland, Thailand, Yugoslavia, El-Salvador, Trinadad&Tobago, Peru, Hong, Holand-Netherlands|

Descriptions of the data can be found [here](https://archive.ics.uci.edu/ml/datasets/adult). 

 ---

## EDA

We completed four main tasks during our exploratory data analysis:

- Imported U.S. Census data
- Checked for missing values (none were found)
- Imputed missing categories as "Other"
- Stripped blank spaces in data

---

## Feature Engineering

In the marketing department, we were not limited in feature engineering, so we modified and created as many new features as possible while maintaining our bias variance tradeoff. All of the preset features were either continuous, categorical, or binary. We started out by changing the y variable (income > or <= $50K) to binary. 

For the categorical features, such as marital status, workclass, education, and occupation, we created dummies so that these could become binary variables. 

Utilizing the feature importances chart for random forest, we were able to determine the features with the strongest relationships with the y variable. Polynomial features were generated using the features with the greatest importance, including Age, Final Weight, Marital status of "married-civ-spouse", Capital Gain, and Education Numerical. These polynomial features had a strong impact on the accuracy score of our model.

Overall, we were able to create 119 total features through our feature engineering process. The 5 features with the most importance after all of our feature engineering were:
- Married to a civilian spouse * education numerical value (account for 25% of model)
- Married to a civilian spouse * hours worked per week 
- Capital Gain
- Age * Marital status of married to a civilian spouse
- Age * Education numerical value

---

## Modeling

Since our modeling was limited to Random Forest, we focused more on tuning the hyperparameters of the model using GridSearch. The parameters for max features, number of estimators, min samples leaf, and max depth, were all tuned for creating the model. 

The final model we used included the following hyperparameters:
- Maximum features: 60
- Number of estimators: 30
- Minimum samples leaf: 4
- Max depth: 11


new messages
train: 0.8851707540683016
test: 0.8635771449841801
best_score: 0.8585835434334174


This model was able to achieve the following accuracy scores on our training data:
- Baseline: 0.75
- Train: 0.885
- Test: 0.863
- Best_score: 0.858
- Specificity: 0.946

With this model, we included most of the original features provided to us as well as the engineered fetures, but allowed the model to specify the 60 most important ones to include. 

---

## Conclusions & Recommendations

Random forest is a reliable and fast model that performed well in predicting an individual's wages, however it did limit us to not have the option to compare this to the performance of any other model. 

Our accuracy score was relatively high performing at 86%, which was an 11% improvement on the baseling of 85%.

We optimized for specificity with a score of 94%, which minimized the amount of individuals that would not have been good loan candidates that were included in our advertising. 

The factors that are most important in predicting one's income are somewhat intuitive - as someone gets older, they have more earning power. As someone's education level increases, their wages increase. When someone is married to a civilian, it's possible they have a more stable family life, but also in our train sample, nearly half of the individuals were married with a civilian spouse.

An important factor to consider is the demographic information included in this model that could introduce unnecessary bias into the model. Including factors such as sex and native country can introduce biases or prejudices in building and predicting this model. 

In summary, we were able to identify qualified candidates for the loan program with 86% accuracy. 

---

## Next Steps

If we were to have more time to work on this in the future, we would:
- Try other models to see if something is more suited for this 
- Try logistic regression and scaling to look at the coefficients
- Get more information from the census data
- More feature engineering
- Map the categorical features to numericals

---

## Sources

- Data: https://archive.ics.uci.edu/ml/datasets/adult
- Additional info on data: http://cseweb.ucsd.edu/classes/sp15/cse190-c/reports/sp15/048.pdf

---