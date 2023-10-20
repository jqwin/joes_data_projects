# Sleep Health and Lifestyle
This synthetic dataset contains sleep and cardiovascular metrics as well as lifestyle factors of close to 400 fictive persons.
Source: https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset/

Questions to answer:
1. Which factors could contribute to a sleep disorder?  
2. Does an increased physical activity level result in a better quality of sleep?
3. Does the presence of a sleep disorder affect the subjective sleep quality metric?

Tools used:
1. PostgreSQL DB
2. PowerBI


## Initial Data Survey:

To understand the landscape of the data, we need to aggregate the data by classifications and available measures. In the code below, each metric is grouped by sleep disorder.

```
SELECT 
sleep_disorder
, avg(daily_steps) AS avg_steps
, avg(quality_of_sleep) AS avg_qual_sleep
, avg(physical_activity_level) AS avg_phy_act
, avg(stress_level) AS avg_stress
, avg(sleep_duration) as avg_sleep_dur
FROM sleep_detail
GROUP by sleep_disorder
ORDER by avg_qual_sleep;
```

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/5a00b56c-e796-4649-9dc1-b01587a4df15)

Based on the data above, we can see having no sleep disorder has the best average quality of sleep at a 7.62 rating. Patients that have insomnia and sleep apnea have lower sleep ratings at 6.53 and 7.20 respectively. A patient having a sleep disorder will likely have a sleep quality that is worse than someone who doesn't have a sleep order. 

Another classification that we can group results by is BMI category.

```
SELECT 
bmi_category
, avg(daily_steps) AS avg_steps
, avg(quality_of_sleep) AS avg_qual_sleep
, avg(physical_activity_level) AS avg_phy_act
, avg(stress_level) AS avg_stress
, avg(sleep_duration) as avg_sleep_dur
, avg(heart_rate) AS avg_heart_rate
FROM sleep_detail
GROUP by bmi_category
ORDER BY avg_qual_sleep;
```

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/a271cc33-07df-43a9-bd1b-97f456a8b466)

In this query, we can see a linear relationship between BMI category and sleep quality. People who are obese and overweight will have worse sleep quality than those who are normal weight or normal. There is also a correlated relationship with average steps and heart rate. Higher heart rate averages will be higher in those that are obese. Those who are obese will have lower than average steps as well. Each of these metrics are likely related to sedentry lifestyle choices. 

Lower heart rates with respect to BMI category indicate an inverse relationship with sleep quality. Meaning that lower heart rate averages are associated with higher sleep quality. To analyze this, we must aggregate the metrics by varying heart rate ranges.

```
SELECT 
CASE
	WHEN heart_rate BETWEEN 65 and 70 THEN '65-70'
	WHEN heart_rate BETWEEN 71 and 75 THEN '71-75'
	WHEN heart_rate BETWEEN 76 and 80 THEN '76-80'
	WHEN heart_rate BETWEEN 81 and 86 THEN '81-86'
END AS heart_range
, avg(quality_of_sleep) AS avg_qual_sleep
, avg(daily_steps) AS avg_steps
, avg(physical_activity_level) AS avg_phy_act
, avg(stress_level) AS avg_stress
, avg(sleep_duration) as avg_sleep_dur
FROM sleep_detail
GROUP by heart_range
ORDER BY heart_range;
```

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/9364c156-b077-46a7-ad11-d04782b4ef4c)

We can see several correlative relationships with average steps, average physical activity, and average stress in respect to quality of sleep and heart rate. In general this reinforces the positive nature of a physically active lifestyle. If a patient is actively walking more and doing more physical activities, these all contribute to a lower heart rate and better sleep quality.

## Visualizations:

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/08b021c4-bfdc-43b7-bd89-56cdeea318b2)

Starting from left to right and top to bottom:
- Sleep Quality Rating and Heart Rate
- Physical Activity Level and Sleep Quality Rating
- Sleep Quality Rating and Sleep Duration
- Stress Level Rating and Sleep Quality Rating

All of these graphs demonstrate varying degrees of correlation between different matrics and sleep quality. If the trendline is steep than the correlation is stronger between the metric and sleep quality. In the first graph, we can see that having a lower heart rate is associated with better sleep quality which reinforces the aggregated metrics earlier. Intuitively, we can also see that sleeping longer is also indicative of better sleep quality. In terms of physical activity level, the data points are nosier but it generally shows a positive relationship between higher activity levels and sleep quality. We can see outliers where there are high quality sleepers with low activity levels and vice versa. The last graph is also intuitive, lower stress ratings are indicative of better sleep quality.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/1786daa5-d2fd-4363-b681-798a3615d482)

Let's consider sleep quality with respect to age. In this scatterplot, we can see a positive slope with a wide dispersion of data points. Generally as you get older, the better quality of sleep you get. This could be due to people getting into retirement age and having more time to sleep because of less work. However, there is siginficant variance in the data since the data points are not closely clustered. This weakens the relationship but it doesn't discount the relationship entirely. There are likely to be stronger factors than age with regards to sleep quality.

## Summary

In our intial data survey, we are able to easily indicate that having a sleep disorder is associated with worse sleep quality than not having one. When analyzig with respect to physical acitivty, higher activity levels are positively correlated with higher sleep quality. Adjacent metrics to physical activity such as number of steps and heart rates are positively correlated with better sleep quality. It can be inferred that patients with more active lifestyles will likely have better sleep quality. This is especially true if the demographic is classified by BMI category and varying heart rate brackets. This is likely due to the stress related benefits of having exercise. Although these metrics mutually reinforcing, it is worth cautioning that the data does not account for idiosyncratic factors related to a patient's lifestyle choices nor do we know if this data is representative of a population. While the mentioned factors are strong, they are by no means completely determinant. 


