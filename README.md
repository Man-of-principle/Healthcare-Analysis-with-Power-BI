
# Healthcare Analysis with Power BI

## Introduction
👋 Hello everyone! Welcome to my latest project where I delve into the world of healthcare analysis using Power BI. In this case study, I've had the incredible opportunity to apply my Power BI skills to real-world healthcare data, aiming to uncover insights and drive efficiency in hospital operations.

### About the Case Study:
As part of this project, I collaborated with HealthStat, a fictional consulting company, to analyze a comprehensive state-wide hospital dataset. The dataset includes New York state-wide hospital discharge data for a year, focusing on patients who underwent elective hip replacement surgery. Each row represents a single inpatient stay, from admission to discharge date. It's important to note that the health information in this dataset is not individually identifiable, ensuring patient privacy.

### The Challenge:
Healthcare efficiency is paramount in ensuring quality patient care. However, achieving optimal efficiency while maximizing resources is no easy feat. In this analysis, we zoomed in on the length of stay (LOS) for patients undergoing elective hip replacement surgery. By understanding the factors influencing LOS, we aimed to streamline processes and reduce associated costs.

## Patient Population for Analysis:
In this case study, our focus is on patients who received hip replacement surgery. This elective procedure is typically sought by patients experiencing hip pain, often due to arthritis. During the procedure, damaged bone and cartilage are surgically replaced with prosthetic components. Hospital stays for such surgeries can range from 0 to 2 or more days.

### Terminology Overview:
Throughout this case study, you'll encounter several key terms:

•	Inpatient: A person admitted to a hospital bed.

•	Discharge: The release of a patient from hospital care by a medical worker.

•	Disposition: The patient's destination or status upon discharge, such as transfer to another facility or return home.

•	Elective Surgery: A planned procedure, not due to an emergency.

### Skills Used:
•	Data Modeling: Structuring the dataset for effective analysis in Power BI.

•	Exploratory Data Analysis: Delving into the dataset to uncover patterns and trends.

•	Root Cause Analysis: Identifying factors contributing to inefficiencies in hospital operations.

•	DAX Calculations: Utilizing DAX functions to perform calculations and derive insights.

•	Report Design: Creating visually engaging dashboards to present key findings and insights.

### What You'll Find:
•	Detailed analysis techniques using Power BI.

•	Insights into hospital efficiency metrics.

•	Challenges faced and solutions implemented.

•	Opportunities for further exploration and improvement.

## Data Preparation
### Dataset Overview:
For this project, we are working with a dataset provided by HealthStat, capturing patient-level data on all hospital stays in a single year for elective hip replacement surgeries across the state of New York. The dataset comprises one single table with 30 columns, with each row representing a single inpatient stay from admission to discharge. It's crucial to note that the dataset does not contain personally identifiable health information, ensuring patient privacy.

### Initial Data Investigation:
Before diving into analysis, the first step is to load the dataset into Power BI (Power Query) and conduct an initial investigation. We'll explore the data types and contents to ensure data quality. One critical aspect to check is that all patients have the same hip replacement procedure code, ensuring consistency in our analysis.

### Exploratory Data Analysis (EDA):
We'll conduct exploratory analysis to profile the entire dataset and investigate column distributions. This step will provide insights into the data structure and help identify any anomalies or inconsistencies that may require cleaning.

### Data Cleaning:
Based on the findings from our exploratory analysis, we'll proceed to clean up the data. One specific task involves removing rows where the procedure description is not "HIP REPLACEMENT, TOT/PRT". This step ensures that we focus our analysis specifically on elective hip replacement surgeries as intended.

### Creating Measures:
Once the data is cleaned, we'll create measures to start analyzing hospital totals. This will provide us with insights into how many hospitals in the state perform our procedure of interest, setting the foundation for deeper analysis.
Stay tuned as we progress through the data preparation phase, ensuring that our dataset is primed for insightful analysis in Power BI!

## Analysis and Visualization
To build an understanding of patient profiles in the dataset, I explored the preliminary demographics such as gender and age. I created a measure "Total Discharges"

     {Total Discharges = COUNTROWS(hospital_discharges)} 
    
 to count total discharges in the dataset and stored it in the _Measures table.

HealthStat assigned a clinical advisor to direct me in some of my tasks. To help guide my analysis from a clinical perspective, the clinical advisor requested to see a breakdown for patients aged 50 and older. I modified my visualization of gender distribution by age group to account for this change.

Corresponding Visual: Gender distribution by age group (Aged 50 and Older) and gender, Total Discharges and Total Discharges by gender is shown below.

![Fig 1](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/d2453261-3139-46de-b1df-ebc375dae955)

Following the initial exploration of total hospitals and discharges in the dataset, as well as insightful demographics on patient profiles, the next step was to investigate the variation of length of stay (LOS) days across different demographic fields.

A measure titled “Average LOS Days”

     { Average LOS Days = DIVIDE(SUM(hospital_discharges[length_of_stay]),COUNT(hospital_discharges[length_of_stay]))}
 was created to compute the average length of stay days, and it was stored in the _Measures table.

