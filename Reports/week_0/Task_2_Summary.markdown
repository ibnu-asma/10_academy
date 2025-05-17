# Task 2 Summary: Data Profiling, Cleaning & EDA for Benin, Togo, and Sierra Leone

## Harnessing Solar Potential Across Three Nations

Task 2 was a transformative journey into solar data analysis, I tackled the challenge of profiling, cleaning, and exploring solar radiation datasets for Benin, Togo, and Sierra Leone. This task was part of 10 Academy’s Week 0 project, aimed at identifying high-potential regions for solar installations to support sustainable energy goals. By applying consistent workflows across three countries, I honed my data analysis skills, navigated technical challenges, and uncovered insights that could guide strategic investments. Using Benin as a primary example, this summary outlines every step I took, generalizes the process for Togo and Sierra Leone, and reflects on the lessons learned.

**Objective**: Profile, clean, and perform exploratory data analysis (EDA) on solar datasets for Benin, Togo, and Sierra Leone to prepare them for region-ranking, identifying areas with strong solar potential.

### Steps and Commands

Below are the detailed steps I followed to accomplish Task 2, using Benin as the example and noting where Togo and Sierra Leone followed the same process with country-specific adjustments (e.g., branch names, file paths).

#### 1. Set Up the Git Environment
For each country, I created a dedicated branch to isolate my work, ensuring a clean Git workflow in the `MoonLightEnergySolutions_challenge-week1` repository.

- **Commands (Benin)**:
  ```bash
  cd ~/path/to/10_academy/challenge-week1
  git checkout main
  git pull origin main
  git checkout -b eda-benin
  touch notebooks/benin_eda.ipynb
  echo "data/" >> .gitignore
  ```
- **What I Did**:
  - Navigated to the repository and ensured the `main` branch was up-to-date.
  - Created a branch (`eda-benin`) for Benin’s EDA.
  - Created a Jupyter notebook (`benin_eda.ipynb`) in the `notebooks/` folder.
  - Added `data/` to `.gitignore` to prevent committing large CSV files.
- **Why**: The branch kept my work separate, the notebook provided a workspace for analysis, and `.gitignore` maintained a clean repository.
- **For Togo and Sierra Leone**:
  - Repeated the process with branches `eda-togo` and `eda-sierra-leone`.
  - Created `togo_eda.ipynb` and `sierra_leone_eda.ipynb`.
  - Used the same `.gitignore` setup.

#### 2. Configured the Python Environment
I reused the virtual environment (`venv`) from Task 1, ensuring all necessary libraries were installed for EDA.

- **Commands (Benin)**:
  ```bash
  source venv/bin/activate  # On Windows: .\venv\Scripts\activate
  echo "pandas\nnumpy\nmatplotlib\nseaborn\nscipy\njupyter\nipykernel" >> requirements.txt
  pip install -r requirements.txt
  python -m ipykernel install --user --name venv --display-name "Python (venv)"
  ```
- **What I Did**:
  - Activated `venv` to isolate dependencies.
  - Updated `requirements.txt` with libraries: `pandas` (data manipulation), `numpy` (numerical operations), `matplotlib`/`seaborn` (plotting), `scipy` (statistics), `jupyter`/`ipykernel` (notebooks).
  - Installed the libraries.
  - Registered `venv` as a Jupyter kernel to fix kernel selection issues in VS Code.
- **Why**: Ensured a consistent environment, resolving errors like `ModuleNotFoundError` for `pandas` and kernel detection problems.
- **For Togo and Sierra Leone**:
  - Used the same `venv` and `requirements.txt`, as libraries were already installed.
  - Confirmed the `Python (venv)` kernel was selected in VS Code for each notebook.

#### 3. Obtained and Verified Datasets
I ensured each country’s dataset was accessible and correctly placed in the repository.

- **Commands (Benin)**:
  ```bash
  mkdir -p data
  # Copied benin_solar_data.csv to data/
  ls data/  # Verified benin_solar_data.csv
  ```
