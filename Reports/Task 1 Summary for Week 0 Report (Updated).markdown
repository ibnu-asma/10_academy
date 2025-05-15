# Task 1 Summary: Git & Environment Setup

## Laying the Groundwork with Git and Environment Setup

Week 0 at 10 Academy kicked off with Task 1, a hands-on dive into version control and development environments. The mission was clear: master Git, set up a Python virtual environment, and create a reproducible workflow using GitHub. This task was our first step toward tackling data-driven challenges, blending technical setup with organizational skills.

**Objective**: Initialize a GitHub repository named `MoonLightEnergySolutions_challenge-week1`, configure a Python virtual environment, create a `setup-task` branch with at least three commits, set up a basic CI pipeline with GitHub Actions, and document everything in a `README.md`. Additionally, nest `MoonLightEnergySolutions_challenge-week1` inside a parent repository called `10_academy` to organize all weekly challenges.

**What I Did**:
1. **Parent Repository Setup**:
   - Created the `10_academy` repository on GitHub as the parent for all weekly challenges.
   - Cloned it locally and set up a minimal structure with a `README.md` to catalog challenges.

2. **Repository Initialization**:
   - Established `MoonLightEnergySolutions_challenge-week1` as a standalone GitHub repository.
   - Cloned it locally inside the `10_academy` folder and initialized a Git repository.
   - Added a `.gitignore` to exclude `data/`, `.csv`, `.ipynb_checkpoints`, and virtual environment files, keeping the repository clean.

3. **Virtual Environment**:
   - Created a Python virtual environment using `venv` (`python -m venv venv`).
   - Activated it and installed dependencies like `pytest` for testing.
   - Generated a `requirements.txt` file with `pip freeze > requirements.txt` to ensure reproducibility.

4. **Branching and Commits**:
   - Created a `setup-task` branch (`git checkout -b setup-task`).
   - Made at least three commits with descriptive messages:
     - `init: add .gitignore`
     - `chore: venv setup`
     - `ci: add GitHub Actions workflow`
   - Pushed the branch to GitHub and merged it into `main` via a Pull Request, practicing collaborative workflows.

5. **Folder Structure**:
   - Implemented the required structure:
     ```
     MoonLightEnergySolutions_challenge-week1/
     ├── .github/workflows/ci.yml
     ├── .vscode/settings.json
     ├── notebooks/
     │   ├── __init__.py
     │   └── README.md
     ├── scripts/
     │   ├── __init__.py
     │   └── README.md
     ├── src/
     ├── tests/
     │   ├── __init__.py
     ├── .gitignore
     ├── README.md
     ├── requirements.txt
     ```
   - This layout is ready for code, notebooks, and tests in future challenges.

6. **Continuous Integration**:
   - Configured a GitHub Actions workflow (`.github/workflows/ci.yml`) to run `pip install -r requirements.txt` and verify the Python version.
   - Confirmed the CI pipeline executed successfully on GitHub, ensuring consistent dependency installation.

7. **Documentation**:
   - Crafted a `README.md` in `MoonLightEnergySolutions_challenge-week1` with clear instructions for cloning, setting up the environment, and installing dependencies:
     ```bash
     git clone https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git
     python -m venv venv
     source venv/bin/activate
     pip install -r requirements.txt
     ```

8. **Nesting in `10_academy`**:
   - Used a Git submodule to nest `MoonLightEnergySolutions_challenge-week1` inside `10_academy` (`git submodule add https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git challenge-week1`).
   - Updated the `10_academy` `README.md` to document the submodule and cloning process:
     ```bash
     git clone --recurse-submodules https://github.com/ibnu-asma/10_academy.git
     git submodule update --init --recursive
     ```
   - Pushed changes to GitHub, mirroring the local structure:
     ```
     10_academy/
     ├── .gitmodules
     ├── README.md
     ├── challenge-week1/  (submodule linking to MoonLightEnergySolutions_challenge-week1)
     ```

**Challenges Faced**:
- **Remote Setup Issues**: Ran into errors like `fatal: 'origin' does not appear to be a git repository` due to a typo (`origion` instead of `origin`). Corrected it with `git remote add origin https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git`.
- **Missing Remote Branch**: Encountered `fatal: couldn't find remote ref main` because the `main` branch hadn’t been pushed. Fixed by pushing with `git push --set-upstream origin main`.
- **Submodule Learning Curve**: Setting up Git submodules was unfamiliar, but it proved ideal for keeping `MoonLightEnergySolutions_challenge-week1` independent yet organized within `10_academy`.

**Key Takeaways**:
- Git is a powerful tool for collaboration, and practices like branching and Pull Requests streamline teamwork.
- A well-crafted `.gitignore` and virtual environment ensure clean, portable projects.
- GitHub Actions automates dependency checks, saving time and preventing environment mismatches.
- Submodules are perfect for managing multiple repositories under a parent project, setting the stage for future weeks.

**Outcome**:
Task 1 was a triumph! The `MoonLightEnergySolutions_challenge-week1` repository is fully configured with a robust structure, a functional CI pipeline, and comprehensive documentation. It’s nested as a submodule in `10_academy`, both locally and on GitHub, poised for upcoming challenges. This setup met the KPIs (Dev Environment Setup) and boosted my confidence in Git, Python environments, and project organization.