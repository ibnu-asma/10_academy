# Task 1 Summary: Git & Environment Setup

## Building a Solid Foundation with Git and Python

Week 0 at 10 Academy was all about hitting the ground running, and Task 1 set the stage by diving into Git and environment setup. The goal was to master version control, configure a Python virtual environment, and create a reproducible workflow on GitHub. This task wasn’t just about ticking boxes—it was about building habits for clean, collaborative coding. Here’s how I tackled it, step by step, with the exact commands that got me there.

**Objective**: Create a GitHub repository named `MoonLightEnergySolutions_challenge-week1`, set up a Python virtual environment, create a `setup-task` branch with at least three commits, configure a GitHub Actions CI pipeline, and document the setup in a `README.md`. Then, nest this repository inside a parent `10_academy` repository as a submodule to organize all weekly challenges.

**Steps and Commands I Followed**:

1. **Setting Up the Parent Repository (`10_academy`)**:
   - Created `10_academy` on GitHub to hold all weekly challenges.
   - Cloned it locally:
     ```bash
     git clone https://github.com/ibnu-asma/10_academy.git
     cd 10_academy
     ```
   - Added a basic `README.md` and committed:
     ```bash
     echo "# 10 Academy Challenges" > README.md
     git add README.md
     git commit -m "Initialize 10_academy with README"
     git push origin main
     ```

2. **Creating `MoonLightEnergySolutions_challenge-week1`**:
   - Created the repository on GitHub (no initial files).
   - Initialized it locally inside `10_academy`:
     ```bash
     cd ~/path/to/10_academy
     mkdir challenge-week1
     cd challenge-week1
     git init
     ```
   - Set the remote:
     ```bash
     git remote add origin https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git
     ```

3. **Fixing Remote Issues**:
   - Encountered a typo (`origion` instead of `origin`):
     ```bash
     git remote rm ori gion
     git remote add origin https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git
     ```
   - Verified the remote:
     ```bash
     git remote -v
     ```

4. **Configuring the Folder Structure**:
   - Created the required structure:
     ```bash
     mkdir -p .github/workflows .vscode src notebooks tests scripts
     touch .gitignore requirements.txt README.md
     touch notebooks/__init__.py notebooks/README.md
     touch tests/__init__.py
     touch scripts/__init__.py scripts/README.md
     touch .vscode/settings.json .github/workflows/ci.yml
     ```
   - Added `.gitignore` content (excluding `data/`, `.csv`, `.ipynb_checkpoints`, `venv/`).

5. **Setting Up the Virtual Environment**:
   - Created and activated a virtual environment:
     ```bash
     python -m venv venv
     source venv/bin/activate  # On Windows: .\venv\Scripts\activate
     ```
   - Installed dependencies and saved them:
     ```bash
     pip install pytest
     pip freeze > requirements.txt
     ```

6. **Creating the GitHub Actions CI Pipeline**:
   - Added `.github/workflows/ci.yml` with content to run `pip install -r requirements.txt`.
   - Committed:
     ```bash
     git add .github/workflows/ci.yml
     git commit -m "ci: add GitHub Actions workflow"
     ```

7. **Branching and Commits**:
   - Created the `setup-task` branch:
     ```bash
     git checkout -b setup-task
     ```
   - Made three commits:
     ```bash
     git add .gitignore
     git commit -m "init: add .gitignore"
     git add requirements.txt
     git commit -m "chore: venv setup"
     git add .github/workflows/ci.yml
     git commit -m "ci: add GitHub Actions workflow"
     ```

8. **Pushing and Merging**:
   - Pushed `setup-task`:
     ```bash
     git push --set-upstream origin setup-task
     ```
   - Created a Pull Request on GitHub and merged `setup-task` into `main`.
   - Synced locally:
     ```bash
     git checkout main
     git pull origin main
     ```
   - Fixed an upstream error for `main`:
     ```bash
     git push --set-upstream origin main
     ```

9. **Documenting in `README.md`**:
   - Added setup instructions to `MoonLightEnergySolutions_challenge-week1`’s `README.md`:
     ```markdown
     # MoonLightEnergySolutions_challenge-week1

     ## Setup
     1. Clone:
        ```bash
        git clone https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git
        ```
     2. Create virtual environment:
        ```bash
        python -m venv venv
        source venv/bin/activate
        ```
     3. Install dependencies:
        ```bash
        pip install -r requirements.txt
        ```
     ```

10. **Nesting as a Submodule in `10_academy`**:
    - Navigated to `10_academy`:
      ```bash
      cd ~/path/to/10_academy
      ```
    - Removed any non-submodule `challenge-week1` folder:
      ```bash
      git rm -r --cached challenge-week0
      rm -rf challenge-week0
      ```
    - Added the submodule:
      ```bash
      git submodule add https://github.com/ibnu-asma/MoonLightEnergySolutions_challenge-week1.git challenge-week1
      ```
    - Updated `10_academy`’s `README.md`:
      ```markdown
      # 10 Academy Challenges

      ## Weekly Challenges
      - [Week 1](./challenge-week1): Git and environment setup.

      ## Setup
      ```bash
      git clone --recurse-submodules https://github.com/ibnu-asma/10_academy.git
      git submodule update --init --recursive
      ```
      ```
    - Committed and pushed:
      ```bash
      git add .gitmodules challenge-week1 README.md
      git commit -m "Add MoonLightEnergySolutions_challenge-week1 as submodule"
      git push origin main
      ```



**Key Takeaways**:
- Git commands like `git remote`, `git push --set-upstream`, and `git submodule add` are essential for managing complex project structures.
- Virtual environments and `.gitignore` keep projects portable and clutter-free.
- GitHub Actions ensures consistent environments, catching issues early.
- Submodules are a game-changer for organizing multiple repositories under one parent.

**Outcome**:
Task 1 was a success! `MoonLightEnergySolutions_challenge-week1` is a fully configured repository with a clean structure, a working CI pipeline, and clear documentation. It’s nested as a submodule in `10_academy`, both locally and on GitHub, ready for future challenges. This setup met the Dev Environment Setup KPIs and solidified my Git and Python skills.