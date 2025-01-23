# RideWise: Optimizing NYC Taxi Demand Forecasts

Get the data from : http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml (2016 data) 

<b>Yellow Taxi: Yellow Medallion Taxicabs</b><br>
These are the famous NYC yellow taxis that provide transportation exclusively through street-hails. The number of taxicabs is limited by a finite number of medallions issued by the TLC. You access this mode of transportation by standing in the street and hailing an available taxi with your hand. The pickups are not pre-arranged.

<b>ML Problem Formulation</b><br>
Time-series forecasting and Regression


- To find number of pickups, given location cordinates(latitude and longitude) and time, in the query region and surrounding regions.
To solve the above we would be using data collected in Jan - Mar 2015 to predict the pickups in Jan - Mar 2016.


<b>Performance metrics</b><br>
Mean Absolute percentage error<br>
Mean Squared error

<b>Data Cleaning</b><br>
In this section we will be doing univariate analysis and removing outlier/illegitimate values which may be caused due to some error


<b>Modelling: <br>

Baseline Models:</b>
Now we get into modelling in order to forecast the pickup densities for the months of Jan, Feb and March of 2016 for which we are using multiple models with two variations<br>
1)Using Ratios of the 2016 data to the 2015 data<br>
2)Using Previous known values of the 2016 data itself to predict the future values<br>

<b>Simple Moving Averages</b><br>
The First Model used is the Moving Averages Model which uses the previous n values in order to predict the next value

<b>Weighted Moving Averages</b><br>
The Moving Avergaes Model used gave equal importance to all the values in the window used, but we know intuitively that the future is more likely to be similar to the latest values and less similar to the older values. Weighted Averages converts this analogy into a mathematical relationship giving the highest weight while computing the averages to the latest previous value and decreasing weights to the subsequent older ones
