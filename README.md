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

<b>Exponential Weighted Moving Averages</b><br>
Through weighted averaged we have satisfied the analogy of giving higher weights to the latest value and decreasing weights to the subsequent ones but we still do not know which is the correct weighting scheme as there are infinetly many possibilities in which we can assign weights in a non-increasing order and tune the the hyperparameter window-size. To simplify this process we use Exponential Moving Averages which is a more logical way towards assigning weights and at the same time also using an optimal window-size.

<b>Comparison between baseline models</b><br>
We have chosen our error metric for comparison between models as MAPE (Mean Absolute Percentage Error) so that we can know that on an average how good is our model with predictions and MSE (Mean Squared Error) is also used so that we have a clearer understanding as to how well our forecasting model performs with outliers so that we make sure that there is not much of a error margin between our prediction and the actual value


<b>Regression Models</b><br>
Train-Test Split<br>
Before we start predictions using the tree based regression models we take 3 months of 2016 pickup data and split it such that for every region we have 70% data in train and 30% in test, ordered date-wise for every region



<b>Features</b>

| Feature                | Description                                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------------------------|
| **VendorID**           | A code indicating the TPEP provider that provided the record:                                                |
|                        | - Creative Mobile Technologies                                                                               |
|                        | - VeriFone Inc.                                                                                              |
| **tpep_pickup_datetime** | The date and time when the meter was engaged.                                                               |
| **tpep_dropoff_datetime** | The date and time when the meter was disengaged.                                                           |
| **Passenger_count**    | The number of passengers in the vehicle. This is a driver-entered value.                                     |
| **Trip_distance**      | The elapsed trip distance in miles reported by the taximeter.                                                |
| **Pickup_longitude**   | Longitude where the meter was engaged.                                                                       |
| **Pickup_latitude**    | Latitude where the meter was engaged.                                                                        |
| **Dropoff_longitude**  | Longitude where the meter was disengaged.                                                                     |
| **Dropoff_latitude**   | Latitude where the meter was disengaged.                                                                      |
| **RateCodeID**         | The final rate code in effect at the end of the trip:                                                        |
|                        | - Standard rate                                                                                              |
|                        | - JFK                                                                                                        |
|                        | - Newark                                                                                                     |
|                        | - Nassau or Westchester                                                                                      |
|                        | - Negotiated fare                                                                                           |
|                        | - Group ride                                                                                                |
| **Store_and_fwd_flag** | Indicates whether the trip record was held in vehicle memory before sending to the vendor (store and forward): |
|                        | - `Y`: Store and forward trip                                                                                |
|                        | - `N`: Not a store and forward trip                                                                          |
| **Payment_type**       | A numeric code signifying how the passenger paid for the trip:                                               |
|                        | 1. Credit card                                                                                               |
|                        | 2. Cash                                                                                                      |
|                        | 3. No charge                                                                                                |
|                        | 4. Dispute                                                                                                   |
|                        | 5. Unknown                                                                                                   |
|                        | 6. Voided trip                                                                                               |
| **Fare_amount**        | The time-and-distance fare calculated by the meter.                                                          |
| **Extra**              | Miscellaneous extras and surcharges (e.g., $0.50 and $1 rush hour and overnight charges).                    |
| **MTA_tax**            | $0.50 MTA tax that is automatically triggered based on the metered rate in use.                              |
| **Improvement_surcharge** | $0.30 improvement surcharge assessed at the flag drop (introduced in 2015).                                |
| **Tip_amount**         | Tip amount – Automatically populated for credit card tips. Cash tips are not included.                        |
| **Tolls_amount**       | Total amount of all tolls paid in the trip.                                                                   |
| **Total_amount**       | The total amount charged to passengers (does not include cash tips).                                          |




<br><br>
<b>Error Metrics</b><br>

| Model                            | Train MAPE         | Test MAPE         |
|----------------------------------|--------------------|-------------------|
| **Baseline Model**               | 0.140052758787     | 0.136531257048    |
| **Exponential Averages Forecasting** | 0.13289968436      | 0.129361804204    |
| **Linear Regression**            | 0.13331572016      | 0.129120299401    |
| **Random Forest Regression**     | 0.0917619544199    | 0.127244647137    |
| **XGBoost Regression**           | 0.129387355679     | 0.126861699078    |





