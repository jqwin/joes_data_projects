# Football Pick-ems Data Analysis

**Data Source:**
This dataset is derived from the CBS sports website where a pool of players(my friends) compete weekly by choosing the NFL or College Football team that they believe will win in a matchup. CBS provides 15-30 matchups every week during the football season. 

Questions to answer:
1. What is the average of correct picks by player during the season?
2. Which teams are picked correctly and incorrectly?
3. What distinguishes players with higher success rates versus those with lower rates?

Tools used:
1. Excel
2. Google Looker

**Data Extraction and Cleanup:**
The data was extracted using a manual process of copy and paste of weekly results into a excel table. The tables were organizes into seperate NFL and CFB results. This data was melted in order to have a time series analysis. In order to get a count of correct and incorrect selections, a matrix was created. This was faciliated with VBA code to count team selections by their color(red and green) and player. The matrix was then melted down in order to have the data in a readable format for Google Looker. 