Two visualizations were crafted to display the average LOS days by age group and gender. Once again, filtering was applied to assess patients aged 50 or older. To achieve this, a new column using DAX called "Age Band" was generated, with values set as "Age 50+" for individuals aged 50 and above, and "Age <50" for those below. Subsequently, this new field replaced the age_group for analysis.

### Corresponding Visuals:
1.	Age band Column created
2.	Average LOS days, Average LOS Days by Age Band (Aged 50 and Older) and Average LOS Days by Gender (Aged 50 and Older)

![fig 2a](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/098cfcbf-214b-4825-825b-b3f9c4457267)

![Fig 2b](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/29e41845-7fd8-4202-9ec5-e6c7af3f82c5)


The leadership team at HealthStat expressed interest in comparing the average length of stay (LOS) days and total discharges across hospitals. Additionally, the clinical advisor emphasized the importance of considering the total number of practicing surgeons by each hospital.

To address these requirements, I developed a line and stacked column chart to visualize both the total discharges and average LOS days across hospitals. The visualization was configured to display data for only the top 15 hospitals by total discharges.

Furthermore, a new measure titled “Total Surgeons”

     { Total Surgeons = DISTINCTCOUNT(hospital_discharges[operating_provider_license_number])} 

 was created to calculate the count of surgeons, and this measure was incorporated into the chart depicting LOS and discharges by hospital as a tooltip.

Corresponding Visualization: Line and stacked column chart showcasing total discharges and average LOS days by hospital, with tooltips displaying the count of surgeons and Total Surgeons.

![fig 3](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/0e96d737-8b60-4f87-bd84-2ed8031cab59)

While we've examined the length of stay (LOS) against certain demographics like age and gender, we have yet to unravel the underlying factors contributing to the variability in LOS between hospitals.

Moving forward, let's shift our focus to another crucial metric: the Average Cost per Discharge

     {Average Cost per Discharge = DIVIDE(SUM(hospital_discharges[total_costs]),[Total Discharges])}
By leveraging this metric, we aim to establish a benchmark for comparing cost efficiency between hospitals and identifying potential areas for improvement in efficiency.

Factors that can impact the cost of patient stay include:
-	Patient severity of condition
-	Age
-	Size of hospital
-	Procedure and type of equipment used.

We'll embark on a comprehensive exploration to identify hospitals that exhibit significant deviations from the state average in terms of both cost and length of stay (LOS). Additionally, we'll investigate whether the size of a surgical program has any discernible impact on LOS and cost efficiency. To achieve this, we'll conduct a root cause analysis to ascertain the primary factors influencing LOS and cost variations across hospitals.

Given that the average cost per discharge and average LOS can vary considerably among hospital facilities, I've devised two metrics to quantify the relative difference between each hospital and the overall state average.

To establish a benchmark for comparison, I created two measures to compute the overall state averages: one for the average cost per discharge and another for average LOS days. These measures have been labeled with "ALL" at the end of their names to distinguish them from other measures in the dataset. Below are the DAX Syntax.

    Average Cost per Discharge ALL = CALCULATE ([Average Cost per Discharge],ALL())

    Average LOS Days ALL = CALCULATE ([Average LOS Days], ALL())


In addition to computing the overall state averages, I've developed two additional measures to quantify the percentage difference in the average cost per discharge and the average LOS days. 
These measures, labeled "% Var Average Cost per Discharge" and "% Var Average LOS Days" respectively, will provide insights into the extent of variation between each hospital's metrics and the state average. Below are the DAX Syntax.

    % Var Average Cost per Discharge = 
        DIVIDE(
         ([Average Cost per Discharge]-[Average Cost per Discharge  ALL]),
         [Average Cost per Discharge ALL])

    % Var Average LOS Days = DIVIDE(
        ([Average LOS Days]-[Average LOS Days ALL]),
         [Average LOS Days ALL])
     
I placed these measures in a table visual and used conditional formatting to indicate where values of average cost and LOS days are higher or equal to the overall values.

![fig 4](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/e2470d9d-302a-4597-a469-5fccd1bf37fa)

To identify outliers effectively, I've crafted a Scatter chart showcasing the relationship between Average LOS Days and Average Cost per Discharge, with each hospital represented as a distinct dot. To provide context, I've incorporated two average lines on the chart. Additionally, to enhance visual clarity, I've utilized the Total Discharges as bubble size and color-coded the bubbles based on the health service area.

Moreover, I've included an additional reference line denoting the 90th percentile. This allows us to readily identify hospitals whose values fall outside this threshold, thereby identifying potential outliers. This comprehensive visualization will enable us to pinpoint hospitals with notable variations in cost and LOS metrics relative to their peers, facilitating targeted analysis and intervention where necessary.

![fig 5](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/1b7a677b-e5d7-496f-91a1-5971a047a40d)

