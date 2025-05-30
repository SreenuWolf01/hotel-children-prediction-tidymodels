# Hotel Booking Prediction: Penalized Logistic Regression with `tidymodels` 🏨👶

## Project Overview

This project focuses on building a **penalized logistic regression model** to predict which hotel bookings include children or babies. Leveraging a comprehensive hotel bookings dataset, the analysis demonstrates a robust machine learning pipeline using the `tidymodels` framework in R, from data preprocessing to hyperparameter tuning.

## Problem Statement

The core objective was to identify and predict hotel stays that included children and/or babies based on various booking characteristics. This type of prediction can be valuable for hotel management in optimizing resource allocation, tailoring services, or targeted marketing.

## Data

The dataset used for this case study is related to hotel bookings, originally from Antonio, Almeida, and Nunes (2019).

* **Source:** A slightly edited version of a #TidyTuesday dataset, publicly available. The data is loaded directly from a URL within the R script.
    * **Direct Data URL:** `https://tidymodels.org/start/case-study/hotels.csv`
* **Description:** The dataset captures demand data for two distinct types of hotels: a resort hotel (H1) and a city hotel (H2).
    * **Size:** Comprises 31 variables with 40,060 bookings for the resort hotel and 79,330 bookings for the city hotel.
    * **Period:** Data spans from July 1, 2015, to August 31, 2017, including both actual and canceled bookings.
    * **Privacy:** Identifiable information regarding hotels or customers has been removed.
* **Key Variables (Examples):** `hotel`, `lead_time`, `stays_in_weekend_nights`, `stays_in_week_nights`, `adults`, `children`, `meal`, `country`, `market_segment`, `distribution_channel`, `arrival_date`, etc. The target variable is `children` (transformed to a binary indicator for presence of children/babies).

## Methodology: Penalized Logistic Regression with `tidymodels`

The project utilizes the `tidymodels` framework in R to build and evaluate the penalized logistic regression model. This framework provides a consistent and efficient way to manage the entire modeling process.

### 1. Recipe (Data Preprocessing)

The `recipe()` function defines the sequence of preprocessing steps applied to the raw data before modeling. Key steps include:

* `step_date()`: Extracts specific parts (e.g., year, month, day) from date variables like `arrival_date`.
* `step_holiday()`: Creates binary (yes/no) indicators for certain holidays based on the `arrival_date`.
* `step_dummy()`: Converts all categorical variables into dummy (one-hot encoded) variables.
* `step_zv()`: Eliminates predictors that have zero variance, as they do not contribute to predictions.
* `step_normalize()`: Adjusts numerical predictors by scaling and centering them. This is crucial for penalized models, which assume predictors are on a uniform scale.

### 2. Workflow

The `workflow()` function acts as a bridge, seamlessly connecting the preprocessing steps (defined in the recipe) with the chosen model (`logistic_reg()` in this case). It ensures that data preparation and model fitting occur together smoothly, promoting reproducibility and consistency.

### 3. Tune Grid (Hyperparameter Tuning)

The `tune_grid()` function is employed to find the optimal hyperparameters for the penalized logistic regression model. It systematically explores a predefined grid of potential hyperparameter values (specifically, various `penalty` values for regularization). For each combination of hyperparameters, the model is trained and evaluated on a validation dataset (`val_set`), allowing us to identify the setup that yields the best performance.

## Model Building and Evaluation

(Based on the PDF, the detailed model creation and evaluation steps would follow the explanations of recipe, workflow, and tune_grid. This would include training the model, evaluating its performance (e.g., using AUC, ROC curves), and selecting the final best model.)

## Tools and Technologies

* **Language:** R
* **Framework:** `tidymodels` (a collection of packages for modeling, including `recipes`, `workflows`, `tune`, `parsnip`, `rsample`, `yardstick`, `dials`, `broom`, `workflowsets`)
* **Libraries:** `readr` (for data import), `vip` (for variable importance, if used).
* **Tools:** RStudio
