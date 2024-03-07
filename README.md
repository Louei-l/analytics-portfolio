# Learning Analytics Portfolio Journey

#### Technical Skills: Python, SQL, Excel, Tableau

### Formal Education
- M.S. International Business @ Wollongong University Dubai (2016)
- B.S. Finance & Marketing @ Al Akhawayn University (2014)


### Additional Education
- Google Data Analyst Professional Certificate (2023)
- Udemy Business Intelligence Analyst 2023 (2023)
- Udemy Python A-Z: Python for Data Science (2023)

### Work Experience
**Account Manager @ RTB House (August 2021 - August 2023)**
- Optimized ROI of Digital Campaigns through data analysis
  - Result: Scaled campaigns by 2x-6x
- Created business reports using multiple data sources
  - Result: Many insights were actioned and resulted in bigger budgets from clients
  

**Senior Media Planner @ Dentsu (August 2017 - March 2021)**
- Created Media Industry Analysis using multiple 3rd Party Sources
  - Result: Insight were used for strategic decks and pitches
- Created Excel Dashboard for e-com client
  - Result: better relationship with client which led to bigger investments
- Created campaign reports with analysis and recommendations
  - Result: Multiple recommendations led to higher ROI 10%+30%


# Data Journey Starts Here 

## Dipping toes into BigQuerry
**Exploring Public Data Sets**

Following the Google certificate path we were working on the dataset for bicycles rental in London I was curious to see how many times were bikes rented overall for each year.

This is the code I have produced on my own initiative

```SQL
SELECT  
  EXTRACT(year FROM end_date) as Year,
  FORMAT("%'d",count(DISTINCT rental_id)) as Total_Number_Rents,
FROM `bigquery-public-data.london_bicycles.cycle_hire` 
GROUP BY Year
ORDER BY Year;
```

![1st Independednt querry in BigQuerry](/assets/img/BigQuerry_London Bicycles_1.PNG)

Interestingly we can see that 2021 and 2022 were the years with most number of rentals. Why is that ? My assumption is either the amount of bikes that could be rented was increased to meet the demand, or because of COVID people got into a habbit of cycling and maintained it. 

- Checking if the number of bikes increased
  
```SQL
SELECT  
  EXTRACT(year FROM end_date) as Year,
  FORMAT("%'d",count(DISTINCT rental_id)) as Total_Number_Rents,
  FORMAT("%'d",count(DISTINCT bike_id)) as Total_Number_Bikes
FROM `bigquery-public-data.london_bicycles.cycle_hire` 
GROUP BY Year
ORDER BY Year;
```

![2nd Independednt querry in BigQuerry](/assets/img/BigQuerry_London Bicycles_2.PNG)

We can see that there was a significant spike in overal number of bikes in 2022. We can also see that in 2020 and 2021 there was an increase in bikes. 

## Data Cleaning
**Picked up some new tricks**

I am no stranger to data cleaning process since working in the digital advertising industry gave me a lot of exposure on this matter. However I am excited to learn SQL functions that can save a ton of time if you were doing same thing on excel. 

For instance converting timestamps into date format was a legthy process on excel, where I had to extract characters as string and then concatinate them into a date format. 
However in SQL all you have to do is use the CAST() function to convert the data from one format to another, amazing ! 

Here we can see that when I try to pull out data, it is in the form of timestamp and not date format. So if I wanted to plot this on a chart it will not appear as dates, and we dont want that.
![Cast function example](/assets/img/timestamp.PNG)

So now if we use the CAST() function and we convert the data format into date the issue is solved ! 

![Cast function example2](/assets/img/date.PNG)

```SQL
SELECT  
  CAST(date as date) as normal_date, 
  transaction_id
  
FROM `polished-will-406507.furniture_customer_data.furniture` 

ORDER BY date DESC 
;
```

There are several other usefull functions that are great to use to double check on data cleanliness 
- TRIM to remove blanc spaces
- COALESE to substitute data with another set incase Null values appear
- CONCAT function to form a new combined string, from several ones, as a new unique ID, 
- SELECT DISTICT to remove duplicates in the output
- LENGTH to check number of characters in a string, usefull when you know the exact length the string needs be i.e. country codes, or postal codes.

I wish I knew SQL when I was back in media agency crunching numbers for reports, it would have saved me a ton of time. 

Also crucial step is to triple check if all data was cleaned once you are done to be 100% there are no mistakes. 
Verify the cleaned data by comparing it to the unclean raw data, by randomly picking unclean entries and comparind it with the clean data set (i.e. one of the columns had a lot of null values, now compare the same to the cleaned data set). 
Also document the cleaning process and steps taken for other teammebers to quickly see what was done.
Once everythig is cleaned and documented, review the problem/objective and confirm whether cleaned data is suitable for the objective.

## Google Professional Data Analyst Certificate - Case Study - Bellabeat

**Introduction and setting**

You are a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused
products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the
global smart device market. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart
device fitness data could help unlock new growth opportunities for the company. You have been asked to focus on one of
Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The
insights you discover will then help guide marketing strategy for the company. You will present your analysis to the Bellabeat
executive team along with your high-level recommendations for Bellabeat’s marketing strategy.

**Phase One - ASK**

