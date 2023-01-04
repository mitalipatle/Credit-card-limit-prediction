# Credit-card-limit-prediction

## Introduction:
Credit card plays an important part of everyone's life as it is not only the safer option than carrying cash but also protects an individual from fraud or scams, where
the maximum amount of money or credit that a financial institution can lend to a credit card customer or client at once is known as the credit limit. These banks consider a number of crucial aspects when determining a client's credit limit, including income, payment history, and debts. As a result, they grant larger credit limits to lower-risk borrowers and vice versa. It is necessary to develop a system that can predict the client's credit limit based on a variety of features because the credit limit is susceptible to vary depending on the client's behavior and expenditure which could make this process challenging and time consuming.

## Scope:
The project aims to solve the regression problem by applying machine learning models to predict credit card limit.
Below is the breif overview of the project workflow:
##### 1). Loading the essential libraries and importing and reading the dataset.
##### 2). Cleaning the dataset to remove irrelevant and missing information using data cleaning and manipulation techniques.
##### 3). Visualising the dataset using graphs, charts and figures to gain better understaning of the data.
##### 4). Detecting and removing oultiers using outliers removal technique.
##### 5). Feature selection using backward elimination approach and performing transformation on response variable(credit limit).
##### 6). Applying multiple machine learning algorithms to train the models and evaluate their performance using different metrics and visualisation.

## Data Description:
The data file Credit_Card_Dataset.csv is a data set of credit card customers from a large bank. The data dictionary is given below.
| Variable | Description |
| --- | --- |
| `CLIENTNUM` | Client ID (not for analysing!) |
| `Attrition_Flag` | Whether or not the customer has left the bank in the last 12 months(**yes or no**) |
| `Customer_Age` | Age of customer in years |
| `Gender` | Gender of customer (**male or female**) |
| `Dependent_count` | Number of dependents (**children**) of the customer |
| `Education_Level` | Education level attained by the customer(**primary, secondary or third level**)|
| `Marital_Status` | **divorced, married/living with partner or single**  |
| `Income_Category` | Yearly income in Euro (to nearest 1k, grouped **<30k, 31-50k,51-70k,71-110k or 111k+**)|
| `Card_Category` | Type of credit card (**Blue or Gold**) |
| `Months_on_book` | Number of months as credit card customer |
| `Credit_Limit` | Credit card limit |
| `Avg_Utilization_Ratio` | A measure of how often the credit card is used |
| `Pay_on_time` | Whether or not the monthly balance on the credit card paid off( **yes or no**) |
|`Random_numbers`| Random Numbers |

## Importing Libraries and Data Cleaning:
**Importing** some essential libraries, such as data manipulation libraries that offer a wide variety of capabilities to help with a range of actions on data, such as organizing or performing mathematical operations.Similarly, data visualization libraries assist in gaining important insight into the data through various graphical representations by revealing hidden patterns and trends and data modelling librabries which helps in building different statistical or machine learning models.

<img src="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/Libraries.png" width=60% height=60%>

Importing the dataset to the notebook using the github link:

<img src="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/Importing%20dataset.png" >


**Cleaning the dataset:**

1). Upon exploring the dataset, it was found that the null values present in the dataset has string datatype and thus need to be converted to null values.

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/converting%20str%20to%20null.png">

2). 217 rows found to have missing values and thus needs to be removed using `dropna()` function.

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/missing%20value%20rows.png" height=200>

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/dropping%20missing%20value.png">

3). Columns like CLIENTNUM that is unique for each customer , Random_numbers and Attrition_Flag does not add any value to credit limit analysis and thus these irrelevant columns can be dropped. 

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/dropping%20irrelevant%20columns.png">

4).One duplicate value was found and dropped from the dataframe and datatypes of the features were found correct which later will need label encoding due to the presence of objects during the model fitting. 

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/duplicates.png">

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/no.%20of%20duplicates.png">

<img src = "https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/data%20type%20check.png">

## Exploratory Data Analysis:

#### Univariate Analysis:

1). From the bar chart of the categorical variables it can be seen that almost all the variables
are found to be deeply imabalanced such as Marital Status, Card Category and payment on time, excpet for the Gender variable as there is slight difference between the number of male and female customers.

<img src="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/Bar_univariate.png">

2). The Pie chart shows the percentage of customers lying in different income categories where 39% customers earn less than 30k and only 8% customers earn more than 111k+ and the histogram displays the distribution of customer's age according to which the average age of a customer is found to be 46 years approximately.

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/pie%20chart%20income.png">


<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/customer%20age%20histogram.png">

3). The histogram below shows the distribution of credit limit(response/dependent variable) that is positively skewed indicating higher number of customers have lower income and tells the direction of outiers towards the left.

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/credit%20limit%20histogram.png">

However,there can be seen a spike on the very right of the distribution as well.On further investigation about customers earning more than 30,000 income it was found that hike is mostly for customers with higher income category, males, a significantly large number of gold card holder out of total gold card holders.

<img src ="https://github.com/mitalipatle/Credit-card-limit-prediction/blob/main/Images/hike%20on%20right.png">

#### Multivariate Analysis:

1).The correlation matrix for numerical variables shows that a postive high correlation exists between Customer Age and Months_on_book(Number of months as credit card customer)with a value of "0.79" ,i.e with the increase in age of customer their number of months as credit card customer increases and vice versa. (Multicollinearity is present between 2 independent variable). Thus only one out of the two variable should be used in the model.

Moreover, a negative moderate correlation exists between Avg_utilization ratio and Credit Limit of "-0.48" which shows that with the increase in avg_utilization ratio (measure of how often the credit card is used) the Credit Limit for that customer decreases moderatly and vice versa.(Inclusion of avg_utilization ratio variable will dpend on it's significance added to the model)

<img src= "">

2). Categorical variable against Credit Limit(Response variable).

(a). **Gender and Credit Limit**:
 
The boxplot shows that the males customers have much higher median credi limit(8791.0) when compared to female customer's median credit limit(2819.0).

<img src= "">

(b). **Marital Status and Credit Limit**:

The median credit limit difference between customers of different marital status is not huge with the median value of single(4511.0),married(4138.5) and divorced(4701.0), inspite of  imbalanced number of customers belonging to different marital status.

<img src= "">

(c). **Income Category and Credit Limit**:
The box plot for the income category against credit limit displays a directly proportional relationship between the variables because with the increase in Income, Credit Limit increases as well.

<img src= "">

d). **Card Category and Credit Limit**

