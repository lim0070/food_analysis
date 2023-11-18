

---


# Research on Food Recipes and Ratings
Made by Brighton Chan and Lincoln Ma


## Introduction
We consume food not only because they give us energy, we also eat food because they taste good. Therefore, restaurants needs reviews and ratings from their consumers so that they know how to improve their recipes. In this project, we hope to see whether the number of ingredients used in the recipe tend to receieve a higher average rating.

---


The dataset that we collected is from food.com. There are two dataframes that we used, a dataframe with all the recipes and another one with the ratings. In the recipes dataframe, there are 83,782 rows and 12 columns. Some of the relevant columns in the recipe dataframe are id, ingredients, n_ingredients. In the ratings dataframe, there are 731,927 rows and 5 columns. Some of the relevant columns in the ratings dataframe are recipe_id and rating. We are going to merge the two dataframes using the id column of the recipe dataframe and recipe_id column of the ratings dataframe. We are going to conduct a permutation test on the n_ingredients and rating columns to see whether they come from the same distribution to determine whether the number of ingredients used in a recipe affects the average rating.

---

## Cleaning and EDA (Exploratory Data Analysis)
###Checking the types of data in the dataframes
We realized that the columns tags, nutrition, steps, description, and ingredients are all string representations of a list, which means if we were to query for those elements we can't get the elements inside the list. Therefore, we changed the data type of those columns from string objects to lists.
Specifically, we believe that all the elements in the list for the nutrition column are valuable information. Therefore, we assgined each of the elements in the nutrition list as an individual column in the dataframe, which are 'calories', 'total fat (PDV)', 'sugar (PDV)', 'sodium (PDV)', 'protein (PDV)', 'saturated fat (PDV)', and 'carbohydrates (PDV)' respectively, which each of the columns has a data type of float, which would be more convenient if we want to use these data for aggregation.


### Merging the Ratings and Recipes Dataframes Together
In order to see which ratings the recipes correspond too, we have to merge the two dataframes together as the ratings dataframe only provides the "recipe_id" and not the other information that the recipes dataframe provides. To merge the two dataframes together, we merged them by the "recipe_id" column of the ratings dataframe and the "id" column of the recipes dataframe.


### Adding an average rating column to the merged dataframe
Given the ratings provided by every consumer of the recipes, it is logical to find the average rating of each recipe to determine which recipe is better than the other. We realized that there are some ratings that has a value of 0 and this might happen because people just didn't fill this column in. Therefore, we decided the set all the values 0 to nan instead to show that the person didn't fill the rating in. We then assigned the newly calculated average ratings as a new column in the merged dataframe.


### Cleaned and Merged Dataframe


## Bivariate Analysis

We believe calories do have an association between calories and rating of the recipe, so we did bivariate analysis on those two variable


<iframe src="assets/bi_fig1.html" width=600 height=600 frameBorder=0></iframe>

When we plot the calories on x axis and y on average rating, there maybe a weak positive linear relation between two variable, but higher calories tend to have higher average rating on average, so it is not assciate linearlly, but there is possitive association between two variable

In the second graph, we want to discover the relation between the steps of receipe between the average rating, so we use a line plot the find the relation between steps and rating.

<iframe src="assets/bi_fig2.html" width=600 height=600 frameBorder=0></iframe>

From the plot, we can`t say there is a linear relation between the two variables, but receipes have more steps tend to have a larger variation of average rating among receipes with less steps.

## Interesting Aggregates

In the aggregates analysis, we will study minutes on average rating

|    mean |   max |   min |   median |
|--------:|------:|------:|---------:|
| 5       |     5 |     5 |  5       |
| 4.78565 |     5 |     1 |  5       |
| 4.75684 |     5 |     1 |  4.94737 |
| 4.73303 |     5 |     1 |  4.85714 |
| 4.57981 |     5 |     1 |  4.75    |

This is a pivot table of rating on minutes, it tells us about the range, mean and the median of the data, below is the box plot of the rating of first 5 mins

<iframe src="assets/agg_fig.html" width=600 height=600 frameBorder=0></iframe>





## a and b

Null mar
Alter mcar

graph missingless

We use permutation test to shuffle the missingless of rating 1000 times and get the absolute different between the original dataset and the shuffled dataframe. we use a two sided 95% confidence level test (0.025) to determine the missingless.

pval chat

The p value of the above stat is 0.0, which we can reject that the 



---
