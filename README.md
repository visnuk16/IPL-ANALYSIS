IPL Analysis
________________________________________
Overview
This document provides a comprehensive overview of the IPL Analysis Dashboard, including the DAX functions used and the insights presented through various visualizations. This dashboard offers an interactive way to explore IPL statistics, understand team and player performances, and analyze match outcomes.
Key Features:
•	Title Winner
•	Batter Runs & Boundaries
•	Bowler Wickets, Economy, and Strike Rate
•	Team and Venue-Based Match Wins
•	Toss Decisions & Winning Percentage
•	Result Type Breakdown
________________________________________
Visual Insights
1. Title Winner & Player Achievements
•	Title Winner: Displays the latest IPL title-winning team.
•	Orange Cap (Top Run Scorer): Highlights the highest run-scorer in the tournament.
•	Purple Cap (Top Wicket-Taker): Shows the bowler with the most wickets.
These insights help quickly identify standout teams and players.
2. Batting and Bowling Statistics
•	Batting Stats:
o	Total Runs, 4’s, 6’s, and Strike Rate.
o	Select batsmen interactively to view their stats.
•	Bowling Stats:
o	Total Wickets, Economy, Average, and Bowling Strike Rate.
o	Interactive selection of bowlers to dig into their performance.
These metrics give a detailed view of player contributions.
3. Match Outcomes by Venue and Team Wins
•	Matches Win by Venue: Breakdown of wins at major stadiums, categorized by result type (Runs, Wickets, Super Over, No Results).
•	Total Wins by Team per Season: Bar chart showing the number of wins by each IPL team across seasons. This helps analyze team strengths across different grounds.
4. Toss Decisions & Result Types
•	Winning % Based on Toss Decision: Pie chart splitting wins by choosing to field or bat.
•	Matches Win by Result Type: Pie chart classifying wins by wickets, runs, super overs, or no results.
________________________________________
DAX Functions Explained
1. Title Winner
•	Title_Winner =
VAR max_date = CALCULATE(
    MAX('Calender Table'[Date]),
    ALLSELECTED(ipl_matches_2008_2022),
    VALUES(ipl_matches_2008_2022)
)
VAR Title_Winner = CALCULATE(
    SELECTEDVALUE(ipl_matches_2008_2022[winning_team]),
    'Calender Table'[Date] = max_date
)
RETURN Title_Winner
2. Batter Runs & Strike Rate
•	Batter Runs = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[batsman_run]), " RUNS ")

•	Strike Rate = (SUM(ipl_ball_by_ball_2008_2022[batsman_run]) / COUNT(ipl_ball_by_ball_2008_2022[ball_number]) * 100)
3. Bowler Wickets, Economy, Average and Bowling strike rate
•	Bowler Wickets = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery]), " Wickets ")

•	Economy = DIVIDE(
SUMX(FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type] <> "legbyes" && ipl_ball_by_ball_2008_2022[extra_type] <> "byes"), ipl_ball_by_ball_2008_2022[total_run]), (COUNT(ipl_ball_by_ball_2008_2022[overs]) / 6))

•	Average of Bowler = DIVIDE(
SUMX(FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type] <> "legbyes" && ipl_ball_by_ball_2008_2022[extra_type] <> "byes"),
ipl_ball_by_ball_2008_2022[total_run]),
SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery]))

•	Bowling SR = COUNT(ipl_ball_by_ball_2008_2022[bowler])/SUM(ipl_ball_by_ball_2008_2022[iswicket_delive])

________________________________________
Conclusion
The IPL Analysis Dashboard leverages Power BI’s interactive capabilities and powerful DAX calculations to present key IPL statistics. From individual player performances to team-level insights, this dashboard helps fans, analysts, and teams understand the game better and make data-driven decisions.

