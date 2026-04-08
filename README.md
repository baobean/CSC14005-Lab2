# Big Mart Sales Prediction

This repository contains a complete regression workflow for the Big Mart Sales problem, from exploratory data analysis and data preparation to model experimentation and an interactive Streamlit application. The project focuses on explaining and predicting `Item_Outlet_Sales` using linear-regression-based approaches, with the deployed app using a transformed-target pipeline with Box-Cox inversion for final predictions.

## Objectives

The project is built around a retail sales forecasting task using the Big Mart dataset. The main objectives are:

- Understand the structure and quality of the dataset through exploratory analysis
- Clean inconsistent values and prepare model-ready training and test sets
- Compare several linear modeling strategies
- Preserve a saved model pipeline for inference
- Expose the final predictor through a Streamlit interface

The raw dataset is stored in `data/raw/big_mart_sales.csv`, and prepared splits are available under `data/train_data/` and `data/test_data/`.

## Repository Contents

```
📦 Root
├── 📁 EDA
│   └── 📓 EDA.ipynb
├── 📁 Data_Preparation
│   └── 📓 data_preparation.ipynb
├── 📁 Model
│   ├── 📓 feature_subset_selection.ipynb
│   ├── 📓 interaction term model.ipynb
│   ├── 📓 polynomial_feature_model.ipynb
│   ├── 📓 transformed_variables_model.ipynb
│   └── 📁 saved_model
├── 📁 application
│   └── 📝 app.py
├── 📁 data
│   ├── 📁 raw
│   ├── 📁 train_data
│   └── 📁 test_data
└── 📄 requirements.txt
```

- `EDA/EDA.ipynb`: dataset understanding, variable inspection, and exploratory analysis.
- `Data_Preparation/data_preparation.ipynb`: cleaning, imputing missing values, standardizing labels, feature engineering, and creating prepared splits.
- `Model/`: notebook-based experiments for feature subset selection, interaction terms, polynomial features, and transformed variables.
- `Model/saved_model/`: serialized artifacts used by the application, including the trained model, scaler, Box-Cox parameter, column schema, and saved predictions for evaluation.
- `application/app.py`: Streamlit application for prediction, model diagnostics, and data exploration.
- `data/`: raw dataset plus prepared training and test CSV files.

## Methodology

The workflow implemented in this repository is:

1. `EDA`: inspect the dataset, variable meanings, distributions, and potential modeling issues.
2. `Data Preparation`: standardize categorical labels, fix business-logic inconsistencies, handle placeholders and missing values, and build clean train/test data.
3. `Modeling`: evaluate multiple linear-regression-oriented variants, including:
   - feature subset selection
   - interaction-term models
   - polynomial-feature models
   - transformed-variable models
4. `Saved Pipeline`: store the final artifacts required for inference in `Model/saved_model/`.
5. `Application`: serve predictions and diagnostics through Streamlit.

The deployed application loads a linear regression pipeline together with preprocessing artifacts from `Model/saved_model/`. The prediction is generated on the transformed scale and then converted back using Box-Cox inversion.

## Results

The current application uses saved evaluation artifacts from `Model/saved_model/` and reports the following held-out test performance:

- `R2 = 0.6058`
- `RMSE = 1035.06`
- `MAE = 717.59`

The Streamlit app also exposes:

- A prediction tab for entering product and outlet attributes
- An analytics tab with regression metrics and diagnostic plots
- A discovery tab for exploring the prepared dataset visually

## Setup and Usage

From the repository root:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Run the application:

```bash
streamlit run application/app.py
```

The app expects the following repository structure to remain unchanged:

- Saved artifacts in `Model/saved_model/`
- Prepared CSV files in `data/train_data/` and `data/test_data/`

## Deployed App

You can visit the app we have deployed on Streamlit Community Cloud [here](https://csc14005-lab2-group6.streamlit.app/).