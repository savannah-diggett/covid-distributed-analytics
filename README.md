# Distributed COVID-19 Analytics with Spark and Bigtable

## Project Overview

This project analyzes global COVID-19 pandemic data using distributed computing tools on Google Cloud Platform. The analysis progresses from low-level distributed processing with **Spark RDDs**, to structured analytics using **Spark DataFrames and Spark SQL**, and finally to NoSQL data storage and querying using **Google Bigtable**.

The goal of this project is to explore pandemic trends, vaccination progress, and healthcare system pressure across countries while demonstrating how different distributed data processing frameworks support scalable analytics.

The workflow moves progressively through multiple levels of abstraction:

- Low-level distributed processing with **Spark RDDs**
- Structured analytics with **Spark DataFrames**
- SQL-style analytics with **Spark SQL**
- NoSQL storage and analytics using **Google Bigtable**

---

## Dataset

The dataset used in this project comes from **Our World in Data (OWID)** and contains global COVID-19 indicators across countries and time.

Dataset source:  
https://ourworldindata.org/coronavirus

Key variables used in the analysis include:

- `iso_code` — country identifier  
- `continent` — continent classification  
- `location` — country name  
- `date` — observation date  
- `total_cases` — cumulative confirmed cases  
- `new_cases` — daily new cases  
- `icu_patients` — number of ICU patients  
- `hosp_patients` — hospitalized patients  
- `total_vaccinations` — cumulative vaccinations  
- `new_vaccinations` — daily vaccinations  
- `population` — total population  
- `total_deaths` — cumulative deaths  

The dataset is large and time-series based, making it well suited for distributed data processing.

---

## Project Architecture

The analysis pipeline follows a multi-stage distributed computing workflow:
# Distributed COVID-19 Analytics with Spark and Bigtable

## Project Overview

This project analyzes global COVID-19 pandemic data using distributed computing tools on Google Cloud Platform. The analysis progresses from low-level distributed processing with **Spark RDDs**, to structured analytics using **Spark DataFrames and Spark SQL**, and finally to NoSQL data storage and querying using **Google Bigtable**.

The goal of this project is to explore pandemic trends, vaccination progress, and healthcare system pressure across countries while demonstrating how different distributed data processing frameworks support scalable analytics.

The workflow moves progressively through multiple levels of abstraction:

- Low-level distributed processing with **Spark RDDs**
- Structured analytics with **Spark DataFrames**
- SQL-style analytics with **Spark SQL**
- NoSQL storage and analytics using **Google Bigtable**

---

## Dataset

The dataset used in this project comes from **Our World in Data (OWID)** and contains global COVID-19 indicators across countries and time.

Dataset source:  
https://ourworldindata.org/coronavirus

Key variables used in the analysis include:

- `iso_code` — country identifier  
- `continent` — continent classification  
- `location` — country name  
- `date` — observation date  
- `total_cases` — cumulative confirmed cases  
- `new_cases` — daily new cases  
- `icu_patients` — number of ICU patients  
- `hosp_patients` — hospitalized patients  
- `total_vaccinations` — cumulative vaccinations  
- `new_vaccinations` — daily vaccinations  
- `population` — total population  
- `total_deaths` — cumulative deaths  

The dataset is large and time-series based, making it well suited for distributed data processing.

---

## Project Architecture

The analysis pipeline follows a multi-stage distributed computing workflow:

OWID COVID Dataset
↓
Spark RDD Processing
↓
Spark DataFrame Transformations
↓
Spark SQL Analytics
↓
Country-Level Summary Tables
↓
Google Bigtable Serving Layer
↓
Impact Score Analytics


Each stage introduces a higher level of abstraction for large-scale data analysis.

---

## Technologies Used

- Python  
- PySpark  
- Spark RDD API  
- Spark DataFrames  
- Spark SQL  
- Google Cloud Dataproc  
- Google Bigtable  
- Jupyter Notebook  

---

# Analysis Structure

## Part A — Spark RDD Analysis

The first part of the project uses **Spark RDDs**, focusing on low-level distributed transformations and aggregations.

Key tasks included:

- Creating a **baseline RDD** with relevant COVID indicators
- Aggregating **total confirmed cases by continent**
- Identifying the **top two countries per continent by cumulative cases**
- Computing **weekly case growth by country**
- Ranking countries by **average daily vaccination intensity**

RDDs provide full control over distributed transformations but require more manual data handling compared to higher-level APIs.

---

## Part B — Spark DataFrame Analysis

The second stage uses **Spark DataFrames**, enabling more structured analytics and optimized execution.

Tasks included:

- Loading the dataset into a **baseline Spark DataFrame**
- Computing **average ICU load per country**
- Ranking countries by **healthcare system pressure**
- Measuring **vaccination momentum relative to population size**

DataFrames provide better performance and easier analytics through schema awareness and optimized query planning.

---

## Part C — Spark SQL Analysis

In this stage, the dataset is queried using **Spark SQL**, enabling SQL-style analytics over distributed datasets.

Two key summary tables were generated.

### Pandemic Severity Summary

For each country:

- Maximum cumulative cases
- Maximum cumulative deaths
- Case fatality ratio (CFR)

