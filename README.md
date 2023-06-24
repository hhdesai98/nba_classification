# All-NBA Classification Project

### Project Goals

In this project I aim to create a classifier to predict whether a given NBA player will be All-NBA or not at the end of season. All-NBA honors are given at the end of each NBA season, where 3 teams are constructed: 1st Team All-NBA, 2nd Team All-NBA, and 3rd Team All-NBA. Each team consists of 2 guards, 2 forwards and 1 center. Awards are voted on based by various media members and outlets selected by the NBA.

### Methods

I will be fitting 4 main models for this classification task: Logistic Regression, Random Forests, XGboost, and an ensemble Voting classifier using the prior 3 models. I will fit the models first disregarding the positions, and then I will fit each model on only players from the 3 positions (G, F, C). I will compare the results of running 1 larger model vs the combined results of 3 smaller models. 

### Data Sourcing

All data was sourced from Basketball-Reference. The data collected includes player box-score statistics, advanced statistics, and All-NBA selections. The years were selected as 1980-2023. 1980 was chosen as the minimum year because that is the first year the 3 point line was introduced, starting the "Modern NBA".

The data was scraped using the Python pandas and beautifulsoup4 packages.

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_scripting_merging.ipynb` 

### Feature Engineering and Data Normalization

The primary data consists of almost all numeric variables, with basic box score stats and advanced statistics describing player performance. The main features added by me, were the seed of the teams for each player in a given year and the number of All-NBA selections they had recieved in the past. 

However, since the NBA is an ever-evolving league, NBA statistics from year to year are constantly changing. For example, in the 2000-2001 NBA season teams scored an average of 94.8 points per game. In 2023 they scored 114.7. This means overall player points per game is increasing as well. Since All-NBA teams are awards based on a players performance respective to their peers in a given season, we must somehow adjust these season stats so they are all on the same scale. In order to account for this, each seasons statistics will be transformed so that each individual season has mean 0 and standard deviation 1 for each numerical feature. This will allow for season vs season comparison, since each stat will now represent where a player stood amongst their peers in that season. This will also mean that the overall dataset will now have mean 0 and sd 1 for each statistic as well, giving us similar numerical stability as standardizing the entire dataset, but with slightly different values. This normalization was done for the entire dataset (rather than just on a training set), since it requires a full season of player data in order to work. 

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_cleaning_test_train.ipynb` 

### Training and Test Split

For my test set I randomly selected 9 seasons rom the training data. I selected full seasons in order to evaluate what All-NBA teams may look like in their entirety.

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_cleaning_test_train.ipynb` 

### Results

We have for our Aggregrated Model results (combining 3 positional models):

#### Aggregated Model Results

| Model                | Accuracy               | Precision              | Recall                 | F-1 Score              | ROC-AUC                 |
| -------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | ----------------------- |
| Logistic Regression  | 0.9548                 | 0.825                  | 0.825                  | 0.825                  | 0.9893                  |
| Random Forest        | 0.9483                 | 0.800                  | 0.800                  | 0.800                  | 0.9875                  |
| XGBoost              | 0.9483                 | 0.800                  | 0.800                  | 0.800                  | 0.9858                  |
| Ensemble             | 0.9569                 | 0.8333                 | 0.8333                 | 0.8333                 | 0.9926                  |


We have for our Full Model results (using all the positions as training data) as:

#### Full Data Results

| Model                | Accuracy               | Precision              | Recall                 | F-1 Score              | ROC-AUC                 |
| -------------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | ----------------------- |
| Logistic Regression  | 0.9548                 | 0.825                  | 0.825                  | 0.825                  | 0.9751                  |
| Random Forest        | 0.9419                 | 0.775                  | 0.775                  | 0.775                  | 0.9729                  |
| XGBoost              | 0.9440                 | 0.7833                 | 0.7833                 | 0.7833                 | 0.9739                  |
| Ensemble             | 0.9462                 | 0.7917                 | 0.7917                 | 0.7917                 | 0.9755                  |


### Discussion 

We see here that across almost every metric, the aggregated model (combing the 3 positional models), outperforms the larger model. This confirms my theory that different All-NBA positions have slightly different criteria. We saw overall that advanced statistics like VORP and PER were some of the most impactful features across almost all the models, indicating that they are some of the statistics that may come into consideration when voting for these players. 

For future work, I'd like to add sentiment analysis to these models. That is primarily because these players are voted on by media members to recieve these awards, making it a subjective criteria. Creating a sentiment analysis across data such as articles or tweets would help reveal the opinions of these pundits throughout the season and their view of these players. 


