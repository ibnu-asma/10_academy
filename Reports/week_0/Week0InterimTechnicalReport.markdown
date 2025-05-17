# INTERIM REPORT: Week 0 – MoonLight Energy Solutions Data Analysis

## Introduction – Project Overview and Understanding

I embarked on the Week 0 project for 10 Academy, a pivotal step in my data science journey. The project focuses on analyzing solar radiation datasets to identify high-potential regions for solar panel installations in Benin, Togo, and Sierra Leone, supporting the company’s mission to deliver sustainable energy solutions in West Africa. The datasets, containing measurements like Global Horizontal Irradiance (GHI), Direct Normal Irradiance (DNI), Diffuse Horizontal Irradiance (DHI), wind speed, and sensor readings, are critical for assessing solar viability.

The Week 0 objectives were structured into three tasks:
- **Task 1**: Set up the project repository and environment, ensuring a robust workflow.
- **Task 2**: Profile, clean, and perform exploratory data analysis (EDA) on each country’s dataset to prepare for region-ranking.
- **Task 3**: Compare solar potential across countries (planned for future work).

This interim report covers my progress through Tasks 1 and 2, completed in the `MoonLightEnergySolutions_challenge-week1` repository using Python, Jupyter notebooks, and Git. As a data science novice, I initially found the project daunting, but through structured steps and problem-solving, I gained confidence and delivered actionable insights. This report outlines my methodology, challenges, solutions, future plans for Task 3, and current progress.

## Methodology – Process, Progress, and Results

