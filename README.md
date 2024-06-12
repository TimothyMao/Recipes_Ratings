# Exploratory Data Analysis on Recipes and Ratings


## Introduction

The data set we chose was the Recipe and Ratings dataset. Our project focuses on whether or not recipes that are macro friendly (proteins per calorie = 0.25) on average (> 50%), have an average rating of at least 4.0 stars. Readers should care about this dataset as it provides valuable information on how recipes receive their ratings and whether or not there is some specific reasons as to which recipe receives higher ratings. We were interested in this dataset and came up with an interesting question that proposes the idea that healthier foods which are macro friendly would have higher ratings due to its benefits to health. 

Our dataset has a total of 234429 rows and the relevant columns that we use consists of: 

- 'recipe id': the id of the recipe
- 'name': the name of the recipe
- 'minutes': the number of minutes it takes to prepare the recipe
- 'tags': tags from the website Food.com used for categorizing recipes
- 'nutrition': a list that consists of [calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates]
- 'proteins_per_calorie': column which we made that gives the ratio of proteins to calories in terms of calories
- 'n_steps': number of steps it takes to complete the recipe
- 'description': user provided descriptions of the recipe
- 'rating': the rating given to the recipe (0-5) stars
- 'avg_rating': the average rating of each unique recipe (0-5) stars
- 'review': user provided reviews of each recipe. 


## Data Cleaning and Exploratory Data Analysis

The first step we took was merging the two dataframes: Recipe and Ratings. After merging, we saw that ratings had missing values but they were all categorized with 0's so we filled in the 0's with np.NaN's. We then proceeded to make an average rating column in which we use as our predictor variable. In order to get the ratio of proteins to calories, we accessed the 'nutrition' column and extracted the protein and calorie information and created a new column called 'proteins_per_calorie'. There were some values that were missing due to 0 calories or proteins so we filled those values in with 0. 

| name                               |   minutes |   proteins_per_calorie |   n_steps |   avg_rating |
|:-----------------------------------|----------:|-----------------------:|----------:|-------------:|
| impossible macaroni and cheese pie |        50 |                   0.42 |        11 |            3 |
| impossible macaroni and cheese pie |        50 |                   0.42 |        11 |            3 |
| impossible macaroni and cheese pie |        50 |                   0.42 |        11 |            3 |
| impossible rhubarb pie             |        55 |                   0.14 |         6 |            3 |
| impossible seafood pie             |        45 |                   0.45 |         7 |            3 |

The table above shows a shortened version of the dataframe we merged and cleaned.

<iframe
    src="assets/fig_hist_protein_per_calorie.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

The figure above displays a univariate analysis of the proteins per calorie column. We can see how there is a right skew present with a mean around 0.1.


<iframe
    src="assets/box_fig.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

The figure above displays a bivariate analysis of proteins per calorie and its effect on average rating. There are slightly higher ratings for recipes that have a higher ratio of protein to calorie.


<iframe
    src="assets/pivot_table.html"
    width="400"
    height="600"
    frameborder="0"
></iframe>

The table above displays a pivot table that groups the columns 'proteins per calorie', 'n_steps', and 'minutes' by each unique value and gets an aggregate analysis of the mean average rating. We start to see higher ratings with less proteins per calorie, n_steps, and minutes, and the ratings start to go down as they increase. However, as we approach the end, where 'proteins per calorie', 'n_steps', and 'minutes' are all at their highest, the mean average ratings are similar to the ones in the beginning. We suspect the reasoning behind this is people usually enjoy recipes that are quick and easy to make and not the longer ones as much. However, people also enjoy very long recipes as usually recipes with a long preparation result in an extremely tasty dish.



## Assessment of Missingness
<iframe
    src="assets/fig_name.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

The distribution above shows a column in which 'average rating' does not depend on, namely, 'name'. We can see the observed statistic was 0.77 while there is a mean around 0.73 which is very close.


## Hypothesis Testing

The null hypothesis that we implemented in our model was that the ratio of recipes that are macro-friendly (proteins per calorie = 0.25) and have an average rating of at least 4.0 stars is equal to 0.5. Conversely, the alternative hypothesis was that the recipes that are macro friendly have an average rating less than 4.0 stars. To determine this, we decided that we would use a difference of means as a test-statistic as we approached the model with a permutation test. The test statistic observed the difference of the observed proportion of data given by the macro-friendly recipes subtracted by an observance level of 0.5 since that is the value being tested through the null and alternative hypothesis. We believed that a permutation test was applicable for this model since we didn’t know what the population distribution looked like. Similarly, a difference in means fit the test based on the data we observed because this is a one sided t test. Given our choice of significance level, which was 0.05 because we believed this was reasonable in relation to the data, after the computation of the p-value came out to be 0.0, we concluded we have sufficient evidence to reject the null hypothesis.

<iframe
    src="assets/fig_permutation_test.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

