
Introduction: 
Football, better known as soccer in the US and Canada, is arguably the most popular sport in the world. It thus, necessitates the need to better understand the game by making some analysis of the game to explore more insights. In this task, I make some analysis and subsequently create an ML model that predicts the outcome of a football match (win, draw, or lose by the home team).
I was provided with the European Soccer Dataset for this task, which can be found at: https://www.kaggle.com/datasets/hugomathien/soccer 

Problem Statement and Approach:
The database consists of 7 tables, which each contains numerous features. The first step I took was to thoroughly explore the database given, and to decide on the table(s) and features to consider in this task. The match table, which is the core of this task, contains a lot of features which either contributes little or no relevance to the task at hand. As such, I devoted time deciding on the features to include in this task. Since basically, the goals scored in a match determines the outcome of the game, I decided to focus on features that contain information about goals. 
The selected features for this task is as shown below.
 
The decision to consider the English Premiere League for this task is due to the fact that, it is arguably the most competitive and most followed league in the world presently. Hence, making an analysis based on the EPL will thus, be much appreciated by the many who love the ‘game’!
The first ten rows of the table obtained is as shown below.
 
The next step I took was to check for any missing values. Apparently, missing values can normally lead to degradation of the performance of machine learning models and as such, there is the need to check for them, when implementing an ML.
The result of this part of the task is as shown below.
 
As can be seen from the result above, All the features considered in this task does not contain any missing value. (A sigh of relief ). Next, I checked for outliers and to correct them, if existed any. 
Afterwards, I checked the statistics of the dataset. The result is as shown below.
 
The following observation can be made from the results obtained above.
1.	On average, home teams score about (~2) goals per game, while away teams score about a goal (~1) per game. This implies that on average, home teams should be winning more games than away teams. The checks I made revealed that, this assumption is true, as about 46% of the time, home teams won the match, about 26% of the time, the game ended in a draw, and about 28% of the time, the away team carried the day. 
2.	On the 25th quantile, home teams score 1 goal while away teams don’t score a goal. This implies that, on 1/4th of the time, home teams win by a goal to nil.
3.	The maximum number of goals ever scored by a home team is 9. This might be an outlier in the dataset (true outlier). The maximum goals scored by an away team is 6. This information, proves the fact that home teams seem to win more matches, which it is, of course.
4.	The standard deviation also reveals that; the home teams’ goals are more ‘spread out’ than the away teams; sometimes they score high goals, and sometimes they score low goals. This is obvious because when a ‘big’ team (like Chelsea) plays against a ‘small’ team (like Norwich City), then the tendency for the home team (Chelsea) to score more goals is high. When Norwich city happen to be the home team, then the probability that the home team will record less number of goals is high.

Moving forward, the prediction of the outcome of a game will be based on the average number of goals scored per season by a team, and the average number of goals they have scored against their opponents. The later might seem to provide enough information to make a prediction, but I realized that each team is different each season, at least, according to the dataset used in this task. Although if we consider only the previous games played between two teams for the prediction, we might have a good score (accuracy), but in reality, the outcome of a game doesn’t only depend on the previous records of the two teams. The performance of a team during a particular season might have an influence on the outcome of a game. As an aside, if we base our prediction of a game between Manchester United and Liverpool FC, in 2022, on their previous matches, the outcome will obviously be that, Manchester United will win the game (since Manchester United has more wins against Liverpool in history). But that won’t be the case in reality. For example, Liverpool FC trashed Manchester United by 4 goals to nil (sorry if you are a United fan at this moment) in 2022, which would have been contrary to the outcome, if we had based our prediction on just the previous matches between the two teams without considering their present form.

The Model:
To build a model, we need the input features and the target values. Till this point, we have decided and worked on the input features, but we don’t have the target values yet. The target values, were obtained by iterating over the dataset, and if the home team’s goals were more than the away team’s, a value of 1 was assigned, if the score was equal, a value of 0 was assigned, otherwise, a value of -1 was assigned to indicate the home team lost the game. 
A sample of the transformed dataset is as shown below.
 
Note the following abbreviations and their meanings.
HTAGS – Home Team Average Goals per Season
HTAGT – Home Team Average Goals per Team (average goals scored against their opponents).
ATAGS – Away Team Average Goals per season
ATAGT – Away Team Average Goals per Team
The first four columns are the input features, and the last column represents the target values (target feature). 
When it comes to model selection, there are tons of options available to choose from, but I decided to go for Sklearn’s ‘KNeighborsClassifier’ since it is easy to implement, beginner friendly, and provides good results.
I used 80% of the dataset for training the model, and reserved the remaining 20% for testing. The results obtained, indicated that the model made the right prediction 57.89% of the time.
The confusion matrix, when calculated and plotted, had the results as shown below.
 
From the results above, the following conclusions can be made.
1.	During 92 games, the home team lost the game and the model correctly predicted it. 11 times, the home team lost the game and the model predicted it as a draw. For about 78 times, the home team lost the game and the model predicted it as a win. This is probably due to the fact that most teams perform differently each season. This is particularly true for ‘middle performing’ teams (like Everton in the EPL). During some seasons, they perform very well, and during others, their performance can be bad.
2.	Home teams drew 42 games and the model predicted it as a lose, 9 games, the model predicted it rightly as a draw, and for a whopping 81 times, the model predicted the home team will win the game while they actually drew the match. This too, is a real life scenario; most big teams when expected to win a game, normally end up drawing the game.
3.	The last row of the results above indicates that; 34 games were won by home teams while the model predicted it as a lost. This can be explained for, by the fact that most ‘small teams’ usually pull a surprise win at their home grounds. For about 251 games, the model correctly predicted the match as a win for the home team, which indeed, was true. This implies that most of the times, the features feed into the model, helped it make the right decision.

Conclusion and suggestions:
Though, the approach incorporated into this task was easy and simple, I believe it was a great way to have my hands on a real-world project. I was able to explore more insights from the dataset.
I believe, with further research and reconsideration of the features selected for this task, the accuracy level of 57.89% can be increased. For example, if the attributes of teams (like defense ability, strength level of the team, information of the first eleven players to play the match, etc) and player attributes (like goal scoring ability, defense ability, overall rating of players, etc) are considered, the accuracy level can be better.   
