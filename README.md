# clinical-trial-tfls-automation-r
Automated Clinical Trial TFL Generation using R
Below is a **complete project write-up structure** you can use for **GitHub, resume portfolio, or documentation**. You can copy this into **README.md or a project report**.

---

# Clinical Trial TFL Automation Using R

## 1. Abstract

Clinical trials generate large volumes of patient data that must be summarized into standardized **Tables, Listings, and Figures (TFLs)** for analysis and regulatory submission. Manual creation of these outputs is time-consuming and prone to errors.

This project develops an **automated reporting pipeline using R** that processes clinical datasets and generates key outputs including demographic summaries, laboratory statistics, adverse event tables, shift analyses, graphical visualizations, and an interactive dashboard. The system integrates multiple R packages for data manipulation, visualization, reporting, and interactive analytics.

The project demonstrates how automation can improve efficiency, reproducibility, and accuracy in clinical data analysis workflows.

---

# 2. Introduction

Clinical trials are conducted to evaluate the **safety and effectiveness of medical treatments**. During a trial, data such as patient demographics, laboratory results, and adverse events are collected.

Before results are reviewed or submitted to regulators like the U.S. Food and Drug Administration or European Medicines Agency, the data must be summarized into standardized **Tables, Listings, and Figures (TFLs)**.

Traditional clinical reporting requires significant manual programming and repetitive work. Automation using R can streamline this process.

This project focuses on building a **fully automated clinical reporting pipeline** capable of generating:

* Demographic tables
* Laboratory summary tables
* Shift analysis tables
* Adverse event summaries
* Graphical visualizations
* Interactive dashboards

The objective is to simulate real-world clinical programming tasks commonly performed in pharmaceutical and CRO organizations.

---

# 3. Objectives

The main objectives of this project are:

1. Automate the generation of clinical **Tables, Listings, and Figures (TFLs)**.
2. Perform statistical summaries of laboratory data.
3. Analyze adverse events across treatment groups.
4. Visualize clinical trial trends using graphs.
5. Develop an interactive **Shiny dashboard** for data exploration.
6. Generate formatted clinical reports automatically.

---

# 4. Tools and Technologies Used

| Tool      | Purpose                      |
| --------- | ---------------------------- |
| R         | Data analysis and automation |
| dplyr     | Data manipulation            |
| tidyr     | Data transformation          |
| ggplot2   | Data visualization           |
| flextable | Table formatting             |
| officer   | Word report generation       |
| shiny     | Interactive dashboard        |

---

# 5. Dataset Description

The project uses **simulated clinical trial datasets** representing common structures used in clinical programming.

### ADSL Dataset (Subject-Level Data)

Contains demographic and treatment information for each subject.

| Variable | Description               |
| -------- | ------------------------- |
| USUBJID  | Unique subject identifier |
| TRT01A   | Treatment group           |
| AGE      | Age of subject            |
| SEX      | Gender                    |
| RACE     | Ethnicity                 |

Example:

| USUBJID | TRT01A  | AGE | SEX |
| ------- | ------- | --- | --- |
| SUBJ01  | Placebo | 45  | M   |
| SUBJ02  | Drug A  | 50  | F   |

---

### ADLB Dataset (Laboratory Data)

Contains laboratory measurements collected during visits.

| Variable | Description     |
| -------- | --------------- |
| USUBJID  | Subject ID      |
| PARAM    | Lab parameter   |
| AVAL     | Lab value       |
| AVISIT   | Visit time      |
| TRT01A   | Treatment group |

Example:

| USUBJID | PARAM      | AVAL | AVISIT   |
| ------- | ---------- | ---- | -------- |
| SUBJ01  | Hemoglobin | 13.5 | Baseline |

---

### ADAE Dataset (Adverse Events)

Contains information about adverse events experienced during the study.

| Variable | Description        |
| -------- | ------------------ |
| USUBJID  | Subject ID         |
| AEDECOD  | Adverse event term |
| AESER    | Serious event flag |
| AESEV    | Severity           |

---

# 6. Input

The project requires three datasets:

```
ADSL.csv
ADLB.csv
ADAE.csv
```

These datasets serve as the **input for generating statistical summaries and visualizations**.

---

# 7. Methodology / Workflow

The workflow of the project includes the following steps:

1. **Load datasets**
2. **Clean and prepare data**
3. **Generate demographic summary tables**
4. **Compute laboratory statistics**
5. **Perform shift analysis**
6. **Generate adverse event tables**
7. **Create graphical visualizations**
8. **Export tables into Word report**
9. **Launch interactive dashboard**

Workflow:

```
Clinical Data
      ↓
Data Processing
      ↓
Statistical Analysis
      ↓
TFL Generation
      ↓
Report + Dashboard
```

---

# 8. Code Implementation (Example)

### Loading Data

```r
library(dplyr)
library(ggplot2)

adsl <- read.csv("ADSL.csv")
adlb <- read.csv("ADLB.csv")
adae <- read.csv("ADAE.csv")
```

---

### Demographic Table

```r
demo_table <- adsl %>%
  group_by(TRT01A) %>%
  summarise(
    N = n(),
    Mean_Age = mean(AGE),
    SD_Age = sd(AGE)
  )
```

---

### Lab Summary Table

```r
lab_summary <- adlb %>%
  group_by(TRT01A, AVISIT) %>%
  summarise(
    Mean = mean(AVAL),
    SD = sd(AVAL),
    Min = min(AVAL),
    Max = max(AVAL)
  )
```

---

### Adverse Event Table

```r
ae_table <- adae %>%
  group_by(TRT01A, AEDECOD) %>%
  summarise(
    Subjects = n_distinct(USUBJID),
    Events = n()
  )
```

---

### Lab Trend Visualization

```r
ggplot(adlb, aes(x = AVISIT, y = AVAL, group = USUBJID)) +
  geom_line() +
  geom_point() +
  facet_wrap(~TRT01A)
```

---

# 9. Output

The project generates the following outputs:

### Tables

* Demographic summary table
* Laboratory statistics table
* Shift analysis table
* Adverse event summary table

### Figures

* Laboratory trend graphs
* Treatment comparison plots

### Reports

* Word document containing formatted tables

### Dashboard

* Interactive Shiny dashboard for clinical data exploration

Example outputs:

* Clinical report (DOCX)
* Lab trend figure (PNG)
* Interactive dashboard

---

# 10. Advantages of the Project

* Automates clinical reporting
* Reduces manual errors
* Improves efficiency
* Provides interactive visualizations
* Demonstrates real clinical programming workflow

---

# 11. Limitations

* Uses simulated data
* Simplified statistical analysis
* Not fully CDISC-compliant
* Requires adaptation for large real datasets

---

# 12. Applications

This project can be used in:

* Clinical trial reporting
* Pharmaceutical research
* Regulatory submissions
* Clinical data analysis training

Organizations performing such work include:

* IQVIA
* Parexel
* Syneos Health

---

# 13. Conclusion

This project demonstrates how **R programming can automate the generation of clinical trial Tables, Listings, and Figures**. The automated pipeline improves efficiency and ensures reproducibility in clinical data analysis.




