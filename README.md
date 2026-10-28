# Yelp Big Data Analytics & Predictive Modelling

## Project Overview

This project presents an end-to-end big data analytics and predictive modelling case study using the **Yelp Open Dataset**.

It focuses on understanding business performance, customer engagement, customer check-in behaviour, seasonal demand patterns, and the relationship between business reputation and foot traffic.

The project combines **Python, PySpark, Spark SQL, machine learning, Apache Kafka streaming concepts, and Tableau dashboards** to transform large-scale data into actionable business insights.

**Project Type:** Big Data Analytics & Business Intelligence  
**Dataset:** Yelp Open Dataset  
**Development Environment:** Google Colab  
**Primary Technologies:** Python, PySpark, Spark SQL, Tableau  
**Machine Learning:** PySpark MLlib  
**Streaming:** Apache Kafka and Spark Structured Streaming demonstration  
**Project Status:** Academic analytics and predictive modelling project

---

## 1. Business Problem

Businesses need to understand customer behaviour to make better decisions about staffing, marketing, operational capacity, service quality, and customer engagement.

Customer ratings and reviews provide information about perceived service quality, while check-in activity provides insights into actual customer engagement and demand patterns.

However, analysing large datasets presents challenges relating to data quality, scale, complex data formats, and identifying meaningful relationships.

This project investigates how business information and customer check-in data can be processed, analysed, modelled, and visualized to support evidence-based decisions.

## 2. Project Objectives

The objectives were to:

- Clean and preprocess large-scale Yelp datasets using PySpark.
- Convert raw JSON files into structured CSV datasets.
- Perform descriptive analytics using Spark DataFrames and SQL.
- Analyse business categories, locations, ratings, and review counts.
- Identify customer check-in patterns and demand seasonality.
- Engineer time-based features for predictive modelling.
- Develop machine learning models using PySpark MLlib.
- Explore publish-subscribe streaming through Apache Kafka.
- Build Tableau dashboards for business intelligence reporting.
- Evaluate data quality, model performance, limitations, and ethical considerations.

---

## 3. Technologies and Tools

| Technology | Purpose |
|---|---|
| Python | Data processing, analysis, and streaming logic |
| PySpark | Distributed-style data processing and transformation |
| Spark SQL | Structured querying and business analysis |
| PySpark MLlib | Classification and regression modelling |
| Apache Kafka | Producer-consumer streaming demonstration |
| Spark Structured Streaming | Processing simulated incoming check-in events |
| Tableau | Interactive business intelligence dashboards |
| Pandas | Supporting data manipulation |
| Matplotlib | Analytical charts and model evaluation |
| Google Colab | Cloud-based notebook execution |
| Google Drive | Dataset storage during development |

The work was developed primarily in Google Colab rather than on a production Spark cluster.

---

## 4. Dataset

The project uses the Yelp Open Dataset, a public research dataset containing information about businesses, customer reviews, users, tips, and check-in activity.

