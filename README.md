# Exploratory Data Analysis of IQ, Life Expectancy, Population Density, and More
Author
Daniel Hernandez
Date: October 9, 2024

## Project Overview

This project performs an **Exploratory Data Analysis (EDA)** on multiple datasets related to various socio-economic factors such as **IQ**, **life expectancy**, **population density**, and **quality of life**. The goal is to analyze these datasets, clean the data, handle missing values, and explore relationships between the variables using statistical summaries and visualizations.

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

