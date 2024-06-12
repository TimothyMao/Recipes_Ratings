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

|   recipe_id | name                               |   minutes | tags                                                                                                                                                                                                                                              | nutrition                                    |   proteins_per_calorie |   n_steps | description                                                                                                                  |   rating |   avg_rating | review                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------:|:-----------------------------------|----------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|-----------------------:|----------:|:-----------------------------------------------------------------------------------------------------------------------------|---------:|-------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      275022 | impossible macaroni and cheese pie |        50 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'eggs-dairy', 'pasta', 'easy', 'cheese', 'dietary', 'high-calcium', 'high-in-something', 'pasta-rice-and-grains', 'elbow-macaroni']               | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0]    |                   0.42 |        11 | one of my mom's favorite bisquick recipes. this brings back memories!                                                        |        4 |            3 | Easy comfort food! I definitely thought it was impossible, but it worked. :D  I used 6 egg whites in place of the eggs and skim milk.  It came out super fluffy.  Thanks, Wendy!                                                                                                                                                                                                                                                                                                                                                                                   |
|      275022 | impossible macaroni and cheese pie |        50 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'eggs-dairy', 'pasta', 'easy', 'cheese', 'dietary', 'high-calcium', 'high-in-something', 'pasta-rice-and-grains', 'elbow-macaroni']               | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0]    |                   0.42 |        11 | one of my mom's favorite bisquick recipes. this brings back memories!                                                        |        1 |            3 | I was looking for an easy Macaroni and Cheese for dinner.  My macaroni was hard and there were just too many eggs.  I think I might try again and precook the macaroni and only use 2 eggs.  It was just very disappointing.                                                                                                                                                                                                                                                                                                                                       |
|      275022 | impossible macaroni and cheese pie |        50 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'eggs-dairy', 'pasta', 'easy', 'cheese', 'dietary', 'high-calcium', 'high-in-something', 'pasta-rice-and-grains', 'elbow-macaroni']               | [386.1, 34.0, 7.0, 24.0, 41.0, 62.0, 8.0]    |                   0.42 |        11 | one of my mom's favorite bisquick recipes. this brings back memories!                                                        |        4 |            3 | Very easy recipe, nice presentation.  I used 2 cups  skim milk and 1/3 cup half and half.  Followed recipe exactly but left out hot sauce.  Macaroni was slightly al dente.  If you prefer well cooked macaroni, par boil it first for a few minutes.  Let baked pie cool for at least 15 minutes with foil covering the top.  This will allow the pie to &quot;settle&quot; so that it slices  into nicely formed wedges.  Definitely worth a try.  Am serving this with sauteed porto bello mushroms, sliced, on top of pie wedge, accompanied by a green salad. |
|      275024 | impossible rhubarb pie             |        55 | ['60-minutes-or-less', 'time-to-make', 'course', 'preparation', 'healthy', 'pies-and-tarts', 'desserts', 'pies', 'dietary']                                                                                                                       | [377.1, 18.0, 208.0, 13.0, 13.0, 30.0, 20.0] |                   0.14 |         6 | a childhood favorite of mine. my mom loved it because it cut down on how much time to make it.                               |        3 |            3 | When I found myself needing a dessert and having rhubarb on hand this recipe fit the bill.  I did however find it to be too overly sweet.  I would try it again, using less  sugar.  Thank you Starfire for sharing the recipe.                                                                                                                                                                                                                                                                                                                                    |
|      275026 | impossible seafood pie             |        45 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'very-low-carbs', 'main-dish', 'eggs-dairy', 'seafood', 'crab', 'cheese', 'dietary', 'low-sodium', 'low-calorie', 'low-carb', 'low-in-something', 'shellfish'] | [326.6, 30.0, 12.0, 27.0, 37.0, 51.0, 5.0]   |                   0.45 |         7 | this is an oldie but a goodie. mom's stand by for company. good enough for us on a special occasion or if company came over! |        1 |            3 | Sorry, this one didn&#039;t work out so well. I did make some modifications that may have affected the taste of the recipe. I used imitation crabmeat, egg substitute, and fat free half-and-half. Unfortunately the end result was very bland--it definitely could have used some more spice. I really wanted to like this one but I won&#039;t be making this again. Thanks for posting anyway.                                                                                                                                                                  |
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

The distribution above demonstrates that we do not have significant evidence to reject the null hypothesis that the proportion recipes that are macro-friendly (proteins per calorie = 0.25) and have an average rating of at least 4.0 stars is equal to 0.5. There are no values in which the permuted result is was less than our observed statistic.

