
# Velora Hotel Dashboard


## Problem Statement

This dashboard helps Velora Hotel to enhance its operational efficiency and strategic decision making by providing realtime insights into key perfomance metrics . It helps the hotel to monitor and analyze critical data related to bookings ,cancellations,revenue, customer demographics and length of stay. 

## Objectives
- Tracking Booking Count
- Analyze Cancellation of bookings
- Revenue Analysis
- Customer Demographics
- Length of Stay Analysis
- Peak Days Analysis


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor,and promoted headers & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : Changing data types to the correct data format was perfomed


              Table.TransformColumnTypes (#"Promoted Headers",{  {"Booking ID", type text}, {"Booking Date", type date}, {"Booking Channel", type text}, {"Loyalty Level", type text}, {"Status", type text}, {"Stay Date", type date}, {"Number of nights", Int64.Type}, {"Room Rate", type number}})


- Step 5 : For calculating  revenue, a column was added with the multiplication  of number of nights and room rate per night.
- Step 6 : For the calculation of how far away is the booking from the stay date, a subtraction calculation column was added where the 

            Duration.Days([Stay Date] - [Booking Date]), Int64.Type)
      
The column was renamed to "How far away"

- Step 7 : A conditional column was added to group "How far away" into different categrories

               Table.AddColumn(#"Renamed Columns1", "How far away bucket", each if [#"How far away?"] <= 7 then "1. Before a week" else if [#"How far away?"] <= 14 then "2. Before 2 weeks" else if [#"How far away?"] <= 28 then "3. Before 4 weeks" else "4. More than 4 weeks")


- Step 8 : Insertion of two added columns namely day name for stay date and day of the week .
- Step 9 : From power query the creation of measures was launched, Use of DAX to formulate measurement metrics  

       a) Booking Count = COUNTROWS(bookings)

       b) Cancellation Count = CALCULATE([Booking Count], bookings[Status] = "Cancelled")

       c) Cancellation % = DIVIDE([Cancellation Count], [Booking Count])

       d) Loyal Customer Booking Count = CALCULATE([Booking Count], bookings[Loyalty Level]<>"0.Non-member")

       e) Multi-night booking count = CALCULATE([Booking Count], bookings[Number of nights]>1)

       f) Not Loyal Customer Booking Count = CALCULATE([Booking Count], bookings[Loyalty Level]="0.Non-member")

       g) Single night booking count = CALCULATE([Booking Count], bookings[Number of nights]=1)

       f) Total Revenue = SUM(bookings[Revenue])

       g) Total Room Nights = SUM(bookings[Number of nights])



- Step 10 : In report view, a navigation column was setup with a selected theme, company logo and naviagation buttons.  
- Step 11 : In the report view, 5 Key Perfomance Indicator cards where inserted to track 

  (a) Booking Count

  (b) Cancellation Percentage
  
  (c) Total Revenue
  
  (d) Total Room Nights
  
  (e) Average Room Rate 
  

   ![Screenshot 2024-12-11 083554](https://github.com/user-attachments/assets/13ffeca8-ac18-4407-a961-4256be8ecad9)
  


- Step 12 : In the report view, under the insert tab, a line chart was inserted to track the number of stays per day throughout the month.
   
   ![Screenshot 2024-12-11 085044](https://github.com/user-attachments/assets/7b9c676c-a446-43a1-b442-592b6a138385)

Formatting was perfomed on the chart to suit the theme conditions.

- Step 13 : In the report view, under the insert tab, a clustered column chart was inserted to track the peak days throughout the week. The chart was used to visualize the days where most booking were recorded.

    ![Screenshot 2024-12-11 090133](https://github.com/user-attachments/assets/ace592b1-38e8-4867-9025-721fe1b32b3c)

  The chart was formatted in such a way to seperate weekdays and weekends in trackingthe booking activity.
       
        
     
- Step 15 : A clustered bar chart was used to visualize "Who stays with us ?" . The people were already classified in our data set according to loyalty level

![Screenshot 2024-12-11 095428](https://github.com/user-attachments/assets/0a7cd047-2f0b-41a3-abd0-65b7aeb7bc86)

The chart was sorted by loyalty level and in ascending order.

              
 - Step 16 : A column clustered chart was used to visualize how far our clients book accomodation before they stay in
    
    ![Screenshot 2024-12-11 100055](https://github.com/user-attachments/assets/578251ff-c52e-4961-9344-61cd01838dae)

 
 - Step 17 : A matrix was used to visualize the booking channels used and booking counts per booking channel also categorized by loyalty membership.
 
 ![Screenshot 2024-12-11 101505](https://github.com/user-attachments/assets/2d489334-23d1-4915-8c0d-274534e80fed)

 Conditional formatting was performed to highlight the booking channels with the most booking counts.
 

 
 - Step 18 : A slicer with days that spread throughout the whole month in analysis was insetred in th report.
     
     ![Screenshot 2024-12-11 102813](https://github.com/user-attachments/assets/e2fd0c9d-21a0-406e-bef4-5f41b0bfdc99)
 

 # Report Snapshot (Power BI DESKTOP)

 
![Screenshot 2024-12-11 103213](https://github.com/user-attachments/assets/9ecd4ba5-7086-4980-b968-83f67edacd06)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following insights can be drawn from the dashboard;

### Key Perfomance Indicators
       a) Booking Count = 5 000
       b) Booking Cancellation Percentage = 28.5 %
       c) Total Revenue = $1 million 
       d) Total Room Nights = 9 000
       e) Average room per night = $ 148

           
### [2] Booking insights

    a) Day with most bookings - Thursday 03 October 2024, 133 Booking Counts
    b)Day with least bookings - Monday 28 October 2024, 59 Booking Counts
    c) Most booked day - Thursday
    d) Least booked day - Sunday
    e) Most clients book a week away from their stay-in
    
  
  ### [3] Client Insights 
  
      a) Non-members of the loyalty spectrum have the most booking with 1938 bookings
      b) From members in the loyalty level Essential members had the most bookings, 986 bookings
      

 ### [4] Some other insights
 
 - Most of the booking were made through this channel in this order
       a) At the hotel
       b) Application

 

