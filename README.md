![page1image39361024](https://user-images.githubusercontent.com/102244119/163694373-be0fae51-2232-43de-b2ee-65b53334f875.png)


## About the company
Bellabeat’s a high-tech company that manufactures health-focused smart products. The co-founder has used her background as an artist to develop beautifully designed technology that informs and inspires women around the world. Collecting data on activity, sleep, stress, and reproductive health has allowed Bellabeat to empower women with knowledge about their own health and habits. 


## Scenario
You are a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the global smart device market. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart device fitness data could help unlock new growth opportunities for the company. You have been asked to focus on Bellabeat’s wearable product Leaf. Leaf is Bellabeat’s classic wellness tracker that can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress. 


## Stakeholders
* Urška Sršen: Bellabeat’s co-founder and Chief Creative Officer 
* Sando Mur: Mathematician and Bellabeat’s cofounder; a key member of the Bellabeat executive team 
* Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy. 


## Business Task
Analyze smart device data to gain insight into how consumers are using their current wearable devices. The insights you discover will then help guide the marketing team’s strategy for the company. 


## Data Source
The data provided is FitBit Fitness Tracker Data (CC0: Public Domain, dataset made available through Mobius, https://www.kaggle.com/arashnic): This Kaggle data set contains personal fitness tracker information from thirty Fitbit users, generated by a survey via Amazon Mechanical Turk between 2016-03-12 and 2016-05-12. Data limitations include the limited number of participants and the lack of consistency in participants’ recording data. For example, although there were 33 participants that had daily activity, calorie, and step information, only 24 participants recorded sleep information and even less than that (eight) logged weight loss information. There are also inconsistencies in some of the data, like calories, where it’s obvious that some days were not accurately or completely tracked.


## Preparation, processing, and analysis of the data
Uploaded CSV data files for daily activity, daily calories, sleep a day, and weight loss in BigQuery. The sleep_day and weight_loss CSV files had the incorrect date and time format to be uploaded to BigQuery, so I corrected the format to YYYY-MM-DD HH:MM. 


Started exploring the dataset, including checking the number of rows in the data starting with the daily activities table. Repeated this query for the daily calories, sleep a day, and weight loss tables. The result was a count of 940 rows for daily activity, 940 rows for daily calories, 413 rows for sleep day, and 67 rows for weight loss.

![BigQuery1-1](https://user-images.githubusercontent.com/102244119/163735355-7619cd7c-2d35-4df0-a0a4-54345524c192.png)

Checked the user Id’s to ensure consistency in the number of character length of all Id’s, using the CAST() function to convert data type (from INTEGER to STRING). I verified that no rows came back to Id's that were less than or more than 10 characters in length. I performed the following query for the daily activity table and then repeated it for the additional three tables.

![BIgQuery2-1](https://user-images.githubusercontent.com/102244119/163735426-a010f001-c595-4d57-9dcf-34d83088b78b.png)
![BigQuery2-2](https://user-images.githubusercontent.com/102244119/163735429-b3e9b65f-3a82-4a4b-bcd3-f441a3515c5f.png)

Checked for duplicates, and verified how many total (unique) user ids were in each of the tables. Performed the following query for the daily activity table and then repeated it for the additional three tables. Results were 33 distinct user ids in the daily activity table, 33 distinct user ids in the daily calories table, 24 distinct user ids in the sleep a day table and 8 distinct user ids in the weight loss table.

![BigQuery3](https://user-images.githubusercontent.com/102244119/163735462-7dc91d3e-9788-4a83-aba4-eb1513516545.png)

Ran queries to pull the information for minimum, maximum, and average steps per day. I also ran an additional query to see the minimum steps per day when excluding those recorded as zero.

![BigQuery4-1](https://user-images.githubusercontent.com/102244119/163735593-7689b3f7-23ca-4efc-b0fb-1af5a2bd0232.png)
![BigQuery4-2](https://user-images.githubusercontent.com/102244119/163735596-e7dbfb24-d384-499c-99c1-529d9091f387.png)
![BigQuery4-3](https://user-images.githubusercontent.com/102244119/163735598-cd1c6625-2a56-449f-9e04-07b92df0379f.png)
![BigQuery4-4](https://user-images.githubusercontent.com/102244119/163735601-4dc42227-678d-410c-80a3-42d1da635eb8.png)

Next, I checked each unique user’s average daily steps.

![BigQuery5](https://user-images.githubusercontent.com/102244119/163735677-42332b38-5eaf-40dd-a446-37804fbe172d.png)

To compare levels of activeness for each unique user Id, I compared the four different levels of active minutes. 

![BigQuery6](https://user-images.githubusercontent.com/102244119/163735696-f9067e68-b31d-4b45-84e2-08abb19122c4.png)

Verified how many users logged activities over 0.0 in distance. 

![BigQuery_UpdatedSS](https://user-images.githubusercontent.com/102244119/165190698-717c5c3c-c2c1-4717-bf50-20a64ae2e731.png)

Checked daily calories for minimum, maximum, and average steps per day. I also ran an additional query to see how what the minimum calories were per day when excluding those recorded as zero.

![BigQuery8-1](https://user-images.githubusercontent.com/102244119/163735972-289fad28-087e-45cb-a0c5-ff9fc87de29a.png)
![BigQuery8-2](https://user-images.githubusercontent.com/102244119/163735975-f98c36e5-a088-4682-852a-ce3995868a86.png)
![BigQuery8-3](https://user-images.githubusercontent.com/102244119/163735978-a17aa6c9-8a47-4908-bec6-0eff1587ebcd.png)
![BigQuery8-4](https://user-images.githubusercontent.com/102244119/163735980-73f691a0-f8d7-4971-b0de-342d0b498e36.png)

Then, I checked the average number of calories per day by each unique user Id:

![BigQuery9](https://user-images.githubusercontent.com/102244119/163735995-1100256e-d745-46b1-b447-a21c8e3d1d46.png)

I wanted to verify how accurate the average calorie intake was with users, to do this I checked how many entries were entered as less than 1,000 calories per day. Results showed that 12 users reported less than 1,000 calories in a day. Further querying shows that 4 of these entries reported 0 calories in a day.

![BigQuery10-1](https://user-images.githubusercontent.com/102244119/163736044-1e9b7113-116b-4763-a4b4-cc3478d59ecd.png)
![BigQuery10-2](https://user-images.githubusercontent.com/102244119/163736050-23db1f9d-d075-4022-a56f-07406d632de4.png)

Verified the average number of sleep for users, in minutes and then converted the results to hours. I also compared the average time in bed versus the total time users were actually asleep.

![BigQuery11-1](https://user-images.githubusercontent.com/102244119/163736121-5ab0e116-ffea-4ab8-b1f9-e7e52e36e750.png)
![BigQuery11-2](https://user-images.githubusercontent.com/102244119/163736126-c88aec7b-ca62-4d1e-9244-6a660f2e23f1.png)
![BigQuery11-3](https://user-images.githubusercontent.com/102244119/163736129-2719a47f-ef0e-4cdc-a910-1444ae60a46d.png)

I wanted to join the daily_activities table and sleep table to perform a comparison of active minutes versus sleep minutes that each distinct user is getting. I did that with the following query. The results show that activity levels have an impact on sleep levels. Users clearly get more sleep on more active days.

![Screen Shot 2022-04-26 at 8 34 11 AM](https://user-images.githubusercontent.com/102244119/165311902-4dc76f84-1f64-4d04-9a01-e2bf86e67921.png)

I checked to see how many users are actively keeping track of their weight as well as the maximum and minimum weight of each unique user. Additionally, I verified the average weight (in pounds) and average BMI of users.

![BigQuery12-1](https://user-images.githubusercontent.com/102244119/163736172-c6ab34ac-66e0-481f-b424-16304e8646b3.png)
![BigQuery12-2](https://user-images.githubusercontent.com/102244119/163736175-dedda2dd-37a1-4aad-8dcb-81e93fa0031c.png)
![BigQuery12-3](https://user-images.githubusercontent.com/102244119/163736179-c6ce6490-b5ef-48d9-bff7-6c4c010088f5.png)


## Data visualizations of key findings and takeaways
### **Most users had a less active lifestyle with most time spent being sedentary or only lightly active. You can see the comparison of levels of activeness and how many minutes are spent in each compared to the others.**
![Bellabeat_Sedentary-vs-LightlyActive](https://user-images.githubusercontent.com/102244119/163734188-df4e1ea9-b270-4a82-a9ff-9ae3d5e73749.png)
![Bellabeat_FairlyActive-vs-VeryActive](https://user-images.githubusercontent.com/102244119/163734193-8ea13c32-99d4-43fc-b026-46aa5ce1296e.png)

### **Users consistency in tracking activities declined throughout the month, showing that users prefer not to have to manually track everything. In addition, only four users tracked activity with a distance over 0.0.**
![Bellabeat_LoggedActivities-vs-LoggedDistance](https://user-images.githubusercontent.com/102244119/163734211-b328929d-89d7-42e6-9831-d3d4e9762260.png)

### **Sleep tracking was the highest priority with users, with over 72% of users taking the time to track sleep.**
![Bellabeat_SleepTracking](https://user-images.githubusercontent.com/102244119/163734245-1e0630da-bf76-482b-af11-5f4ec3ec1b0c.png)

### **Users averaged an average of 6.99 hours (419.46 minutes) in bed, however of that time users spend an average of 39 minutes awake in bed.**
![BellaBeat_TimeInBed-vs-TimeAsleep](https://user-images.githubusercontent.com/102244119/163734289-9077e03a-323d-4c18-b13a-cafd727bd375.png)

## Recommendations
- Create a pulse alert through the Leaf device or through the Bellabeat app that encourages movement regularly throughout the day and promotes a healthier and more active lifestyle.
- Implement a "Total Days Tracked" contest or something similar to incentivize users to be more consistent in tracking habits.
- Magnify the Leaf's sleep tracking accuracy to support users with better sleeping habits, leading to better quality sleep.
- Market how Leaf is easy to use, automatically syncs with the Bellabeat app throughout the day and helps keep track of your health with minimum effort for the user. Make sure this information is readily available on the Leaf's product page. 
- Promote the Leaf's ability to automatically connect to the Bellabeat app for not only tracking health information but for insights on when you need to lessen stress, get better sleep, and even celebrate users’ achievements. 
