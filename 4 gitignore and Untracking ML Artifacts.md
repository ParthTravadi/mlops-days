# Lab 4: Gitignore and Untracking ML Artifacts

## 1. Scenario
The xFusionCorp Industries fraud-detection repository was committed without a .gitignore file. As a result, Python caches, a trained model file, a virtual environment, notebook checkpoints, and a local secrets file have all been included in version control. Your task is to create a .gitignore file and appropriately stop tracking the artifacts that should not be included in Git.

The Git repository is at `/root/code/fraud-detection/`. Standard Python / ML artifacts were committed before any .gitignore existed, so ignoring them is not enough — a .gitignore never untracks files Git already tracks.

The end state must satisfy the following:
- a `.gitignore` at the repository root excludes the standard Python / ML artifacts:
  - Python bytecode caches — `__pycache__/` and `*.pyc`;
  - virtual environments — `venv/`;
  - Jupyter checkpoints — `.ipynb_checkpoints/`;
  - trained model files — `*.pkl`;
  - local environment files — `.env`;
- those artifacts are removed from Git's index (while remaining on disk) and the cleanup is committed;
- the project sources remain tracked: everything under `src/fraud_detection/`, `README.md`, and `requirements.txt`.

---

## 2. Memorable Technique: The "CVJMS" Hit List

To easily remember the 5 things you need to ignore in ML projects, remember the acronym **CVJMS** ("**C**atch **V**ampires **J**umping, **M**ake **S**ure"):
1. **C** - **C**ache (`__pycache__/`, `*.pyc`)
2. **V** - **V**env (`venv/`)
3. **J** - **J**upyter (`.ipynb_checkpoints/`)
4. **M** - **M**odel (`*.pkl`)
5. **S** - **S**ecrets (`.env`)

**The Untrack Command:** To remove files from Git tracking *without* deleting them from your hard drive, you must use `--cached`. A pro-level best practice is to test what will happen first using `--dry-run`!

---

## 3. Step-by-Step Solution

Run these commands on the `controlplane` host:

```bash
# 1. Navigate to the working repository
cd /root/code/fraud-detection/

# 2. Create the .gitignore file with the CVJMS artifacts
cat <<EOF> .gitignore
__pycache__/
*.pyc
venv/
.ipynb_checkpoints/
*.pkl
.env
EOF

# 3. SAFE CHECK: Preview what Git will untrack without actually executing it
git rm -r --cached --dry-run .
# Note: You can also use the shorthand -n instead of --dry-run

# 4. Untrack everything from the Git index (leaves files on disk)
git rm -r --cached .

# 5. Re-add files (Git will now respect the new .gitignore)
git add .

# 6. Commit the cleanup
git commit -m "Add .gitignore and remove ML artifacts from tracking"


## 4. Active Recall Review
Test yourself: Read the prompt, write down the exact command from memory, then verify against the answers below.

Q1: What five categories of ML files do you need to add to the .gitignore? (Hint: CVJMS)

Answer:

Caches (__pycache__/, *.pyc)

Venvs (venv/)

Jupyter checkpoints (.ipynb_checkpoints/)

Models (*.pkl)

Secrets (.env)

Q2: How can you safely test or preview which files Git will remove from tracking before actually running the removal command?

Answer: Append the --dry-run or -n flag: git rm -r --cached --dry-run .

Q3: What exact Git command removes files from the Git index but leaves them safely on your hard drive?

Answer: git rm -r --cached .

Q4: After clearing the cache, what two commands finalize the cleanup?

Answer: git add . (to stage the remaining valid files + the new .gitignore) and git commit -m "cleanup message".
