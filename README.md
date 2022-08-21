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

Our R-squared value is somewhat low at 49%, so let's check some assumptions

#### Linearity
We'll plot the relationship between price and sqft_living to see if it follows a linear pattern

![assumption1](https://user-images.githubusercontent.com/45251340/185805249-b6c491af-2f34-4229-9095-064f0f7a876b.JPG)

#### Normality
We'll plot the residuals against a standard normal distribution 

![assumption2](https://user-images.githubusercontent.com/45251340/185805283-6e947fcf-d804-4a63-b426-ac300026df4a.JPG)

#### Homoscedasticity

We'll see if the regression plots resemble a cone shape

![assumption3](https://user-images.githubusercontent.com/45251340/185805350-8c9a9777-8bdf-4663-ba7c-9f46b85bde97.JPG)

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


