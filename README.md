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



