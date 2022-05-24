
# Module 9 – Surfs up!
# Unit Challenge
## Overview of the Project 
The main objective of this module was to determine how profitable a Surf Shop would be all year round in Hawaii. Before receiving any funding from our main stakeholder, he has requested a analysis about the weather conditions of the future location of our shop.

Now, as part of our final challenge, we need to compare the all available temperature observations for the months or June and December. This comparison will allow us to determine how big is the difference between the hotest time of the year versus the coldest. This will help us answering our profitability question. 

## Statistical analysis and Results
To get started with the statistical analysis, let's first share the basic numbers for both queries:

**Observations for June**

![Observations for June](/resources/june_tobs.png)

**Observations for December**

![Observations for December](/resources/december_tobs.png)

After observing the statistics for both June and December, we can conclude:

1. There are more observations for the month of june (1,700 vs 1,517)
2. The mean temperatures are very close, 74.9 (June) vs 71 (December)
3. For minimum temperatures, we have 64 (June) Vs. 56 (December)
4. For maximum temperature, the temperatures almos see no variation. We have 85 (June) Vs 83 (December)

If you ask me, I do not think there is a hugh difference in temperatures between June and December. I would say the weather is pretty much stable. I do not see a solid reason to either close the shop during the winter or introduce a different set of services or products during this time of year. 

The small variation in temperature may have an impact in the water temperature. If the water gets "too" cold, we can consider selling wetsuits for suerfers' protection. Also, adding a manu of hot beverages may be a good idea (in case we have customers very sensible to weather variations!).

I think temperature observations alone are not enough to determine the probability of success during winter time. Other measurements we can consider are:
1. Precipitation - The amount of precipitation may affect the influx of tourists that are not into surfing, but just having a relaxing time in the beach.
2. Hurricane data - Hurricanes will scare away surfers and tourists. We should consider when is the time of the year when it is more likely we will be facing this nature phenomenon.
3. Tourists flow during winter time - If we have little to no movement of tourists during this time of year, we have to consider closing for a few months. Can we afford that?

Of course, this list is not exhaustive, but adding these measurements would make our analysis more interesting. 

## Summary and conclusion
### Current situation
As a conclusion, I keep holding my assertion: Temperature observations are not enough to conclude that December is not going to be a good month. We need more data. If we focus on what we have now, we should be also considering:

1. Precipitacion data
Let's quickly review precipitation data for June and December. To get the following data (see the screenshots below, we used the following code):

'''
june_results_prcp = session.query(Measurement.date, Measurement.prcp).\
filter(extract('month',Measurement.date) == 6).all()

june_prcp_list = []
for item in june_results_prcp:
    june_prcp_list.append(item[1])
    
june_prcp_list_df = pd.DataFrame(june_prcp_list, columns=['june_prcp'])
june_prcp_list_df.describe()

december_results_prcp = session.query(Measurement.date, Measurement.prcp).\
filter(extract('month',Measurement.date) == 12).all()

december_prcp_list = []
for item in december_results_prcp:
    december_prcp_list.append(item[1])
    
december_prcp_list_df = pd.DataFrame(december_prcp_list, columns=['december_prcp'])
december_prcp_list_df.describe()
'''

**Precipitation for June**

![Observations for June](/resources/june_prcp.png)

**Precipitation for December**

![Observations for December](/resources/december_prcp.png)

By looking at the data, we can see we have more measurements for June. Also, we can see the mean precipitation for December is higher than (mean) precipitation in June. This, combined with the "cold" weather can reduce the number of visitors to our shop.

The way to get the same data using "standard SQL", is as follows (please note we are not adding any loginc to add this data into a DataFrame. We are just demostrating how to get this using a simple SQL query):

'''
import sqlite3
con = sqlite3.connect('hawaii.sqlite')
cur = con.cursor()

for row in cur.execute('SELECT tobs FROM Measurement where substr(date, 6,2) == \'06\' limit 20'):
        print(row)
        
print("----------------")
        
for row in cur.execute('SELECT prcp FROM Measurement where substr(date, 6,2) == \'06\' limit 20'):
        print(row)
'''

### Future efforts
As stated before, we can also look for data on:
1. Hurricanes and severity
2. Tourists influx
3. Volcano activity

Getting these data would are more variables into our analysis. It think it is important to consider al natural phenomenons, not only temperature and precipitation. Also, by analyzing the influx of tourists, we can discober where are we getting more visitors form, and the reasong why they are so fond of Hawaii. 




 