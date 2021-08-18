# Holmusk-Project

The goal of this project was to find the variables driving the cost of hospital bills. The data analyzed in this project included 3 datasets with various data about patient demographics, medical histories, symptoms, and date of admission and discharge. These datasets were merged and irrelevant data that did not have an effect on bill amounts, such as bill id, were dropped. 

The provenance of the data was not provided. Values that differed slightly in the dataframe but were supposed to signify the same information were updated: for example, in the race column "chinese" was updated to "Chinese". There were 13,600 individual bills and 3000 individual patients indicating there are patients that have been admitted multiple times. I calculated age of the patient and length of stay as these are variables that can often influence the cost of care. I also looked at the day of the week and the month of the year that patients were admitted as seasonality can influence cost of care for certain illnesses. There were missing values for medical history 2 and medical history 5, which I replaced with 0 as I did not want to drop this data and there were few enough missing values that I did not think it would affect the data analysis. 

### Distribution of the Bill Amounts 

![distribution of bill amount](https://user-images.githubusercontent.com/66225041/129909655-ecd87703-9224-453f-b845-56500259ebce.png)

The data for bill amounts is very skewed. I will need to use a model that is resilient against skewness or transform this data using a log transformation, or other type of transformation. I also want to see if there are any outliers with the data since the range is so large. 

### Bill Amount Outliers 

![bill boxplot](https://user-images.githubusercontent.com/66225041/129910285-2e363795-3673-430f-b6bd-a4bc72fee6a5.png)

There are many outliers for bill amount. However, since there are such a large numbers of outliers, I plan to create a model incorporating the outliers and compare it against a model without the outliers. This number of outliers means that this may be a pattern that should be included as part of the model, as opposed to cases where a few outliers skew the rest of the data. 

### Heatmap of Medical History and Amount of Bill 

![medical_history_corr](https://user-images.githubusercontent.com/66225041/129902458-3468a320-0a8f-48f2-80a6-6939b3f304df.png)

There does not seem to be much correlation between the various medical histories and the amount of the hospital bill. The is a slight correlation between medical history 6 and medical history 1, but nothing is jumping out as an important driver of cost. 

### Heatmap of Preop Medication Administered and Amount of Bill

![preop medication corr](https://user-images.githubusercontent.com/66225041/129903158-5d89522e-b18f-4f57-b512-f347703de91f.png)

There is very little correlation between the preop medication administered and the amount of the bill, so these medications are possibly similar in cost. 

### Heatmap of Symptoms and Amount of Bill 

![symptom corr](https://user-images.githubusercontent.com/66225041/129904200-a0f3910d-8e7a-4de7-bb5e-c678cd6a83ab.png)

There is some correlation between several of the symptoms and the amount of the bill, particularly symptom 5. This symptom maybe be one that requires treatment that is more costly than the treatment for the other symptoms. 

### Medical History by Bill Amount

![Medical History by bill amount](https://user-images.githubusercontent.com/66225041/129910973-b7be483a-e6c4-4bfa-b263-882549f43b93.png)

I created individual boxplots of the medical histories compared to the amount of the bill. This is a different visualization of the information shown in the heatmap correlation, but I think it further illustrates that a slight difference can be seen for medical history 1, but otherwise there is not much of an onservable difference. 

### Preop Medication by Bill Amount 

![preop medications by amount](https://user-images.githubusercontent.com/66225041/129912990-d0504dbf-4d16-426e-bdaf-5755d27d6f7a.png)

Once again, individual visualizations of each preop medication does not reveal any correlation with the amounts of the bills. 

### Resident Status and Amount of Bill

![resident status by amount ](https://user-images.githubusercontent.com/66225041/129913272-228a380a-7676-467f-8dcb-44f0706b83a0.png)

It appears that resident status has a noticeable effect on the amount of the bills. Foreigners receive much higher bills than permanent residents and Singapore citizens. This makes sense as citizens probably have more reliable access to health insurance. This is assuming that the bill amounts charged represent the amount that the patient was asked to pay after insurance payments have been applied. 

### Race and Amount of Bill

![race and bill amount ](https://user-images.githubusercontent.com/66225041/129915635-bedd7564-0a7f-492a-95b9-4fa7b2b72033.png)

There seems to be a correlation between race and the amount of the bill. This may be tied to people of various races be more or less likely to be permanent residents of Singapore or foreigners. It appears that Malay people have the highest bills while Chinese people have the lowest bills. It also appears that women have lower bills in general. I'm not sure what the explanation for this could be. Women are often charged more for health insurance as they are deemed "higher risk" patients. Perhaps women are more likely to have health insurance and therefore receive lower bills. 

### Age by Amount of Bill 

![age and weight by amount](https://user-images.githubusercontent.com/66225041/129916371-f8284ce6-61b6-49d6-acf1-cb5695790428.png)

### Weight by Amount of Bill 

![weight by bill](https://user-images.githubusercontent.com/66225041/129923021-d3d564b6-3402-440e-86f8-a7706703267b.png)

Weight and age seem to be slightly associated with a higher bill amount, particularly age. It seems that there are low bills for people of all ages and then very high bills are mostly found among middle-age or older people, which makes sense intuitively. There may also be a slight relationship between weight and bill amount where people who weigh more are more likely to have a higher bill. 

### Amount of Bill by Gender 

![gender bill](https://user-images.githubusercontent.com/66225041/129923597-b762031a-64e9-456c-be24-cac741ef3ea0.png)

Although there is a slight difference in bill amounts for separate genders seen between different races, in general bill amounts seem similar between the genders surveyed in this dataset. There are outliers for bill amounts for men that make it seem like it is more likely for a man to have a very high bill. 

## Modeling

### Random Forest 

Random forest builds a number of decision trees and merges them to arrive at a result that is best able to predict the data. It is a versatile algorithm that can be used for both classification and regression. Random forests are not prone to overfitting, but they can be slow depending on the number of trees generated and the amount of data. For this dataset, random forest is an excellent candidate. 

### XGBoost 

The extreme gradient boosting model can offer fast computational speeds and is excellent at creating regression models. It is a decision tree based algorithm and creates new models to correct the errors made by existing models. 

## Testing Different Models 

I implemented both algorithms, which resulted in very high values for the mean absolute error (MAE), or the difference in amount of the bill predicted by the model versus the actual bill amounts. For the first Random Forest the MAE was 7256 degrees, or about $7,256 off from the actual value of the bill. This is a high value, however, keeping in mind that there is a range of bill amounts that is more than $80,000, this might not be a bad estimate. The MAE of the XGBoost algorithm was 6970, which is a slightly better estimate. The most important features for the XGBoost algorithm were whether patients were foreigners, Malay, Chinese, a Singapore citizen, and whether they had symptom 5 or symptom 3. The most important feature is whether a patient is a foreigner. 

### Most Important Features for XGBoost Model - All Data

![xgboost 1](https://user-images.githubusercontent.com/66225041/129935377-b78771e6-274b-49b6-bfb7-4eb6de2eb0dc.png)

In order to see if dropping outliers over $20,000 improved the model, I modified the datatset to exclude these values. After evaluating the data with XGBoost again I found an MAE of 4416, the best value so far. The most important feature is whether a patient is a foreigner and the least important feature among the top ten is whether they had symptom 2.  

### Most Important Features for XGBoost Model - Outliers Removed

![xgboost 2 ](https://user-images.githubusercontent.com/66225041/129935717-b874cc32-f8cf-4abd-8f69-dee2a2ada63b.png)

The XGBoost algorithm was best at predicting the amount of a patient bill and the top ten most important features driving cost for bills under $20,000 are whether a patient is Malay, whether they have medical history 1, whether they are a Singapore citizen, whether they have symptom 5, whether they are a foreigner, whether they have medical history 6, whether they are Chinese, and whether they have symptoms 2, 3, or 4. 

These results indicate that different features drive the cost of care for different levels of bills. Foreigners are more likely to accrue large bills, as are people with symptom 5 and people who are Malay. This may be due to the racial composition found among Singapore citizens and permanent residents. Being a Singapore citizen results in a lower bill generally. 

Overall, where patients live and their race drives the cost of care, along with symptoms 2, 3,4 and 5, as well as medical history 1 and 6. 

