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

**Average Correct Picks**

To understand how players fare during the season, I tallied the correct picks by each player and drilled down into CFB and NFL picks. This was a simple average that I calculated and presented as a standalone number on the dashboard. I also created a time series analysis with a running average trend line. 

Players on average correctly picked 73% of CFB matches from Week 1 to Week 18. For the NFL, the average is 53%.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/afd9e892-92bb-4e4b-888a-ffa07a8d7fe8)

Players are more likely to pick college games correctly versus NFL games. Correctly picking upsets is difficult for both levels of play.

**Most Correctly Picked and Incorrectly Picked Teams**

Similar to the average, the picks must be tallied by team and player. The count is then visually listed on the dashboard which is filterable by each player.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/3824a333-6fb8-46b8-82ba-1b8bad1f0088)

The majority of teams picked are NFL teams but this is likely due to a higher number of NFL games later in the seasons as well as less NFL teams to choose from. 

**Key Factors in Success Rate**

CBS provides percentage odds for each match and so players can make relatively informed picks. Picking the favorite is reliable but in order to separate from the average, players must take risks on picking upsets. There are more games in the first half of the seasons because of college football and it becomes more difficult to climb rankings later in the season when there is less games. Since there is not much data on teams early in the saason, its difficult to gauge which teams will be dominant or weak. In the NFL game, average correct picks are much lower then CFB. The chance of upsets for NFL games are much higher because of the relative competitve parity between teams. The recommendation for players is to choose more upsets for NFL games and to quickly determine strong and weak teams early in the season. 
