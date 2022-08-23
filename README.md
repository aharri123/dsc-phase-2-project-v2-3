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

#### Linearity
We'll plot the relationship between price and sqft_living to see if it follows a linear pattern

![assumption1](https://user-images.githubusercontent.com/45251340/185805249-b6c491af-2f34-4229-9095-064f0f7a876b.JPG)

#### Normality
We'll plot the residuals against a standard normal distribution 

![assumption2](https://user-images.githubusercontent.com/45251340/185805283-6e947fcf-d804-4a63-b426-ac300026df4a.JPG)

#### Homoscedasticity

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

### Let's check our assumptions again ###
#### Linearity 

![assumption1](https://user-images.githubusercontent.com/45251340/185806299-dd537b70-7f5e-44a9-9117-256708c91f33.JPG)

#### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/185806311-cf818dad-2efc-42b8-b450-779553adb131.JPG)

#### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/185806322-b9a48b10-f00b-4b5d-8841-2b0d9be08cc8.JPG)

#### Let's check for multicollinearity

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

#### Linearity

![assumption1](https://user-images.githubusercontent.com/45251340/185806959-85337a01-2fef-4c61-ba7f-1345b45eb81c.JPG)

#### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/185806963-b07b27d4-3cfd-4132-aef9-cf06619608d8.JPG)

#### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/185806973-4ba2b581-098f-440c-b526-f5af0a868230.JPG)


After log transforming our price variable we can see that:

* Our linearity assumption has drastically improved
* The model residuals now follow a more normal distribution
* Our residuals now form a more homoscedastic pattern
* Multicollinearity (above .70) is not a major issue for our data

## We make some other modifications ##

### Such as logtransforming sqft_living

After log transforming sqft_living:

![third_model_results](https://user-images.githubusercontent.com/45251340/185807855-547483ca-bab0-40e6-abc4-3fe6b8f444ca.JPG)

#### Linearity

![removing yr_built assumption1](https://user-images.githubusercontent.com/45251340/186255558-abf7291e-11fc-401c-bc84-6ee71162c83f.JPG)


#### Normality

![removing yr_built assumption2](https://user-images.githubusercontent.com/45251340/186255574-1e21d16e-2519-4919-801f-d52991827387.JPG)


#### Homoscedasticity

![removing yr_built assumption3](https://user-images.githubusercontent.com/45251340/186255601-ab7b04fc-d908-4ad7-899f-3d2056c9d8a1.JPG)

From our data we can see that:
* All our independent variable p values are less than 0.05, indicating the relationships between those variables and the target variable price are statistically significant.
* Our R-squared score has improved slightly by .002
* Our assumption plots have worsened

## We also experiment with dropping the waterfront and yr_built columns ###

### Removing yr_built variable ###

![third_model_results](https://user-images.githubusercontent.com/45251340/186254504-56b4ecdc-8fd1-4af4-9641-477bad526c3c.JPG)

#### Linearity

![assumption1](https://user-images.githubusercontent.com/45251340/186254922-a1fa6692-234b-42e9-804f-34dec3c55cfe.JPG)

#### Normality

![assumption2](https://user-images.githubusercontent.com/45251340/186254939-3db7a7c7-4fe4-4b2b-91ec-0d831166bea7.JPG)


#### Homoscedasticity

![assumption3](https://user-images.githubusercontent.com/45251340/186254956-ee0c07ec-171a-44c0-8a2d-63604bd825ac.JPG)

### Removing yr_built without log transforming sqft_living

![non_yr_built results](https://user-images.githubusercontent.com/45251340/186281042-1c92ddb0-11c5-47ef-af83-c386bf2515c4.JPG)

#### Linearity ####

![non_yr_built 1](https://user-images.githubusercontent.com/45251340/186281130-4c91d2f4-b02f-439b-9c98-72af3b54dc5a.JPG)

#### Normality ####

![non_yr_built 2](https://user-images.githubusercontent.com/45251340/186281137-1c1afa92-685b-48d0-a23c-9e00603a5aae.JPG)

#### Homoscedasticity ####

![non_yr_built 3](https://user-images.githubusercontent.com/45251340/186281151-2027627d-bb93-4be4-89ea-06e62396a971.JPG)

### Removing waterfront variable ###

![waterfront results](https://user-images.githubusercontent.com/45251340/186256334-9f9a7d67-9cc1-46c6-a20f-7156dae93684.JPG)

#### Linearity

![waterfont 1](https://user-images.githubusercontent.com/45251340/186256555-3e9767d3-225d-46a7-a5b6-1073591d976b.JPG)


#### Normality

![waterfont 2](https://user-images.githubusercontent.com/45251340/186256567-40a55e9e-62f7-4c4e-86f8-1d7e116e9f1e.JPG)


#### Homoscedasticity

![waterfont 3](https://user-images.githubusercontent.com/45251340/186256585-728bb5bc-5b80-4c33-8689-e07b3a101fe6.JPG)


### Removing waterfront variable without log transforming sqft_living ###

![non_waterfront results](https://user-images.githubusercontent.com/45251340/186281567-e3949d8c-819d-4c12-80fd-a7df92d64edc.JPG)

#### Linearity ####

![non_waterfront 1](https://user-images.githubusercontent.com/45251340/186281584-097ded9a-6304-49d8-b577-ba12e6d8535e.JPG)

#### Normality ####

![non_waterfront 2](https://user-images.githubusercontent.com/45251340/186281596-22f6992c-9847-4d80-a6d1-d6e76e501ad2.JPG)

#### Homoscedasticity ####

![non_waterfront 3](https://user-images.githubusercontent.com/45251340/186281609-d0722ca6-a5d0-43ce-9c73-d92867d057f8.JPG)


### Removing both ###

![both results](https://user-images.githubusercontent.com/45251340/186257016-5c0bfc09-7cd3-46d8-968d-baa8c56a2496.JPG)

#### Linearity

![both 1](https://user-images.githubusercontent.com/45251340/186257291-676ced9a-97e0-426c-81aa-7ab9d53a8475.JPG)

#### Normality

![both 2](https://user-images.githubusercontent.com/45251340/186257311-a66008e7-37b3-4ce7-8725-67753ba43e76.JPG)

#### Homoscedasticity

![both 3](https://user-images.githubusercontent.com/45251340/186257331-129c9b32-8d6e-4034-9300-a2cd3ed91901.JPG)

### Removing both without log transforming sqft_living ###

![non both results](https://user-images.githubusercontent.com/45251340/186282334-9772694f-d4cf-4705-9005-bdacf98f1942.JPG)

#### Linearity

![non both 1](https://user-images.githubusercontent.com/45251340/186282346-c1d04215-8b88-4695-b058-3a3e5429a146.JPG)

#### Normality

![non both 2](https://user-images.githubusercontent.com/45251340/186282351-a9728a5a-7105-4b6b-9c22-e3bcd3440a03.JPG)

#### Homoscedasticity

![non both 3](https://user-images.githubusercontent.com/45251340/186282364-1f21c79f-4ab2-4e27-8027-cf97e1bcff9a.JPG)


## Final Verdict
It seems the most advantageous thing to do is to log transform only price and remove the waterfront variable. The assumptions are somewhat improved when we remove the yr_built variable, but the R-squared score decreases by .065 when sqft_living is still log transformed, and .058 when not. However when we remove the waterfront variable, it only decreases by .006 (regardless of log transformation of sqft_living). Log transforming sqft_living makes it harder to conceptualize in terms of coefficients, so we will keep it untransformed.  Therefore the final changes we make are log transforming price and removing the waterfront variable.

## Interpreting the results

First off, we can see that our base house price is about $22.64. Then from there, we can look at the coefficients. Because we log transformed our target variable price, our variable coefficients (apart from sqft_living) can be represented as percentage changes of price for each unit increase. The sqft_living coefficient will be interpreted as a percentage change in price for each percentage change in sqft_living. By using math and applying it to each coefficient, we can get the following interpretations:

* For each additional bedroom added our price will go down by about 2.9%
* For each additional bathroom addded, our house price will go up by about 9.6%
* For each 1% increase in sqft_living, the price will increase by .02%
* For each additional floor added, the price will increase by about 8.2%
* For each increase in condition value ranking , the house price will increase by about 1.8%
* For each increase in grade value ranking, the house price will increase by about 25.5%
* For each year newer the house is, the price will decrease by about .60%

## Conclusion
Our goal for this project was to use previous King County housing data from 2014-2015 to identify which features would best increase the value of a house in order for it to be sold (Keeping in mind the person selling the house would need to be able to renovate these features). After identifying these features, we will then present our data to the Real Estate agency, so that they may communicate to their customers which features would be most advantageous to renovate.

Since the customer selling the house needs to be able to renovate the features chosen, we can rule out some of the features. The yr_built and waterfront variables can be eliminated, since one cannot change the year that the house was built, and a waterfront cannot be simply built. A similar situation with the floor variable occurs, where it would not be worthwhile to add an entire new floor level for the price to only go up by about 8%. Without adding or changing anything else, an increase in bedrooms would actually bring down the price by about 3.5%. Finally, there's the issue of the condition variable. Increasing the condition ranking of the house will only increase the price by about 1.5%. Therefore the variables that should be picked are **number of bathrooms**, **living square footage**, and **grade of the house**.

Increasing the number of bathrooms , while also increasing the total square footage would be beneficial, since each increase brings its own price percentage increase. Increasing the grade rating of a house goes hand in hand with the other two features, since the grade rating is based on construction quality of renovations made to the house. A higher rating is associated with more square footage, as well as higher quality bathroom fixtures. Other improvements to the house can be made such as increasing the quality of the woodwork and adding more luxurious materials such as marble.

 