In preparation for the root cause analysis, I took into account the impact of surgical program size as requested by my boss. Since our source data doesn't explicitly provide information on surgical program size, I leveraged DAX functions to create a new table summarizing total discharges and surgeons by hospital.

Next, I updated our data model to incorporate this new table, named "surgical_program_volume_summary," and established a relationship with the existing "hospital_discharges" table. To categorize hospitals based on their surgical program size, I grouped the total discharges into 200s and labeled them accordingly, creating a more defined grouping that served as our column for Surgical Program Size. This enhancement will allow us to analyze the impact of surgical program size on cost and LOS metrics, providing valuable insights for our root cause analysis.

![fig 6a](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/5591ed33-48e8-4ebf-9514-38a04eb2e2e5)

Dax syntax 

    surgical_program_size_summary = SUMMARIZECOLUMNS(
    Hospital_Discharges[facility_name],"Total Discharges", [Total Discharges], "Total Surgeons", [Total Surgeons])

![fig 6b](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/b5b8930b-4268-48e0-8d13-c4d604708ef3)


To investigate the root causes impacting cost and LOS, we've identified a list of factors provided by the clinical advisor for assessment:
-	Risk of mortality
-	Severity of illness description
-	Diagnosis description
- Patient disposition
- 	Gender
-	Age Bins
-	Surgical program size
-	Health service area
  
In order to analyze the influence of these factors on Average LOS Days, I've created a column chart for each factor. While reviewing these charts, it's evident that certain factors exhibit notable variations in Average LOS Days. However, discerning which factor has the most significant influence on average LOS days remains challenging.

By examining these charts collectively, we can identify trends and patterns that may provide insights into the factors driving variations in LOS. Further analysis and statistical techniques may be necessary to quantify the impact of each factor accurately. This iterative approach will enable us to pinpoint the root causes and develop targeted interventions to optimize cost and LOS metrics effectively.

![fig 7](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/b8c19de7-5b0d-434d-b6e0-ba7d24c2648a)

To further explore the influence of the eight variables assessed on both Average LOS Days and Average Cost Per Discharge, I introduced the Key Influencer visual. This powerful tool allows us to analyze the impact of each variable on the selected metrics and identify significant contributors to variations in LOS and cost.

By leveraging the Key Influencer visual, we can gain deeper insights into the relationship between the variables and the target metrics. This analysis will enable us to prioritize factors that have the most significant influence on both Average LOS Days and Average Cost Per Discharge, thereby guiding our efforts to optimize hospital efficiency and resource allocation.

![fig 8](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/833b871e-1b17-4bea-87ea-a2ec515c4a8f)


## Insights from Analysis: Elective Hip Replacement Surgeries in New York State

-	Hospital Landscape: New York State boasts a total of 151 hospitals offering elective hip replacement surgeries, contributing to a substantial volume of over 26,000 total discharges.

-	Length of Stay (LOS): On average, patients undergoing elective hip replacement surgery experienced a LOS of approximately 2.65 days. However, there was notable variability in LOS among different hospital facilities.

-	Cost Analysis: The average cost per discharge for elective hip replacement surgeries was estimated at $20,910. Similar to LOS, there was significant variability in costs across hospital facilities.

-	Root Cause Analysis Findings: Through root cause analysis, it was revealed that certain attributes exerted a pronounced influence on both cost and average LOS. Notably, extreme illness severity and major mortality risk emerged as top influencers, significantly impacting efficiency.

-	Regional Disparities: Hospitals located in New York City exhibited the highest LOS and cost metrics overall, highlighting regional disparities in healthcare delivery. Additionally, patient disposition to a skilled nursing home was identified as a significant factor influencing LOS.

By uncovering these insights, healthcare providers can better understand the factors driving variations in LOS and cost, enabling targeted interventions to improve efficiency and optimize patient outcomes.

## Creating an Interactive Dashboard: Uniting Insights with Healthstat Branding

To enhance accessibility and user experience, I integrated all vital visual subsets of insights into a comprehensive report template, incorporating Healthstat branding elements for a cohesive presentation.

## Designing a User-Friendly Interface: Navigating Insights Seamlessly

To facilitate seamless exploration, I curated a "Home" page within the dashboard, offering users quick access to navigate between different sections of the report. This intuitive design allows stakeholders to effortlessly access and digest the wealth of insights presented within the report, empowering informed decision-making and strategic planning.

Below are snapshots of the Dashboard. To access the interactive dashboard (the PowerBI file) Click -> https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/blob/main/HEALTH%20CASE%20STUDY.pbix

![Dashboard - Home](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/0bfd27c6-374a-476d-90e6-df2e236a348e)


![Dashboard - LOS Comparison](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/18e3cc6f-6928-4be1-8a3d-90f8c597fc08)


![Dashboard - Cost Comparison](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/8f92e8e8-9d4e-4cb5-806a-db0ab238badf)


![Dashboard - Hospital profile ](https://github.com/Man-of-principle/Healthcare-Analysis-with-Power-BI/assets/126421029/49c3f53b-de84-470b-974f-fc4c1459c16c)
