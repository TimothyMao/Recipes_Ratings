# Exploratory Data Analysis on Recipes and Ratings
## Project for DSC 80 at UCSD

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
  src="assets/box_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>