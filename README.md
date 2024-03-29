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
- 5 files were on a daily time frame, meaning each observation/entry was for one day. Moreover one of these files was a compilation of four daily separate data sets, which leaves us only with 2 unique data sets for daily time frame which are activity and sleep.
- 12 files were on an hourly time frame and one such file aligns perfectly activity, the hourly steps data completments the daily activity data.
- 1 file contains too little data. I have pivoted the file in excel and found out that only 8 of the 30 participants had recorded data. It is too few participants to be able to draw any reliable conclusions.
- conclusion: I will be working with 3 files that are on daily time frame which are "dailyActivity_merged" , "sleepDay_merged", and "hourlySteps_merged"

Here is the screenshot of the pivot table in excel containing 8 unique ids from the pivoted file
![ 8 unique ids](/assets/img/weighloss_low paricipants.PNG)

**Phase Three - Process**

Key tasks
1. Check the data for errors.
2. Choose the tools.
3. Transform the data so you can work with it effectively.
4. Document the cleaning process.

I will be using R-Studio for this case study to perform data cleaning, exploration, analysis and visualization.

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
library(ggpubr)
```
and now I will upload the two data set files that I will be cleaning and analyzing.

```R
activty_df <- read.csv("dailyActivity_merged.csv")
sleep_df <- read.csv("sleepDay_merged.csv")
hr_steps_df <- read.csv("hourlySteps_merged.csv")
```

Next I will have a quick look at files using the **head** and **str** function to get a feel of what the data set looks like. 

```R
head(activty_df)
str(activty_df)
head(sleep_df)
str(sleep_df)
head(hr_steps_df)
str(hr_steps_df)
```

Looking at the below output we can notice that the "ActivityDate",  "SleepDay" and "ActivityHour" columns are in a wrong format which is "chr". Normaly it should be in date format. 

![wrong date format](/assets/img/Activity1PNG.PNG)

![wrong date format](/assets/img/Sleep1.PNG)

![wrong date format](/assets/img/hour.PNG)


Now I will proceed to converting these columns from chr format to date format and split them into weekeday. I have also removed the 12:00:00 AM time stamp from sleep dataframe as we do not need it. However for the hourly steps I will need the horly data so I will split the data into Date and Hour colums

```R
activity_df$ActivityDate = as.Date(activity_df$ActivityDate, format="%m/%d/%Y")
activity_df <- activity_df %>% mutate( Weekday_Active = weekdays(ActivityDate))
sleep_df$SleepDay <- (gsub('12:00:00 AM', '', sleep_df$SleepDay)) 
sleep_df$SleepDay = as.Date(sleep_df$SleepDay, format = "%m/%d/%Y")
sleep_df <- sleep_df %>% mutate( Weekday_Sleep = weekdays(SleepDay))
hr_steps_df <- hr_steps_df %>% separate(ActivityHour, c("Date", "Hour"), sep = "^\\S*\\K")
hr_steps_df$Date = as.Date(hr_steps_df$Date, format="%m/%d/%Y")
```

Next we check for NA values and duplicates
```R
colSums(is.na(activity_df))
colSums(is.na(sleep_df))
sum(duplicated(activity_df))
sum(duplicated(sleep_df))
sum(duplicated(hr_steps_df))
```

We foudn 3 duplicates in sleep_df, we can check what they are just to get a visual idea and to double check as well
```R
get_dupes(sleep_df)
```

now we proceed to remove the 3 duplicate obervations from sleep dataframe
```R
sleep_df <- sleep_df[!duplicated(sleep_df), ]
```

As a last step we will merge the two daily dataframes to have an easier time working on it
```R
merged_df <- merge(activity_df, sleep_df, by = "Id", all = TRUE)
```
**Phase Four - Analysis**

Moving to analysis of data let's have a quick descriptive overview of the data to find averages and any outliers

```R
summary(merged_df[c('TotalSteps', 'VeryActiveMinutes', 'FairlyActiveMinutes', 'LightlyActiveMinutes', 'SedentaryMinutes', 'Calories', 'TotalMinutesAsleep', 'TotalTimeInBed')])
summary(hr_steps_df[c('StepTotal')])
```
![descriptive_summary](/assets/img/Summary_descriptive.PNG)

![descriptive_summary](/assets/img/steps_descriptive.PNG)

We find that on average a person does 8K steps a day and spends 806 minutes (13.4hr) being sedentary. On the calory side the mean is 2.3K a day while mean sleep time is 409 mins (7hr). 
Also we can see that the mean for hourly steps is 320. 

Let's see how many steps on average happen on each week day. Sunday has the lowest number of steps while Tuesday has the highest.

```R
ggplot(merged_df) + geom_bar(aes(Weekday_Active, TotalSteps, ), position = "dodge", stat = "summary", fun = "mean")
```
![descriptive_summary](/assets/img/avg_steps_day.PNG)

Shifting to sleep data, I will plot the average sleep hours per week day. We can see that Sunday has the highest average sleep time.  

```R
ggplot(merged_df) + geom_bar(aes(Weekday_Active, TotalSteps, ), position = "dodge", stat = "summary", fun = "mean")
```

![descriptive_summary](/assets/img/avg_sleep_day.PNG)

Moving to next point, I will visualize the activity levels of the users. The tracker has ceveral categories of activitly level: Very Active, Fairly Active, Lightly Active, Sedentary. So this data was tracked with how many minutes are attributed to each category.

```R
activity_lvl <- merged_df %>%
  summarize(very = sum(VeryActiveMinutes),
            fairly = sum(FairlyActiveMinutes),
            lightly = sum(LightlyActiveMinutes),
            sedentary = sum(SedentaryMinutes)) %>%
  select(very, fairly, lightly, sedentary) %>%
  as.data.frame() %>%
  t() %>%
  as.data.frame() %>%
  rownames_to_column(var = "Category") %>%
  rename(Minutes = V1)%>%
  mutate(Percentage = sprintf("%.2f%%", (Minutes / sum(Minutes)) * 100))

