# **Microsoft-Fabric-Project-NYC-Taxi-Analysis**

## **Introduction:**
This project analyzes one year of NYC Yellow Taxi trip data using Microsoft Fabric. 
The goal is to ingest, process, and visualize large-scale transportation data 
to uncover patterns in trip volume, fares, distances, and peak travel times. 
By leveraging Fabric’s end-to-end analytics capabilities, the project demonstrates scalable data engineering, 
analytics, and reporting for real-world urban mobility data.

## **Datasets:**
NYC Taxi trip record data
NYC Yellow Taxi data captures detailed information about taxi trips across New York City, including pickup and drop-off locations, trip duration, and fares. It is widely used to analyze urban mobility patterns, demand trends, and transportation efficiency.

dataset used for this project : \
source of the dataset : https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page \
We have taken data for the year 2024 into consideration for this project.

## **Project Overview:**
In this project we have used 2 pipelines to ingest, process and prepare business ready data.

1. to ingest and clean data from the landing zone to staging schema.
2. to use the data from the staging schema and make it presentation ready and load in presentation schema.

![Project Architectue](screenshots/Project_architectute.png)

# **Project Steps:**

1. Create a workspace for NYC taxi project : NYC_Taxi_Fabric_Project.
2. Create a Lakehouse as landing zone for all the data files : NYCTaxiLakehouse
3. Create two separate folders inside NYCTaxiLakehouse:
    - NYCTaxi_Yellow
    - NYCTaxi_Lookup_Zone
4. Now upload the NYC Taxi trip data files in NYCTaxi_Yellow folder. There are total 12 parquet files for the year 2024(jan to dec).
    - yellow_tripdata_2024-01
    - yellow_tripdata_2024-02
    - yellow_tripdata_2024-03
    - yellow_tripdata_2024-04
    - yellow_tripdata_2024-05
    - yellow_tripdata_2024-06
    - yellow_tripdata_2024-07
    - yellow_tripdata_2024-08
    - yellow_tripdata_2024-09
    - yellow_tripdata_2024-10
    - yellow_tripdata_2024-11
    - yellow_tripdata_2024-12

> [!IMPORTANT]
> Upload the January Datafile only first to test the pipelines.

5. Upload taxi_zone_lookup.csv files in NYCTaxi_Lookup_Zone folder.
6. Create a warehouse to host staging schema : NYCTaxi_Warehouse.
7. Now we will start working on our first pipeline to ingest data and store in NYCTaxi_Warehouse.
   ### **Pipeline 1:**
     #### **pl_staging_zone_lookup_pipeline :**

   ![pl_staging_zone_lookup_pipeline](screenshots/pl_staging_zone_lookup_pipeline.png) 
     #### **Pipeline Components:**
       Copy Activity: Copy Taxi Zone Lookup Table \
       Source: NYCTaxiLakehouse/NYCTaxi_Lookup_Zone/taxi_zone_lookup.csv \
       Destination: NYCTaxi_Warehouse.staging.taxi_zone_lookup (new table) \
8. Start working on our sesond pipeline to ingest data in NYCTaxi_Warehouse, stagin schema.
    ### **Pipeline 2:**
     #### **pl_staging_nyctaxi_processing_pipeline :**

    ![pl_staging_nyctaxi_processing_pipeline](screenshots/pl_staging_nyctaxi_processing_pipeline.png)
    #### **Pipeline Components:**
     **Script Activity : Latest Processed Data** 
   
        select top 1 
            latest_processed_pickup 
            from metadata.processing_log 
            where table_processed = 'staging.NYCTaxi_yellow' 
            order by latest_processed_pickup desc;
   

 

