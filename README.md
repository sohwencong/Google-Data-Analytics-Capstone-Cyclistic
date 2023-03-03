## Table of Contents
1. [Background](README.md#background)
2. [Objectives](README.md#objectives)
3. [Steps](README.md#steps)
4. [Process & Analyze](README.md#process--analyze)
5. [Analyze & Share](README.md#analyze--share)
6. [Insights & Recommendations](README.md#insights--recommendations)

## Background
In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime. 

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

## Objectives
* **Role**: A junior data analyst in Cyclistic marketing analytics team.
* **Goal**: Design marketing strategies aimed at converting casual riders into annual members.
* **Business Task**: How do annual members and casual riders use Cyclistic bikes differently? 


## Steps
1. One year of data, from Aug 2020 to Jul 2021, was downloaded from [here](https://divvy-tripdata.s3.amazonaws.com/index.html). 

2. Loaded files into Python and performed exploratory data analysis. The dataset was then wrangled, cleaned and added with additional features. Next, it was exported as a csv file for further analysis. 

3. Finally, dashboards were created using MS PowerBI. Insights were derived from the visualizations. 

## Process & Analyze
### Python
1. The downloaded dataset csv files were initially opened with MS Excel. However, the opening of the files took longer than usual due to the large file sizes. The file sizes ranged from 9MB to 150MB.

2. The 12 csv files were loaded into pandas dataframes and inspected. The column or feature names were ‘ride_id’, ‘rideable_type’, ‘started_at’, ‘ended_at’, ‘start_station_name’, ‘start_station_id’, ‘end_station_name’, ‘end_station_id’, ‘start_lat’, ‘start_lng’, ‘end_lat’, ‘end_lng’ and ‘member_casual’.

| Dataframe Name | Number of Rows |	Number of Columns |
| :---: | :---: | :---: |
| aug20	| 622,361 | 13 |
| sep20	| 532,958	| 13 |
| oct20	| 388,653	| 13 |
| nov20	| 259,716	| 13 |
| dec20	| 131,573	| 13 |
| jan21	| 96,834	| 13 |
| feb21	| 49,622	| 13 |
| mar21	| 228,496	| 13 |
| apr21	| 337,230	| 13 |
| may21	| 531,633	| 13 |
| jun21	| 729,595	| 13 |
| jul21	| 822,410	| 13 |

3. They were combined into a single dataframe with 4,731,081 rows and 13 columns. 

4. Column names were renamed to a more intuitive description. They were 'trip_id', 'bikeid', 'start_time', 'end_time', 'from_station_name', 'from_station_id', 'to_station_name', 'to_station_id' and 'usertype’.

5. 'start_time' and 'end_time' were changed into datetime datatype. 

6. A new feature 'ride_length' was created by taking the difference of 'end_time' and 'start_time'. It was then converted into minutes and hour in the 2 new features 'ride_length_min' and 'ride_length_hr'. 

7. A new feature ‘day_of_week’ was created from ‘start_time’, where 0 : Monday and 6 : Sunday. However, this wasn’t quite intuitive and thus I replaced the numbers 0 to 6 to string abbreviations Mon to Sun. 
(On hindsight, this did not prove to be the best way as my visualizations involving ‘day_of_week’ didn’t appear in order. I should have left ‘day_of_week’ in integers and convert in PowerBI using Power Query.)

8. A new feature ‘month’ was extracted from ‘start_time’, where 1 : Jan and 12 : Dec. However, similar to the above, I replaced the numbers 1 to 12 to string abbreviations Jan to Dec.
(On hindsight, it was not necessary as ‘month’ was automatically available under ‘start_time’s date hierarchy.)

9. A new feature ‘time’ was extracted from ‘start_time’. 
(On hindsight, this was not too helpful as there was no ‘time hierarchy’ unlike that of date.)

10. A new feature ‘hour’ was extracted from ‘start_time’.

11. There were negative values in 'ride_length_min' which did not make sense. A total of 8619 data points with negative values were discovered. As this was only 0.18% of the total dataset, I proceeded to drop them.

12. The final dataset consisted of 4,722,462 rows and 20 columns. It was then exported out as csv format for further analysis. 

## Analyze & Share
### MS PowerBI
1. Loaded the csv file into PowerBI. It took around 10 minutes for the data to be loaded as the files files was more than 1.1GB.  

2. I checked for data type consistency and existence null values. There were null values present in the dataset. Fortunately, the columns that I was interested in did not contain any null values.  

3. The 2 measures that I was interested were the number of trips and ride duration. Hence, I designed the dashboard and created 8 visualizations based on number of trips analysis and average ride duration analysis. 

   a.	By Usertype

   b.	By Hour (of Day)

   c.	By Days (of Week)

   d.	By Month

## Insights & Recommendations
### Insights
1. 55.5% of the total trips were made by members and 45.5% by casual riders.

2. Highest number of trips were made in the months of Jun, July and Aug. These may be due to the fact that the weather is more favourable for cycling. 

3. The number of trips by member was relatively constant throughout the days of the week, while it spiked during the weekends for casual riders. The number of trips made on Saturdays by casual riders was almost twice that of weekdays. 

4. 1700hrs to 1759hrs was the peak hour for both members and casual riders. 

5. Average ride duration by casual riders was 36.8 minutes (71.4%) in contrast to 14.7 minutes (28.6%) by members. In general, average ride duration by casual riders more than doubled that of members. 

6. The average ride duration for both casual riders and members was relatively constant over the months with the peak in Feb. 

7. Ride duration was the highest during the weekends for both casual riders and members. 

8. For casual riders, longest average ride durations occurred from 11pm to 4am, ranging from 43 minutes to 60 minutes. 

### Recommendations
1. From insight 2, we know that the number of trips for casual riders were lower than members during the colder months. We can offer a discounted memebership package during these colder months to entice casual riders.

2. From insight 3 and 7, we can come up with a weekend membership promotion package to target the weekend casual riders. 

3. From insight 5, we can come up with a promotion to convert ride duration and the distance travelled into incentives. 

4. From insight 8, we can come up with a night rider membership package to target the longest ride durations from 11pm to 4am. 
