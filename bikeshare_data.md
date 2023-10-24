# Divvy Bikeshare Analysis

## Data Source:
This dataset contains information on Divvy Bikes, a bikeshare program that provides residents and visitors of Chicago with a convenient way to explore the city.

The workspace is set up with one CSV file containing bikeshare activities at the peak of the summer-July 2023. Columns include ride ID, bike type, start and end times, station names and IDs, location coordinates, and member type. Feel free to make this workspace yours by adding and removing cells, or editing any of the existing cells.

Questions to answer:
1. What portion of rides are member versus casual?
2. What patterns can we see in terms of the location of these rides?
3. What are popular times to ride bikes in Chicago?
4. What is the average ride time?

Tools used:
1. PostgreSQL Database
2. Tableau

Portionality of member versus casual riders:

For this question, we need to understand the demographic layout and see if there are patterns to their behaviors. Let's first look at the number of these riders by their respective class.

```
SELECT member_casual
, COUNT(member_casual) as count
FROM bikeshare_records
GROUP BY member_casual;
```
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/5ae70b1e-2a81-4ed6-b430-4ed60b7046c3)

Immmediately we can tell that the majority of rides during this date are members. Casaul users make a siginificant portion of rides as well. For a stakeholder, they will need to consider the behaviors and preferences of these groups.

Another answer we can answer is the average ride time during this day.
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
In this query, we need to normalize the time stamps in terms of seconds. So the EXTRACT function is utlized to pull the minutes and seconds which we then convert the minutes to get total_seconds. The conversion is done in a nested query which we can then calculate the average in the outer query.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/340d31f5-c7ee-4976-9ed3-fcd87157ff84)

The average ride lasts approximately 798 seconds or 13 minutes. 

