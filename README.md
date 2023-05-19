# League of Legends: What is the Best Champion?

## Introduction
### Introduction and Question Identification
What is the best champion in the game? That is every gamers' first question they start playing a game to have an easy and enjoyable time. Even experienced players' ask this same question to maximize their success in the game. The game we will be analyzing today is League of Legends, a multiplayer online battle arena video game where 2 teams of five battle it out in an all out skirmish to see who can destroy the enemy's nexus. The first one who destroys the opposing team's nexus wins. The dataset we have here has 149400 rows and the main columns we want to mainly focus on today are the champion, position, result, and kills columns. Champion: the name of character, position: the role played, result: win or lost, and kills: the amount of individual takedowns.

## Cleaning and EDA
In the data cleaning process, I included the columns: 'gameid','datacompleteness','position','champion','result','kills','deaths','assists','doublekills','triplekills','quadrakills','pentakills', 'dpm', 'totalgold', 'total cs', 'cspm','damagetochampions'. The rest of the other columns were dropped as they were not relavent to the analysis. Then, I removed the team data as I want to focus on individual player data. I also created two separate columns called 'win' and 'lose' that interprets the result column in type bool to clearly decipher if a player lost or won a particular game. Finally, I filled in NaN values of the multikill columns with 0.0 because likely if a multikill is NaN then it was not achieved and the value would be 0.
(Show head of cleaned DF)


## Assessment of Missingness


## Hypothesis Testing
