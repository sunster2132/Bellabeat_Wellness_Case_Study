# Bellabeat_Wellness_Case_Study
Google Data Analytics Capstone Project
## Description

For the Google Data Analytics Capstone Project, Google provided real-life scenarios and public data sets. In this case study, I am analyzing smart device fitness data for a company called: Bellabeat. They are a high-tech manufacturer of health-focused products for women. I primarily use R programming language and RStudio to make data-driven recommendations for advertising direction for the company.

## Business Task

Urška Sršen is Bellabeat's co-founder and COO. She has asked the marketing analysis team to identify trends in consumers' smart device usage to lead Bellabeat's marketing strategies for their products. My individual task was to focus on *Spring*, a water bottle that tracks daily water intake using smart technology. In doing so, I analyzed consumers' smart device usage from FitBit to gain insight into exactly how people are using their smart devices and how Bellabeat can apply to this to *Spring*.

## Data Sources Used
As previously mentioned, I will be using provided public data sets by the course. This is specially from a FitBit database of consumers who wore their device. It contains daily, hourly, and minute outputs for physical activities, heart rate, and sleep monitoring.
```{r}
#import data

library(tidyverse)
library(readr)

Daily_Activites <- read_csv("dailyActivity_merged.csv")
Daily_Calories <- read_csv("dailyCalories_merged.csv")
Hourly_Calories <- read_csv("hourlyCalories_merged.csv")
Minute_Calories_Narrow <- read_csv("minuteCaloriesNarrow_merged.csv")
Minute_Calories_Wide <- read_csv("minuteCaloriesWide_merged.csv")
Daily_Intensities <- read_csv("dailyIntensities_merged.csv")
Hourly_Intensities <- read_csv("hourlyIntensities_merged.csv")
Minute_Intensities_Narrow <- read_csv("minuteIntensitiesNarrow_merged.csv")
Minute_Intensities_Wide <- read.csv("minuteIntensitiesWide_merged.csv")
Daily_Steps <- read_csv("dailySteps_merged.csv")
Hourly_Steps <- read_csv("hourlySteps_merged.csv")
Minute_Steps_Narrow <- read_csv("minuteStepsNarrow_merged.csv")
Minute_Steps_Wide <- read_csv("minuteStepsWide_merged.csv")
Heart_Rate_secs <- read_csv("heartrate_seconds_merged.csv")
Days_of_Sleep <- read_csv("sleepDay_merged.csv")
Sleep_Mins <- read_csv("minuteSleep_merged.csv")
Weight <- read_csv("weightLogInfo_merged.csv")
Minute_METS_Narrow <-read_csv("minuteMETsNarrow_merged.csv")
```

## Data Cleaning & Manipulation

Step 1: I got an overview of each daily category to get insight on what kind of data I am working with.
```{r}
library(dplyr)
library(lubridate)

View(Daily_Activites)
View(Daily_Calories)
View(Daily_Intensities)
View(Daily_Steps)
View(Days_of_Sleep)
View(Weight)
View(Minute_METS_Narrow)
```
Step 2: I will make a short summary of Daily Calories, Daily Steps, and Days of Sleep for each individual. Each summary will include average, minimum, and max.
```{r}
# Calories
Individual_Daily_Calories_Summary <-
  Daily_Calories %>%
  group_by(Id) %>%
  summarise(average_daily_calories = mean(Calories),
            min_daily_calories = min(Calories),
            max_daily_calories = max(Calories))
head (Individual_Daily_Calories_Summary)

# Steps
Individual_Daily_Steps_Summary <-
  Daily_Steps %>%
  group_by(Id) %>%
  summarise(average_daily_steps = mean(StepTotal),
            min_daily_steps = min(StepTotal),
            max_daily_steps = max(StepTotal))
head (Individual_Daily_Steps_Summary)

# Sleep
Individual_Daily_Sleep_Summary <-
  Days_of_Sleep %>%
  group_by(Id) %>%
  summarise(average_daily_sleep = mean(TotalMinutesAsleep),
            average_time_in_bed = mean(TotalTimeInBed),
            min_daily_sleep = min(TotalMinutesAsleep),
            min_daily_time_in_bed = min(TotalTimeInBed),
            max_daily_sleep = max(TotalMinutesAsleep),
            max_daily_time_in_bed = max(TotalTimeInBed))
head (Individual_Daily_Sleep_Summary)
```

## Data Visualizations & Key Findings
```{r}
library(ggplot2)

ggplot(data = Individual_Daily_Sleep_Summary) +
  geom_smooth(mapping = aes(x = Id, y = average_daily_sleep)) +
  labs(title = "Average Daily Sleep Per Person")

ggplot(data = Individual_Daily_Sleep_Summary) +
  geom_line(mapping = aes(x = Id, y = average_daily_sleep)) +
  geom_line(mapping = aes(x = Id, y = average_time_in_bed),color = "blue") +
  labs(title = "Average Daily Sleep Vs. Actual Time In Bed",
       subtitle = "comparision between recorded sleep time and time in bed (ex: laying around)",
       x = "ID of each person",
       y = "Time (mins)") +
  guides( color = guide_legend( title = "legend"))



```

## Reccomendations Based on Analysis
So, based on my analysis consumers do not log their every move using the FitBit. However, when they go to sleep it shows that within a few minutes, the consumer falls asleep. This has proven Fitbit to be accurate. Going forward, my recommendation for Bellabeat is that in their marketing campaign they should focus on their products accuracy at identifying sleep patterns and other health information.
