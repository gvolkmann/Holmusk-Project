# Holmusk-Project

The goal of this project was to find the variables driving the cost of hospital bills. The data analyzed in this project included 3 datasets with various data about patient demographics, medical histories, symptoms, and date of admission and discharge. These datasets were merged and irrelevant data that did not have an effect on bill amounts, such as bill id, were dropped. 

The provenance of the data was not provided. Values that differed slightly in the dataframe but were supposed to signify the same information were updated: for example, in the race column "chinese" was updated to "Chinese". There were 13,600 individual bills and 3000 individual patients indicating there are patients that have been admitted multiple times. I calculated age of the patient and length of stay as these are variables that can often influence the cost of care. I also looked at the day of the week and the month of the year that patients were admitted as seasonality can influence cost of care for certain illnesses. There were missing values for medical history 2 and medical history 5, which I replaced with 0 as I did not want to drop this data and there were few enough missing values that I did not think it would affect the data analysis. 

### Distribution of the Bill Amounts 



### Heatmap of Medical History and Amount of Bill 

![medical_history_corr](https://user-images.githubusercontent.com/66225041/129902458-3468a320-0a8f-48f2-80a6-6939b3f304df.png)

There does not seem to be much correlation between the various medical histories and the amount of the hospital bill. The is a slight correlation between medical history 6 and medical history 1, but nothing is jumping out as an important driver of cost. 

### Heatmap of Preop Medication Administered and Amount of Bill

![preop medication corr](https://user-images.githubusercontent.com/66225041/129903158-5d89522e-b18f-4f57-b512-f347703de91f.png)

There is very little correlation between the preop medication administered and the amount of the bill, so these medications are possibly similar in cost. 

### Heatmap of Symptoms and Amount of Bill 

![symptom corr](https://user-images.githubusercontent.com/66225041/129904200-a0f3910d-8e7a-4de7-bb5e-c678cd6a83ab.png)

There is some correlation between several of the symptoms and the amount of the bill, particularly symptom 5. This symptom maybe be one that requires treatment that is more costly than the treatment for the other symptoms. 