Result:
  Category  Minutes Percentage
     very   300394      2.28%
   fairly   216559      1.64%
  lightly  2517370     19.11%
sedentary 10137640     76.96%
```

It looks like users spend almost 80% of their time being sedentary and only 2.3% being very active.

Now we will look at the hourly steps and check if certain hours of the day clock the most steps

```R
ggplot(hr_steps_df_order) + geom_bar(mapping = aes(x=Time_Period, y = StepTotal, fill = Time_Period, color = Time_Period), stat = "identity")
```
![descriptive_summary](/assets/img/hourly_steps.PNG)

We can see that in the evening between 6-7PM the steps are the highest followed by 12-2PM time.

I would like to also see how the distance affects the calorie usage of the users. 
So lets run some test to determine if there is any relationship and if there is what is the impact. 
Four sets of distance: Very_Active_Distance,	Moderately_Active_Distance,	Light_Active_Distance, and Sedentary_Active_Distance. I will drop the Sedentary one because it is counterintuitive for the business to promote being Sedentary. So we will work on the three remaining. 
First lets see if there is a strong relationship between the three Distance categories and Calories (Logically there should be, but we never know). 

```R
correlation_matrix <- merged_df %>%
  select(VeryActiveDistance,
         ModeratelyActiveDistance, LightActiveDistance, Calories) %>%
  cor()
```
![descriptive_summary](/assets/img/Correlation.PNG)

We can see that there is indeed correlation between the distance and calories

- Very_Active_Distance has a moderate positive correlation of 0.453
- Moderately_Active_Distance has a weak positive correlation of 0.122
- Light_Active_Distance has a moderate positive correlation of 0.398

Now I am currious to see which of the distance categories has the biggest effect on the calories. To do this I will use the reggression analysis approach

```R
lm_model <- lm(Calories ~ LightActiveDistance + ModeratelyActiveDistance + VeryActiveDistance, data = merged_df)
summary(lm_model)
```

Interestingtly we see a surprising result when it comes for Moderately_Active_Distance, it has a negative Estimate. This means that for every one unite increase in Moderately_Active_Distance Calorie usage decreases by 42.83. 
To have a better understanding it ideal to have more data that shows what activities go into Moderately_Active_Distance. So for now I will play safe and drop this one. 

![descriptive_summary](/assets/img/Regression.PNG)

To have another more intuitive spin on the regression analysis and how the Active_Distance categories impact calorie usage we can plot a line to forecast outcome 

```R
install.packages("ggeffects")
library(ggeffects)
ggpredict(lm_model, terms = c("LightActiveDistance")) |> plot()
ggpredict(lm_model, terms = c("VeryActiveDistance")) |> plot()
```

here are the two graphs, you can see the projection of both categories. It is easy to see the impact the Very_Active_Distance has on calories, a good reference poin is 10 distance units. 
So in case of Very_Active_Distance at 10 units it corresponds to roughly 3,800 claories. If we look at Light_Active_Distance, 10 units corresponds to 3,600 calories. 

![descriptive_summary](/assets/img/Light_Active.PNG)

![descriptive_summary](/assets/img/Very_Active.PNG)


**Phase Five - Recommendations**

- 77% of time is spent being sedentary. 
- Sunday has the lowest step count and also the highest sleep time.
- 6:00PM-7:59PM has the most steps among all time slots
- Very Active and Light Activite Activities that produce Distance have a significant effect on calorie burn. Among the two Very Active is the bigger one.

So from these insights we can recommend some ideas for the marketing approach. 

1) Tackle the sedentary issue, and provide some kind of incentive for users to be less sedentary. The could create a leaderboard on a country/region/state level and show which user was the most active and walked the biggest distance. This can create arouse a small competitive instinct among people and make them move a bit.
2) Also the marketing team could focus higher maketing budgets on digital ads on sunday to make a bigger impact on users and gently remind them that Sundays are not to be lazy, but to be active !
3) Encourage users to be very active as it helps burn the most calories.
4) Create a point system of steps walked, and active minutes and allow users to use these points as discount vouchers for Belabeat products. If possible make a partnership with sport wear brands that could accept the points and give discounts on their products as well. This could potentially be a very good incentive system for people to avoid being sedentary. 
