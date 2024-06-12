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
<iframe
    src="assets/fig_permutation.html"
    width="800"
    height="600"
    frameborder="0"
></iframe>

The distribution above demonstrates that we do not have significant evidence to reject the null hypothesis that recipes that are macro-friendly (proteins per calorie = 0.25) on average (> 50%), have an average rating of at least 4.0 stars.

The null hyothesis that we implemented in our model was to determine whether recipes that are macro-friendly (proteins per calorie = 0.25) on average (> 50%), have an average rating of at least 4.0 stars. Conversely, the alternative hypothesis was the the recipes that are macro friendly have an average rating less than 4.0 stars. To determine this, we decided that we would use an absolute difference of means as a test-statistic as we approached the model as a permutation test. The test statistic observed the absolute difference of the observed proportion of data given by the macro-friendly recipes subtracted by an observance level of 0.5 since that is the value being tested through the null and alternative hypothesis. We believed that a permutation test was applicable for this model as we were comparing different distributions and not referring to the a population parameter. Similarly, an absolute difference in means fit the the test based on the data we observed. Given our choice of significance level, which was (fill here) because we believed this was reasonable in relation to the data, after the computation of the p-value came out to be (fill here), we concluded we do not have sufficient evidence to reject the null hypothesis and therefore it is likely that the macro-friendly recipes have an average rating of at least 4 stars. *could change last sentence here

## Framing a Prediction Problem
## Baseline Model
## Final Model
## Fairness Analysis