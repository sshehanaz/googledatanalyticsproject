Google Data Analytics Capstone Project 

The aim of this project is to complete the case study on Cyclistic bike share through Data analysis. In this project, I will follow the steps of Ask, Prepare, Process which are taught in the Google Data Analytics Course.

Cyclistic Case Study
Cyclistic is a bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno (the director of marketing and my manager) believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

ASK
The below questions are asked to obtain more information about the end goal of the project.
How do annual members and casual riders use Cyclistic bikes differently?
Why would casual riders buy Cyclistic annual memberships?
How can Cyclistic use digital media to influence casual riders to become members?

PREPARE
I will use Cyclistic’s historical trip data to analyze and identify trends from Jan 2022 to Dec 2022 which can be downloaded from divvy_tripdata. The data has been made available by Motivate International Inc. under this license.

This is public data that can be used to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit from using riders’ personally identifiable information. This means that we won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes. There are 12 files with naming convention of YYYYMM-divvy-tripdata and each file includes information for one month, such as the ride id, bike type, start time, end time, start station, end station, start location, end location, and whether the rider is a member or not. The corresponding column names are ride_id, rideable_type, started_at, ended_at, start_station_name, start_station_id, end_station_name, end_station_id, start_lat, start_lng, end_lat, end_lng and member_casual.

PROCESS 
SQL Query - 
I used SQL query to combine datasets and clean the data. 12 csv files are uploaded as tables in the dataset '2022_tripdata'. Another table named "combined_data" is created, containing 5,667,717 rows of data for the entire year. I have also explored the data to observe the consistencies and differences.

Explore Data - 

The table below shows the all column names and their data types. The ride_id column is our primary key.

![observations1](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/069a7402-059b-40ae-9919-bae21bda1985)

The below table shows number of null values in each column. Some columns have missing values. 

![observations2](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/c6a2cc91-1049-4cc0-a59d-2d034afe3d23)

As ride_id has no null values, let's use it to check for duplicates.

![observations3](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/49d0e238-9019-4676-bc41-9dc25da79448)

There are no duplicate rows in the data.

All ride_id values have length of 16 so no need to clean it.

There are 3 unique types of bikes(rideable_type) in our data.

![observations4](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/f6c8d7c0-1529-4309-962b-d239999ac295)

The started_at and ended_at shows start and end time of the trip in YYYY-MM-DD hh:mm:ss UTC format. New column ride_length can be created to find the total trip duration. There are 5360 trips which has duration longer than a day and 122283 trips having less than a minute duration or having end time earlier than start time so need to remove them. Other columns day_of_week and month can also be helpful in analysis of trips at different times in a year.

Total of 833064 rows have both start_station_name and start_station_id missing which needs to be removed.

Total of 892742 rows have both end_station_name and end_station_id missing which needs to be removed.

Total of 5858 rows have both end_lat and end_lng missing which needs to be removed.

member_casual column has 2 uniqued values as member or casual rider.

![observations5](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/a23063ab-77d3-4d59-9b11-34e94c80383f)

Columns that need to be removed are start_station_id and end_station_id as they do not add value to analysis of our current problem. Longitude and latitude location columns may not be used in analysis but can be used to visualise a map.

CLEAN DATA - 

All the rows having missing values are deleted.
3 more columns ride_length for duration of the trip, day_of_week and month are added.
Trips with duration less than a minute and longer than a day are excluded.
Total 1,375,912 rows are removed in this step.

ANALYZE & SHARE

The data is stored and is now prepared for analysis. I queried multiple relevant tables for the analysis and visualized them in Tableau.
The analysis question is: How do annual members and casual riders use Cyclistic bikes differently?

First of all, member and casual riders are compared by the type of bikes they are using.

![analyze1](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/43ce620a-ff01-4997-99d2-0fe1e7b0449a)

The members make 59.7% of the total while remaining 40.3% constitutes casual riders. Each bike type chart shows percentage from the total. Most used bike is classic bike followed by the electric bike. Docked bikes are used the least by only casual riders.

Next the number of trips distributed by the months, days of the week and hours of the day are examined.

![analyze2](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/47a41457-9e35-41ce-b2ff-9bd417ff85fb)
When it comes to monthly trips, both casual and members exhibit comparable behavior, with more trips in the spring and summer and fewer in the winter. The gap between casuals and members is closest in the month of july in summer.

![analyze3](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/a441a343-1219-4aba-a6c0-795e3f086732)
When the days of the week are compared, it is discovered that casual riders make more journeys on the weekends while members show a decline over the weekend in contrast to the other days of the week.

![analyze4](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/6cd6f1b6-ea6e-4d00-aa03-096b32a4045f)
The members shows 2 peaks throughout the day in terms of number of trips. One is early in the morning at around 6 am to 8 am and other is in the evening at around 4 pm to 8 pm while number of trips for casual riders increase consistently over the day till evening and then decrease afterwards.

Ride duration of the trips are compared to find the differences in the behavior of casual and member riders.

![ride1](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/79d3941c-e867-4a00-be2f-4754b1bd9b81)

![ride2](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/6506b6dc-5f66-497d-940b-d6b09e2b7714)

![ride3](https://github.com/sshehanaz/googledatanalyticsproject/assets/147394026/e0e49bf1-b687-4c6d-bce5-1b8aecbe78fe)

Note that casual riders tend to cycle longer than members do on average. The length of the average journey for members doesn't change throughout the year, week, or day. However, there are variations in how long casual riders cycle. In the spring and summer, on weekends, and from 10 am to 2 pm during the day, they travel greater distances. Between five and eight in the morning, they have brief trips.

These findings lead to the conclusion that casual commuters travel longer (approximately 2x more) but less frequently than members. They make longer journeys on weekends and during the day outside of commuting hours and in spring and summer season, so they might be doing so for recreation purposes.


ACT

After identifying the differences between casual and member riders, marketing strategies to target casual riders can be developed to persuade them to become members.
Below are my recommendations:

Marketing campaigns might be conducted in spring and summer at tourist/recreational locations popular among casual riders.
Casual riders are most active on weekends and during the summer and spring, thus they may be offered seasonal or weekend-only memberships.
Casual riders use their bikes for longer durations than members. Offering discounts for longer rides may incentivize casual riders and entice members to ride for longer periods of time.