Each stage introduces a higher level of abstraction for large-scale data analysis.

---

## Technologies Used

- Python  
- PySpark  
- Spark RDD API  
- Spark DataFrames  
- Spark SQL  
- Google Cloud Dataproc  
- Google Bigtable  
- Jupyter Notebook  

---

# Analysis Structure

## Part A — Spark RDD Analysis

The first part of the project uses **Spark RDDs**, focusing on low-level distributed transformations and aggregations.

Key tasks included:

- Creating a **baseline RDD** with relevant COVID indicators
- Aggregating **total confirmed cases by continent**
- Identifying the **top two countries per continent by cumulative cases**
- Computing **weekly case growth by country**
- Ranking countries by **average daily vaccination intensity**

RDDs provide full control over distributed transformations but require more manual data handling compared to higher-level APIs.

---

## Part B — Spark DataFrame Analysis

The second stage uses **Spark DataFrames**, enabling more structured analytics and optimized execution.

Tasks included:

- Loading the dataset into a **baseline Spark DataFrame**
- Computing **average ICU load per country**
- Ranking countries by **healthcare system pressure**
- Measuring **vaccination momentum relative to population size**

DataFrames provide better performance and easier analytics through schema awareness and optimized query planning.

---

## Part C — Spark SQL Analysis

In this stage, the dataset is queried using **Spark SQL**, enabling SQL-style analytics over distributed datasets.

Two key summary tables were generated.

### Pandemic Severity Summary

For each country:

- Maximum cumulative cases
- Maximum cumulative deaths
- Case fatality ratio (CFR)

  
CFR = (max total deaths / max total cases) × 100

This metric enables cross-country comparisons of pandemic severity.

---

### Health System and Vaccination Indicators

For each country:

- Average hospital patients
- Average ICU patients
- Vaccinations per 1000 people

This allows comparison of **healthcare system pressure and vaccination progress**.

---

## Part D — Bigtable NoSQL Serving Layer

The final stage stores the summary indicators in **Google Bigtable**, a distributed NoSQL database optimized for large-scale analytics.

### Bigtable Schema Design

Each row represents a **country**, with the country name used as the **row key**.

Column families:

**meta**
- continent
- population

**severity**
- max_total_cases
- max_total_deaths
- case_fatality_ratio

**health_vax**
- avg_hosp_patients
- avg_icu_patients
- vax_per_1k

The schema is **denormalized** to ensure fast single-row queries.

---

## Composite COVID Impact Score

Using the Bigtable data, a composite metric was created to rank countries by pandemic impact.

### Normalized Healthcare Burden

This metric enables cross-country comparisons of pandemic severity.

---

### Health System and Vaccination Indicators

For each country:

- Average hospital patients
- Average ICU patients
- Vaccinations per 1000 people

This allows comparison of **healthcare system pressure and vaccination progress**.

---

## Part D — Bigtable NoSQL Serving Layer

The final stage stores the summary indicators in **Google Bigtable**, a distributed NoSQL database optimized for large-scale analytics.

### Bigtable Schema Design

Each row represents a **country**, with the country name used as the **row key**.

Column families:

**meta**
- continent
- population

**severity**
- max_total_cases
- max_total_deaths
- case_fatality_ratio

**health_vax**
- avg_hosp_patients
- avg_icu_patients
- vax_per_1k

The schema is **denormalized** to ensure fast single-row queries.

---

## Composite COVID Impact Score

Using the Bigtable data, a composite metric was created to rank countries by pandemic impact.

### Normalized Healthcare Burden

This metric enables cross-country comparisons of pandemic severity.

---

### Health System and Vaccination Indicators

For each country:

- Average hospital patients
- Average ICU patients
- Vaccinations per 1000 people

This allows comparison of **healthcare system pressure and vaccination progress**.

---

## Part D — Bigtable NoSQL Serving Layer

The final stage stores the summary indicators in **Google Bigtable**, a distributed NoSQL database optimized for large-scale analytics.

### Bigtable Schema Design

Each row represents a **country**, with the country name used as the **row key**.

Column families:

**meta**
- continent
- population

**severity**
- max_total_cases
- max_total_deaths
- case_fatality_ratio

**health_vax**
- avg_hosp_patients
- avg_icu_patients
- vax_per_1k

The schema is **denormalized** to ensure fast single-row queries.

---

## Composite COVID Impact Score

Using the Bigtable data, a composite metric was created to rank countries by pandemic impact.

### Normalized Healthcare Burden
normalized_burden =
((avg_hosp_patients + avg_icu_patients) / population) × 100000


### Impact Score

impact_score = normalized_burden − (vax_per_1k / 1000)

Countries with **lower impact scores** are interpreted as having better pandemic management outcomes.

---

# Key Insights

- Countries with high vaccination rates generally showed **lower normalized healthcare burden**, though exceptions exist.
- ICU occupancy varied significantly across countries even with similar vaccination coverage.
- Case fatality ratios differed widely between countries, likely reflecting differences in healthcare capacity, demographics, and reporting practices.


# Notes

This project was implemented using **Google Cloud Dataproc** for distributed Spark processing and **Google Bigtable** for scalable NoSQL storage.

Intermediate development and prototyping were performed using Jupyter notebooks.
