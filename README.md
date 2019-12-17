# NYT_Bestsellers
## The Question
Can we predict whether or not a book will become a New York Times Bestseller?

## The Data
I webscraped data from the top books of 2017-2019 lists on Goodreads.com, as well as called the NYT Bestsellers API for 2017-2019 bestsellers and identified books as Bestsellers or Non-bestsellers. Variables included publisher, author's number of followers on Goodreads, Genre, Pages, Publisher, Part of a Series, and Rating on Goodreads. Finally, I scraped books that appeared on celebrity bookclub lists from Barnes & Noble.com as identified on a list they maintain. In total, I wound up with 1,309 datapoints.

## Features
Author Follower’s distribution is skewed right, therefore I performed a log transformation. I also created Dummy variables for all categorical data.
![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/pages.pngstyle=centerme) ![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/ratings.pngstyle=centerme) ![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/author_followers.pngstyle=centerme)

## Modeling
### Base Model
72.4% of the dataset is non-bestsellers, therefore a Dummy Classifier achieved 72.6% accuracy. Due to the nature of the dataset, we care about Precision, not accuracy. The dataset is skewed towards non bestsellers, therefore high accuracy is not meaningful. High Precision means that if a publisher takes on a book as a result of this model, there is a high chance that the book will become a Bestseller.
Poor recall means opportunity cost, but for the sake of this model I chose to focus on Precision to ensure a good investment.
![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/baselinecm.png)

### SMOTE for Class Imbalance
I used SMOTE to deal with the class imbalance of Non-bestsellers over bestsellers.
![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/class_imbalance.png)

### Final Model - Logistic Regression
Logistic Regression with GridSearch optimized parameters (C = 1, Penalty = 11) was the best resulting model with an ROC of 0.72.
![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/ROCcurve.png)
Precision: 71%
Accuracy: 72%
Recall: 49%
F1: 5%

## Feature Importance
1. Author’s # of Followers
2. Book Rating
3. Genre: Romance, Nonfiction
4. Publisher: Farrar, Straus, and Giroux, Knopf Publishing Group
5. Part of a series
![alt text](https://github.com/clareblessen/NYT_Bestsellers/blob/master/Images/feature_importance.png)

## Significance
The model’s predictors are fairly common sense: a book by a famous author with a good publishing house has the best chance of being a NYT Bestseller. However, there are some interesting things to infer from the model: Romance and Nonfiction books are more likely to be bestsellers. Going forward, I would be interested in addressing this question from a Natural Language Processing standpoint of the book descriptions, along with more data.