**Dataset source:** [Yelp Open Dataset on Kaggle](https://www.kaggle.com/datasets/yelp-dataset/yelp-dataset)

### Selected Datasets

**Business Dataset**

Contains information including:

- Business identifiers
- Business names
- Cities and states
- Categories
- Operating status
- Average star ratings
- Review counts
- Geographic information

**Check-in Dataset**

Contains:

- Business identifiers
- Timestamped check-in activity
- Customer visit patterns
- Temporal demand information

These datasets were selected to examine business reputation and customer engagement.

The original large datasets are not redistributed in this repository. Users should obtain them from the source in accordance with the dataset's terms.

---

## 5. Data Processing Pipeline

The project follows a structured data analytics workflow.

**Raw Yelp JSON → CSV Conversion → PySpark Ingestion → Data Cleaning → Feature Engineering → Spark SQL Analysis → Predictive Modelling → Tableau Visualization**

### 5.1 Data Ingestion

Raw Yelp datasets were imported into Google Colab from Google Drive and loaded into Spark DataFrames.

### 5.2 Data Cleaning

The business and check-in datasets were processed through:

- Duplicate record removal
- Null value handling
- Data type correction
- Column normalization
- Invalid record filtering
- Timestamp parsing
- Outlier handling
- Data validation

### 5.3 Feature Engineering

The analysis generated features including:

- Primary business category
- Business operating status
- Check-in date
- Day of the week
- Hour of the day
- Weekend indicators
- Daily check-in totals
- Lag features
- Rolling averages
- High-traffic indicators

These features supported descriptive analysis, business segmentation, and machine learning.

---

## 6. Descriptive Analytics

### 6.1 Business Analysis

The business analysis examines:

- Total number of businesses
- Open and closed business proportions
- Distribution of star ratings
- Review count distributions
- Businesses by city and state
- Leading business categories
- Relationships between review counts and ratings

### 6.2 Customer Check-in Analysis

The check-in analysis examines:

- Overall customer check-in activity
- Daily and weekly demand patterns
- Peak demand periods
- Weekend versus weekday behaviour
- Hourly check-in intensity
- Monthly seasonality
- Top businesses by check-in volume
- Historical footfall trends

### 6.3 Combined Business and Check-in Analysis

Business characteristics were joined with check-in activity to investigate:

- High-traffic businesses
- Highly rated businesses with relatively low traffic
- Businesses with high traffic but low ratings
- Category-level demand
- Business operating status and customer ratings
- Weekly demand persistence

---

## 7. Spark SQL Analysis

Spark SQL was used to analyse business and check-in data.

The queries explore:

1. Business concentration by state.
2. Top businesses by check-in volume.
3. Weekend-driven business activity.
4. Peak check-in hours.
5. High-traffic but low-rated businesses.
6. Highly rated but low-traffic businesses.
7. Categories with the strongest customer engagement.
8. Differences between open and closed businesses.

The analysis also demonstrates data normalization, temporary views, aggregations, ranking, and joins.

**Notebook:** [SQL_Analysis.ipynb](notebooks/SQL_Analysis.ipynb)

---

## 8. Predictive Analytics and Machine Learning

The project uses PySpark MLlib for classification and regression.

### 8.1 Business Predictive Analysis

#### Logistic Regression — High Business Ratings

A Logistic Regression model was used to classify whether a business has a high rating of four stars or above.

Reported performance:

- ROC-AUC: approximately 0.68
- F1 score: approximately 0.63

These results indicate moderate predictive ability. Business characteristics provide some useful signals, but they do not fully explain customer ratings.

#### Random Forest Regression — Review Counts

A Random Forest regression model was used to predict review counts on a transformed scale.

Reported performance:

- R²: approximately 0.43
- RMSE: approximately 0.66

The model captures some engagement patterns but has difficulty predicting businesses with exceptionally high review counts.

**Notebook:** [Business_Predictive.ipynb](notebooks/Business_Predictive.ipynb)

### 8.2 Check-in Predictive Analysis

#### Logistic Regression — High-Traffic Days

A classification model was developed to identify high-traffic days using temporal features.

The project applied a time-based training and testing split.

Reported performance:

- ROC-AUC: approximately 0.99
- Accuracy: approximately 0.992

These results are from the academic experiment and should not be interpreted as evidence of performance on new real-world data.

#### Gradient Boosted Trees — Check-in Volume

A Gradient Boosted Tree regression model was used to predict check-in volume using temporal and historical demand features.

Reported performance:

- R²: approximately 0.71
- RMSE: approximately 0.29 on the transformed scale

The model captured broad demand patterns while showing greater uncertainty during lower-demand periods.

**Notebook:** [Checkin_Predictive.ipynb](notebooks/Checkin_Predictive.ipynb)

---

## 9. Streaming Demonstration

The project includes an Apache Kafka and PySpark Structured Streaming notebook illustrating a publish-subscribe architecture for customer check-in events.

### Proposed Workflow

1. A customer check-in is represented as an event.
2. A Python producer publishes the event to a Kafka topic.
3. Kafka provides the message transport.
4. A Spark Structured Streaming consumer subscribes to the topic.
5. Incoming events are analysed using windowed aggregations.
6. High-traffic indicators and other metrics are produced.

The notebook demonstrates:

- Kafka broker and topic setup
- Event publishing using a Python producer
- Structured Streaming consumption
- Windowed check-in aggregations
- Weekday and hour intensity analysis
- High-traffic flag generation

**Notebook:** [Kafka.ipynb](notebooks/Kafka.ipynb)

This represents a local streaming demonstration and not a production-deployed Kafka system.

---

## 10. Tableau Dashboards

Three dashboards were developed to communicate findings from the processed data.

### Dashboard 1 — Business Overview

Provides insights into business locations, categories, ratings, review counts, and operating status.

![Business Overview Dashboard](dashboards/business-overview.png)

### Dashboard 2 — Footfall Dynamics

Displays customer check-in patterns, historical trends, weekday and weekend variation, peak activity periods, and seasonality.

![Footfall Dynamics Dashboard](dashboards/footfall-dynamics.png)

### Dashboard 3 — Quality Traffic Signals

Explores the relationship between customer engagement, business reputation, traffic intensity, rating distributions, and operating status.

![Quality Traffic Signals Dashboard](dashboards/quality-traffic-signals.png)

The dashboards support both exploratory analytics and explanatory reporting.

---

## 11. Key Findings

The academic analysis identified the following patterns.

### Business Characteristics

- The cleaned business dataset contained approximately 150,000 business records.
- Around 80% of businesses were identified as operating.
- The average business rating was approximately 3.6 stars.
- Business activity was concentrated in major urban areas.
- Restaurants and other service-based businesses represented major categories.

### Customer Footfall

- The analysis covered more than 13 million check-in events.
- Weekend check-ins accounted for approximately 40% of activity.
- Customer activity followed noticeable daily, weekly, and seasonal patterns.
- Long-term activity showed a significant change around 2020.

### Business Quality and Demand

- Business popularity and average ratings were not strongly correlated.
- Around 40.5% of businesses were classified as highly rated.
- Approximately 25.8% of days were classified as high-traffic.
- Recent check-in patterns showed strong relationships with subsequent demand.

These are findings from the analysed historical dataset, not live measurements of current Yelp activity.

---

## 12. Business Recommendations

The findings suggest several possible applications.

**Demand-Aware Staffing**

Businesses can use historical footfall patterns to plan staffing and operational capacity around expected busy periods.

**Targeted Marketing**

Promotional campaigns can be aligned with seasonal demand and customer engagement patterns.

**Reputation Monitoring**

Ratings and review counts should be assessed together rather than assuming popularity indicates service quality.

**Business Performance Evaluation**

Combining reputation data and check-in activity may help identify businesses with strong customer satisfaction but relatively low visibility.

**Predictive Planning**

Time-based forecasting can support planning, although model limitations and changes in consumer behaviour must be considered.

These are analytical recommendations rather than interventions implemented in the businesses represented by the dataset.

---

## 13. Project Structure

    Yelp-Big-Data-Analytics-and-Predictive-Modelling/
    ├── notebooks/
    │   ├── Business.ipynb
    │   ├── Checkin.ipynb
    │   ├── SQL_Analysis.ipynb
    │   ├── Business_Predictive.ipynb
    │   ├── Checkin_Predictive.ipynb
    │   └── Kafka.ipynb
    ├── dashboards/
    │   ├── business-overview.png
    │   ├── footfall-dynamics.png
    │   └── quality-traffic-signals.png
    ├── docs/
    │   └── Big_Data_Analytics_Report.pdf
    ├── data/
    │   └── .gitkeep
    ├── README.md
    └── .gitignore

---

## 14. How to Explore the Project

### Prerequisites

- Python
- Google Colab or a compatible Jupyter environment
- PySpark
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Yelp business and check-in datasets
- Google Drive, if reproducing the original Colab setup

Additional dependencies may be required for individual notebooks.

### Suggested Notebook Order

1. `Business.ipynb` — Clean and analyse business data.
2. `Checkin.ipynb` — Clean and analyse check-in data.
3. `SQL_Analysis.ipynb` — Run SQL analysis on the cleaned datasets.
4. `Business_Predictive.ipynb` — Explore business prediction models.
5. `Checkin_Predictive.ipynb` — Explore customer demand prediction models.
6. `Kafka.ipynb` — Examine the streaming demonstration independently.

### Important Reproducibility Notes

The notebooks were originally developed in Google Colab and reference project-specific Google Drive paths.

To reproduce the work:

1. Download the source datasets.
2. Upload the datasets to your own storage location.
3. Adjust the input and output paths in the notebooks.
4. Install the required packages.
5. Execute the notebooks in dependency order.

The Kafka notebook also requires a compatible Java, Kafka, and Spark streaming environment.

The notebooks are provided as academic source artefacts and are not packaged as a one-click production pipeline.

---

## 15. Skills Demonstrated

### Data Engineering

- Big Data Processing
- PySpark DataFrames
- JSON and CSV Processing
- Data Cleaning and Transformation
- Data Quality Assessment
- Feature Engineering
- Data Aggregation
- Apache Kafka Concepts
- Spark Structured Streaming

### Data Analytics and Business Intelligence

- Exploratory Data Analysis
- Descriptive Statistics
- Spark SQL
- Customer Behaviour Analysis
- Business Performance Analysis
- Tableau Dashboard Development
- Data Visualization
- KPI Reporting
- Evidence-Based Business Recommendations

### Machine Learning

- Predictive Modelling
- Logistic Regression
- Random Forest Regression
- Gradient Boosted Trees
- Classification and Regression Evaluation
- ROC Curves and Confusion Matrices
- Precision, Recall and F1 Score
- R² and RMSE
- Time-Based Train/Test Splitting

---

## 16. Project Documentation

The accompanying academic report presents the business problem, methodology, data cleaning, SQL analysis, predictive modelling, visualization approach, findings, and critical evaluation.

[View Complete Big Data Analytics Report](docs/Big_Data_Analytics_Report.pdf)

---

## 17. Limitations and Future Improvements

The project has several limitations:

- The analysis uses historical Yelp data rather than live business activity.
- Data quality and platform participation can affect representativeness.
- The project was executed in Google Colab rather than on a production distributed cluster.
- Machine learning performance varies considerably between tasks.
- The Kafka demonstration is not a production streaming deployment.
- The existing notebooks require environment-specific path configuration.
- Model predictions may be affected by changes in customer behaviour over time.

Potential improvements include automated data ingestion, improved reproducibility, external validation, richer predictive features, and production-oriented streaming infrastructure.

---

## 18. Academic Context

This project was developed for **CC6058ES – Big Data and Visualisation** as part of an academic assessment.

It demonstrates practical application of big data processing, exploratory analytics, predictive modelling, SQL-based analysis, streaming concepts, and business intelligence reporting.

## Disclaimer

This repository is an academic data analytics and visualization project.

The model metrics and findings represent results documented in the coursework and are not guarantees of real-world predictive accuracy. The repository does not represent a production-deployed analytics platform or live Yelp monitoring service.

Yelp data remains subject to the original dataset provider's applicable terms and licensing conditions.
