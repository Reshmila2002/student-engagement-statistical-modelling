# Student Engagement in Online Learning: Statistical Modelling Using R

## Project Overview

This project investigates the relationship between students' online learning engagement and their academic performance. Using the **Online Learning Engagement Dataset**, the analysis applies statistical modelling techniques in R to identify factors associated with students' final grades.

The main modelling technique is **Multiple Linear Regression (MLR)**. The project also examines correlations, checks multicollinearity, compares variable-selection methods, evaluates regression assumptions, and measures predictive performance using separate training and testing datasets.

This is a group academic project completed for **STAT 31631 – Statistical Modelling** at the **University of Kelaniya, Sri Lanka**.

## Project Objectives

- Explore student characteristics, online learning activities, and academic performance.
- Investigate the relationships between online learning variables and final grades.
- Develop a Multiple Linear Regression model to explain variation in final grades.
- Identify important predictors using variable-selection techniques.
- Detect multicollinearity using Variance Inflation Factors (VIF).
- Examine regression assumptions using diagnostic plots.
- Evaluate model performance on training and unseen test data.

## Dataset

- **Dataset:** Online Learning Engagement Dataset
- **Source:** [Kaggle – Online Learning Engagement Dataset](https://www.kaggle.com/datasets/ssssws/online-learning-engagement-dataset)
- **Format used in the analysis:** CSV
- **Expected cleaned dataset:** 49,204 observations and 18 columns

The analysis script uses a cleaned version of the dataset named:

`cleaned_student_data_final.csv`

The CSV file is not included in this project archive. Download the dataset from the source above and prepare the cleaned CSV before running the analysis.

### Variables Used in the Regression Analysis

The response variable is `final_grade`. The initial full model uses the following 11 predictors:

| Variable | Description |
|---|---|
| `age` | Student age |
| `internet_speed_mbps` | Internet connection speed |
| `study_hours_weekly` | Weekly study hours |
| `login_frequency_weekly` | Number of weekly logins |
| `avg_session_duration_min` | Average session duration |
| `video_watch_time_min` | Video watch time |
| `assignments_submitted` | Number of submitted assignments |
| `forum_posts` | Number of forum posts |
| `quiz_attempts` | Number of quiz attempts |
| `avg_quiz_score` | Average quiz score |
| `attendance_rate` | Attendance rate |

The script excludes `student_id` because it is an identifier, `engagement_score` because it is a composite variable highly correlated with weekly study hours, and `gender`, `country`, `device_type`, and `dropout` from this particular MLR analysis.

## Statistical Methods

The project follows these main stages:

1. **Data preparation:** Load the cleaned CSV file, inspect its structure, select relevant variables, and check for missing values.
2. **Training and testing split:** Divide the observations into 80% training data and 20% testing data. A fixed random seed (`123`) is used for reproducibility.
3. **Correlation analysis:** Examine relationships between the response and predictors, and visualize the correlation matrix.
4. **Full Multiple Linear Regression model:** Fit an initial model using all 11 selected predictors.
5. **Multicollinearity assessment:** Calculate VIF values to identify possible multicollinearity among predictors.
6. **Best Subset Selection:** Compare candidate models using Adjusted R², Mallows' Cp, and BIC.
7. **Backward Elimination:** Evaluate models formed by progressively removing predictors.
8. **Stepwise AIC Selection:** Apply both-direction stepwise selection using the Akaike Information Criterion (AIC).
9. **Final model development:** Fit a five-predictor regression model using the variables specified in the R Markdown script.
10. **Regression diagnostics:** Use residual plots, a Normal Q-Q plot, and residuals against run order to examine model assumptions.
11. **Model evaluation:** Compare training and testing performance using R², RMSE, and MAE.
12. **Actual vs. predicted analysis:** Visualize the relationship between actual and predicted final grades on the test dataset.

## Final Regression Model

The five-predictor model specified in the analysis is:

```r
final_model <- lm(
  final_grade ~ avg_quiz_score +
    study_hours_weekly +
    assignments_submitted +
    quiz_attempts +
    video_watch_time_min,
  data = train_df
)
```

The model investigates how these five learning-related variables are associated with students' final grades.

## Tools and R Packages

- **R:** Statistical analysis and model development.
- **RStudio:** Recommended environment for running the R Markdown file.
- **Microsoft Excel:** Supporting data inspection and preparation.
- **`car`:** Variance Inflation Factor (VIF) analysis.
- **`corrplot`:** Correlation matrix visualization.
- **`leaps`:** Best Subset Selection and Backward Selection.
- **`MASS`:** Stepwise model selection using AIC.
- **`ggplot2`:** Data visualization package loaded in the analysis.
- **`Metrics`:** RMSE and MAE calculations.

## Project Structure

```text
student-engagement-statistical-modelling/
│
├── README.md
│
├── student_engagement_analysis.Rmd
│
└── STAT 31631_Group04 (1).pdf
```

- `README.md` – Project description and instructions.
- `student_engagement_analysis.Rmd` – Main R Markdown file containing the statistical analysis and model evaluation.
- `STAT 31631_Group04 (1).pdf` – Project report.

The cleaned CSV dataset is required separately and is not included in the archive.

## How to Run the Project

### 1. Install R and RStudio

Install [R](https://cran.r-project.org/) and [RStudio Desktop](https://posit.co/download/rstudio-desktop/).

### 2. Download the dataset

Download the Online Learning Engagement Dataset from [Kaggle](https://www.kaggle.com/datasets/ssssws/online-learning-engagement-dataset), prepare the cleaned dataset, and save it as:

`cleaned_student_data_final.csv`

### 3. Place the dataset in your project folder

Keep the cleaned CSV file in the project folder, or update the file path in the `read.csv()` command in `student_engagement_analysis.Rmd`.

For example, to read the CSV from the project folder, use:

```r
df <- read.csv("cleaned_student_data_final.csv")
```

**Important:** The current R Markdown file contains a machine-specific Windows path (`D:/cleaned_student_data_final.csv`). Update this path before running the project on another computer.

### 4. Install the required packages

Run the following commands in the R console. Package installation is normally needed only once.

```r
install.packages(c(
  "car",
  "corrplot",
  "leaps",
  "MASS",
  "ggplot2",
  "Metrics"
))
```

### 5. Run the analysis

1. Open `student_engagement_analysis.Rmd` in RStudio.
2. Confirm that the CSV file path is correct.
3. Run the code chunks from top to bottom, or use **Knit** to generate the report.
4. Review the model summaries, selection results, VIF values, diagnostic plots, and evaluation metrics.

## Key Findings

The existing project summary reports the following findings from the analysed dataset:

- Average quiz score was the strongest predictor in the selected regression model.
- Weekly study hours, assignments submitted, quiz attempts, and video watch time were also positively associated with final grades.
- The selected five-predictor model explained approximately **69.13%** of the variation in final grades in the analysed dataset.
- Regression diagnostics and test-set performance metrics were used to assess the model.

These findings describe relationships observed in the dataset. They do not, by themselves, establish that the learning activities cause changes in final grades.

## Model Evaluation Metrics

| Metric | Purpose | Preferred result |
|---|---|---|
| R² | Measures the proportion of variation in final grades explained by the model | Higher |
| RMSE | Measures the typical size of prediction errors, with larger errors penalized more heavily | Lower |
| MAE | Measures the average absolute prediction error | Lower |

Training and testing results are compared to assess how well the model performs on observations that were not used to fit it.

## Academic Information

- **Project:** Student Engagement in Online Learning – Statistical Modelling Using R
- **Course:** STAT 31631 – Statistical Modelling
- **Institution:** University of Kelaniya, Sri Lanka
- **Academic Year:** 2024/2025
- **Project Type:** Group Academic Project

## Note

This project is an academic statistical analysis based on a publicly available Kaggle dataset. Results depend on the dataset, preprocessing decisions, and selected regression model. The reported findings should be interpreted as statistical associations rather than causal conclusions.
