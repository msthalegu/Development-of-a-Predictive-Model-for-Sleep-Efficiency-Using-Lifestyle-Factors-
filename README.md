# Development of a Predictive Model for Sleep Efficiency Using Lifestyle Factors  

## Authors 
- **Alejandra Sierra Guerra** - [LinkedIn](https://www.linkedin.com/in/alejandra-sierra-guerra-profile/)  
- **Ali Afkhami** - [LinkedIn](http://www.linkedin.com/in/ali-afkhami)  
- **Daniela Mañozca Cruz** - [LinkedIn](https://www.linkedin.com/in/danielamanozcacruz)  
- **Evan Losier** - [LinkedIn](https://www.linkedin.com/in/evan-losier/?originalSubdomain=ca)
- **Ruby Nouri Kermani** - [LinkedIn](https://www.linkedin.com/in/parnian-nouri-kermani-532b86198)  

## MOTIVATION
### Context
Sleep is a fundamental biological need for humans, as highlighted in Maslow’s hierarchy of needs. However, sleep alone is not sufficient; it must be efficient. Sleep efficiency refers to the proportion of time spent actually sleeping while in bed. Understanding sleep efficiency is critical because poor sleep quality can negatively impact individuals across multiple dimensions, including cognitive, emotional, and physical health. For example:

- Cognitive decline: Poor sleep efficiency has been linked to neuronal cell loss and impaired brain health (Wang & Aton, 2022).
Mental health: Inefficient sleep is associated with symptoms of depression (Pan et al., 2022).
- Brain health: Short sleep duration increases the risk of reduced cognitive function and brain health (Fjell et al., 2023).
Gut health: Sleep quality also affects the gut microbiota, which plays a role in overall health (Deng et al., 2024).
These issues not only affect an individual’s body, but also their social and professional lives. Therefore, understanding the factors that influence sleep efficiency is essential for improving overall well-being.

### Problem
The primary problem this project aims to address is identifying the key factors that influence sleep efficiency and understanding how these factors interact to affect sleep quality. We will investigate which factors provided in the dataset are most significant for predicting sleep efficiency and will visualize the construction of the model along the way.

### Challenges
  This problem is challenging because everyone’s sleep schedule and habits are different, so we might encounter barriers when trying to create a model that accurately predicts sleep efficiency for everyone. For example, none of us have backgrounds in sleep or health, so we had to build our understanding of the various predictors and how they might relate to sleep efficiency.

## OBJECTIVES
### Overview
By identifying the factors that influence sleep efficiency, we can provide evidence-based recommendations to help individuals improve their sleep quality and, consequently, their overall quality of life.

### Goals & Research Questions
- Analyze how specific factors (e.g., bedtime, wake-up time, sleep duration, REM sleep, deep sleep, light sleep, awakenings, caffeine/alcohol consumption, smoking status, and exercise frequency) influence sleep efficiency.
- Provide actionable recommendations for improving sleep quality based on the findings.


## METHODOLOGY  

### Data 
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

### Approach 
We used R to investigate various assumptions for the multilinear regression model and found the best additive, interaction, and higher order model to better predict the target variable.

### Workflow
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

## Results
Overall, our results indicate that we were able to create a multiple linear regression model to predict sleep efficiency with a variety of significant predictors from the dataset. First, when investigating the multicollinearity assumption, we discovered that our predictors included a set of three variables that had multicollinearity with each other and had to exclude the least significant of the three from our initial additive model. When assessing the linearity of the initial additive model, we discovered that interaction and higher-order terms were required (fig.2). 

*Fig 2. Initial linearity of the additive model*
![image](https://github.com/user-attachments/assets/8d0fab01-c7e0-4c43-86ab-49e8963d9609)
Source: Author's own work

In our initial additive model we noted that of the seven selected predictors, deep sleep percentage was most significant with a p-value less than 2^10-16  and exercise frequency was least significant with a p-value of 0.02267. To obtain an interaction model that would improve our linearity and adjusted R2 values, we used a stepwise procedure to include significant interaction terms. We discovered that smoking status, age, and awakenings all interact with deep sleep percentage, while awakenings also interact with REM sleep percentage. These interaction effects only slightly improved the linearity of the model (fig. 3), suggesting that the model requires higher-order terms to meet the assumption.

*Fig 3. Linearity of the interaction model*
![image](https://github.com/user-attachments/assets/278df1be-4b50-4546-9504-2333aeb058b1)
Source: Author's own work

We tested a variety of higher-order models that included higher-order terms for deep sleep percentage, awakenings, and age. The linearity assumption for our model was improved in all cases where we added higher-order predictors, the results of one of which can be found in the (fig. 4). 

Fig 4. Linearity of one higher-order model
![image](https://github.com/user-attachments/assets/a081d9bb-8617-4eb7-991d-a49d8764ba3f)
Source: Author's own work


The process of removing a predictor to avoid multicollinearity and creating a higher-order model to improve linearity was an expected part of reaching our final model. With a baseline set of higher-order models established, we proceeded with investigating the other assumptions. While investigating outliers, we found that although no points had a large Cook’s distance, the leverage of some points in what ended up being our final selected model (fig. 5) were more pronounced than the leverage for any points in our other investigated models (fig. 6). 

*Fig 5. Cook’s distance/leverage of our selected higher-order model*
![image](https://github.com/user-attachments/assets/1dbf968c-359d-4d28-b4ee-691eb732ccd0)
Source: Author's own work

*Fig 6. Cook’s distance/leverage of one of our unused higher-order models*
![image](https://github.com/user-attachments/assets/584ec52e-ed4f-47ae-b508-ad2ca0f3f309)
Source: Author's own work

This result was slightly surprising, but could likely be explained by the presence of higher-order terms with larger exponents, which could exponentially inflate the leverage of predicted points having large values for those specific higher-order terms. For the independence assumption, we know that since each row in the data is associated with a unique test subject and are not related to each other in a time-series, we can safely assume that the measurements are independent. If we suspected the measurements might not be independent, we could plot error terms in the order in which they occurred in the dataset and try to observe any pattern in the plot. 

*Fig 7. Residual plot to investigate equal variance*
![image](https://github.com/user-attachments/assets/577770e3-6bd3-47e2-87f3-8d1e42f0a82d)
Source: Author's own work

*Fig 8. Scale-location plot to investigate equal variance*
![image](https://github.com/user-attachments/assets/a8958b12-cccd-4a86-ac93-e1f0065aa300)
Source: Author's own work

The equal variance assumption was investigated using residual plots (fig. 7) and scale-location plots (fig. 8), accompanied by Breusch-Pagan tests to determine if the models had homoscedasticity or heteroscedasticity. The null hypothesis of the Breush-Pagan test is that the model has homoscedasticity (which is what we desire for the model) and the alternate hypothesis is that the model has heteroscedasticity (undesired). 
One of our unused models had a p-value of 0.03796, meaning we rejected the null hypothesis and concluded the model had heteroscedasticity. However, the model we ultimately selected as our final model had a p-value of 0.2247, meaning we fail to reject the null hypothesis and conclude the model has homoscedasticity. Finally, when investigating the normality assumption, we discovered that despite our other assumptions being met and the model not having any clear outliers, the residuals were not normally distributed. 

*Fig 9. Q-Q-Plot for normality of residuals*
![image](https://github.com/user-attachments/assets/dfbd7f2b-516b-464b-adfe-82341dda361f)
Source: Author's own work

Our Q-Q-plot (fig. 9) had a distinct bow shape and only followed the ideal diagonal line with the middle few results, suggesting that the error terms were not normally distributed. We confirmed this with a Shapiro-Wilk normality test which returned a p-value of 2.285^10-5, meaning we reject the null hypothesis that the residuals are normally distributed, and accept the alternate hypothesis that the residuals are not normally distributed. Although we were not able to verify all the assumptions for our selected model, we were able to solve the problems that arose with all the assumptions except for normality. Our best model that had all significant predictors, a relatively high adjusted R-squared value, and met the most assumptions can be written as:


![image](https://github.com/user-attachments/assets/597d7322-b302-408d-8d35-5d869ce6dc88)

Since this model contains a categorical predictor of smoking status, we can more easily interpret the model by analyzing two submodels instead; one for smokers and one for non-smokers. The model for smokers can be written as:

![image](https://github.com/user-attachments/assets/0a972021-e8a6-4b88-b41a-e94ade6d36e3)

The model for non-smokers can be written as:
![image](https://github.com/user-attachments/assets/40836a20-090f-439f-8a21-70d0c062b0ce)


The interpretation of models with interaction and higher-order predictors is difficult to clearly state, but the interpretation for the additive variables of the full model is that sleep efficiency (represented as a proportion of time spent asleep while in bed between 0 and 1) will have a baseline, or intercept, of -2.308. An increase in REM sleep (as a percentage of total time spent asleep) of 1 percent will increase the proportion of sleep efficiency by 0.0058. An increase in age of 1 year will increase the proportion of sleep efficiency by 0.1067. The age variable demonstrates a complex, non-linear relationship with sleep efficiency, as evidenced by its polynomial expansion up to the 5th degree in our model. 

An increase in awakenings of 1 awakening per night will increase the proportion of sleep efficiency by 0.0779, which is counter-intuitive, but serves as a good reminder that interpreting only the additive terms does not reflect the total effect of awakenings due to the presence of interaction and higher-order terms. An increase in exercise frequency of 1 time per week will increase the proportion of sleep efficiency by 0.0071. However, this relationship is nuanced - we observed a compensatory interaction with deep sleep percentage, where smokers show a slight increase in deep sleep's positive effect on efficiency. Importantly, this mitigating effect (+0.0022 through the interaction term) remains substantially smaller than smoking's overall detrimental impact, resulting in a net negative influence on sleep efficiency. 

An increase in alcohol consumption of 1 ounce in the previous 24 hours will decrease the proportion of sleep efficiency by 0.0054. Finally, an increase in deep sleep (as a percentage of total time spent asleep) in its additive term increases sleep efficiency by +0.288. However, this variable includes a polynomial term up to the 5th degree, with two of these terms being negative, which complicates the relationship with sleep efficiency. Nevertheless, it can be observed that both too little and too much sleep can be detrimental to sleep efficiency. Overall, this model has an adjusted R2 value of 0.8544, meaning that 85.44% of the variation of the response variable can be explained by the model.

## CONCLUSION AND DISCUSSION

The analysis conducted provides promising insights into how various lifestyle and physiological factors influence sleep efficiency, even if the model is not perfectly suited for individual-level predictions. The final model explains 85.44% of the variance in sleep efficiency, highlighting key influences such as exercise, alcohol, smoking, age, awakenings, and deep sleep percentage.

Alcohol consumption and smoking both demonstrate negative effects on sleep efficiency, with smoking showing a particularly strong detrimental impact. These findings align with existing medical research about substance use and sleep quality. Interestingly, while smoking generally reduces sleep efficiency, the model suggests deep sleep may slightly mitigate this effect, possibly due to nicotine's temporary relaxing properties.

The relationship between age and sleep efficiency proves complex, following a nonlinear pattern that changes across different life stages. This likely reflects how various life circumstances and health factors influence sleep differently at various ages, rather than being solely caused by biological aging itself.

Sleep architecture plays a crucial role in sleep efficiency. REM sleep shows a clear positive association with better sleep quality, supporting its importance for cognitive restoration. Deep sleep presents a more nuanced relationship, where moderate amounts are beneficial but excessive duration may become counterproductive, indicating balance is key.

The unexpected positive association between nighttime awakenings and sleep efficiency warrants further investigation. While initially counterintuitive, this effect is likely explained by the negative offset provided by the interaction between awakenings and deep sleep percentage. Individuals who are able to achieve a large percentage of deep sleep seem to be less affected by awakenings since they can still achieve enough deep sleep. The positive interpretation of awakenings might also suggest measurement limitations in the study design.


## REFERENCES
Deng, Z., Liu, L., Liu, W., Liu, R., Ma, T., Xin, Y., Xie, Y., Zhang, Y., Zhou, Y., & Tang, Y. (2024). Alterations in the fecal microbiota of methamphetamine users with bad sleep quality during abstinence. BMC Psychiatry, 24(1), 324-12. https://doi.org/10.1186/s12888-024-05773-5

ENSIAS. (2021). Sleep Efficiency Dataset. Kaggle. Retrieved [March 11, 2025], from https://www.kaggle.com/datasets/equilibriumm/sleep-efficiency/data 

Fjell, A. M., Sørensen, Ø., Wang, Y., Amlien, I. K., Baaré, W. F. C., Bartrés-Faz, D., Boraxbekk, C., Brandmaier, A. M., Demuth, I., Drevon, C. A., Ebmeier, K. P., Ghisletta, P., Kievit, R., Kühn, S., Madsen, K. S., Nyberg, L., Solé-Padullés, C., Vidal-Piñeiro, D., Wagner, G., . . . Walhovd, K. B. (2023). Is short sleep bad for the brain? brain structure and cognitive function in short sleepers. The Journal of Neuroscience, 43(28), 5241-5250. https://doi.org/10.1523/JNEUROSCI.2330-22.2023

Maslow, A. H. (1943). A theory of human motivation. Psychological Review, 50(4), 370-396.

Pan, L., Li, L., Peng, H., Fan, L., Liao, J., Wang, M., Tan, A., & Zhang, Y. (2022). Association of depressive symptoms with marital status among the middle-aged and elderly in rural china: Serial mediating effects of sleep time, pain and life satisfaction. Journal of Affective Disorders, 303, 52-57. https://doi.org/10.1016/j.jad.2022.01.111

Wang, L., & Aton, S. J. (2022). Perspective – ultrastructural analyses reflect the effects of sleep and sleep loss on neuronal cell biology. Sleep (New York, N.Y.), 45(5), 1. https://doi.org/10.1093/sleep/zsac047



























