# Divvy Bikeshare Analysis

**Data Source:**
This dataset contains information on Divvy Bikes, a bikeshare program that provides residents and visitors of Chicago with a convenient way to explore the city.
https://divvybikes.com/system-data

The dataset is one CSV file containing bikeshare activities for September 2023. Columns include ride ID, bike type, start and end times, station names and IDs, location coordinates, and member type.

Questions to answer:
1. What portion of rides are member versus casual?
2. What pattern can we see in terms of the location of these rides?
3. What are popular times to ride bikes in Chicago?
4. What is the average ride time?

Tools used:
1. PostgreSQL Database
2. PowerBI

**Portionality of member versus casual riders:**

For this question, we need to understand the demographic layout and see if there are patterns to their behaviors. Let's first look at the number of these riders by their respective class.

```
SELECT member_casual
, COUNT(member_casual) as count
FROM bikeshare_records
GROUP BY member_casual;
```
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/5ae70b1e-2a81-4ed6-b430-4ed60b7046c3)

Immmediately we can tell that the majority of rides during this date are members. Casual users make a siginificant portion of rides as well. A deeper data analysis will be required to see if theres any correlation between ridership metrics and membership.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/1ad5c018-355b-41c0-b960-439080c16a60)


**Location Analysis:**

In order to view patterns in location, I uploaded the data into a esri powered map in PowerBI. I initially wanted to use a 3D map to help plot density as height but this requires a corporate license. 

![PBIDesktop_r0M3asepAt](https://github.com/jqwin/joes_data_projects/assets/138724732/3a76d07e-e766-48a9-93ed-ff0a91bd7a9a)

Each point in this map is a record of a ride during September 1st. We generally see a pattern of rides clustered in the innermost urban sections of the city like Lincoln Park and River North. We do not see any obvious migration patterns because it is likely due to the short nature of these rides. However we do see a relatively heavier density in downtown areas versus the suburbs. 

**Popular times to ride a bike:**

A good way to answer this question is to create a histogram. A histogram is not a native chart type on PowerBI but there are workarounds for creating one. The method I chose was to bin the timestamps into standard increments like hour or minute. I binned the data via the grouping feature in terms of hour by creating a separate column to transform the original timestamp. In this transformation, I removed the minutes and seconds to classify each row by hour. 

Once the data is binned, I used the bar chart template and used the column as the X and/or Y axis. For the Y axis, I made sure to use the count function which ensured the data counts by the hour grouping. The first shows one day of data(Sep 1) and the second shows monthly average of September by hour.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/a69a56ea-ccd0-44e2-9993-bdda662a3b65)

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/d7e75dd2-604a-4842-ba68-f76d7686ccd1)

For both histograms, we can see a couple of trends:
- Around 7-10am, we can begin to see rides start to climb as people start their day
- This rate gradually increases and begins to peak towards the early evening around 4pm-6pm
- Rides begin to decrease after 6pm and activity is at its lowest in the early morning
- Patterns are relatively the same but Sept 1 shows above average activity from 12pm-4pm

**Average ride time:**

To answer average ride time, we need to calculate the difference between ride end time and start time. 
```
SELECT(AVG(total_seconds)) AS avg_seconds	
FROM
	(	
	SELECT
		(EXTRACT(MINUTE FROM (ended_at - started_at)) * 60) +
		(EXTRACT(SECOND FROM (ended_at - started_at))) AS total_seconds
	FROM bikeshare_records
	)
subquery;
```
In this query, we need to normalize the time stamps in terms of seconds. So the EXTRACT function is utlized to pull the minutes and seconds which we then convert the minutes to eventually get total_seconds. The conversion is done in a nested query which we can then calculate the average in the outer query.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/340d31f5-c7ee-4976-9ed3-fcd87157ff84)

The average ride lasts approximately 798 seconds or ~13 minutes.

**Summary:**

THere are some insights that can be drawn from this dataset. I was able to identify the proportionality of membership where members make nearly 2/3rds of rides during the month of September. The data was plotted onto a map to see if there migration patterns but there are no obvious patterns besides the density of points in inner-urban areas. I also created several histograms to view the frequency of rides during the day and we can generally see a repeating and strong pattern of rides throughout the day but it peaks typically late in the afternoon to early evening. Lastly, I calculated the average ride time in September to be approximately 13 minutes.
