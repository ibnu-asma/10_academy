Task 2 Summary: Data Profiling, Cleaning & EDA

Uncovering Solar Insights with EDA

Task 2 plunged me into the world of solar data, where I analyzed Benin’s solar radiation measurements to support MoonLight Energy Solutions’ sustainability goals. I profiled, cleaned, and explored the dataset, revealing patterns that could guide strategic solar investments. This task was a crash course in turning raw data into actionable insights.

Objective: Profile, clean, and perform exploratory data analysis (EDA) on Benin’s solar dataset to prepare it for region-ranking, identifying high-potential areas for solar installations.

Steps and Commands:


Set Up the Git Branch:

cd ~/path/to/10_academy/challenge-week1
git checkout -b eda-benin
touch notebooks/benin_eda.ipynb



Updated Environment:

echo "pandas\nnumpy\nmatplotlib\nseaborn\nscipy\njupyter\nipykernel" >> requirements.txt
source venv/bin/activate
pip install -r requirements.txt



Performed EDA in benin_eda.ipynb:





Computed summary statistics and identified missing values.



Detected outliers using Z-scores and imputed missing values with medians.



Plotted time series, correlations, wind distributions, temperature relationships, and a bubble chart.



Exported cleaned data:

df.to_csv('../data/benin_clean.csv', index=False)



Fixed Kernel Issue:

python -m ipykernel install --user --name venv --display-name "Python (venv)"



Committed and Pushed:

git add notebooks/benin_eda.ipynb notebooks/figures/ requirements.txt
git commit -m "Complete EDA for Benin"
git push --set-upstream origin eda-benin

Challenges Faced:





Library Errors: A ModuleNotFoundError for pandas stalled progress, resolved by installing libraries in venv.



Kernel Setup: The virtual environment wasn’t listed as a Jupyter kernel, fixed by registering it with ipykernel.



Data Cleaning: Handling missing values and outliers required careful decisions to preserve data integrity.

Key Takeaways:





EDA is like detective work—each plot uncovers clues about the data’s story.



Statistical tools like Z-scores and correlations provide objective insights.



A clean environment (both data and venv) is critical for reliable analysis.