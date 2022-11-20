# Credit for the Data

Credit for this data goes to Pro Football Reference. Learn more at https://www.pro-football-reference.com/

# Parsing the Data

Pro Football Reference provides passing data and from scrimmage data (which includes rushing stats and receiving stats) for many NFL seasons. Since quarterbacks can accrue from scrimmage stats and running backs and wide receivers can accrue passing stats, it was necessary to combine the passing and from scrimmage data into one table to calculate how many fantasy points a player got in a given year. We did this with the built-in Pandas funciton merge(). Many players are also missing certain stats (for example many wide receivers have no rush attempts), so we imputed all missing values to 0. Finally, we created several new columns to have at our disposal for when we go to run our regressions. These include boolean variables for whether or not a player made the pro bowl, a boolean for whether or not a player got named to first team all pro, columns for many important stats averaged over the number of games played by that player that season, PPR fantasy points, and PPR fantasy points per game. (Note: PPR stands for point per reception - it's a popular scoring system for fantasy football).

We then built a master table that includes the data from the years 2015-2019 with an extra column for the year those stats were recorded in and a column for the number of fantasy points scored in the following season. For example, for a row with a player's stats from 2017, the year column would have 2017, and the next year's fantasy points column would have the number of points that player scored in 2018.

# Regression Assumptions

1. a player's performance from more than one year prior is uncorrelated their performance in the upcoming season
2. the residuals of each data point are uncorrelated
3. residuals are normally distributed
