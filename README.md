# Lead Scoring Case Study

## PROBLEM STATEMENT

An education company named X Education sells online courses to industry professionals. On any given day, many professionals 
who are interested in the courses land on their website and browse for courses.

The company markets its courses on several websites and search engines like Google. Once these people land on the website, 
they might browse the courses or fill up a form for the course or watch some videos. When these people fill up a form 
providing their email address or phone number, they are classified to be a lead. Moreover, the company also gets leads 
through past referrals. Once these leads are acquired, employees from the sales team start making calls, writing emails, etc.
Through this process, some of the leads get converted while most do not. The typical lead conversion rate at X education is 
around 30%.

Now, although X Education gets a lot of leads, its lead conversion rate is very poor.



## BUSINESS GOAL

- X Education requires a model to be built for selecting the most promising leads.
- The business wants you to create a model in which you give each lead a lead score so that leads with higher lead scores 
have a better likelihood of converting, while leads with lower lead scores have a lesser chance of converting. The goal lead 
conversion rate was mentioned as being something in the neighborhood of 80% by the CEO in particular.



## STEPS / STRATEGY

### Step 1: Reading and Understanding data
Imported the dataset and check the basics of the dataset to get an understanding of the 
data initially. [shape, describe, info]

### Step 2: Data Cleaning and Preparation
  - Checked for NULL values
  - Converted the ‘Select’ values in certain variables to NaN
  - Treated all the NULL values
      * If the NULL values in the column exceeded 40%, dropped the column
      * imputing – Mean and Median [Numerical data], Mode [Categorical data]
      * Dropped the rows if they were insignificant
  - Combined some categories in certain variables to a single entity as they did not show 
    much difference alone.
  - Removed variables where only 1 value dominated 
  - Visualized the Numerical and Categorical data and made observations.

### Step 3: Preparing the data for Modelling
Created dummy variables for the categorical data.

### Step 4: Train-Test Split
Then it was time to divide the dataset to build the model, took a 70%-30% ratio for model 
building. 
  - Performed scaling of the 70% train dataset. Used StandardScaler() on the data which 
     has mean as 0 and standard deviation as 1.
  - Checked for correlation using a heatmap.

### Step 5: Model Building
Used the RFE (Recursive Feature Elimination) to reduce the pool of leads to 15 features. 
Then, went ahead with manual model selection (statsmodel) and dropped features with high 
p-value ( > 0.005) and high VIF (>= 5) until they were neutralized.
  - Checked for correlation with a heatmap.

### Step 6: Model Evaluation
Now, prediction on the train set. Initially used 0.5 as the threshold and obtained the overall 
accuracy, confusion matrix, sensitivity, and specificity.
         Accuracy – 93.32 %, Sensitivity – 88.67 %, Specificity – 96.23 %
         Precision – 93.65 %, Recall – 93.65 %
  - Checked for the area under the ROC curve as a metric to evaluate the model – 0.98
  - Found the optimal threshold - to be 0.3
    Predicted the conversion this time with 0.3 as the threshold and calculated the overall 
    accuracy, confusion matrix, sensitivity, and specificity [which turned out to be better than 
    0.5 as the threshold].
        Accuracy – 92.64 %, Sensitivity – 91.94 %, Specificity – 93.08%
        Precision – 89.28 %, Recall – 91.94 %

### Step 7: Prediction on the Test set
  - Scaled the test dataset using the StandardScaler() as in the train set [expect this time 
    only transform was done and not fit]

Finally, prediction on the test set using 0.3 as the threshold cut-off. Calculated the overall 
accuracy, confusion matrix, sensitivity, and specificity. Which was very close to the 
percentages on the training dataset. Achieving more than 90% sensitivity.
        Accuracy – 91.73 %, Sensitivity – 90.29 %, Specificity – 92.61 %
        Precision – 87.46 %, Recall – 90.29 %


## MODEL BUILDING

- Splitting the data into training and testing sets 
- Currently, we have around 50 variables in the dataset the data cleaning and preparation process, we cannot possibly use all 
  these variables for model building. We have to choose the most appropriate variables/features that add value to our 
  business goal so as to have a high accuracy and sensitivity and specificity. So we will be using both RFE (to narrow down to a 
  small pool from a large number of features) and stats model for further feature selection.
- Using RFE with 15 variables as output.
- Using stats model to build a logistic regression model.
- Eliminating variables from a model whose p-value is higher than 0.05 and VIF value is higher than 5.
- Predictions on test data 
- Obtaining overall accuracy


## CONCLUSION
- We can see that when the leads are marked with tags such as 'Closed by Horizzon', 'Lost to EINS’, and 'Will revert after 
reading the email' are likely to get converted to paid customers and are considered as hot/potential leads. Likewise, 
leads from sources like Welingak Website or the last activity is an SMS Sent are likely to be converted to paid customers. 
The sales team must monitor the leads from these sources and occupations and be quick with their first approach or 
send out brochures to lock the client as soon as possible. Also, if a user is spending more time on the website browsing 
for courses, that user is likely a potential lead, so the sales team has to keep an eye out for users spending a high total 
time on their website as well. These leads would be the potential leads that will be converted if given the time and 
effort from the sales team. This will increase the conversion from 30% up to or more than 80%.

- The sales team can come to a conclusion internally that if the lead score is greater than 90 then they can invest more 
time in a day to these customers for a better conversion rate and gradually decrease the time invested in each customer 
as the lead score decreases
