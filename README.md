# Project Title

Developing a More Robust NFL Strength of Schedule (SoS) Metric

## Description

In this code file, I develop an alternate approach thinking about and quantifying NFL Strength of Schedule (SoS). The metric is typically defined as the average of a team's opponents' win percentages from the prior season, and is used to measure the difficulty or ease of a team's schedule. I believe this definition and practice of SoS to be far too simple and shallow however, as it fails to capture many aspects of a team's schedule that can influence its difficulty (number of rest days in between games, distance traveled to and from games, etc...).

To combat this issue, I combine techniques of data collection from different sources, preprocessing, and transformation to make SoS a more robust measurement. Included in this file is a walkthrough of my methods, a few plots to visualize the variables in the new "Adjusted Strength of Schedule" (Adj_SoS) statistic, and an aggregated score of each NFL team's Adj_SoS for the upcoming (2024) Regular Season.

Although a relatively simple approach was taken, I do believe that there is merit for this type of analysis in today's NFL landscape filled with a plethora of statistics and quantitative measurements. Combining retrospective and prospective statistics regarding a team's opponents, and information on a team's rest days and travel miles per game (and how they compare to their opponents') can provide a far more detailed measurement of a team's SoS.

Below, we describe the *Adj_SoS* statistic in more detail...

## Adjusted_SoS

The main result from this project was each team's *Adj_SoS* metric, which quantifies a team's SoS based on the following variables. Note that *Adj_SoS* was calculated, for each team, by standardizing (z-score) each of these variables, applying a weight to them when necessary, and then taking each team's averages of these standardizations. An *Adj_SoS* below 0 corresponds to an easier schedule, and an *Adj_SoS* above 0 corresponds to a harder schedule. We see from the *Adj_SoS_plot.png* file (given below), that the Falcons, by far, have the easiest schedule next year according to *Adj_SoS*.
[Adj_SoS_plot.png].

### Variables Used to Calculate Adjusted_SoS

- **Adj_Opponent_2023_Win_Percentage**: Avg win percentage (for 2023 games) of each teams' opponents in home or away games, depending on where they are playing. Consider the example below for clarification...

    - Consider a 3-game schedule where the Eagles play the Giants at home, Cowboys away, Ravens at home. The Adj_Opponent_2023_Win_Percentage would be the average of the Giants win percentage away, Cowboys win percentage at home, and Ravens win percentage away (all in 2023).
    - This statistic aims to capture a more robust SoS measurement (while still capturing only information on a teams' opponents, like the old SoS measurement) by considering how a team's opponents did in 2023 in the types of games (home/away) they will play against a team.
    - Note that for neutral-site games (for example, the Eagles play the Packers in Week 1 in Brazil), for simplicity, the team considered as the "home team" according to the NFL was also considered as the "home team" for this step of the project (so the Packers are considered the away team here, and the Eagles are considered the home team).

- **Mean_Distance_Traveled_Per_Week** & **Median_Distance_Traveled_Per_Week** (miles): Each team's mean and median distance traveled to each game (or back home for their BYE week) during the season. Because I included both the mean and median values, both standardized variables were weighted by .5 in the final Adj_SoS calculation.

- **Net Travel Edge** (miles): Each team's travel to each game was compared to that of their opponent. For each game that a team played, the difference in the distance they traveled vs their opponent traveled to a game was calculated, with these differences being added for each team to get a **Net Travel Edge**.

- **Net Rest Edge** (days): Similar to Net Travel Edge, however this time we are comparing the days of rest since last game for a team and each of their opponents. Note that this is the only variable where a high value is beneficial to a team, so each standardized score was multiplied by -1.

- **Avg of Opponents Expected Wins**: Using the Vegas over/under wins line for each teams' opponents, paired with the odds of the over hitting, we calculate each teams' average of their opponents' expected wins for the 2024 season. Note that this prospective measurement accounts for improvements or losses that teams made or suffered since the 2023 season.
  
## Repo-Contents

*team-logos*: Directory that contains .tif files of each NFL team's logo. This is used when plotting in the .ipynb file to create the Adj_SoS_plot.png and Rest_Travel_Edges_plot.png files. 

*2024_old_SoS_rankings.csv*: SoS rankings according to the way of measuring SoS that we try to improve in this repo

*Adj_SoS_plot.png*: Plot output from .ipynb file that gives each team's Adjusted SoS metric. Note that there is jitter in this plot to avoid overlap in logos.

*NFL_SoS_code.ipynb*: Code file where the *Adj_SoS* metric is created, and the data for it is collected and preprocessed. This file gives descriptions of the methods used and why they were used.

*Rest_Travel_Edges_plot.png*: Output (from the .ipynb file) scatterplot of each team's rest edge by their travel edge. These variables, and the others that make up *Adj_SoS* are described in the above [Adjusted_SoS](adjusted_sos) section.

*locations.csv*: Information on each team's stadium location. This was used as an input in the .ipynb code file.

*requirements.txt*: Necessary libraries and their versions for running the .ipynb file/

## Installation & Usage

1.) Clone the repo

https://github.com/gabecardealership/NFL_SoS_Project.git

2.) Install dependencies

pip install requirements.txt

3.) Run the .ipynb file (See the above [Repo Contents](#repo-contents) section for more on the inputs & outputs of this Notebook File)





