# Project 3: 911 Call Data Mining
##Data Mining
* Association:  
Apriori Algorithm
* Supervised learning (classification)
Decision Tree  
Bayesian Classification  
SVM-Support Vector Machine   
K-Nearest Neighbor  
Random Forest  
Two approaches to **avoid overfitting**: prepruning, postpruning
* Unsupervised learning (clustering)

##Challenges:
This is a spatio temporal data mining problem. We have LiDAR data for the Downtown Lincoln, which consists of 734,000 points; 911 services calls data crawled from government sites; NOAA weather data. We also contacted the electricity system and water system. But they said the data are sensitive and cannot disclose.

The big problem is that we have different kinds of data based on location. However, they are not overlapped with each other. If the overlapped part dataset is small, it is highly possible that the result would be overfitted. On the other hand, the datasets are not exactly overlapped.  

So we first write a program to clean the data and to find the relatively high overlapped data points. However, the data is so big and our program is crashed on my computer. Then we think whether we can use the computer center to process our data. But for student they only allocate small memory to do this. Finally, we came up an idea whether we can plot the data in different color, and see which area has high density. Then it worked! 
