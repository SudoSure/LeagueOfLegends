# League of Legends: What is the Best Champion?

## Introduction
### Introduction and Question Identification
What is the best champion in the game? That is every gamers' first question they start playing a game to have an easy and enjoyable time. Even experienced players' ask this same question to maximize their success in the game. The game we will be analyzing today is League of Legends, a multiplayer online battle arena video game where 2 teams of five battle it out in an all out skirmish to see who can destroy the enemy's nexus. The first one who destroys the opposing team's nexus wins. The dataset we have here has 149400 rows and the main columns we want to mainly focus on today are the champion, position, result, and kills columns. Champion: the name of character, position: the role played, result: win or lost, and kills: the amount of individual takedowns.

## Cleaning and EDA
### Data Cleaning
In the data cleaning process, I included the columns: 'gameid','datacompleteness','position','champion','result','kills','deaths','assists','doublekills','triplekills','quadrakills','pentakills', 'dpm', 'totalgold', 'total cs', 'cspm','damagetochampions'. The rest of the other columns were dropped as they were not relavent to the analysis. Then, I removed the team data as I want to focus on individual player data. I also created two separate columns called 'win' and 'lose' that interprets the result column in type bool to clearly decipher if a player lost or won a particular game. Finally, I filled in NaN values of the multikill columns with 0.0 because likely if a multikill is NaN then it was not achieved and the value would be 0.
(Show head of cleaned DF)

### Univariate Analysis
This is a distribution of the winrates of the champions. As you can see, it is somewhat normally distributed as most champions hover around the 50% range as they should. Any champion lower than a 40% winrate or higher than a 60% would definitely need tuning from the game balancing team. (Show histogram)
### Bivariate Analysis
This is a scatterplot of the average kills of a champion compared to its winrate. As you can see, there is not much correlation between the two as if we were to theoretically fit a line through the points, then the slope would be mostly flat. This champions that get more kills do not always win more. There are plenty other factors that would affect winrate like team composition, objective control, total gold earned, team synergy, etc. This also shows that you champions with a low average kill like support champions, still have an equal impact as kill- focused champions. (Show scatterplot)

### Interesting Aggregates


## Assessment of Missingness


## Hypothesis Testing
