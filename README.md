

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
| name                                 |     id |   minutes | nutrition                                                        |   n_ingredients |   rating |
|:-------------------------------------|-------:|----------:|:-----------------------------------------------------------------|----------------:|---------:|
| 1 brownies in the world    best ever | 333281 |        40 | ['138.4', ' 10.0', ' 50.0', ' 3.0', ' 3.0', ' 19.0', ' 6.0']     |               9 |        4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 | ['595.1', ' 46.0', ' 211.0', ' 22.0', ' 13.0', ' 51.0', ' 26.0'] |              11 |        5 |
| 412 broccoli casserole               | 306168 |        40 | ['194.8', ' 20.0', ' 6.0', ' 32.0', ' 22.0', ' 36.0', ' 3.0']    |               9 |        5 |
| 412 broccoli casserole               | 306168 |        40 | ['194.8', ' 20.0', ' 6.0', ' 32.0', ' 22.0', ' 36.0', ' 3.0']    |               9 |        5 |
| 412 broccoli casserole               | 306168 |        40 | ['194.8', ' 20.0', ' 6.0', ' 32.0', ' 22.0', ' 36.0', ' 3.0']    |               9 |        5 |







### Exploratory Data Analysis

​​## Univariate Analysis
### Distribution of Average Rating


We made a histogram visualizing the distribution of average rating from the merged dataframe. According to the plot, it is right skewed, meaning that most of the average ratings lie in between 4.5 to 5.0, which means that most recipes on the dataset are pretty good or consumers are just being too lenient when rating the recipes.


<iframe src="assets/uni_fig1.html" width=800 height=600 frameBorder=0></iframe>



### Distribution of Minutes


We made another histogram visualizing the distribution of the time taken to make the food and we used the minutes column in the merged dataframe to do so. According to the plot, it is left skewed, meaning there is a small amount of cases where the dish takes so long to make and most dishes falls in the range in between 0 and 100 minutes.


<iframe src="uni_fig2.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis

We believe calories do have an association between calories and rating of the recipe, so we did bivariate analysis on those two variable


<iframe src="assets/bi_fig1.html" width=800 height=600 frameBorder=0></iframe>

When we plot the calories on x axis and y on average rating, there maybe a weak positive linear relation between two variable, but higher calories tend to have higher average rating on average, so it is not assciate linearlly, but there is possitive association between two variable

In the second graph, we want to discover the relation between the steps of receipe between the average rating, so we use a line plot the find the relation between steps and rating.

<iframe src="assets/bi_fig2.html" width=600 height=600 frameBorder=0></iframe>

From the plot, we can`t say there is a linear relation between the two variables, but receipes have more steps tend to have a larger variation of average rating among receipes with less steps.

### Interesting Aggregates

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

## Assessment of Missingness
### NMAR Analysis
We believe the column that might be NMAR is "review" as there might be people who don’t have time to fill in the ratings survey so they only filled in the "rating" column as it takes less time. In order to make the column MAR, we should add an additional column that contains data about the time taken for the consumers to fill in the survey so that the missingness would be explained by another column in the dataframe.


### Missingness Dependency
We conducted missingness dependency tests to find whether some of the missingness in one column depends on another column or not. We tested whether the missingness of the "rating" column depends on the columns "minutes" and "fill this in".


### Checking Whether Missingness of Rating Depends on Minutes
Null hypothesis: The missingness of rating values is independent of the minutes column (MCAR)
Alternate hypothesis: The missingness of rating values is dependent of the minutes column (MAR)
Test Statistic: The difference in means between the distributions where the rating column has missing values and doesn't have missing values


The distribution plots of the two distributions are listed below, where True represents that there are missing elements in the rating column and False represents that there aren’t any missing elements.


<iframe src="assets/miss_rating_distribution.html" width=800 height=600 frameBorder=0></iframe>


In order to determine whether they come from the same distribution, we ran a permutation test by shuffling the rating column 1000 times to get 1000 results of the test statistic to compare with the observed test statistic. Here is the distribution that we got from the permutation test.


<iframe src="assets/permutation_test_MCAR.html" width=800 height=600 frameBorder=0></iframe>


The p-value that we got is 0.114, which is larger than the 0.05 threshold. Therefore, we fail to reject the null hypothesis and that the missingness in the "rating" column isn't dependent on the "minutes" column. We can then conclude that the missingness in the "rating" column is MCAR as the missingness in "rating" isn't dependent on "minutes".





## a and b

Null mar
Alter mcar

graph missingless

We use permutation test to shuffle the missingless of rating 1000 times and get the absolute different between the original dataset and the shuffled dataframe. we use a two sided 95% confidence level test (0.025) to determine the missingless.

pval chat



The p value of the above stat is 0.0, which we can reject that the 



---
