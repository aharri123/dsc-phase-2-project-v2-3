# Phase 2 Project


## Project Overview

For this project, you will use multiple linear regression modeling to analyze house sales in King County.

### Business Problem

We're working with a real estate agency that helps customers buy and sell houses. Using Linear Regression to analyze the given dataset, we will help the agency determine which features of a house will increase the value (price) the most. Using that data, we will help the agency advise customers about how renovations made to the house will increase the value of the house, and by how much.

### The Data

This project uses the King County house sales dataset (kc_house_data.csv), which contains 21,597 different entries of houses sold between 2014 and 2015. Each entry contains information about the house such as number of bedrooms, number of bathrooms, total square footage, etc. A full list and description of the column/variables can be found in "column_names.md". Here is our initial data after checking for null values and duplicates: 

![house_data](https://user-images.githubusercontent.com/45251340/185804066-454e137b-15aa-4768-aa4a-c1f4232dad06.JPG)


## Initial Model

We'll start modeling by choosing the feature that is most correlated with our target variable (price), and build and evaluate a linear regression model with just that feature. To do this we'll create a heatmap:

![heatmap_data](https://user-images.githubusercontent.com/45251340/185804144-87bd9dd6-454c-4509-b5ed-3eb30eb2323e.JPG)

From this heatmap, we can see that the variable most strongly correlated is sqft_living. Let's create our regression formula using price and sqft_living.

![initial_model](https://user-images.githubusercontent.com/45251340/185804430-5c60d18f-50c0-46fb-bc3d-712c187fc4ff.JPG)

After running our model, we get the following summary: 

![initial_model_results](https://user-images.githubusercontent.com/45251340/185804471-7b7b01eb-731e-40e1-8856-4fda0c8df338.JPG)

**Our R-squared value is somewhat low at 49%, so let's check some assumptions**

### Linearity
We'll plot the relationship between price and sqft_living to see if it follows a linear pattern

![assumption1](https://user-images.githubusercontent.com/45251340/185805249-b6c491af-2f34-4229-9095-064f0f7a876b.JPG)

### Normality
We'll plot the residuals against a standard normal distribution 

![assumption2](https://user-images.githubusercontent.com/45251340/185805283-6e947fcf-d804-4a63-b426-ac300026df4a.JPG)

### Homoscedasticity

We'll see if the regression plots resemble a cone shape

![assumption3](https://user-images.githubusercontent.com/45251340/185805350-8c9a9777-8bdf-4663-ba7c-9f46b85bde97.JPG)


From testing our assumptions we can see:

* Our R-squared value is somewhat low at 49%
* There is only a slight linear relationship between price and sqft_living
* The model residuals do not follow a full normal distribution
* For our regression plots for sqft_living, we see a cone shape which indicates heteroscedasticity\

Since our R-squared is low and our regression assumptions are not met, we can say that sqft_living is not ideal for soley modeling a relationship with price. We will need to take a look at additional variables and build a better model. To do this requires multilinear regression.


## Second Model

Our data has quite a lot of variables, so let's see if we can eliminate some of them based on correlation strengths and worldly logic. Let's consult our heatmap again: 

![heatmap_data](https://user-images.githubusercontent.com/45251340/185805578-9c7bc55b-8a41-4c5f-bef5-e182be424317.JPG)


### Looking at the heatmap correlation strengths, we can eliminate some low correlation variables:
* id (also a unique identifier which will not help us in the future for predictions)
* sqft_lot
* yr_renovated
* zipcode
* long
* lat (If we don't need longitude, it doesn't make sense to only put latitude)
* sqft_lot15 (We are not concerned about other neighbor's properties)

### We can eliminate some other variables as well:
* date (not in heatmap, but we're worried about the future and not the past)
* sqft_above (don't need this when we have total square footage)
* sqft_basement (not in heatmap, but sqft of basement is already included in sqft_living)
* sqft_living15 (we are not concerned about other neighbor's properties)

Our data now looks like this: 

![house_data](https://user-images.githubusercontent.com/45251340/185805664-a7766cd5-0a84-48fd-bf66-3775be9c00a9.JPG)

We can see there are some categorical variables, so after coverting to numeric variables, our data finally looks like this: 

![house_data](https://user-images.githubusercontent.com/45251340/185805982-ccb74ec1-5b6d-40f3-b740-aa1c0eab4f7d.JPG)


### GitHub Repository

Recall that the GitHub repository is the cloud-hosted directory containing all of your project files as well as their version history.

The requirements are the same as in [Phase 1](https://github.com/learn-co-curriculum/dsc-phase-1-project-v2-3#github-repository), except for the required sections in the `README.md`.

For this project, the `README.md` file should contain:

* Overview
* Business and Data Understanding
  * Explain your stakeholder audience here
* **Modeling**
* **Regression Results**
* Conclusion


