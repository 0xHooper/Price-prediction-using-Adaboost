# Price-Prediction-Using-Adaboost

Target of the project was to build a program that can simulate placing long positions on a financial instrument market.
The strategy to do so is generated by Adaboost algorithm. The idea was to create a model that would tell if the market will rise by x%(reward level), not falling below y%(risk level).

As the exemplary dataset I have downloaded Ethereum to USD pair in 4H timeframe from tradingview.com, which you can find in the resources dir.

For the given pair and variables values, model has 72% accuracy.

## Whole simulation process is about changing:
- Training set starting date and size
- Reward/Risk ratio
- Number of steps and maximum iteration in Adaboost algorithm
- Position size
- Technical analysis indicators. I have used only RSI(14) and MACD(12, 26), as it was enough for ETH/USD

## Metodology and solution:
Program consists of 7 classes
| Class | Responsibility |
| ----- | -------------- |
| Main | Setting variables to use other classes |
| PriceData | Wrapper of data used in program |
| DataImporter | Imports data from csv file into a list of PriceData Type |
| DataPreparation | Prepares imported data for simulation |
| Adaboost | Creates strong classifier to predict price moves |
| Stump | Creates weak classifier |
| ModelTester | Test the strategy created in Adaboost class |

#### Main 
- Initialize DataImporter class with a given file name
- Initialize DataPreparation class with given data, reward and risk
- Initialize Adaboost class with given training set, number of steps in each iteration of creating a Stump, maximum number of weak classifiers in a model and names of columns in the training set
- Initialize ModelTester class with given model and testing set

#### PriceData
- contains date, values of prices and indicators, label

#### DataImporter
- read column names from csv and pass it to list
- read date
- read prices and indicators, parse it to double
- creates PriceData object

#### DataPreparation
- Labels data for binary classification. 
- Changes position of indicators values in order for algorithm to not have data, that it wouldn’t have in real time environment.
- Splits data into training and testing sets.

#### Adaboost
- Generate stumps
- Update weights after creation of each Stump
- Classify data with list of Stumps

#### Stump
- Count best Stump from possible columns and treshold values
- Calculate error and alpha 
- Classify data

#### ModelTester
- Count number of profitable trades and all trades made
- Count precision
- Count max wins and losses in a row
- Count potential profit for a given position size


## Output
Program outputs on the console
- Starting point of training set
- Starting point of testing set
- treshold, operation, indicator name and alpha for each stump in the model
- Number of won trades and all trades
- Precision
- Maximum number of wins and losses in a row
- Potential profit for given position size
