# League of Legends: What is the Best Champion?

## Introduction
### Introduction and Question Identification
What is the best champion in the game? That is every gamers' first question they start playing a game to have an easy and enjoyable time. Even experienced players' ask this same question to maximize their success in the game. The game we will be analyzing today is League of Legends, a multiplayer online battle arena video game where 2 teams of five battle it out in an all out skirmish to see who can destroy the enemy's nexus. The first one who destroys the opposing team's nexus wins. The dataset we have here has 149400 rows and the main columns we want to mainly focus on today are the champion, position, result, and kills columns. Champion: the name of character, position: the role played, result: win or lost, and kills: the amount of individual takedowns.

## Cleaning and EDA
### Data Cleaning
In the data cleaning process, I included the columns: 'gameid', 'datacompleteness', 'position', 'champion', 'result', 'kills', 'deaths', 'assists', 'doublekills', 'triplekills', 'quadrakills', 'pentakills'. The rest of the other columns were dropped as they were not relavent to the analysis. Then, I removed the team data as I want to focus on individual player data. I also created two separate columns called 'win' and 'lose' that interprets the result column in type bool to clearly decipher if a player lost or won a particular game. Finally, I filled in NaN values of the multikill columns with 0.0 because likely if a multikill is NaN then it was not achieved and the value would be 0.

| gameid                | datacompleteness   | position   | champion   |   result |   kills |   deaths |   assists |   doublekills |   triplekills |   quadrakills |   pentakills | win   | lose   |
|:----------------------|:-------------------|:-----------|:-----------|---------:|--------:|---------:|----------:|--------------:|--------------:|--------------:|-------------:|:------|:-------|
| ESPORTSTMNT01_2690210 | complete           | top        | Renekton   |        0 |       2 |        3 |         2 |             0 |             0 |             0 |            0 | False | True   |
| ESPORTSTMNT01_2690210 | complete           | jng        | Xin Zhao   |        0 |       2 |        5 |         6 |             0 |             0 |             0 |            0 | False | True   |
| ESPORTSTMNT01_2690210 | complete           | mid        | LeBlanc    |        0 |       2 |        2 |         3 |             0 |             0 |             0 |            0 | False | True   |
| ESPORTSTMNT01_2690210 | complete           | bot        | Samira     |        0 |       2 |        4 |         2 |             0 |             0 |             0 |            0 | False | True   |
| ESPORTSTMNT01_2690210 | complete           | sup        | Leona      |        0 |       1 |        5 |         6 |             0 |             0 |             0 |            0 | False | True   |

### Univariate Analysis
<iframe src="univariate.html" width=800 height=600 frameBorder=0></iframe>

This is a distribution of the winrates of the champions. As you can see, it is somewhat normally distributed as most champions hover around the 50% range as they should. Any champion lower than a 40% winrate or higher than a 60% would definitely need tuning from the game balancing team.

### Bivariate Analysis
<iframe src="bivariate.html" width=800 height=600 frameBorder=0></iframe>

This is a scatterplot of the average kills of a champion compared to its winrate. As you can see, there is not much correlation between the two as if we were to theoretically fit a line through the points, then the slope would be mostly flat. This means that champions that get more kills do not always win more. There are plenty other factors that would affect winrate like team composition, objective control, total gold earned, team synergy, etc. This also shows that you champions with a low average kill, like support champions, still have an equal impact as kill-focused champions.

### Interesting Aggregates
The table below shows the champions with the highest winrate. As we can see, Darius, Rell, Wukong, Twister Fate, and Taliyah are our highest winrate champions with at least a sufficient total amount of games played. Using domain knowledge, we know that Darius is often used as a counter pick to tank top laners and any weak early game champion. Teams probably only picked Darius knowing if the opposing team chose their top laner first, which scales the winrate up. Darius's oppressive early game often dominates the opposing top laner, making them have significantly less impact in the game as whole. For Rell, she is a support that is often picked as a champion that provides engage power to the team. Rell's crowd control and play-making potential can heavily carry games. For Wukong, he is a jungler strong skirmisher with a strong early and mid game that ensures the team enough early power to secure objectives and snowball the game. For Twisted Fate and Taliyah, they are midlaners with strong map presence as they have ultimate abilities that affect the whole map as well as strong crowd control spells that provide single target damage and control.

| champion     |   winrate |
|:-------------|----------:|
| Darius       |  0.569061 |
| Rell         |  0.561497 |
| Wukong       |  0.560832 |
| Twisted Fate |  0.555126 |
| Taliyah      |  0.552226 |

## Assessment of Missingness
#### NMAR Analysis
I believe that the double kill column would be NMAR because often most players do not get double kills every game or ever. Depending what role or what champion you play, it could be easier or much harder to obtain a double kill in a given game.
#### Missingness Dependency
<iframe src="missing.html" width=800 height=600 frameBorder=0></iframe>
The missingness of double kills depends on the champion, whereas the missingness of the double kills does not depend on position. With information, you are welcome to play any position you want even if you want to go for double kills, but the champion you pick might affect how easy or hard it will be to get a double kill.

## Hypothesis Testing
Let's specify and generalize the question. 

Null Hypothesis: The average number of kills for top laners is the same as the average number of kills for mid laners.