The distribution above demonstrates that we have significant evidence to reject the null hypothesis that the proportion recipes that are macro-friendly (proteins per calorie = 0.25) and have an average rating of at least 4.0 stars is equal to 0.5. There are no values in which the permuted result is was less than our observed statistic which means our p-value was 0.0.

## Framing a Prediction Problem

Our prediction problem is focusing on whether or not recipes that are macro-friendly can predict a higher average rating. With this prediction problem at hand, we determined that this problem is classified under a regression type. Our model is a classifier that focuses on binarizing the data, so we performed binary classification in the model experiment. The response variable we are predicting is the average rating as we were hoping to determine if macro-friendly recipes were considered above average in rating, and that was the main factor. The metric we are using to evaluate the model was RMSE or root mean squared error and the reason we decided on this metric was that we found it to be more accurate with the training model, than the other test metrics. The only information that we know of are characteristics of the recipes such as how many minutes it takes to complete, number of steps to complete, and nutritional value of the recipe. We wouldn’t know information about the reviews written and the ratings it received yet.

## Baseline Model

The model is a pipeline that performs on the features but is classified by linear regression. The preprocessing step involves binarizing three features: minutes, n_steps, and proteins_per_calorie.
The features used in the model are:
1. minutes: Quantitative
2. n_steps: Quantitative
3. proteins_per_calorie: Quantitative
The target variable is ‘avg_rating’ for our model.
The pipeline in our baseline model consists of two main steps, which is applying the binarization to the specified features and using linear regression to fit the model on the preprocessed data. In terms of model performance, the model is evaluated using the root mean squared error (RMSE) and the R-squared score on both the training and test sets. The model that was developed we did not consider “good” as the factors that we looked into when determining the performance whether the RMSE values were lower in value which indicates a better fit or the R-squared score was close to 1. Based on our results, we determined it was difficult to state that the performance was “good” definitively,  and there were definitely areas for improvement in which the model could be more fitting as there were some discrepancies between the train and test scores that were messing with its general performance and test accuracy.

## Final Model

In the final model, the features selected are minutes, proteins_per_calorie, and tags. These features were chosen for the following reasons:
1. Minutes: This feature represents the time required to prepare the dish. It is a relevant factor as the preparation time can impact the overall rating of the recipe. Dishes that take too long might be rated lower if the outcome isn't perceived as worth the effort.
2. Proteins per Calorie: This feature captures the nutritional density of the dish in terms of protein content. High-protein diets are popular for health and fitness reasons, and recipes that offer more protein per calorie could be rated higher due to being healthier options.
3. Tags: This categorical feature includes various labels associated with the recipe (e.g., vegan, dessert, quick). These tags can significantly influence ratings  based on the type of dish and whether it meets dietary preferences or occasions.
The modeling algorithm chosen is Ridge Regression, which is a regularized linear regression technique. Regularization helps prevent overfitting by penalizing large coefficients.
The hyperparameters that ended up performing the best are:
* alpha: This parameter controls the strength of the regularization. The best performing values found in the grid search were in the range of [0.1, 1.0, 10.0, 100.0].
* fit_intercept: The boolean parameter indicates whether to fit the intercept term or not. 
The hyperparameters were selected using GridSearchCV, which performs a search over specified parameter values for an estimator. The grid search was done using  a cross-validation strategy involving cv=5, and scored using the negative mean squared error (neg_mean_squared_error). The method allowed us to evaluate all combinations of the provided hyperparameter values and select the combination with the optimal performance, using the score method.
To evaluate the performance improvement of the final model over the baseline model, the following metrics were compared: Train Score, Test Score, RMSE Train, and RMSE Test. These metrics gave an insightful view of the model's performance in terms of both fit and predictive accuracy. Improvement is expected in terms of lower RMSE and higher R-squared scores. Overall, these changes in metrics used as well as the ridge regression method allowed for a better predictive performance that was more well fit than the baseline model we had created, which allowed for more accurate results when determining our conclusions to the tests.

## Fairness Analysis

Group X: Group 1 (recipes with minutes less than or equal to the mean minutes)
Group Y: Group 2 (recipes with minutes greater than the mean minutes)
The Evaluation Metric used in the model was the R-squared score, used to evaluate the model on different groups.
Hypotheses
* Null Hypothesis (H0): Our model is fair. There is no difference in model performance (R-squared score) between Group 1 and Group 2. Any observed difference is due to random chance.
* Alternative Hypothesis (H1): Our model is unfair. There is a significant difference in model performance (R-squared score) between Group 1 and Group 2.
The observed difference between the R-squared scores of Group 1 and Group 2 is used as the test statistic.
Significance Level:
The chosen significance level that depicted the experiment was 5% or 0.05
The resulting p-value is calculated as the proportion of permuted differences that are greater than or equal to the absolute observed difference.
Based on the analysis of the model, the p-value suggests we would reject the null hypothesis, as we can deduce there is a significant difference in model performance between groups 1 and 2 under the given significance level.
