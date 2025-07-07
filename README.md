# DATA SCIENCE: OUTLIER DETECTION APP
---
## FLASK & PYTHON: An Overview

This document provides a step-by-step explanation of the functionalities implemented in the application, focusing on outlier detection, statistical analysis, and data cleaning using Winsorization.

---
## Table of Contents
- [Introduction](#introduction)
- [Technologies and Libraries Used](#technologies-and-libraries-used)
- [NORMAL DISTRIBUTION, RULE OF 68-95: Outlier Detection and Analysis (Home Page)](#normal-distribution-rule-of-68-95-outlier-detection-and-analysis-home-page)
  - [Data Loading and Basic Statistics](#data-loading-and-basic-statistics)
  - [Empirical Rule Interpretation](#empirical-rule-interpretation)
  - [Probability Density Function (PDF) Plot and Outlier Identification](#probability-density-function-pdf-plot-and-outlier-identification)
- [DATA CLEANING: WINSORIZATION RULE OF PERCENTILE (Cleaned Data Page)](#data-cleaning-winsorization-rule-of-percentile-cleaned-data-page)
  - [Dataset Preparation](#dataset-preparation)
  - [Winsorization Process](#winsorization-process)
- [Conclusion](#conclusion)

---
## Introduction
This application provides a comprehensive tool for understanding and managing outliers in a dataset. It offers visual and statistical insights into data distribution on the home page and demonstrates a practical method for data cleaning through Winsorization on a dedicated page.

---
## Technologies and Libraries Used
This application leverages the following Python libraries and frameworks to provide its functionality:

* **Flask**: A micro web framework for Python, used to build the web application and handle routing.
* **Pandas**: A powerful data manipulation and analysis library, used for loading and processing the dataset (`outlier.csv` and `dataset.csv`).
* **NumPy**: A fundamental package for scientific computing with Python, used for numerical operations, array manipulation, and statistical calculations (e.g., `np.percentile`, `np.clip`).
* **SciPy** (`scipy.stats`): A library for scientific and technical computing, specifically `norm` for normal distribution calculations (PDF) and `sem` for standard error of the mean, and `zscore` for Z-score calculation.
* **Plotly Graph Objects** (`plotly.graph_objs`): A graphing library for creating interactive, publication-quality graphs. Used to generate the Probability Density Function (PDF) plot.
* **Plotly I/O** (`plotly.io`): Used to convert Plotly figures into HTML for embedding in web pages.
* **OS Module**: Provides a way of using operating system dependent functionality, used here to check for file existence (`os.path.exists`).

---
## NORMAL DISTRIBUTION, RULE OF 68-95: Outlier Detection and Analysis (Home Page)
The home page of the application is designed to provide an overview of the dataset's statistical properties and identify potential outliers.

### Data Loading and Basic Statistics
The application first loads the dataset, which is expected to contain an 'age' column. Upon loading, it calculates fundamental statistical measures for the 'age' column:

* **Mean Age**: The average age of individuals in the dataset.
* **Standard Deviation**: A measure of the dispersion or spread of age values around the mean.
* **Standard Error**: An estimate of how much the sample mean is likely to vary from the population mean.

### Empirical Rule Interpretation
The application then applies the **Empirical Rule** (also known as the 68-95-99.7 rule) to the 'age' data. This rule states that for a normal distribution:

* Approximately **68%** of the data falls within one standard deviation ($\pm1\sigma$) of the mean.
* Approximately **95%** of the data falls within two standard deviations ($\pm2\sigma$) of the mean.
* Approximately **99.7%** of the data falls within three standard deviations ($\pm3\sigma$) of the mean.

Based on the calculated standard deviation, the application provides a qualitative interpretation of the data's spread:

* If the standard deviation is less than 5, most age values are considered close to the mean.
* If it's between 5 and 10, there's a moderate spread.
* If it's greater than 10, age values are widely spread out.

### Probability Density Function (PDF) Plot and Outlier Identification
A **Probability Density Function (PDF)** plot, representing a normal distribution, is generated for the 'age' data. This plot visually illustrates the distribution of ages.
Simultaneously, outliers are identified using the **Z-score method**. A Z-score measures how many standard deviations an element is from the mean. Values with a Z-score greater than 3 or less than -3 are typically considered outliers, indicating they are significantly far from the average. These identified outliers are marked on the PDF plot for visual emphasis and also listed in a separate table.
All these statistical insights and the generated plot are then displayed on the home page via the `index.html` template.

---
## DATA CLEANING: WINSORIZATION RULE OF PERCENTILE (Cleaned Data Page)
The "Cleaned Data" page focuses on treating outliers using the **Winsorization** method.

### Dataset Preparation
Before applying Winsorization, the application ensures the dataset is available. If a `dataset.csv` file is not found, a dummy dataset is created for demonstration purposes. This dummy dataset includes a mix of typical age values and some intentionally placed low and high outliers. The application then loads this dataset, checking specifically for the 'age' column.

### Winsorization Process
**Winsorization** is a robust statistical method that limits the effect of extreme outliers without completely removing them. Instead, it replaces the extreme values with values at a specified percentile. In this application, a **5% Winsorization** is applied, meaning:

* Values below the **5th percentile** are replaced with the value of the 5th percentile itself.
* Values above the **95th percentile** are replaced with the value of the 95th percentile itself.

This process helps to reduce the impact of extreme values on statistical analyses while preserving the overall shape and distribution of the data more effectively than simply removing them.
The original 'age' values and their corresponding 'winsorized_age' values are then prepared and displayed in a table on the `clean_data.html` template, allowing for a direct comparison of the data before and after Winsorization.

---
## Conclusion
This application provides a comprehensive tool for understanding and managing outliers in a dataset. It offers visual and statistical insights into data distribution on the home page and demonstrates a practical method for data cleaning through Winsorization on a dedicated page.
