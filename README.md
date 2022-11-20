# Credit for the Data

Credit for this data goes to Pro Football Reference. Learn more at https://www.pro-football-reference.com/

# Introduction

Through the project, we intend to predict NFL Fantasy Football statistics for the upcoming year based upon input data from previous years. Following the inception of the game virtually, fantasy football not only experiences high popularity as exemplified by its 60 million annual players, but also serves as a driving force for the sport's growth itself. In particular, the ability to replicate the role of a General Manager draws into a user's managerial aspirations, while the social interconnectivity of the game creates an intrinsic network effect. Statistically, fantasy football makes an interesting candidate for prediction modelling due to the abundance of available data on each player and the importance of predicting player performance. Within the game, the initial drafting of players represents the most crucial stage for user success, so an understanding of their statistical projections certainly serves as a benefit. At the same time, since each position acculumates different statistics, the assessment of players based on different models creates further interesting subtopics in the analysis. With the combination of these factors, the project implements the linear regression of multiple predictors to draw player PPR Fantasy Projections given the input of this year's data.  

# Methodology




# Parsing the Data

Pro Football Reference provides passing data and from scrimmage data (which includes rushing stats and receiving stats) for many NFL seasons. Since quarterbacks can accrue from scrimmage stats and running backs and wide receivers can accrue passing stats, it was necessary to combine the passing and from scrimmage data into one table to calculate how many fantasy points a player got in a given year. We did this with the built-in Pandas funciton merge(). Many players are also missing certain stats (for example many wide receivers have no rush attempts), so we imputed all missing values to 0. Finally, we created several new columns to have at our disposal for when we go to run our regressions. These include boolean variables for whether or not a player made the pro bowl, a boolean for whether or not a player got named to first team all pro, columns for many important stats averaged over the number of games played by that player that season, PPR fantasy points, and PPR fantasy points per game. (Note: PPR stands for point per reception - it's a popular scoring system for fantasy football).

We then built a master table that includes the data from the years 2015-2019 with an extra column for the year those stats were recorded in and a column for the number of fantasy points scored in the following season. For example, for a row with a player's stats from 2017, the year column would have 2017, and the next year's fantasy points column would have the number of points that player scored in 2018.

# Regression Assumptions

1. a player's performance from more than one year prior is uncorrelated their performance in the upcoming season
2. the residuals of each data point are uncorrelated
3. residuals are normally distributed

# Analysis

## Interpretation of Coefficients

The coefficient on each parameter represents the average increase in fantasy output in the following year for a one unit increase in that parameter. However, several of the parameters are correlated (such as touchdown percentage and completion percentage), so their coefficients cannot be determined independently. Instead, the model will be more equipped to find the sum of such coefficients.

### Quarterback Regression Parameters
1. Adjusted net yards per attempt (average yardage per passing attempt accounting for touchdowns and interceptions)
2. Touchdown percentage
3. Completion percentage
4. Yards per completion
5. Rushing touchdowns
6. Age

### Running Back Regression Parameters
1. Rush attempts
2. Rush yards per attempt
3. Rush yards per game
4. Yards per touch
5. Receptions per game
6. Reception yards

### Wide Receiver Regression Parameters
1. Receiving yards per game
2. Receptions per game
3. Yards per reception
4. Total receiving yards
5. Targets
6. Age


## Potential Confounding Variables

Even our best multivariable regression models don't have R-squared values about 0.3. Low R-squared means that much of the variation in the output variable is not explained by the parameters. This is not surprising considering how simple these models are and how complicated football is. We record future exploration of this topic include the following in all models:

1. a metric of strength of schedule (power rankings of opposing defenses)
2. a metric for liklihood of injury (could be found using a player's injury history)
3. extra parameters for fantasy production in previous years (not just 1 season before the season we are trying to predict)