The business task is to identify growth opportunity, and generate insights that will be the base of the next marketing strategy.
 
Key Stakeholders: Are the two founders, one of whom is a creative person while the second is a mathematician. Knowing this it will be important to stike a good balance in my report with well made visuals/charts as well as logic behind numbers and thought process.
Urška Sršen: Bellabeat's cofounder and Chief Creative Officer
Sando Mur: Mathematician and Bellabeat’s co-founder

These questions will guide your analysis:
1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat marketing strategy?

**Phase Two - Prepare**

Data used for this case study is found on Kaggle [FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit). 

It is generated by 30 eligible Fitbit users who consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. Variation between output represents use of different types of Fitbit trackers and individual tracking behaviors / preferences.

In total there were 18 csv files. Some of the files had data in long format and some were in wide format. 

**ROCCC Analysis**

- **Realiablity of data - not realiable** - the data is based only on 30 users and we have no idea if these users are representative of Bellabeat customers. Also the data is gathered by different fitbit products hence we do not have an identical way of data capture, each product is tuned in a slightly different manner.
- **Originality of data - not original** - the data is third party, coming from a survey via Amazon Mechanical Turk 
- **Comprehensivness of data - highly comprehensive** - the data contains multitude of information that will help answering the business task
- **How current is the data - not current** - the data is old coming from 2026. User behavior could have changed over the years.
- **Is data cited - yes** - the data is properly cited 

Upon further examination of the 18 data sets by looking at file names and quickly opening them in excel: 
- 5 files were on a daily time frame, meaning each observation/entry was for one day. Moreover one of these files was a compilation of four daily separate data sets, which leaves us only with 2 unique data sets for daily time frame. 
- 12 files were on an hour or minute or seconds time frames. Based on my experience in advertising it will be hard to come up with solid insights whcih are based on such short time frames hence I will not be using these data sets. 
- 1 file contains too little data. I have pivoted the file in excel and found out that only 8 of the 30 participants had recorded data. It is too few participants to be able to draw any reliable conclusions.
- conclusion: I will be working with 2 files that are on daily time frame which are "dailyActivity_merged" and "sleepDay_merged".

Here is the screenshot of the pivot table in excel containing 8 unique ids from the pivoted file
![ 8 unique ids](/assets/img/weighloss_low paricipants.PNG)

**Phase Three - Process**

Key tasks
1. Check the data for errors.
2. Choose the tools.
3. Transform the data so you can work with it effectively.
4. Document the cleaning process.

I will be using R-Studio for quick data exploration and visualization, BigQuerry for data cleaning and manipulation, and finally Tableau as a secondary visualization tool.

First lets start with exploring the data in R. 
Loading librares that I will most likely use.
```R
library(janitor)
library(tidyverse)
library(readr)
library(readxl)
library(writexl)
library(dplyr)
library(lubridate)
```
and now I will upload the two data set files that I will be cleaning and analyzing.

```R
activty_df <- read.csv("dailyActivity_merged.csv")
sleep_df <- read.csv("sleepDay_merged.csv")
```

Next I will have a quick look at both files using the **head** and **str** function to get a feel of what the data set looks like. 

```R
head(activty_df)
str(activty_df)
head
```

Immediately we can see that the data in the "ActivityDate" and "SleepDay columns is in a wrong format which is "chr". Normaly it should be in date format. 

![wrong date format](/assets/img/Activity1PNG.PNG)

![wrong date format](/assets/img/Sleep1.PNG)


Now I will proceed to converting these columns from chr format to date format and split them into weekeday. I have also removed the 12:00:00 AM time stamp from sleep dataframe as we do not need it.

```R
activity_df$ActivityDate = as.Date(activity_df$ActivityDate, format="%m/%d/%Y")
activity_df <- activity_df %>% mutate( Weekday_Active = weekdays(ActivityDate))
sleep_df$SleepDay <- (gsub('12:00:00 AM', '', sleep_df$SleepDay)) 
sleep_df$SleepDay = as.Date(sleep_df$SleepDay, format = "%m/%d/%Y")
sleep_df <- sleep_df %>% mutate( Weekday_Sleep = weekdays(SleepDay))
```

Next we check for NA values and duplicates
```R
colSums(is.na(activity_df))
colSums(is.na(sleep_df))
sum(duplicated(activity_df))
sum(duplicated(sleep_df))
```

We foudn 3 duplicates in sleep_df, we can check what they are just to get a visual idea and to double check as well
```R
get_dupes(sleep_df)
```

now we proceed to remove the 3 duplicate obervations from sleep dataframe
```R
sleep_df <- sleep_df[!duplicated(sleep_df), ]
```

As a last step we will merge the two dataframes to have an easier time working on it
```R
merged_df <- merge(activity_df, sleep_df, by = "Id", all = TRUE)
```
**Phase Four - Analysis**

Moving to analysis of data let's have a quick descriptive overview of the data to find averages and any outliers

```R
summary(merged_df[c('TotalSteps', 'VeryActiveMinutes', 'FairlyActiveMinutes', 'LightlyActiveMinutes', 'SedentaryMinutes', 'Calories', 'TotalMinutesAsleep', 'TotalTimeInBed')])
```
![descriptive_summary](/assets/img/Summary_descriptive.PNG)