Alternative Hypothesis: The average number of kills for top laners is different from the average number of kills for mid laners.

As we can see, there a significant difference in the average number of kills between top laners and mid laners when hypothesis testing. If we use domain knowledge, we know that often mid lane is in the middle map, which has equal access to all of the map, which provides availability to get kills to be easier than top lane which is usually isolated from the rest of the map. Top lane also often contains scaling picks like tanks, which do not get kills or impact the game until later in the game, while mid lane is often impactful early game as they must help the jungler in secure objectives as well as roam to other lanes to secure kills and towers. They are also impactful late game with strong area of effect damage and/or crowd control which tend to secure more kills.

# League of Legends Prediction Model

## Framing the Problem

Prediction Problem: Predict if a team will win or lose a game based on post-game data.

Type: Binary Classification

Response Variable: Game result (Win/Loss)

Predicting the outcome of a League of Legends game can be useful for analyzing team performance and making strategic decisions. By predicting whether a team will win or lose based on post-game data, we can gain insights into factors that contribute to a team's success.

Evaluation Metric: Accuracy

Accuracy is appropriate for this classification problem as it measures the overall correctness of the predictions. We want to accurately classify whether a team will win or lose a game to evaluate the model's predictive performance.


## Baseline Model

The model used is a RandomForestClassifier.
The selected features in the model are 'firstblood' and 'firsttower'. Both of these features are nominal categorical variables. 'firstblood' indicates whether the team achieved the first kill in the game and 'firsttower' indicates whether the team destroyed the first tower.
The OneHotEncoder transformer is used for the given categorical features. In this case, since both 'firstblood' and 'firsttower' have two categories (Yes/No or 1.0/0.0 in this case), they are one-hot encoded into two binary features each.
The performance of the model is evaluated using accuracy. 

Considering the accuracy and domain knowledge, the baseline model is pretty good as the accuracy is ~66% which is above 50% in a binary style decision metric. Knowing domain knowledge in League of Legends has some correlation to the data as knowing if a team gets the first blood often gives a player/team a massive advantage especially when gathering data from professional players who know how to utilize this advantage. First tower usually indicates a given team's tempo in the game, which often correlates to a more organized team that would likely secure objectives and win the game. However, getting a first blood and/or first tower does not always gurantee an instant win as they are other factors in the game to consider and plenty ways to comeback as a losing team hence why the accuracy is about ~66% and not any higher. First blood and first tower provides an advantage to the given team but does not always gurantee their win. Given the information, this model is fairly good in the grand scheme of things.


## Final Model

The features added to the model are 'damagetochampions' and 'kills', both related to the performance of the teams in terms of damage dealt to champions and the number of kills. These features are relevant for the prediction task because they provide insights into the teams' offensive capabilities and their ability to eliminate opponents, which can significantly impact the outcome of the game.
Considering the data generating process, these features capture important gameplay dynamics. Teams that can deal higher damage to champions and secure more kills are generally more likely to win the game. By including these features in the model, we are incorporating valuable information that can improve the model's ability to distinguish between winning and losing teams.

The modeling algorithm chosen for this task is the RandomForestClassifier, which is an ensemble of decision trees. Random forests are well-suited for this prediction task because they can handle both numerical and categorical features, capture complex interactions between variables, and provide robust predictions by averaging the predictions of multiple trees.
Hyperparameters were tuned using grid search with cross-validation (5-fold). The hyperparameters that ended up performing the best were the middle 'n_estimators' (number of trees in the forest) and 'max_depth' (maximum depth of the trees). The grid search explored different combinations of these hyperparameters and selected the best combination based on the performance metric (accuracy).
The final model's performance is evaluated using accuracy. By comparing the performance of the final model with the baseline model, we can assess whether the additional features and hyperparameter tuning have led to an improvement in predictive performance.

Overall, the final model's performance is an improvement over the baseline model due to the inclusion of additional informative features and the optimization of hyperparameters. The feature transformations and encoding techniques allow the model to capture the relationships between the features and the target variable more effectively, while the hyperparameter tuning helps to find the optimal configuration of the model, leading to improved predictive accuracy.


## Fairness Analysis

For the permutation test, I will choose the following groups:

Group X: Blue team

Group Y: Red team

Null Hypothesis: The model is fair. The precision for the blue team and red team is roughly the same, and any differences are due to random chance.

Alternative Hypothesis: The model is unfair. The precision for the blue team is lower than the precision for the red team.

The evaluation metric I will use is precision. I chose precision because it provides insight into the model's ability to correctly identify the positive class (in this case, the blue team winning). The test statistic used is the difference in precision between the blue team and the red team. We will perform a two-sided test with a significance level of 0.05.
Based on the calculated p-value, we can draw conclusions about the fairness of the model's precision for the blue team compared to the red team. If the p-value is less than the significance level (0.05), we can reject the null hypothesis and conclude that the model's precision is significantly different between the two groups. Conversely, if the p-value is greater than or equal to the significance level, we fail to reject the null hypothesis and conclude that there is no significant difference in precision between the blue team and the red team. In this case, it looks like we fail to reject the null hypothesis since p-value is greater than the given threshold meaning the precision for the blue team and red team is roughly the same, and any differences are due to random chance.



