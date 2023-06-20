# All-NBA Classification Project

### Project Goals

In this project I aim to create a classifier to predict whether a given NBA player will be All-NBA or not at the end of season. All-NBA honors are given at the end of each NBA season, where 3 teams are constructed: 1st Team All-NBA, 2nd Team All-NBA, and 3rd Team All-NBA. Each team consists of 2 guards, 2 forwards and 1 center. Awards are voted on based by various media members and outlets selected by the NBA.

### Methods

I will be fitting 3 main models for this classification task: Logistic Regression, Random Forests, and XGboost. 

### Data Sourcing

All data was sourced from Basketball-Reference. The data collected includes player box-score statistics, advanced statistics, and All-NBA selections. The years were selected as 1980-2023. 1980 was chosen as the minimum year because that is the first year the 3 point line was introduced, starting the "Modern NBA".

The data was scraped using the Python pandas and beautifulsoup4 packages.

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_scripting_merging.ipynb` 

### Feature Engineering and Data Normalization

Since the NBA is an ever-evolving league, NBA statistics from year to year are constantly changing. For example, in the 2000-2001 NBA season teams scored an average of 94.8 points per game. In 2023 they scored 114.7. This means overall player points per game is increasing as well. Since All-NBA teams are awards based on a players performance respective to their peers in a given season, we must somehow adjust these season stats so they are all on the same scale. In order to account for this, each seasons statistics will be transformed so that each individual season has mean 0 and standard deviation 1 for each numerical feature. This will allow for season vs season comparison, since each stat will now represent where a player stood amongst their peers in that season. This will also mean that the overall dataset will now have mean 0 and sd 1 for each statistic as well, giving us similar numerical stability as standardizing the entire dataset, but with slightly different values. This normalization was done for the entire dataset (rather than just on a training set), since it requires a full season of player data in order to work. 

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_cleaning_test_train.ipynb` 

### Training and Test Split

I utilized an 80/20 training-test split in order to evaluate the performance of my models.

The code and notebooks associated with this section can be found in the Data_Scripting_Cleaning folder, specifically in `data_cleaning_test_train.ipynb` 

### EDA