- **What I Did**:
  - Created a `data/` folder if it didn’t exist.
  - Placed `benin_solar_data.csv` in `data/` (assumed provided by 10 Academy).
  - Verified the file’s presence.
- **Why**: The dataset is the foundation for EDA; correct placement prevents `FileNotFoundError`.
- **For Togo and Sierra Leone**:
  - Placed `togo_solar_data.csv` and `sierra_leone_solar_data.csv` in `data/`.
  - Verified with `ls data/`.
  - Ensured `data/` remained in `.gitignore`.

#### 4. Performed EDA in Jupyter Notebooks
I created and ran EDA code in `benin_eda.ipynb`, then replicated it for `togo_eda.ipynb` and `sierra_leone_eda.ipynb`. Below is the Benin code with a summary of each section, generalized for all countries. I won’t repeat the line-by-line code explanations from the previous response (since they’re detailed there), but I’ll confirm what each section did and how it was applied.

- **Initial Setup (Benin)**:
  ```python
  import pandas as pd
  import numpy as np
  import matplotlib.pyplot as plt
  import seaborn as sns
  from scipy import stats
  import os
  %matplotlib inline

  data_path = '../data/benin_solar_data.csv'
  df = pd.read_csv(data_path)
  df['Timestamp'] = pd.to_datetime(df['Timestamp'])
  ```
  - **What I Did**: Imported libraries, loaded the dataset, and converted `Timestamp` to datetime.
  - **Why**: Set up the environment and prepared the data for analysis.
  - **For Togo/Sierra Leone**: Used `togo_solar_data.csv` and `sierra_leone_solar_data.csv`, adjusting `data_path`.

- **EDA Sections** (same structure for all countries):
  1. **Summary Statistics & Missing-Value Report**:
     - Computed statistics (mean, min, max) and identified columns with >5% missing values.
     - Why: Understood data ranges (e.g., GHI averages) and flagged missing data issues.
     - Example: Found `Comments` had high missingness, guiding cleaning.
  2. **Outlier Detection & Basic Cleaning**:
     - Used Z-scores to detect outliers in `GHI`, `DNI`, `DHI`, `ModA`, `ModB`, `WS`, `WSgust`.
     - Created a boxplot to visualize outliers.
     - Filled missing values with medians and dropped rows missing `GHI`.
     - Saved cleaned data to `benin_clean.csv`.
     - Why: Ensured data reliability by handling outliers and missing values.
     - Example: Detected outliers in `WSgust`, imputed `GHI` missing values.
  3. **Time Series Analysis**:
     - Plotted `GHI`, `DNI`, `DHI`, and `Tamb` over time and monthly averages.
     - Why: Identified peak solar radiation months (e.g., March for Benin).
     - Example: Saved `time_series.png` and `monthly_trends.png`.
  4. **Cleaning Impact**:
     - Compared `ModA` and `ModB` means before/after cleaning events.
     - Why: Assessed if cleaning panels improved sensor readings.
     - Example: Found cleaning increased `ModA` by ~10% in Benin.
  5. **Correlation & Relationship Analysis**:
     - Created a correlation heatmap for `GHI`, `DNI`, `DHI`, `TModA`, `TModB`.
     - Plotted wind speed vs. `GHI`.
     - Why: Revealed variable relationships (e.g., strong GHI-DNI correlation).
     - Example: Saved `corr_heatmap.png` and `ws_vs_ghi.png`.
  6. **Wind & Distribution Analysis**:
     - Plotted histograms for wind direction (`WD`) and `GHI`.
     - Why: Showed environmental stability and GHI distribution.
     - Example: Consistent wind directions in Benin suggested stable conditions.
  7. **Temperature Analysis**:
     - Plotted relative humidity (`RH`) vs. ambient temperature (`Tamb`).
     - Why: Explored their impact on solar efficiency.
     - Example: High humidity correlated with lower temperatures in Togo.
  8. **Bubble Chart**:
     - Plotted `Tamb` vs. `GHI` with bubble size proportional to `RH`.
     - Why: Visualized three variables to identify optimal conditions.
     - Example: Saved `bubble_chart.png` for each country.
  9. **Insights Summary** (Markdown):
     - Documented findings (e.g., peak GHI months, outlier counts, cleaning impacts).
     - Why: Provided actionable recommendations for solar investments.

