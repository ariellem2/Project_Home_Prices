# Project 2: Predict Home Prices in Ames, Iowa


Arielle Miro 
DSI-7

### EXECUTIVE SUMMARY

---

Zillow will often proivde "Estimated home prices" or "Zestimates" on their platform in order to inform users about current real estate market rates. Eventhough certain homes are not yet explicitly for sale, this feature allows users to browse properties and their current market values. More accurate depictions of home values translate into more confidence in Zillow's product and will therefore grow Zillow's user base. This in turn translates into more advertising revenue and a compettive edge over similar sites such as Redfin and Trulia. 

### Introduction

**Objective**: Our goal is to grow Zillow’s user base & advertising revenue by increasing confidence in our product.
- We will build an accurate model that best predicts home prices in Ames, Iowa.
- More accurate depictions of home prices means more confidence in the Zillow platform.
 
---

### Overview
    
**Data**
- Source: Ames Assessor's office http://jse.amstat.org/v19n3/decock/DataDocumentation.txt 
- Information: Provides assessed values, home features, and feature quality for individual residential properties sold from 2006 to 2010. 
- Size: 2930 observations, 82 variables

**Tools**
- Python (Pandas, Matplotlib, Seaborn, Scikit-Learn)

### Methodology 

**Regression Models **
Several regression models were built to predict home sale price. 

- Cleaning the data was crucial in creating a smooth model. 
    - Ordinal columns: computed their rankings so the ordinal values could be used in the modeling process. Many "quality" fields       are crucial in determining the overall quality of a home, therefore the rankings are important to use for the model. 
    - Nominal columns: used feature engineering to account for all possible home characteristics that could affect sale price. 
    - Numerical columns: this included both discrete and continuous variables.
- Scaling & Tuning:
    - Scaling was imperative in creating the model. It creates an even playing field for each home characteristic (feature) to           ensure that we are comparing apples to apples. For example, number of bedrooms and square feet are features on very               different scales. 
    - Using alpha, a tuning parameter, we could adjust the scores of the train and test data in order to minimize the difference         between those scores. 
- Regularization:
    - After scaling the data, the 2 methods of Ridge and Lasso helped regularize the models. 
    - Regularization helped solve for overfitting in the model and provided more control, by eliminating or reducing the features       with a less predicitve capabilities for our specific target, in this case sale price. 

**Obstacles**
- Null Values: 
    - The tough question of how to address null values arose several times during the process. Should we delete them? Compute the       mean instead? 
    - The intuative decision was made to replace null values in numerical columns with 0. 
    - For ordinal columns, NA's were in fact the lowest possible rank in the list. A house with no fireplace would obviously have       a 0 rank for fireplace quality. These were replaced accordingly, for example "No Fireplace". 
    - For nominal columns, NA's were addressed by creating dummy columns out of the categorical options within each column. The         new 0/1 boolean columns automatically dropped the NA's.  
- Outliers:
    - Per the data dictionary, there were 5 outliers in the data with a square footage of over 4,000 sq ft. Rather than removing         the outliers, a dummy column for these large homes was created and included in the model in order to account for future           outlier properties (specifically in the test data).  

### Conclusion & Recommendations

Based on research and EDA, the below findings and recommendations emerged from the model. 

**Findings**
- New homes tend to be more expensive. Due to newer materials and conditions, this is fairly intuative. 
- Homes with larger basements are more expensive. More square footage increases the value of the house. 
- Homes with a larger 1st floor square footage are more expensive. More square footage increases the value of the house. 
- As the overall quality ranking of the house increases by one unit (on a scale of 1 to 10, with 1 being the lowest and 10 being the highest), the sale price of the home increases by $12,818. 
    
**Final Model**
The Lasso regression was chosen as the final model to predict home prices in Ames. 
- The train and test scores for this model were closest, which ensures minimal overfitness. This will allow for accurate application of the model to future (unseen) housing data. 
- With the alpha tuning variable, we are able to adjust the scores and maintain the weight. 
- Because it is a regularized model, we can ensure that our coefficients will be scaled and comprarable. 
    
**Recommendations**
- Test the Lasso Model on recent data for 2010-2018. 
- Refine the model accordingly, and assess whether it works on future data. 
- Roll out the model on the website to test for 30 days.

