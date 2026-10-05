# Can We Predict NFL Game Outcomes Using Previous Team Performance?
# Problem Overview
Predicting NFL games is difficult because many different factors can influence whether a team wins or loses. Team strength can be measured through statistics such as scoring, passing and rushing production, turnovers, previous wins, and opponent performance, but unexpected events can still change the outcome of a game.
For this project, my goal was to use machine learning to determine whether an NFL team's previous performance statistics could predict whether the team would win its next regular-season game. I treated this as a binary classification problem, where a win was represented by 1 and a loss by 0.
My main research question was: Can an NFL team's previous performance statistics be used to predict whether the team will win its next regular-season game?
# Data and Process
The data for this project came from nflverse and was accessed in Python using the nflreadpy package. I used the NFL schedule and weekly team statistics from the 2021 through 2025 regular seasons.
The original team game dataset contained 2,718 observations. I created pregame statistics including previous win percentage, recent win percentage, average points scored and allowed, passing and rushing yards, turnover differential, opponent performance, and home field status.
One of the most important parts of preparing the data was preventing data leakage. Since I wanted to predict games before they happened, I shifted the historical calculations so that the statistics from the current game were never included in its predictors.
Some observations at the beginning of each season had missing values because there were not enough previous games to calculate historical averages. After removing these observations, the final dataset contained 2,238 observations: 1,116 wins and 1,122 losses.
I used the 2021–2024 seasons to train the final models and the 2025 season for testing. This allowed the models to learn from previous seasons before being evaluated on a later season.
# Models
I created three models for comparison, the first was a Dummy Classifier that served as my baseline. It always predicted the most common outcome and achieved an accuracy of about 50.2%. This gave me a simple benchmark that my machine learning models needed to outperform.
My second model was Logistic Regression. On the 2025 test data, it achieved 62.1% accuracy, 62.7% precision, 58.7% recall, and a 60.6% F1 score.
My third model was Random Forest. It achieved 62.5% accuracy, 62.6% precision, 61.4% recall, and a 62.0% F1 score. Random Forest performed slightly better on the 2025 test set, but the difference between the two models was small.
Because the models were so close, I also compared their performance across previous seasons. Logistic Regression achieved accuracies of 61.7% in 2022, 58.7% in 2023, and 69.0% in 2024, averaging about 63.1%. Random Forest achieved 53.1%, 58.9%, and 63.6%, averaging about 58.5%.
Based on these results, I selected Logistic Regression as my final model. Although Random Forest performed slightly better in 2025, Logistic Regression performed better across multiple seasons and was easier to interpret.
# Results
The results show that previous NFL performance statistics contain useful information for predicting future game outcomes. Both machine learning models improved substantially over the 50.2% baseline, with the final Logistic Regression model achieving approximately 62% accuracy on the 2025 season.
Opponent win percentage had the strongest negative coefficient in the Logistic Regression model. This suggests that playing against a stronger opponent lowered a team's predicted probability of winning. Passing yards, home field status, recent winning percentage, and average points scored were positively associated with predicted wins.
The model was far from perfect. During error analysis, I found several games where it was confident but incorrect. For example, Tennessee was given only about a 16.5% probability of beating Arizona, but Tennessee won. The Chargers were given about an 80.2% probability of beating the Giants, but they lost.
These mistakes show one of the main limitations of the model. Historical statistics cannot account for everything that happens in an NFL game. Injuries, quarterback changes, weather, coaching decisions, turnovers during the game, and individual performances can all influence the result.
Another limitation is that each game is represented by two team observations. Since one team's win is the other team's loss, those observations are related. In a future version of this project, I would create one observation per game and directly compare the statistics of the two teams. I would also include additional pregame information such as injuries, quarterback availability, rest, and weather.
Overall, my results suggest that previous team performance can help predict NFL game outcomes, but it cannot predict them with certainty. The approximately 62% test accuracy shows that the model learned meaningful patterns while also demonstrating how much uncertainty remains in NFL games.
# Correlation Matrices
<img width="1122" height="889" alt="image" src="https://github.com/user-attachments/assets/45994dff-4f0a-4ada-8103-9c433d60acc8" />
<img width="528" height="453" alt="image" src="https://github.com/user-attachments/assets/36db44e4-acb5-4aff-a71f-0b753b424e96" />
<img width="528" height="453" alt="image" src="https://github.com/user-attachments/assets/3903e70a-65b7-445e-80c6-f512c62e7efc" />


References:

Code: 

AI disclaimer: ChatGPT assisted me to help troubleshoot and problem solve for my visuals.