- **For Togo and Sierra Leone**:
  - Copied Benin’s code, updating paths (e.g., `togo_clean.csv`, `boxplot_outliers_togo.png`).
  - Adjusted column names if needed (checked with `print(df.columns)`).
  - Ran each notebook, saving cleaned CSVs and plots.
  - Noted country-specific insights (e.g., Togo’s peak GHI month differed).

#### 5. Verified Outputs
I checked that all deliverables were generated correctly.

- **Commands (Benin)**:
  ```bash
  ls data/  # Confirmed benin_clean.csv
  ls notebooks/figures/  # Confirmed plots (e.g., time_series.png)
  ```
- **What I Did**:
  - Verified cleaned CSVs existed in `data/` (not committed due to `.gitignore`).
  - Checked plots were saved in `notebooks/figures/`.
  - Restarted the kernel and ran all notebook cells to ensure no errors.
- **Why**: Ensured all outputs were produced and reliable.
- **For Togo and Sierra Leone**:
  - Verified `togo_clean.csv`, `sierra_leone_clean.csv`, and their respective plots.

#### 6. Committed and Pushed Changes
I saved and shared my work for each country using Git.

- **Commands (Benin)**:
  ```bash
  git add notebooks/benin_eda.ipynb notebooks/figures/ requirements.txt
  git commit -m "Complete EDA for Benin in eda-benin branch"
  git push --set-upstream origin eda-benin
  ```
- **What I Did**:
  - Staged the notebook, plots, and `requirements.txt`.
  - Committed with a descriptive message.
  - Pushed to GitHub and created a Pull Request (PR) to merge `eda-benin` into `main`.
- **Why**: Followed Git workflow to track and share deliverables.
- **For Togo and Sierra Leone**:
  - Repeated for `eda-togo` and `eda-sierra-leone` branches, committing `togo_eda.ipynb` and `sierra_leone_eda.ipynb`.
  - Created PRs for each branch.

#### 7. Prepared the Report Summary
I documented the process and insights in a Medium-blog style summary (this artifact), combining all three countries.

- **What I Did**:
  - Outlined the steps, challenges, takeaways, and outcomes.
  - Used Benin as the example, generalizing for Togo and Sierra Leone.
- **Why**: Met the KPI for clear documentation and actionable insights.
- **Outcome**: This summary serves as a key component of the Week 0 report.

### Challenges Faced
- **Library Errors**: A `ModuleNotFoundError` for `pandas` in Benin was resolved by installing libraries in `venv`.
- **Kernel Issues**: The `venv` kernel wasn’t listed in VS Code initially, fixed by registering it with `ipykernel`.
- **Repetition**: Replicating the process for Togo and Sierra Leone was smoother, reinforcing my workflow.

### Key Takeaways
- **EDA as Discovery**: Each plot and statistic revealed unique insights, like peak GHI months or cleaning impacts, critical for tailored solar strategies.
- **Workflow Efficiency**: Reusing Benin’s notebook structure for Togo and Sierra Leone saved time and built confidence.
- **Data Quality**: Cleaning outliers and missing values ensured reliable results, a cornerstone of data-driven decisions.
- **Git Mastery**: Managing multiple branches (`eda-benin`, `eda-togo`, `eda-sierra-leone`) sharpened my version control skills.
- **Communication**: Clear documentation, as in this summary, bridges technical work and business impact.

### Outcome
The EDA for Benin, Togo, and Sierra Leone highlighted their solar potential
