# **Microsoft-Fabric-Project-NYC-Taxi-Analysis**

## **Introduction:**
This project analyzes one year of NYC Yellow Taxi trip data using Microsoft Fabric. 
The goal is to ingest, process, and visualize large-scale transportation data 
to uncover patterns in trip volume, fares, distances, and peak travel times. 
By leveraging Fabric’s end-to-end analytics capabilities, the project demonstrates scalable data engineering, 
analytics, and reporting for real-world urban mobility data.

## **Datasets:**
dataset used for this project : \
source of the dataset : https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page \
We have taken data for the year 2024 into consideration for this project.

## **Project Overview:**
In this project we have used 2 pipelines to ingest, process and prepare business ready data.

1. to ingest and clean data from the landing zone to staging schema.
2. to use the data from the staging schema and make it presentation ready and load in presentation schema.

![Project Architectue]([Project_architectute.png](https://github.com/sudhanshu03shukla/Microsoft-Fabric-Project---NYC-Taxi-Analysis/blob/main/screenshots/Project_architectute.png))