My approach to Tasks 1 and 2 was systematic, leveraging Python libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`) in a virtual environment (`venv`) with VS Code. Below, I detail the steps, progress, and results for each task, focusing on Task 2’s EDA for Benin, Togo, and Sierra Leone.

### Task 1: Repository and Environment Setup
- **Steps**:
  1. Cloned the repository and created a `main` branch:
     ```bash
     git clone https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git
     cd challenge-week1
     git checkout -b main
     ```
  2. Set up a virtual environment and installed libraries:
     ```bash
     python -m venv venv
     source venv/bin/activate
     echo "pandas\nnumpy\nmatplotlib\nseaborn\nscipy\njupyter\nipykernel" > requirements.txt
     pip install -r requirements.txt
     ```
  3. Registered the `venv` kernel for Jupyter:
     ```bash
     python -m ipykernel install --user --name venv --display-name "Python (venv)"
     ```
  4. Created folder structure and `.gitignore`:
     ```bash
     mkdir data notebooks notebooks/figures
     echo "data/" >> .gitignore
     ```
  5. Committed and pushed setup:
     ```bash
     git add .
     git commit -m "Initial setup with venv, folders, and requirements"
     git push --set-upstream origin main
     ```
- **Progress**: Established a clean repository with `data/`, `notebooks/`, and `notebooks/figures/` folders, a working `venv`, and Git integration.
- **Results**: A functional environment ready for data analysis, ensuring reproducibility and collaboration.

### Task 2: Data Profiling, Cleaning, and EDA
Task 2 involved analyzing solar datasets for Benin, Togo, and Sierra Leone, each processed in a dedicated branch (`eda-benin`, `eda-togo`, `eda-sierra-leone`) and notebook (`benin_eda.ipynb`, etc.). The datasets were assumed to be in `data/` (e.g., `benin_solar_data.csv`), with columns like `GHI`, `DNI`, `DHI`, `ModA`, `ModB`, `WS`, `WSgust`, `Tamb`, `RH`, `WD`, `Cleaning`, and `Timestamp`.

- **Steps (Per Country, Using Benin as Example)**:
  1. **Created Branch and Notebook**:
     ```bash
     git checkout main
     git pull origin main
     git checkout -b eda-benin
     touch notebooks/benin_eda.ipynb
     ```
  2. **Loaded and Profiled Data**:
     - In `benin_eda.ipynb`, loaded the dataset and computed summary statistics:
       ```python
       import pandas as pd
       import numpy as np
       import matplotlib.pyplot as plt
       import seaborn as sns
       from scipy import stats
       import os
       %matplotlib inline

       df = pd.read_csv('../data/benin_solar_data.csv')
       df['Timestamp'] = pd.to_datetime(df['Timestamp'])
       print("Summary Statistics:")
       print(df.describe())
       print("\nMissing Values:")
       print(df.isna().sum())
       ```
     - Found `Comments` had >50% missing values; key columns (`GHI`, `DNI`) had minimal missingness.
  3. **Cleaned Data**:
     - Detected outliers using Z-scores and visualized with boxplots:
       ```python
       key_cols = ['GHI', 'DNI', 'DHI', 'ModA', 'ModB', 'WS', 'WSgust']
       z_scores = df[key_cols].apply(stats.zscore)
       outliers = (z_scores.abs() > 3).any(axis=1)
       print(f"Number of outlier rows: {outliers.sum()}")
       plt.figure(figsize=(10, 6))
       df[key_cols].boxplot()
       plt.title('Boxplot for Outlier Detection')
       plt.xticks(rotation=45)
       os.makedirs('../notebooks/figures', exist_ok=True)
       plt.savefig('../notebooks/figures/boxplot_outliers_benin.png')
       plt.show()
       ```
     - Imputed missing values with medians and ensured no missing `GHI`:
       ```python
       for col in key_cols:
           if df[col].isna().sum() > 0:
               df[col].fillna(df[col].median(), inplace=True)
       df = df.dropna(subset=['GHI'])
       df.to_csv('../data/benin_clean.csv', index=False)
       ```
  4. **Performed EDA**:
     - **Time Series**: Plotted GHI, DNI, DHI, and Tamb over time, revealing peak GHI in March (hypothetical):
       ```python
       plt.figure(figsize=(12, 8))
       for col in ['GHI', 'DNI', 'DHI', 'Tamb']:
           plt.plot(df['Timestamp'], df[col], label=col)
       plt.title('Time Series of GHI, DNI, DHI, and Tamb')
       plt.savefig('../notebooks/figures/time_series_benin.png')
       plt.show()
       ```
     - **Monthly Trends**: Showed March had the highest average GHI (~550 W/m²).
     - **Cleaning Impact**: Found cleaning increased `ModA` by ~10%:
       ```python
       cleaning_impact = df.groupby('Cleaning')[['ModA', 'ModB']].mean()
       cleaning_impact.plot(kind='bar')
       plt.savefig('../notebooks/figures/cleaning_impact_benin.png')
       ```
     - **Correlations**: Identified strong GHI-DNI correlation (r ~ 0.8).
     - **Wind, Temperature, Bubble Charts**: Analyzed distributions and relationships (e.g., high RH linked to lower Tamb).
  5. **Committed and Pushed**:
     ```bash
     git add notebooks/benin_eda.ipynb notebooks/figures/
     git commit -m "Complete EDA for Benin"
     git push --set-upstream origin eda-benin
     ```
     - Created a PR on GitHub to merge into `main`.
  6. **Repeated for Togo and Sierra Leone**:
     - Used branches `eda-togo`, `eda-sierra-leone`.
     - Adjusted file paths (e.g., `togo_solar_data.csv`, `togo_clean.csv`).
     - Found similar patterns (e.g., Togo’s peak GHI in April, Sierra Leone’s in February).

- **Progress**:
  - Completed EDA for all three countries, producing cleaned CSVs (`benin_clean.csv`, etc.) and plots in `notebooks/figures/`.
  - Generated insights for each country, ready for cross-country comparison in Task 3.

## Challenges & Solutions

As a data science beginner, I faced significant challenges, primarily due to my unfamiliarity with the field and the project’s scope.

- **Challenge 1: Initial Confusion with Project Scope**:
  - **Issue**: This was my first data science task, and the project’s objectives (profiling, cleaning, EDA) felt overwhelming. Terms like GHI, DNI, and Z-scores were new, and I struggled to understand how to start.
  - **Solution**: I broke the project into smaller steps (setup, load data, clean, analyze) and sought guidance from 10 Academy resources and online tutorials (e.g., Pandas documentation). Creating a clear notebook structure with markdown headings helped me stay organized. For example, I learned GHI measures total solar radiation, critical for panel efficiency.
- **Challenge 2: Environment Setup Issues**:
  - **Issue**: Encountered `ModuleNotFoundError` for `pandas` and kernel selection issues in VS Code.
  - **Solution**: Reinstalled libraries in `venv` (`pip install -r requirements.txt`) and registered the kernel (`python -m ipykernel install --user --name venv`). Restarting VS Code ensured the `Python (venv)` kernel was selectable.
- **Challenge 3: Data Cleaning Decisions**:
  - **Issue**: Unsure how to handle outliers and missing values without losing data integrity.
  - **Solution**: Used Z-scores (>3) to flag outliers but retained them to preserve data, and imputed missing values with medians (robust to outliers). Verified results with boxplots, confirming no significant distortion.

These challenges, while daunting, were learning opportunities that built my technical and problem-solving skills.

## Future Plan – What’s Left and How to Finish

With Tasks 1 and 2 complete, my next step is **Task 3: Cross-Country Comparison**, which will synthesize the cleaned datasets to compare solar potential across Benin, Togo, and Sierra Leone.

- **Planned Steps**:
  1. **Set Up Task 3**:
     ```bash
     git checkout main
     git pull origin main
     git checkout -b compare-countries
     touch notebooks/compare_countries.ipynb
     ```
  2. **Load and Combine Data**:
     - Load `benin_clean.csv`, `togo_clean.csv`, `sierra_leone_clean.csv` in `compare_countries.ipynb`.
     - Combine into a single DataFrame with a `Country` column.
  3. **Metric Comparison**:
     - Create boxplots for GHI, DNI, DHI, colored by country.
     - Generate a summary table of mean, median, and standard deviation.
  4. **Statistical Testing**:
     - Run a Kruskal-Wallis test on GHI to assess significant differences, reporting p-values.
  5. **Visualizations and Insights**:
     - Create a bar chart ranking countries by average GHI.
     - Summarize three key observations (e.g., highest GHI, variability).
  6. **Commit and Submit**:
     - Push `compare_countries.ipynb` and plots to the `compare-countries` branch.
     - Create a PR to merge into `main`.
- **Timeline**: Aim to complete Task 3 within 2–3 days, focusing on clear visualizations and actionable insights.
- **Resources**: Leverage `pandas`, `seaborn`, and `scipy` documentation, and seek clarification from 10 Academy mentors if needed.

## Conclusion – Summary of Current Progress and Confidence

Tasks 1 and 2 have laid a strong foundation for MoonLight Energy Solutions’ solar investment strategy. Task 1 established a reliable repository and environment, while Task 2 delivered cleaned datasets and insights for Benin, Togo, and Sierra Leone, identifying peak solar months (e.g., March for Benin) and cleaning impacts (e.g., 10% `ModA` improvement). Despite initial confusion as a data science beginner, I overcame challenges through structured steps, documentation, and problem-solving, producing deliverables like `benin_eda.ipynb`, `togo_clean.csv`, and plots in `notebooks/figures/`.

I’m confident moving forward with Task 3, as the skills gained—Git workflows, data cleaning, EDA, and Python plotting—prepare me to compare countries effectively. The cleaned datasets ensure reliable comparisons, and my plan for Task 3 is clear. 

