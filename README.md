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



## Modeling

### Random Forest 

Random forest builds a number of decision trees and merges them to arrive at a result that is best able to predict the data. 

