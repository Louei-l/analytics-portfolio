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


