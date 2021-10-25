# nyc_taxi

## Notebook 1) import_and_data_manipulation.ipynb

### Prepare Schema and read CSV 
### there are space in columns names of data here and there. Needs tidying up.

### Data Cleansing

#### A) tripdata

#### rows before clesing: 15100468
#### rows after removing missing dropoff coordinates: 15100322
#### rows after removing 0 passenger trips: 15100239
#### rows after removing 0 time trips: 15062346
#### rows after removing 0 distance trips: 14976785
#### rows after removing suspicious pickup/dropoff latitude/longitue: 14734920
#### rows after removing identical pickup/dropoff: 14617675

#### B) tripfare

#### remove rows with extreme values at cutoff (99.5 percentile) below
#### cutoff_fare_amount:52.0
#### cutoff_tolls_amount:5.33
#### cutoff_surcharge:1.0
#### cutoff_tip_amount:11.56
#### cutoff_total_amount:69.39
#### rows before clesing: 15100468
#### rows after removing extreme amounts above 99.5 percentile: 14971573

### Enhance data
#### 1) use reverse geocode from geopy package to get suburb name from coordinates
#### 2) geo distance between pickup and dropoff coordinates
#### 3) create pickup_date
#### 4) create trip_id, taxi_id, driver_id and taxi_driver_id

### Save data
#### 1) Save combined trip data as Parquet

## Notebook 2) eda_and_cluster_analysis.ipynb

### Enhance data
#### 1) add fare_per_mile and sec_per_mile

### EDA
#### 1) Fare distribution
#### 2) Time distribution
#### 3) Fare per mile distribution
#### 4) Seconds per mile distribution
#### 5) Time of day distribution
#### 6) Time of week distribution
#### 7) pickup / dropoff location distribution
#### 8) Trip category (from which suburb to which suburb)

### Cluster Analysis
#### 1) K-means clustering based on fare_per_mile and sec_per_mile
#### 2) Profile clusters to explain the difference
#### 3) Prove that fare and time mean by cluster provide narrower error than overall mean

### Save data
#### 1) Select and save data for predicting fare and tips as Parquet
#### 2) Select and save data for maximizing revenue and revenue per hour as Parquet

## Notebook 3) maximizing_revenue_and_rev_per_hour.ipynb

### Aggregate data
#### 1) driver-pickup date level
#### 2) taxi-pickup date level

### Build forecasting model
#### 1) GBT Regressor for predicting driver's daily revenue
#### 2) GBT Regressor for predicting driver's revenue per hour

### Stats
#### 1) Build correlation matrix to show influence of #drivers occupying taxi in a day to revenue and hours

## Notebook 4) predicting_fare_and_tip.ipynb

### Build forecasting model
#### 1) GBT regressor for predicting fare
#### 2) GBT regressor for predicting tip


Questions
a. In what trips (feel free to have your own definition of “trips”) can you confidently use
respective means as measures of central tendency to estimate fare, time taken, etc.
b. Can we build a model to predict fare and tip amount given pick up and drop off coordinates,
time of day and week?
c. If you were a taxi owner, how would you maximize your earnings in a day?
d. If you were a taxi owner, how would you minimize your work time while retaining the average
wages earned by a typical taxi in the dataset?
e. If you run a taxi company with 10 taxis, how would you maximize your earnings?