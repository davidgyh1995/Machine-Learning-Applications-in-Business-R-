# Machine-Learning-Applications-in-Business-R-

The goal of this project is to dig out the relationship between house complements and their sale prices in Ames, Lowa. The data set contains 2930 observations and a large number of explanatory variables in order to be able to predict the future housing prices in the nearby areas. This project not only focuses on predicting the future house prices but also to determine the variables that are causing increases in the final price while we do not really care much about them.

## Data

• Sources 

  We found the data sources on Kaggle. Here is the website url https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data?select=data_description.txt. 
The Ames Housing dataset was first compiled by Dean De Cock for educational use which then was used for the Kaggle competitions. 

• Cleaning 

  There is a huge amount of data in our dataset: 81 different columns(variables), and 1460 lines (records) of data, therefore we need to do data cleaning (pre-processing) before we do any model predictions. First, we eliminate all non-numerical variables (including id, which is just an increasing number to indicate the order or records), which may not contribute to the final result, after this step, we have 36 variables left. Second, we check how many numeric variables have NA value. There are only two variables that have NA values (LotFrontage and GarageYrBlt) , after comparing the results, we decided to use the median value to replace all NA values. After that, we checked the correlation coefficient between all the remaining variables. After that, we chose the variables which have a correlation coefficient with our prediction variable SalePrice that is greater than 0.5. After this step, we have 10 variables left. Now we finished all data cleaning, we separated it into a train set and validation set by ratio 8 to 2. Now we are ready to do modelling!

• Challenges 

  There are a lot of variables that are highly correlated with each other which may affect our final predictions later on. We would like to adjust the correlated relations in our model when we do feature selection. There are some outliers in our dataset, we also need to decide on which methods could be excluded. 

## Methods

### Linear regression
  In linear regression, we first built the base model lm1 with all the variables and then used residuals to determine if there were any outliers in our training data. We have eliminated one outlier and retrained our data under model lm_no_outlier. Before we continued with our testing data set, we retrained the model with fewer variables that were determined by p values and redone the outlier steps under model lm2 and lm2_no_outlier. By comparing four models’ performance in the validation set, we have chosen lm2_no_outlier to perform our test. In addition to the outlier methods, we also performed the best subset method in order to figure out the best combination of variables among reduced ones. The final Root Mean Squared Error before denormalization is 0.184 which is quite impressive. 

### Random Forest 
  For the random forest method, we similarly built the base model rf for the starting point. We plot the model in order to find the number of trees with the lowest mean squared error. After determining the optimal number of trees, we have tuned our tree model with hyper_grid. The optimal parameters that we were trying to adjust are mtry, node_size and sample_size with a predetermined number of trees. The final accuracy that we performed on the validation set is 0.193. 

### Elastic Net 
  For the Elastic Net method, first we separated our dataset into x(independent variable) and y(dependent variable). Then we use the trainset to train the model, by using cross validation for 10 times, for selecting the best model with the best alpha and lambda, which is 0.1 and 4248. Based on the best parameter we have here, we have our final model. Then we could use our final model to make predictions on the test data. The final Root Mean Squared Error before denormalization is 0.191. 

### Boosting
  For the boosting method, we have taken similar steps with the random forest including finding the optimal number of trees, tuning the parameters, and testing on our validation set. We have first used 1000 trees for our base model, however, we did not see any converge trend appearing as we grew the number of trees. We then increased the maximum number of trees to 10,000 and then decided to do 4000 trees for our final model. For the tuning process, we have set up the grid search in order to find out the best combinations of parameters. The final Root Mean Squared Error before denormalization is 0.205. 

## Results and Conclusion

In this project, we used Root Mean Squared Error to determine a model's performance. RMSE gives us a quantified number on how far apart the predicted values are from the observed values in our dataset. Since we have normalized our independent variables and took log transformation of our dependent variable beforehand, we have generated outcomes with relatively low ranges. The Root Mean Squared Error ranged from 0.184 to 0.205 which linear regression did the best job out of our four models. 

As discussed in previous sections, we decided to choose the linear regression as the final implementation of our Ame housing price prediction model. When we looked at the results, we intuitively thought tree models would do the best job. However, linear regression with eliminating extra outliers and doing much careful feature selections performed better on our validation set. 

We did see a linear trend on the known data set and figured out that overall quality of the house is the main concern that buyers would consider. In addition to the quality itself, issues related to the garage are also vital to the house prices in general. No matter is the garage size or the number of cars that garage can park, they arise the final sale prices in the past years. Back to the reason why we would like to invest in this data set, it helps not only the sales to do house listings, but also to make sure that if customers do not care about the garage issue, sales could offer them relatively low prices quickly. 

![WeChat Image_20220414012358](https://user-images.githubusercontent.com/43740678/163319325-5422e0f5-5cb4-4128-99e9-2e21f380154e.png)

![WeChat Image_20220414012405](https://user-images.githubusercontent.com/43740678/163319336-8934e0cb-b064-49e9-88e8-037ba0746d47.png)

![WeChat Image_20220414012411](https://user-images.githubusercontent.com/43740678/163319343-ca558391-6985-4ef6-beb0-1c7107fb8c92.png)
