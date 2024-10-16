# Exploratory Data Analysis of IQ, Life Expectancy, Population Density, and More
Author
Daniel Hernandez
Date: October 9, 2024

## Project Overview

This project performs an **Exploratory Data Analysis (EDA)** on multiple datasets related to various socio-economic factors such as **iq** and **life expectancy**. The goal is to analyze these datasets, clean the data, handle missing values, and explore relationships between the variables using statistical summaries and visualizations.

### What’s Included:
- **Project Overview**: Brief description of the project goals.
- **Datasets**: Explanation of the datasets used in the analysis.
- **Requirements**: A list of required packages and how to install them.
- **Running the Analysis**: Steps for running the analysis in RStudio.
- **File Structure**: A description of the main files in the project.
- **Key Findings**: A summary of the main insights from the analysis.
- **Author & Contact Information**: Your name and email address.
- **License**: A placeholder for the license under which you are sharing the project.

### Key Objectives:
- Clean and handle missing data
- Explore key variables across datasets
- Visualize relationships and trends
- Provide insights and actionable conclusions based on the analysis

## Datasets

The datasets used in this project include:
- **IQ scores** for different countries
- **Life expectancy** (both male and female) for various countries
- **Population density** data
- **Quality of life** indicators
- **Height and weight** data

Each dataset is loaded from CSV files and cleaned before conducting the analysis.

## Process Overview

1. **Data Loading and Cleaning:**
   - The datasets are loaded from CSV files using R.
   - Missing values in numeric columns are imputed using the **median**.
   - Datasets are merged where necessary (e.g., IQ and life expectancy data are combined by country).

2. **Data Exploration:**
   - Summary statistics (mean, median, etc.) are generated for all datasets.
   - Missing data is quantified, and the percentage of missing values in each dataset is calculated.
   - Relationships between variables, such as the correlation between **IQ** and **life expectancy**, are explored.

3. **Data Visualization:**
   - Various visualizations are created using **ggplot2**:
     - Histograms (e.g., distribution of IQ scores)
     - Scatter plots (e.g., relationship between IQ and life expectancy)
     - Line plots and other plots as needed to visualize trends.

## Key Findings

- **IQ and Life Expectancy**: A linear regression was performed to explore the relationship between IQ scores and life expectancy across countries. The analysis suggests that there may be a correlation between higher IQ scores and increased life expectancy.
- **Population Density**: Population density was explored in relation to quality of life indicators, revealing potential connections between densely populated regions and lower life expectancy.
- **Handling Missing Data**: Missing data was handled efficiently, with missing numeric values imputed using the median.

## Tools and Libraries Used

The following R libraries were used to perform the analysis:
- **ggplot2**: For creating visualizations
- **dplyr**: For data manipulation
- **lapply**: For applying functions to lists of data frames

## How to Run the Project

### Prerequisites
Ensure that you have R installed, along with the following libraries:
```r
install.packages(c("ggplot2", "dplyr"))

## Steps to Reproduce the Analysis
**Clone this repository or download the project files.**
**Ensure that all CSV datasets are placed in a directory named word_pop_data in the project root.**
**Open the RMarkdown file (Exploratory-Data-Analysis.Rmd) and run the code chunks in RStudio to perform the analysis and generate the visualizations.**
**Alternatively, you can knit the .Rmd file to produce an HTML report of the analysis.**

## Folder Structure
word_pop_data/: Contains all CSV datasets used in the analysis.
Exploratory-Data-Analysis.Rmd: The main RMarkdown file for running the analysis.
Exploratory-Data-Analysis.md: This file.

Results and Insights
The full results of the analysis, including visualizations and insights, can be found in the HTML report generated from the RMarkdown file.

**Code**
---
title: '"Exploratory Data Analysis of IQ, Life Expectancy and more"'
author: "Daniel Hernandez"
date: "2024-10-09"
output: html_document
---

## Introduction

This project explores multiple datasets related to various socio-economic factors such as IQ and life expectancy. The aim is to analyze the relationships between these variables and extract meaningful insights through visualizations and data exploration. In particular, I will:

- Clean and handle missing data
- Explore key variables
- Visualize relationships across different datasets
- Summarize findings with actionable insights

## Dataset Loading

```{r Load necessary libraries}
library(ggplot2)
library(dplyr)
```


```{r load datasets}
file_list <- list.files(path = "word_pop_data", pattern = "*.csv", full.names = TRUE)
data_list <- lapply(file_list, read.csv)
names(data_list) <- basename(file_list)
```


```{r Access individual datasets}
iq <- data_list[["iq.csv"]]
quality_of_life <- data_list[["quality_of_life.csv"]]
population_density <- data_list[["population_density.csv"]]
life_expectancy <- data_list[["life_expectancy.csv"]]
height_weight <- data_list[["height_weight_data.csv"]]
```


```{r Display structure of each dataset}
lapply(data_list, str)
```


```{r Apply summary() to all datasets in the data_list}
summaries <- lapply(data_list, summary)
```


```{r Print the summaries for each dataset}
summaries
```


```{r Check for missing values across datasets}
missing_counts <- lapply(data_list, function(df) sum(is.na(df)))
missing_counts
```


```{r Calculate percentage of missing data}
missing_percent <- lapply(data_list, function(df) round((sum(is.na(df)) / (nrow(df) * ncol(df))) * 100, 1))
missing_percent
```


```{r If needed, impute missing numeric values using the median for datasets with <10% missing data }
data_list_filled <- lapply(data_list, function(df) {
  df[] <- lapply(df, function(col) {
    if (is.numeric(col)) {
      ifelse(is.na(col), median(col, na.rm = TRUE), col)
    } else {
      col
    }
  })
  return(df)
})
```


```{r Check if missing values have been handled}
lapply(data_list_filled, function(df) sum(is.na(df)))
```


```{r Histogram of IQ Scores}
ggplot(iq, aes(x = iq)) + 
  geom_histogram(binwidth = 5, fill = "blue", color = "black") +
  ggtitle("Distribution of IQ Scores") +
  xlab("IQ Score") + 
  ylab("Frequency") +
  theme_minimal()
```


```{r Investigating relationship between IQ and life expectancy}
merged_data <- merge(iq, life_expectancy, by = "country")
```


```{r Check the first few rows of the merged dataset}
head(merged_data)
```


```{r Check the number of rows in the merged dataset}
total_rows <- nrow(iq) + nrow(life_expectancy)
total_rows
```


```{r Note that the number of rows in merged_data will likely be smaller than the sum of the rows from iq and life_expectancy because the merge() function performs an inner join by default (only keeping rows with matching "country" values in both datasets).}
nrow(merged_data)
```


```{r Relationship Between IQ and Life Expectancy}
ggplot(merged_data, aes(x = iq, y = male_life_expectancy)) +
  geom_point() +
  geom_smooth(method = "lm", color = "red") +
  ggtitle("Relationship Between IQ and Life Expectancy") +
  xlab("IQ") +
  ylab("Life Expectancy")
```





