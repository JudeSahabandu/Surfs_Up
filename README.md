# Weather Data Analysis
---
## Analysis of weather data in Hawaii for Surf & Ice-Cream Shop development

### Overview of the Analysis

The purpose of the project is to explore a business development opportunity to establish a Surf & Ice-Cream shop in Hawaii. The purpose of the concept is to provide a one stop Surfboard rental for locals and tourists whilst also being a rest spot for people to relax and have Ice Cream or a Shake!

In order to determine feasibility of the business concept, we need to understand the weather data of surfing hotspots across Hawaii. We initially look into a target spot to analyze the weather data across the year and replicate the analysis for other surfing hotspots across the Island. This analytical approach is critical to determine potential of the business idea and will also provide insight on the approach to business expansion.

In order to prepare insightful information to determine business feasibility, the following analytical approach was undertaken;

1. The analytical tools used for the purpose of this analysis is Jupyter Notebook, VS Code and GitHub
2. We also require certain dependencies in Python like Numpy, Pandas and Matplotlib to enable data analysis and visualization
3. In addition, we need to query an SQLite database, for this purpose we need to import relevant SQLAlchemy dependencies
4. Once we have all dependencies, we will create a session query with SQLAlchemy
5. Finally we retrieve data for relevant analysis

### Results of the Analysis

In our main analysis of understanding temperature data for the months of June and December, we try to determine seasonal variations across a key Summer (June) and a key Winter (December) based month. The following descriptions highlight some key information on interpreting the weather data analysis.

* Understanding the differences in mean temperature in the months of June and December

When considering the average temperature for the months of June and December, we obtained the following mean temperature for each month;

1. Average Temperature (June) - 74.54 F
2. Average Temperature (December) - 71.04 F

When trying to identify if there is a seasonal difference in our location, assessing the mean temperatures for polar opposite months will be useful to see if there is a seasonal impact.

When we assess the data for June and December, we see that mean temperatures for both months are above 70 F, which indicates that the location has tropical weather. In light of this, we can determine that the Surf and Shake shop concept is suitable for business all year round, as there is a higher probability for Sunny warm weather all year round.

Although, we need to further evaluate other weather parameters like rainfall, windiness etc. to determine feasibility of concept.

* Understanding the spread of temperature data in the months of June and December

When considering the spread of temperature for the months of June and December, we obtained the following standard deviation values for each month which indicates the spread of data in relation to the mean. The higher the value the higher the dispersion from the mean.

1. Standard Deviation (June) - 3.257
2. Standard Deviation (December) - 3.745

When looking at the spread of temperatures across the mean we can see how variable are the temperatures across the month. This allows us to assess if temperatures are more predictable or unpredictable.

When we assess the data for June and December, we see that standard deviation for June is 3.257 and that of December is 3.745. This indicates that temperatures in December are slightly more varied. When we look at the minimum and maximum temperatures for June and December, we can confirm what the standard deviation indicates;

1. Min and Max Temp (June) - Min is 64 F and Max is 85 F
2. Min and Max Temp(December) - Min is 56 F and Max is 83 F

In addition to spread of data determined through the standard deviation, we can also consider the quartile values to help us approximate the number of days we may be able to have better days for the success of the Surf and Shake shop.

* Understanding number of days where warm weather is present in the months of June and December

Looking at the quartiles for temperature data will allow us to determine the % of days which are likely to have warm weather for the success of the Surf and Shake shop.

1. Q1, Median and Q3 Weather Temp (June) - (Q1 - 73F), (Median - 75F), (Q3 - 77F)
2. Q1, Median and Q3 Weather Temp (December) - (Q1 - 69F), (Median - 71F), (Q3 - 74F)

The above quartile values will allow us to determine how many days reach each temperature value. For example, if we consider the month of June, we know by looking at the quartile values that at least 75% of days have temperatures above 73F, 50% of days have temperatures above 75F and 25% of days have temperatures above 77F. 

Similarly, for the month of December 75% of days have temperatures above 69F, 50% of days have temperatures above 71F and 25% of days have temperatures above 74F. 

### Summary of the Analysis

#### Summary of Temperature Data

Considering our analysis of temperature data, we see that across polar opposite months the weather is warm at a similar level. This allows us to determine from a temperature perspective, how suitable our business concept is across the year. In addition, if we require to determine the remaining months temperature data, we can reuse our query by replacing the month to obtain desired months temperature summary statistics.

```
#Query that filters the Measurement table to retrieve the temperatures for a specific month
results = session.query(Measurement.date, Measurement.tobs).filter(extract ("month", Measurement.date) == no. of month.all()
print(results)

#Convert the temperatures to a list.
list_results = [tup[1] for tup in results]
print(list_results)

#Create a DataFrame from the list of temperatures for the month
Temps = pd.DataFrame(list_results)

#Calculate and print out the summary statistics 
Temps.describe()
```

Weather data has multiple variables, thus determining the temperature data for a location is not sufficient to develop a case study in ascertaining suitability of a location to set up a business that is sensitive to weather parameters.


#### Additional Analysis to be considered

* Ascertaining impact of precipitation data

Warm weather is a key element to the success of a Surf and Shake concept, but we also need to determine the impact of rainfall at a location. We can determine the precipitation statistics for a specific month using the following code;

```
#Query that filters the Measurement table to retrieve the precipitation for a specific month
results = session.query(Measurement.date, Measurement.prcp).filter(extract ("month", Measurement.date) == no. of month.all()
print(results)

#Convert the precipitation to a list.
list_results = [tup[1] for tup in results]
print(list_results)

#Create a DataFrame from the list of precipitation for the month
Precipitation = pd.DataFrame(list_results)

#Calculate and print out the summary statistics 
Precipitation.describe()
```

Given the database containing has only temperature and precipitation data, we can conclude our analysis by reviewing the summary statistics for each weather variable.

We can determine the database columns by using the following code to ascertain the first row of data;

```
#assessing first row of data and columns in the database
first_row = session.query(Measurement).first()
first_row.__dict__
```

Based on the analysis outcome, the data indicates that the Surf and Shake shop is a feasible business concept to invest in!