# Russian Tank Losses in Ukraine Analysis 
### Data Analysis and Engineering Project

## Objectives
1. To understand the effects of tank attrition on the Russian Armed Forces in the 2023 Summer counteroffensive by the Ukrainian Armed Forces.
2. To demonstrate basic data analysis, transformation, storage, and visualization.

## Dataset Used
This project uses a Python script to scrape data from WarSpotting.net into a tabular format. The data is transformed within the script to classify the vehicles into vehicle types. After transformation, the data is pushed into a local PostgreSQL database automatically. I used GPT4 to help code this script.

## Technologies
- Language: Python & SQL
- Extraction: Python with GPT4
- Transformation: Python
- Storage: PostgreSQL
- Visualization: Google Looker

## Data Pipeline
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/1cc03869-f90c-46c6-9ce2-4181d50113fc)

## Data Model
The data model is a simple one table with no relational records. Each line in the table is a record of a vehicle loss in Ukraine.

- ID
- status
- vehicle_name
- class
- location
- date

## Step 1: Extract Data
Extraction is executed by a script that scrapes data and transforms the data into a table format. After the script has scraped the data, I have the program classify the vehicle losses by referencing a static lookup CSV table.

## Step 2: Update and Store
Once all transformations are complete, the data is pushed into a PostgreSQL database and updates previous records if necessary.
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/7b45be7a-e1df-4567-a52f-76eff5f9c34d)

## Step 3: Retrieve and Visualize
A CSV is downloaded from this table and imported into Google Looker for dashboard creation.

To understand the breakdown of losses, the data needed to have a representation of the types of vehicles and their losses over time. I created a simple table with numeric losses by vehicle and a pie chart to show proportionality. I inserted a time series line graph to show losses over time.

![image](https://github.com/jqwin/joes_data_projects/assets/138724732/ae4bdda7-1ad2-454d-bb66-3883b36d8633)

## Step 4: Anaylze
The Ukrainian counteroffensive is an ongoing campaign that started on June 4, 2023. Russian forces are in a defensive posture but are playing an active and intense defense of the southern front. 
To understand the characteristics of the equipment losses of Russia, the losses from the start of the war needs to be compared against with more current data.

**From Feb 24, 2022 to June 3, 2023 - Before the counteroffensive**
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/7db06434-5ec3-4f21-9577-b1113ef63e61)
-	T-80BV tanks are the most numerous type of tank that was lost before the summer counteroffensive(18% of losses)
-	T-72 pattern vehicles are older but approximately are around 40% of losses
-	The Russian ground forces are primary using midline grade tanks with good all-around performance in the T-80BV.
-	The T-80 series of tank has improved mobility and electronics over the T-72 series
-	This usage pattern strikes a balance by providing acceptable capability with older T-72 variants taking the brunt of attrition.

**From June 4, 2023 to now - The ongoing counteroffensive**
![image](https://github.com/jqwin/joes_data_projects/assets/138724732/33eb33af-ead2-4eab-979c-6c446ae72514)
-	The T-80BV still remains the top variant and is **now taking close to 40%** of tank losses
-	Newer variants are becoming more common with the T-90M being increasingly fielded.
-	Overall tank losses are at 1,717 which is a substantial amount of equipment lost
-	Ukrainian government reports a total of 5,112 losses(as of Oct 25)

**Summary**

Russian tank losses are becoming increasingly numerous because of the intensity of the counteroffensive. The tank fleet still primarily uses the T-80BV variant. However, as these stocks dwindle over time, they are increasingly replaced with newer models like the T-90M. Russia still retains large stocks of older T-72 variants which they are fielding to balance out attrition in this counteroffensive. The underlying data is based on visually confirmed evidence and so this data does not provide a complete picture of equipment losses in Ukraine but it provides a rough picture of the battlefield.







