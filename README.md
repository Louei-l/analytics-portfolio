# Learning Analytics Portfolio Journey

#### Technical Skills: Python, SQL, Excel, Tableau, 

### Formal Education
- M.S. International Business @ Wollongong University Dubai (2016)
- B.S. Finance & Marketing @ Al Akhawayn University (2014)


### Additional Education
- Google Data Analyst Professional Certificate (2023)
- Udemy Business Intelligence Analyst 2023 (2023)
- Udemy Python A-Z: Python for Data Science (2023)

### Work Experience
**Account Manager @ RTB House (August 2021 - August 2023)**
- Optimized ROI of Digital Campaigns through data analysis | Impact: Scaled campaigns by 2x-6x
- Created business reports using multiple data sources | Impact: Many insights were actioned and resulted in bigger budgets from clients
  

**Senior Media Planner @Dentsu (August 2017 - March 2021)**
- Created Media Industry Analysis using multiple 3rd Party Sources | Impact: Insight were used for strategic decks and pitches
- Created Excel Dashboard for e-com client | Impact: better relationship with client which led to bigger investments
- Created campaign reports with analysis and recommendations | Impact: Multiple recommendations led to higher ROI 10%+30%


# Data Journey Starts Here 

## Dipping toes into BigQuerry (Google)
**Exploring Public Data Sets**
- Following the Google certificate path we were working on the dataset for bicycles rental in London --> bigquery-public-data.london_bicycles.cycle_hire
  I was curious to see how many times were bikes rented overall for each year.  
 - This is the code I have produced 
```SQL
SELECT 
  EXTRACT(year FROM end_date) as Year,
  FORMAT("%'d",count(rental_id)) as Total_Number_Rents
FROM `bigquery-public-data.london_bicycles.cycle_hire` 
GROUP BY Year
ORDER BY Year;
```

![1st Independednt querry in BigQuerry](/assets/img/BigQuerry_London Bicycles_1.PNG)
