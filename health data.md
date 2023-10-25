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

To understand the data landscape, we need to aggregate the data by classifications and available measures. Below, each metric is grouped by sleep disorder:

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

From the data above, we observe that individuals without a sleep disorder have the highest average sleep quality, with a rating of 7.62. In contrast, those with insomnia and sleep apnea have lower sleep quality ratings, at 6.53 and 7.20 respectively. Thus, having a sleep disorder is likely associated with poorer sleep quality.

Next, we group the results by BMI category:

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

This query reveals a linear relationship between BMI category and sleep quality. Individuals who are obese or overweight tend to have poorer sleep quality than those of normal weight. There is also a correlated relationship with average daily steps and heart rate: higher heart rates are associated with obesity, while lower daily step counts are also observed in this group. These metrics suggest a connection to sedentary lifestyle choices.

Lower heart rates in different BMI categories are inversely related to sleep quality; that is, lower average heart rates are associated with better sleep quality. To analyze this, we must aggregate the metrics across various heart rate ranges:

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

This data supports the positive impact of a physically active lifestyle on heart rate and sleep quality. Higher levels of physical activity and daily steps contribute to lower heart rates and better sleep quality.

## Visualizations:

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/08b021c4-bfdc-43b7-bd89-56cdeea318b2)

Starting from left to right and top to bottom:
- Sleep Quality Rating and Heart Rate
- Physical Activity Level and Sleep Quality Rating
- Sleep Quality Rating and Sleep Duration
- Stress Level Rating and Sleep Quality Rating

All of these graphs demonstrate varying degrees of correlation between different matrics and sleep quality. If the trendline is steep than the correlation is stronger between the metric and sleep quality. In the first graph, we can see that having a lower heart rate is associated with better sleep quality which reinforces the aggregated metrics earlier. Intuitively, we can also see that sleeping longer is also indicative of better sleep quality. In terms of physical activity level, the data points are nosier but it generally shows a positive relationship between higher activity levels and sleep quality. We can see outliers where there are high quality sleepers with low activity levels and vice versa. The last graph is intuitive, lower stress ratings are indicative of better sleep quality.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/1786daa5-d2fd-4363-b681-798a3615d482)

Let's consider sleep quality with respect to age. In this scatterplot, we can see a positive slope with a wide dispersion of data points. Generally as you get older, the better quality of sleep you get. This could be due to people getting into retirement age and having more time to sleep because of less work. However, there is siginficant variance in the data since the data points are not closely clustered. This weakens the relationship but it doesn't discount the relationship entirely. There are likely to be stronger factors than age with regards to sleep quality.

## Summary

Our initial data survey indicates that the presence of a sleep disorder is associated with poorer sleep quality. Conversely, higher levels of physical activity correlate with better sleep quality, as do related metrics such as daily step count and heart rate. Active lifestyles are likely to result in better sleep quality, particularly for individuals classified by BMI category and heart rate brackets. These findings highlight the stress-reducing benefits of exercise. However, while these metrics are mutually reinforcing, it’s important to note that the data does not account for all individual lifestyle choices, and the representativeness of the data to a broader population is unknown. While the identified factors are significant, they are not solely determinative of sleep quality.

