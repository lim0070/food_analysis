

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

---

### Merging the Ratings and Recipes Dataframes Together
In order to see which ratings the recipes correspond too, we have to merge the two dataframes together as the ratings dataframe only provides the "recipe_id" and not the other information that the recipes dataframe provides. To merge the two dataframes together, we merged them by the "recipe_id" column of the ratings dataframe and the "id" column of the recipes dataframe.

---

### Adding an average rating column to the merged dataframe
Given the ratings provided by every consumer of the recipes, it is logical to find the average rating of each recipe to determine which recipe is better than the other. We realized that there are some ratings that has a value of 0 and this might happen because people just didn't fill this column in. Therefore, we decided the set all the values 0 to nan instead to show that the person didn't fill the rating in. We then assigned the newly calculated average ratings as a new column in the merged dataframe.


### Cleaned and Merged Dataframe

Here is our cleaned data frame(and we display some of the impotant columns)


|    | name                                 |   minutes |   n_steps |   n_ingredients |   average_rating |
|---:|:-------------------------------------|----------:|----------:|----------------:|-----------------:|
|  0 | 1 brownies in the world    best ever |        40 |        10 |               9 |                4 |
|  1 | 1 in canada chocolate chip cookies   |        45 |        12 |              11 |                5 |
|  2 | 412 broccoli casserole               |        40 |         6 |               9 |                5 |
|  3 | 412 broccoli casserole               |        40 |         6 |               9 |                5 |
|  4 | 412 broccoli casserole               |        40 |         6 |               9 |                5 |



## Exploratory Data Analysis

### Univariate Analysis

#### Distribution of average Rating

We made a histogram visualizing the distribution of average rating from the merged dataframe. According to the plot, it is right skewed, meaning that most of the average ratings lie in between 4.5 to 5.0, which means that most recipes on the dataset are pretty good or consumers are just being too lenient when rating the recipes.


<iframe src="assets/uni_fig1.html" width=600 height=400 frameBorder=0></iframe>

---
### Distribution of Minutes

We made another histogram visualizing the distribution of the time taken to make the food and we used the minutes column in the merged dataframe to do so. According to the plot, it is left skewed, meaning there is a small amount of cases where the dish takes so long to make and most dishes falls in the range in between 0 and 100 minutes.


<iframe src="assets/uni_fig2.html" width=600 height=400 frameBorder=0></iframe>
---

### Bivariate Analysis

We believe calories do have an association between calories and rating of the recipe, so we did bivariate analysis on those two variable


<iframe src="assets/bi_fig1.html" width=600 height=400 frameBorder=0></iframe>


When we plot the calories on x axis and y on average rating, there maybe a weak positive linear relation between two variable, but higher calories tend to have higher average rating on average, so it is not assciate linearlly, but there is possitive association between two variable

In the second graph, we want to discover the relation between the steps of receipe between the average rating, so we use a line plot the find the relation between steps and rating.

<iframe src="assets/bi_fig2.html" width=600 height=400 frameBorder=0></iframe>

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

<iframe src="assets/agg_fig.html" width=600 height=400 frameBorder=0></iframe>
---

## Assessment of Missingness

### NMAR Analysis
We believe the column that might be NMAR is "review" as there might be people who don’t have time to fill in the ratings survey so they only filled in the "rating" column as it takes less time. In order to make the column MAR, we should add an additional column that contains data about the time taken for the consumers to fill in the survey so that the missingness would be explained by another column in the dataframe.
---

### Missingness Dependency
We conducted missingness dependency tests to find whether some of the missingness in one column depends on another column or not. We tested whether the missingness of the "rating" column depends on the columns "minutes" and "fill this in".


### Checking Whether Missingness of Rating Depends on Minutes
Null hypothesis: The missingness of rating values is independent of the minutes column (MCAR)
Alternate hypothesis: The missingness of rating values is dependent of the minutes column (MAR)
Test Statistic: The difference in means between the distributions where the rating column has missing values and doesn't have missing values


The distribution plots of the two distributions are listed below, where True represents that there are missing elements in the rating column and False represents that there aren’t any missing elements.


<iframe src="assets/miss_rating_distribution.html" width=600 height=400 frameBorder=0></iframe>


In order to determine whether they come from the same distribution, we ran a permutation test by shuffling the rating column 1000 times to get 1000 results of the test statistic to compare with the observed test statistic. Here is the distribution that we got from the permutation test.


