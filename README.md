# Google Data Analytics Capstone Project
# Case Study 2: How Can a Wellness Technology Company Play It Smart?

## 1. Introduction

As part of the Google Data Analytics Program, I am tasked with completing a Capstone case study. The following information is part of the "Share" section of the project in which I present my findings to the stakeholders. I will be presenting the high-level information of each section's deliverable.

The complete project, with code and analysis, can be found in the "capstone_project.Rmd" file.

I have chosen to do this project in R because the dataset file size is too large to comfortably work in spreadsheets (Excel/Google Sheets). This project can be done in SQL, but R has many handy packages such as tidyverse for data cleaning and analysis.

![](Presentation_Pictures\bellabeat_logo.png)

## 2. Overview of Bellabeat and Objectives

Hello, I'm Brandon Luong, and I am part of the marketing analytics team at Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a small successful company but has the potential for growth in the global smart device market. Urška Sršen believes that analyzing smart fitness data could help with this growth and unlock new opportunities for the company.

Bellabeat Mission Statement: Empower women with knowledge about their own health and habits by collecting data on activity, sleep, stress, and reproductive health.

The Bellabeat Products:

- Bellabeat app: The Bellabeat app provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
- Leaf: Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
- Time: This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
- Spring: This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.

Primary stakeholders:

- Urška Sršen: Cofounder and Chief Creative Officer
- Sando Mur: Cofounder and key member of the Bellabeat executive team

Secondary stakeholders:

- Bellabeat marketing analytics team: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy.

There are 3 main questions I want to answer in this analysis:

1. What are some trends in smart device usage?
2. How could these trends apply to Bellabeat customers?
3. How could these trends help influence Bellabeat marketing strategy?

**Business Task: Analyze smart device usage data for trends and insights and apply the new-found knowledge to one Bellabeat product, presenting high-level recommendations for how these trends can improve Bellabeat's marketing strategy.**

## 3. Data Inspection

The dataset can be found on Kaggle: [Fitbit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit "Fitbit Fitness Tracker Data"), by Mobius under the CC0: Public Domain license.

It contains 18 csv files, 3 in wide format, rest in long:

- Data kept for analysis:

  - 'dailyActivity_merged.csv' as `daily_act`
  - 'sleepDay_merged.csv' as `daily_sleep`
  
- Data dropped from analysis:
  - 'dailyCalories_merged.csv'
  - 'dailyIntensities_merged.csv'
  - 'dailySteps_merged.csv'
  - 'hourlyCalories_merged.csv'
  - 'hourlyIntensities_merged.csv'
  - 'hourlySteps_merged.csv'
  - 'minuteCaloriesNarrow_merged.csv'
  - 'minuteCaloriesWide_merged.csv'
  - 'minuteIntensitiesNarrow_merged.csv'
  - 'minuteIntensitiesWide_merged.csv'
  - 'minuteStepsNarrow_merged.csv'
  - 'minuteStepsWide_merged.csv'
  - 'minuteSleep_merged.csv'
  - 'minuteMETsNarrow_merged.csv'
  - 'heartrate_seconds_merged.csv'
  - 'weightLogInfo.csv'
  
**Credibility: Poor**

- Not reliable. Data is severely incomplete and missing information such that it is not representative of the population.
- Not original. Data source is from a third-party user (not from Fitbit, government, or academic source).
- Somewhat comprehensive. There is enough variety of data to gain some insights in order to give recommendations to Bellabeat but with low confidence.
- Not current. Data collected from April 12, 2016 - May 12, 2016 - 5 years old.
- Has citation. Data was gathered via an Amazon survey from 30 consented Fitbit users. Hosted on Kaggle with usability of 10.0, meeting all of Kaggle's uploading requirements.

## 4. Data Cleaning

- Used tidyverse (dplyr), janitor, lubridate, and skimr packages.
- Converted all column names from pascal case to camel case.
- Renamed 'activity_date' and 'sleep_day' columns in `daily_act` and `daily_sleep`, respectively, to 'date'.
- Converted 'date' columns in `daily_act` and `daily_sleep` from character (string) data type to date data type.

- `daily_act` has no missing (NA) values.
- `daily_sleep` has no missing (NA) values.

- Merged `daily_act` and `daily_sleep` into `merged_df` using an inner join.

## 5. Analysis

Drop columns:

- tracker_distance
  - Identical to total_distance, except for 3 rows (0.7% difference).
- logged_activities_distance
  - 95% of values equal 0.
  - Remaining values recorded by 2 users.
- sedentary_active_distance 
  - 98.5% of values equal 0. 
  - Sedentary (mostly sitting as opposed to walking or running) won't be covering much distance if at all.
- total_sleep_records
  - 88.8% are 1, 10% are 2, and 0.72% are 3. 
  - The majority of the observations are 1 sleep record (ie. did not wake up during the middle of the night).
  
Add columns:

- day_of_week
  - Convert date to the day of the week.
- sleep_hours
  - Convert total_minutes_asleep to hours slept.
- in_bed_hours
  - Convert total_time_in_bed to hours in bed.
  
Now to answer the first main question of the analysis:

**Main Question 1. What are some trends in smart device usage?**

Trends:

- Sunday is the least active day.
  - Lowest average steps and distance.
  - Highest average and median number of hours slept.
  - "Lazy Sunday": relax indoors.
- Saturday is the most active day.
  - Highest average steps and distance.
  - Lowest average and median number of hours slept.
  - Free time on Saturday to exercise, go out and have drinks, and socialize.
- Wednesday is the 2nd most hours slept day.
  - "Hump Day": mid-work week tiredness and slump.
- Users slept more consistently on the weekdays and less consistently on the weekends.
- Users did not have any trouble sleeping.
  - in_bed_hours about the same as sleep_hours.
- Walking burns more calories than jogging or sprinting when performed for a longer duration or farther distance.

## 6. Key Findings

![](steps_per_day.png)

![](distance_per_day.png)



Looking at "Median Steps Taken For Each Day of the Week," "Median Distance Traveled For Each Day of the Week," and "Median Calories Burned For Each Day of the Week" plots, Sundays are the least active day and Saturdays are the most active day for most users. 

Looking at "Median Hours Slept For Each Day of the Week," Wednesday is the 2nd most hours slept day of the week. Wednesday is also known as "Hump Day" a reference to a camel's hump in which Wednesday is typically the most stressful day and one has to climb this hill (hump) to get through the work week.

"Median Hours Slept For Each Day of the Week" shows that users sleep more consistently on the weekdays than on the weekends.

"Did Users Have Trouble Falling Asleep?" shows that most users fell asleep within 1 hour of being in bed. There are a couple instances in which users could not sleep for more than 1 hour but are quite few compared to those who slept within an hour.

Looking at "Calories Burned vs Distance Traveled at Various Intensities" and "Calories Burned vs Duration at Various Intensities" all 3 intensity levels initially burn calories at an increasing rate. However, jogging is shown to burn calories at a decreasing rate as the distance or duration increases. Sprinting does burn calories at an increasing rate only if it is performed for a long enough distance or duration, but that is very difficult to realistically maintain; so, sprinting should be kept at short distances and duration. Walking is the only intensity shown to burn calories at an increasing rate as the distance or duration increases.