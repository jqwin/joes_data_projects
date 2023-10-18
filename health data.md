# Sleep Health and Lifestyle
This synthetic dataset contains sleep and cardiovascular metrics as well as lifestyle factors of close to 400 fictive persons.
Source: https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset/

Questions to answer:
1. Which factors could contribute to a sleep disorder?  
2. Does an increased physical activity level result in a better quality of sleep?
3. Does the presence of a sleep disorder affect the subjective sleep quality metric?

Initial Data Survey:

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

Based on the data above, we can see a relationship where having no sleep disorder has the best average quality of sleep at a 7.62 rating. Patients that have insomnia and sleep apnea have lower sleep ratings at 6.53 and 7.20 respectively. A patient having a sleep disorder will likely have a sleep quality that is worse than someone who doesn't have a sleep order. 

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
