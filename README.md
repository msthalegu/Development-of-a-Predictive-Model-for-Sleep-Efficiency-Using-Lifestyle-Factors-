# Development of a Predictive Model for Sleep Efficiency Using Lifestyle Factors  

## Authors 
- **Alejandra Sierra Guerra** - [LinkedIn](https://www.linkedin.com/in/alejandra-sierra-guerra-profile/)  
- **Ali Afkhami** - [LinkedIn](http://www.linkedin.com/in/ali-afkhami)  
- **Daniela Mañozca Cruz** - [LinkedIn](https://www.linkedin.com/in/danielamanozcacruz)  
- **Evan Losier** - [LinkedIn](https://www.linkedin.com/in/evan-losier/?originalSubdomain=ca)
- **Ruby Nouri Kermani** - [LinkedIn](https://www.linkedin.com/in/parnian-nouri-kermani-532b86198)  

# MOTIVATION
## Context
Sleep is a fundamental biological need for humans, as highlighted in Maslow’s hierarchy of needs. However, sleep alone is not sufficient; it must be efficient. Sleep efficiency refers to the proportion of time spent actually sleeping while in bed. Understanding sleep efficiency is critical because poor sleep quality can negatively impact individuals across multiple dimensions, including cognitive, emotional, and physical health. For example:

- Cognitive decline: Poor sleep efficiency has been linked to neuronal cell loss and impaired brain health (Wang & Aton, 2022).
Mental health: Inefficient sleep is associated with symptoms of depression (Pan et al., 2022).
- Brain health: Short sleep duration increases the risk of reduced cognitive function and brain health (Fjell et al., 2023).
Gut health: Sleep quality also affects the gut microbiota, which plays a role in overall health (Deng et al., 2024).
These issues not only affect an individual’s body, but also their social and professional lives. Therefore, understanding the factors that influence sleep efficiency is essential for improving overall well-being.

## Problem
The primary problem this project aims to address is identifying the key factors that influence sleep efficiency and understanding how these factors interact to affect sleep quality. We will investigate which factors provided in the dataset are most significant for predicting sleep efficiency and will visualize the construction of the model along the way.

## Challenges
  This problem is challenging because everyone’s sleep schedule and habits are different, so we might encounter barriers when trying to create a model that accurately predicts sleep efficiency for everyone. For example, none of us have backgrounds in sleep or health, so we had to build our understanding of the various predictors and how they might relate to sleep efficiency.

# OBJECTIVES
## Overview
By identifying the factors that influence sleep efficiency, we can provide evidence-based recommendations to help individuals improve their sleep quality and, consequently, their overall quality of life.

## Goals & Research Questions
- Analyze how specific factors (e.g., bedtime, wake-up time, sleep duration, REM sleep, deep sleep, light sleep, awakenings, caffeine/alcohol consumption, smoking status, and exercise frequency) influence sleep efficiency.
- Provide actionable recommendations for improving sleep quality based on the findings.


# METHODOLOGY  

## Data 
The dataset was obtained from Kaggle which is free to use for project purposes. The dataset contains various factors affecting the sleep efficiency listed in different columns. See Table 1 for a sample of the dataset.

![image](https://github.com/user-attachments/assets/8e863699-71fa-41d1-87fe-b67e8618a32d)

- Age: The participant’s age. Sleep habits and quality might change as a person gets older.
- Gender: A person’s gender. We will investigate if different genders have different patterns in sleep efficiency.
- Bedtime: The time at which a person goes to bed. It is a key part of the body’s natural circadian rhythm.
- Wake-up time: The time a person wakes up. This can disrupt sleep cycles if it is inconsistent or too early.
- Sleep duration: The amount of time spent sleeping. Both insufficient and excessive sleep can harm sleep quality.
- REM sleep: The percentage of total sleep that is REM sleep. It is crucial for cognitive restoration and emotional regulation.
- Deep sleep: The percentage of total sleep that is deep sleep. This phase is essential for physical recovery and immune function.
- Light sleep: The percentage of total sleep that is light sleep. While less restorative, light sleep still plays a role in transitioning between sleep stages.
- Awakenings: The number of times a participant awoke during the night. Frequent awakenings during the night can fragment the sleep stages.
- Caffeine consumption: Amount of caffeine consumed (mg) 24-hour before bedtime. Caffeine could keep someone awake longer than necessary and disrupt their circadian rhythm.
- Alcohol consumption: Amount of alcohol consumed (oz) in the 24-hour before bedtime. Alcohol could keep someone awake longer than necessary and disrupt their circadian rhythm.
- Smoking status: Whether the participant smokes or not. Nicotine is a stimulant that can interfere with falling asleep and staying asleep.
- Exercise frequency: The number of times a participant exercises in a week. Regular physical activity has been shown to reduce stress and improve sleep quality.
- Sleep Efficiency: This will be the response variable, is quantitative, and as stated in the project proposal is measured in percentage. Given there are no values collected as 0 or 100, and the values close to 100 represent less than 3% of the records within the dataset , we see it is viable to try to model the sleep efficiency in this project.

## Approach 
We used R to investigate various assumptions for the multilinear regression model and found the best additive, interaction, and higher order model to better predict the target variable.

## Workflow
- Step 1. Data Cleaning and Data Transformation: First, all columns were checked for missing values and they were replaced by zero to avoid all the errors related to null values present in the dataset. Afterwards, the “Bedtime” and ”Wakeup time” columns were converted to datetime format and shifted to a linear scale of hours past earliest bedtime/wake-up time to be better suited as inputs for the model.
- Step 2. Initial models were used to verify assumptions such as linearity and multicollinearity. The Variance Inflation Factor (VIF) test was applied to identify multicollinearity. If more than two variables exhibited high VIF values, alternative models were constructed to retain the best most appropriate predictors.
- Step 3. The best additive model  was created following the Subset procedure, it was possible given the dataset only had 452 records and there were no computer performance issues.
- Step 4. A two-way interaction model was constructed using a stepwise selection procedure to evaluate interaction effects between variables.
- Step 5. The potential of a higher order model was evaluated through the inspection of a pairs plot and residual plots.
- Step 6. Based on the previous assessments, a higher order model was constructed to capture more complex relationships.
- Step 7. Model assumptions were evaluated : Linearity was assessed via a residuals plot. Independence of errors, was determined to not fully apply in this context given the data is not time series. Equal variance (Homoscedasticity) was assessed through the Breusch Pagan (BP) test. Normality of residuals was evaluated through the Shapiro-Wilk test and Q-Q plots. Finally, outliers were investigated using a residual vs leverage plot.

The process is illustrated in the following schema, which is mainly divided between Non Iterative and Iterative components. Blue sections represent one-time steps, while orange sections represent tasks or steps that were repeated multiple times to optimize the model performance for the dataset analysed in this project.

![image](https://github.com/user-attachments/assets/a625f9a1-2d32-4e74-bfcf-82b6307e833d)

The test or techniques applied during this project are presented in the following summary table 2:
![image](https://github.com/user-attachments/assets/54fa3a39-0742-4104-9aef-3c8a272af5b7)
![image](https://github.com/user-attachments/assets/c2824f19-f2f3-4b28-bb68-506a563bf87a)

All the tests and different statistical techniques applied were run at a significance level of 0.05.

# Results
Overall, our results indicate that we were able to create a multiple linear regression model to predict sleep efficiency with a variety of significant predictors from the dataset. First, when investigating the multicollinearity assumption, we discovered that our predictors included a set of three variables that had multicollinearity with each other and had to exclude the least significant of the three from our initial additive model. When assessing the linearity of the initial additive model, we discovered that interaction and higher-order terms were required (fig.2). 

![image](https://github.com/user-attachments/assets/04750f78-498e-4dfd-83bf-26db26cf2283)

In our initial additive model we noted that of the seven selected predictors, deep sleep percentage was most significant with a p-value less than 2^10-16  and exercise frequency was least significant with a p-value of 0.02267. To obtain an interaction model that would improve our linearity and adjusted R2 values, we used a stepwise procedure to include significant interaction terms. We discovered that smoking status, age, and awakenings all interact with deep sleep percentage, while awakenings also interact with REM sleep percentage. These interaction effects only slightly improved the linearity of the model (fig. 3), suggesting that the model requires higher-order terms to meet the assumption.

![image](https://github.com/user-attachments/assets/a1e2ffc1-b75f-41a4-accb-aca27ab614ab)

We tested a variety of higher-order models that included higher-order terms for deep sleep percentage, awakenings, and age. The linearity assumption for our model was improved in all cases where we added higher-order predictors, the results of one of which can be found in the (fig. 4). 

![image](https://github.com/user-attachments/assets/68541f12-89d6-42c5-a9d0-bc1ae40c6772)


The process of removing a predictor to avoid multicollinearity and creating a higher-order model to improve linearity was an expected part of reaching our final model. With a baseline set of higher-order models established, we proceeded with investigating the other assumptions. While investigating outliers, we found that although no points had a large Cook’s distance, the leverage of some points in what ended up being our final selected model (fig. 5) were more pronounced than the leverage for any points in our other investigated models (fig. 6). 

![image](https://github.com/user-attachments/assets/657ff406-d170-4320-aa36-aa9528627b9b)

![image](https://github.com/user-attachments/assets/9efcfff1-b93d-4fb4-bc20-66af9ac516f7)



This result was slightly surprising, but could likely be explained by the presence of higher-order terms with larger exponents, which could exponentially inflate the leverage of predicted points having large values for those specific higher-order terms. For the independence assumption, we know that since each row in the data is associated with a unique test subject and are not related to each other in a time-series, we can safely assume that the measurements are independent. If we suspected the measurements might not be independent, we could plot error terms in the order in which they occurred in the dataset and try to observe any pattern in the plot. 

![image](https://github.com/user-attachments/assets/9ad9d0c4-7613-472c-9a7f-e64961d9161d)


The equal variance assumption was investigated using residual plots (fig. 7) and scale-location plots (fig. 8), accompanied by Breusch-Pagan tests to determine if the models had homoscedasticity or heteroscedasticity. The null hypothesis of the Breush-Pagan test is that the model has homoscedasticity (which is what we desire for the model) and the alternate hypothesis is that the model has heteroscedasticity (undesired). 
One of our unused models had a p-value of 0.03796, meaning we rejected the null hypothesis and concluded the model had heteroscedasticity. However, the model we ultimately selected as our final model had a p-value of 0.2247, meaning we fail to reject the null hypothesis and conclude the model has homoscedasticity. Finally, when investigating the normality assumption, we discovered that despite our other assumptions being met and the model not having any clear outliers, the residuals were not normally distributed. 

![image](https://github.com/user-attachments/assets/4bbd6af3-d0fb-44b7-9758-0ea021629d99)

Our Q-Q-plot (fig. 9) had a distinct bow shape and only followed the ideal diagonal line with the middle few results, suggesting that the error terms were not normally distributed. We confirmed this with a Shapiro-Wilk normality test which returned a p-value of 2.285^10-5, meaning we reject the null hypothesis that the residuals are normally distributed, and accept the alternate hypothesis that the residuals are not normally distributed. Although we were not able to verify all the assumptions for our selected model, we were able to solve the problems that arose with all the assumptions except for normality. Our best model that had all significant predictors, a relatively high adjusted R-squared value, and met the most assumptions can be written as:






































