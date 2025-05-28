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
The dataset was obtained from Kaggle which is free to use for project purposes. The dataset contains various factors affecting the sleep efficiency listed in different columns. See Table 1 in the Appendix for a sample of the dataset.
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
