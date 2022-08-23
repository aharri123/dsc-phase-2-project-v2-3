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
* For our regression plots for sqft_living, we see a cone shape which indicates heteroscedasticity

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

**We can also see there are some categorical variables. We are unable to run a linear regression model if our data has categorical data, so we must convert to numerical values. After removing the variables and converting our categorical data to numeric types, our data finally looks like this:**

![house_data](https://user-images.githubusercontent.com/45251340/185805982-ccb74ec1-5b6d-40f3-b740-aa1c0eab4f7d.JPG)

### We then run our second model

![initial_model](https://user-images.githubusercontent.com/45251340/185806125-ee25180a-6670-4568-9bd4-bec13744f72e.JPG)

![second_model_results](https://user-images.githubusercontent.com/45251340/185806168-c242d1a9-333d-4f31-8b74-b5020bf77cf3.JPG)

**Let's check our assumptions again**
### Linearity 

![assumption1](https://user-images.githubusercontent.com/45251340/185806299-dd537b70-7f5e-44a9-9117-256708c91f33.JPG)

### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/185806311-cf818dad-2efc-42b8-b450-779553adb131.JPG)

### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/185806322-b9a48b10-f00b-4b5d-8841-2b0d9be08cc8.JPG)

### Let's check for multicollinearity

![heatmap_data](https://user-images.githubusercontent.com/45251340/185806376-8985fc73-e6a8-4a01-8fff-9207f614848e.JPG)


From testing our assumptions we can see:

* We have quite a few outliers, which disrupts the linear assumption
* The model residuals do not follow a full normal distribution
* Our residuals form a cone shape which indicates heteroscedasticity
* Multicollinearity (above .70) is not a major issue for our data

#### Let's see if we can adjust our model to fix any of the assumptions

## Third Model 
To see if we can improve our model, we'll log transform the price variable and see what happens. After log transforming and building our model these are our results and assumptions:

![third_model_results](https://user-images.githubusercontent.com/45251340/185806899-24711dfd-af4c-40e2-a7a5-3c83780fec7b.JPG)

### Linearity

![assumption1](https://user-images.githubusercontent.com/45251340/185806959-85337a01-2fef-4c61-ba7f-1345b45eb81c.JPG)

### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/185806963-b07b27d4-3cfd-4132-aef9-cf06619608d8.JPG)

### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/185806973-4ba2b581-098f-440c-b526-f5af0a868230.JPG)


After log transforming our price variable we can see that:

* Our linearity assumption has drastically improved
* The model residuals now follow a normal distribution
* Our residuals now form a more homoscedastic pattern
* Multicollinearity (above .70) is not a major issue for our data

### We make some other modifications

### Such as logtransforming sqft_living

After log transforming sqft_living:

![third_model_results](https://user-images.githubusercontent.com/45251340/185807855-547483ca-bab0-40e6-abc4-3fe6b8f444ca.JPG)

### Linearity

![assumption1](https://user-images.githubusercontent.com/45251340/185807943-d6e7b7a0-4f9f-46f3-9a59-fb12a85470ef.JPG)


### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/185807948-3f9bdf1c-3e02-40be-a45d-3c7bafa7c1a0.JPG)


### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/185807957-3fc4f02c-15b6-40d8-9e2f-49b1dd5a2f22.JPG)

From our data we can see that:
* All our independent variable p values are less than 0.05, indicating the relationships between those variables and the target variable price are statistically significant.
* Our R-squared score has improved slightly by .002
* Our assumption plots have not drastically changed

### We also experiment with dropping the waterfront and yr_built columns ###

**Removing yr_built variable**

![third_model_results](https://user-images.githubusercontent.com/45251340/186254504-56b4ecdc-8fd1-4af4-9641-477bad526c3c.JPG)

### Linearity

![assumption1](https://user-images.githubusercontent.com/45251340/186254922-a1fa6692-234b-42e9-804f-34dec3c55cfe.JPG)

### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/186254939-3db7a7c7-4fe4-4b2b-91ec-0d831166bea7.JPG)


### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/186254956-ee0c07ec-171a-44c0-8a2d-63604bd825ac.JPG)


**Our final intercept and coefficients are:** 

![image](https://user-images.githubusercontent.com/45251340/185808127-60af8ebf-e7f0-460a-9b33-7ddcb9b69a94.png)

## Interpreting the results

First off, we can see that our base house price is about $20.46. Then from there, we can look at the coefficients. Because we log transformed our target variable price, our variable coefficients (apart from sqft_living) can be represented as percentage changes of price for each unit increase. The sqft_living coefficient will be interpreted as a percentage change in price for each percentage change in sqft_living. By using math and applying it to each coefficient, we can get the following interpretations:

* For each additional bedroom added our price will go down by about 3.5%
* For each additional bathroom addded, our house price will go up by about 9.6%
* For each 1% increase in sqft_living, the price will increase by 39%
* For each additional floor added, the price will increase by about 8%
* If a house DOES have a waterfront view, we can expect the price to increase by about 72.3% as compared to if it does not
* For each increase in condition value ranking, the house price will increase by about 1.5%
* For each increase in grade value ranking, the house price will increase by about 26.2%
* For each year newer the house is, the price will decrease by about .63%

## Conclusion
Our goal for this project was to use previous King County housing data from 2014-2015 to identify which features would best increase the value of a house in order for it to be sold (Keeping in mind the person selling the house would need to be able to renovate these features). After identifying these features, we will then present our data to the Real Estate agency, so that they may communicate to their customers which features would be most advantageous to renovate.

Since the customer selling the house needs to be able to renovate the features chosen, we can rule out some of the features. The yr_built and waterfront variables can be eliminated, since one cannot change the year that the house was built, and a waterfront cannot be simply built. A similar situation with the floor variable occurs, where it would not be worthwhile to add an entire new floor level for the price to only go up by about 8%. Without adding or changing anything else, an increase in bedrooms would actually bring down the price by about 3.5%. Finally, there's the issue of the condition variable. Increasing the condition ranking of the house will only increase the price by about 1.5%. Therefore the variables that should be picked are **number of bathrooms**, **living square footage**, and **grade of the house**.

Increasing the number of bathrooms , while also increasing the total square footage would be beneficial, since each increase brings its own price percentage increase. Increasing the grade rating of a house goes hand in hand with the other two features, since the grade rating is based on construction quality of renovations made to the house. A higher rating is associated with more square footage, as well as higher quality bathroom fixtures. Other improvements to the house can be made such as increasing the quality of the woodwork and adding more luxurious materials such as marble.

 
