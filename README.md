# Credit-Card-Lead-Prediction-JobAThon

This is in accordance to the competetion held by Analytics Vidya. The dataset and entire Problem Statement is shared by them. Below is just the solution I proposed. No intend to copyright or infringe.

Credit Card Lead Prediction
Problem Statement – 
Happy Customer Bank is a mid-sized private bank that deals in all kinds of banking products, like Savings accounts, Current accounts, investment products, credit products, among other offerings.
The bank also cross-sells products to its existing customers and to do so they use different kinds of communication like tele-calling, e-mails, recommendations on net banking, mobile banking, etc. In this case, the Happy Customer Bank wants to cross sell its credit cards to its existing customers. The bank has identified a set of customers that are eligible for taking these credit cards.

Now, the bank is looking for your help in identifying customers that could show higher intent towards a recommended credit card, given:
•	Customer details (gender, age, region etc.)
•	Details of his/her relationship with the bank (Channel_Code, Vintage, 'Avg_Asset_Value, etc.)



Approach –
1)	Understanding the Dataset –
It all started with understanding the data which we are dealing with and using visualizations for capturing the intricacies as well as the holistic big picture.
The training dataset has 245725 datapoints and 11 features with some being of Object type and some of integer datatype. 
      2)  Exploratory Data Analysis and Feature Engineering – 
Univariate Analysis – Analyzed each feature independently by plotting Box Plots, Count Plots etc. 

Observations and approach for feature Engineering –

a) Feature - 'Avg_Asset_Value’ is highly skewed and has many outliers. Though after inspection it is clear that the outliers are genuine and shouldn’t be completely removed as there are high chances that that they might be present in the Test Dataset as well. Here, they are treated with IQR method and only those above 90 Percentile and below 10 percentiles are squashed. 
b) Box Cox transformation is applied on Feature - 'Avg_Asset_Value’ which is a type of Power Transformation and drastically reduced the high skewness.
c) For other features – Robust Scalar is used because of the primarily property of it being robust to outliers and other Standardization Techniques which are not completely suitable in this case. E.g. – Standard Scalar assumes that your data is normally distributed which was not the case in this Problem.

Bivariate Analysis – Here, analyzed features with respect to each other and by understanding the Correlation between them etc. 
Missing Values Imputation –
This is the important step and a determining factor as the number of missing values in Feature Credit Product is sufficiently large. 
For imputing the missing values here – datawig simple imputer technique which specifically also works well with missing values in categorical dataset with taking in consideration the other data features – including the target variable is used. It iterated through to find the best possible solution for the given problem.

Handling Categorical Variables –
a) Label Encoding is used for Encoded feature - Channel_Code.
b)  One Hot Encoding is used for all other Categorical features

Class Imbalance 
For class imbalance problems – that is the class having the minority class is made equal with the Majority class without intrinsically changing the characteristics of the data points with the use of Oversampling technique known as SMOTE. 
Below are all the models opted out for solving the problem at hand -

3) Application of Models –
•	Logistic Regression
-	Hyperparameter Tuning done with Precision and Recall Intersect – Threshold method 
It is observed in this case that the accuracy with Logistic Regression where Weights are set to “Balanced” performed much better that the Threshold Method.
•	Random Forest

-	Hyperparameter Tuning 

In the previous attempts various approaches were tried. Like, using the simpler Mode for imputation, Not specifically handling outliers with 25 -75 rule, under sampling instead of oversampling – SMOTE which is used for the final model, but the approach described in this document worked the best. XG Boost model with the hyperparameter tunning resulted in the decent score on the public Test Data.
•	XG Boost
-	Hyperparameter Tuning with the best hyperparameters are:  
-	
-	{'colsample_bytree': 0.6179708019324046, 'gamma': 8.721558861711202, 'max_depth': 18.0, 'min_child_weight': 7.0, 'reg_alpha': 41.0, 'reg_lambda': 0.4812978401617444}
