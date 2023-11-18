

---


# Research on Food Recipes and Ratings
Made by Brighton Chan and Lincoln Ma


## Introduction
We consume food not only because they give us energy, we also eat food because they taste good. Therefore, restaurants needs reviews and ratings from their consumers so that they know how to improve their recipes. In this project, we hope to see whether the number of ingredients used in the recipe tend to receieve a higher average rating.


The dataset that we collected is from food.com. There are two dataframes that we used, a dataframe with all the recipes and another one with the ratings. In the recipes dataframe, there are 83,782 rows and 12 columns. Some of the relevant columns in the recipe dataframe are id, ingredients, n_ingredients. In the ratings dataframe, there are 731,927 rows and 5 columns. Some of the relevant columns in the ratings dataframe are recipe_id and rating. We are going to merge the two dataframes using the id column of the recipe dataframe and recipe_id column of the ratings dataframe. We are going to conduct a permutation test on the n_ingredients and rating columns to see whether they come from the same distribution to determine whether the number of ingredients used in a recipe affects the average rating.



## Bivariate Analysis

We believe calories do have an association between calories and rating of the recipe, so we did bivariate analysis on those two variable


<iframe src="assets/bi_fig1.html" width=600 height=600 frameBorder=0></iframe>

When we plot the calories on x axis and y on average rating, there maybe a weak positive linear relation between two variable, but higher calories tend to have higher average rating on average, so it is not assciate linearlly, but there is possitive association between two variable

In the second graph, we want to discover the relation between the steps of receipe between the average rating, so we use a line plot the find the relation between steps and rating.

<iframe src="assets/bi_fig2.html" width=600 height=600 frameBorder=0></iframe>

From the plot, we can`t say there is a linear relation between the two variables, but receipes have more steps tend to have a larger variation of average rating among receipes with less steps.

## Interesting Aggregates

In the aggregates analysis, we will study the 
'<table border="1" class="dataframe">\n  <thead>\n    <tr style="text-align: right;">\n      <th></th>\n      <th>mean</th>\n      <th>max</th>\n      <th>min</th>\n      <th>median</th>\n    </tr>\n    <tr>\n      <th>minutes</th>\n      <th></th>\n      <th></th>\n      <th></th>\n      <th></th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <th>0</th>\n      <td>5.000000</td>\n      <td>5.0</td>\n      <td>5.0</td>\n      <td>5.000000</td>\n    </tr>\n    <tr>\n      <th>1</th>\n      <td>4.785655</td>\n      <td>5.0</td>\n      <td>1.0</td>\n      <td>5.000000</td>\n    </tr>\n    <tr>\n      <th>2</th>\n      <td>4.756842</td>\n      <td>5.0</td>\n      <td>1.0</td>\n      <td>4.947368</td>\n    </tr>\n    <tr>\n      <th>3</th>\n      <td>4.733029</td>\n      <td>5.0</td>\n      <td>1.0</td>\n      <td>4.857143</td>\n    </tr>\n    <tr>\n      <th>4</th>\n      <td>4.579813</td>\n      <td>5.0</td>\n      <td>1.0</td>\n      <td>4.750000</td>\n    </tr>\n  </tbody>\n</table>'




---
