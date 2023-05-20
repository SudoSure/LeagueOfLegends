# League of Legends: What is the Best Champion?

## Introduction
### Introduction and Question Identification
What is the best champion in the game? That is every gamers' first question they start playing a game to have an easy and enjoyable time. Even experienced players' ask this same question to maximize their success in the game. The game we will be analyzing today is League of Legends, a multiplayer online battle arena video game where 2 teams of five battle it out in an all out skirmish to see who can destroy the enemy's nexus. The first one who destroys the opposing team's nexus wins. The dataset we have here has 149400 rows and the main columns we want to mainly focus on today are the champion, position, result, and kills columns. Champion: the name of character, position: the role played, result: win or lost, and kills: the amount of individual takedowns.

## Cleaning and EDA
### Data Cleaning
In the data cleaning process, I included the columns: 'gameid', 'datacompleteness', 'position', 'champion', 'result', 'kills', 'deaths', 'assists', 'doublekills', 'triplekills', 'quadrakills', 'pentakills'. The rest of the other columns were dropped as they were not relavent to the analysis. Then, I removed the team data as I want to focus on individual player data. I also created two separate columns called 'win' and 'lose' that interprets the result column in type bool to clearly decipher if a player lost or won a particular game. Finally, I filled in NaN values of the multikill columns with 0.0 because likely if a multikill is NaN then it was not achieved and the value would be 0.
'| gameid                | datacompleteness   | position   | champion   |   result |   kills |   deaths |   assists |   doublekills |   triplekills |   quadrakills |   pentakills | win   | lose   |\n|:----------------------|:-------------------|:-----------|:-----------|---------:|--------:|---------:|----------:|--------------:|--------------:|--------------:|-------------:|:------|:-------|\n| ESPORTSTMNT01_2690210 | complete           | top        | Renekton   |        0 |       2 |        3 |         2 |             0 |             0 |             0 |            0 | False | True   |\n| ESPORTSTMNT01_2690210 | complete           | jng        | Xin Zhao   |        0 |       2 |        5 |         6 |             0 |             0 |             0 |            0 | False | True   |\n| ESPORTSTMNT01_2690210 | complete           | mid        | LeBlanc    |        0 |       2 |        2 |         3 |             0 |             0 |             0 |            0 | False | True   |\n| ESPORTSTMNT01_2690210 | complete           | bot        | Samira     |        0 |       2 |        4 |         2 |             0 |             0 |             0 |            0 | False | True   |\n| ESPORTSTMNT01_2690210 | complete           | sup        | Leona      |        0 |       1 |        5 |         6 |             0 |             0 |             0 |            0 | False | True   |'
# Removed team matchid data to focus on individual player data
# Change result to True and False
# Fill the nan values in double, triple, quadra, penta kills because a nan value in this case means that that type kill
# was not achieved in that game as they are usually rare in professional games
# Removed

### Univariate Analysis
This is a distribution of the winrates of the champions. As you can see, it is somewhat normally distributed as most champions hover around the 50% range as they should. Any champion lower than a 40% winrate or higher than a 60% would definitely need tuning from the game balancing team. (Show histogram)
### Bivariate Analysis
This is a scatterplot of the average kills of a champion compared to its winrate. As you can see, there is not much correlation between the two as if we were to theoretically fit a line through the points, then the slope would be mostly flat. This champions that get more kills do not always win more. There are plenty other factors that would affect winrate like team composition, objective control, total gold earned, team synergy, etc. This also shows that you champions with a low average kill like support champions, still have an equal impact as kill- focused champions. (Show scatterplot)

### Interesting Aggregates
This is a table showing the champions with the highest winrate. As we can see, Darius, Rell, Wukong, Twister Fate, and Taliyah are our highest winrate champions with at least a sufficient total amount of games played. Using domain knowledge, we know that Darius is often used as a counter pick to tank top laners and any weak early game champion. Teams probably only picked Darius knowing if the opposing team chose their top laner first. Darius's oppressive early game often dominates the opposing top laner, making them have significantly less impact in the game as whole. For Rell, she is a support that is often picked as a champion that provides engage power to the team. Rell's crowd control and play making potential can heavily carry games. For Wukong, he is a jungler strong skirmisher with a strong early and mid game that ensures the team enough early power to secure objectives and snowball the game. For Twisted Fate and Taliyah, they are midlaners with strong map presences as they have ultimate abilities that affect the whole map as well as strong crowd control spells that provide single target damage and control.

## Assessment of Missingness
#### NMAR Analysis
I believe that the pentakill column would be NMAR because often most players do not get pentakills every game or ever. Depending what role or what champion you play, it could be easier or much harder to obtain a pentakill in a given game.
#### Missingness Dependency
(Missingness plot and interpretation)

## Hypothesis Testing
Let's specify and generalize the question. 

Null Hypothesis (H0): The average number of kills for top laners is the same as the average number of kills for mid laners.

Alternative Hypothesis (H1): The average number of kills for top laners is different from the average number of kills for mid laners.

As we can see, there a significant difference in the average number of kills between top laners and mid laners when hypothesis testing. If we use domain knowledge, we know that often mid lane is in the middle map, which has equal access to all of the map, which provides availability to get kills to be easier than top lane which is usually isolated from the rest of the map. Top lane also often contains scaling picks like tanks, which do not get kills or impact the game until later in the game, while mid lane is often impactful early game as they must help the jungler in secure objectives as well as roam to other lanes to secure kills and towers. They are also impactful late game with strong area of effect damage and/or crowd control which tend to secure more kills.