<iframe src="assets/permutation_test_MCAR.html" width=600 height=400 frameBorder=0></iframe>


The p-value that we got is 0.114, which is larger than the 0.05 threshold. Therefore, we fail to reject the null hypothesis and that the missingness in the "rating" column isn't dependent on the "minutes" column. We can then conclude that the missingness in the "rating" column is MCAR as the missingness in "rating" isn't dependent on "minutes".

### Checking Whether Missingness of Rating Depends on Steps
We use pd.qcut to cut the steps interval to 10 groups and find the mean rating between all groups, below is the difference accross different groups

| stepq         |   rating_missing = False |   rating_missing = True |
|:--------------|-------------------------:|------------------------:|
| (0.999, 4.0]  |                0.157494  |               0.155893  |
| (4.0, 5.0]    |                0.0757134 |               0.0776802 |
| (5.0, 6.0]    |                0.0803763 |               0.0814711 |
| (6.0, 8.0]    |                0.168219  |               0.170458  |
| (8.0, 9.0]    |                0.0787901 |               0.0789439 |
| (9.0, 10.0]   |                0.0696148 |               0.066507  |
| (10.0, 12.0]  |                0.109771  |               0.112397  |
| (12.0, 14.0]  |                0.0783161 |               0.079742  |
| (14.0, 18.0]  |                0.0946156 |               0.0885209 |
| (18.0, 100.0] |                0.0870903 |               0.0883879 |

the observed statistic were 0.01080357191283944

Null hypothesis: The missingness of rating values is independent of the steps column (MCAR)
Alternate hypothesis: The missingness of rating values is dependent of the steps column (MAR)
Test Statistic: The difference in means between the distributions where the rating column has missing values and doesn't have missing values


The distribution plots of the two distributions are listed below, where True represents that there are missing elements in the rating column and False represents that there aren’t any missing elements.


<iframe src="assets/miss_rating2_distribution.html" width=600 height=400 frameBorder=0></iframe>


In order to determine whether they come from the same distribution, we ran a permutation test by shuffling the rating column 1000 times to get 1000 results of the test statistic to compare with the observed test statistic. Here is the distribution that we got from the permutation test.


<iframe src="assets/permutation_test2_MAR.html" width=600 height=400 frameBorder=0></iframe>


The p-value that we got is 0, which is smaller than the 0.05 threshold. Therefore, we reject the null hypothesis and that the missingness in the rating  column is dependent on the steps column. We can then conclude that the missingness in the"rating column is MAR as the missingness in rating is dependent on steps.
---
### Hypotheis Test

The question we are going to research on is that: do receipe that have more ingredients would have different rating as those have less ingredients

In this part, we will use q cut the seperate the number of ingredients and it definds if a recipe have less than 9 ingredients then it is easy, else it is complex receipe

## Set Up the Testing

Null hypothesis: All Receipe have Same Rating Scale
Alternate hypothesis: Receipe 
Test Statistic: The receipe with less ingredient have higher average rating since the effect of a bad rating have less effect on the overall rating

|    |   average_rating |   n_ingredients | difficult   |
|---:|-----------------:|----------------:|:------------|
|  0 |                4 |               9 | easy        |
|  1 |                5 |              11 | complex     |
|  2 |                5 |               9 | easy        |
|  3 |                5 |               9 | easy        |
|  4 |                5 |               9 | easy        |

We perform one side test because we think easier receipe tend to have better rating

here is the different between two group
| difficult   |    mean |
|:------------|--------:|
| easy        | 4.67743 |
| complex     | 4.67524 |

The observed stat was 0.0021929539853315916

## Permutation Test

<iframe src="assets/permutation_test.html" width=600 height=400 frameBorder=0></iframe>

We use permutation test to shuffle the missingless of rating 1000 times and get the absolute different between the original dataset and the shuffled dataframe. we use a one sided 95% confidence level test (0.05) to determine the missingless.

## Hypothesis Test conclusion
The p-value that we got is 0.148, which is larger than the 0.05 threshold. Therefore, we fail to reject the null hypothesis and receipe with more or less ingredients is rated under the same scale. It may happen because the number of ingredients does not totally represent the complexity of a receipe, like some of the receipe require lots of spices, but people may just blend them and cook in a pot, so we should find a better definition of difficulty and find out the true effect of difficulty on rating

---
