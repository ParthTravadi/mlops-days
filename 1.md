# Day 1: xFusionCorp ML Environment Setup

## 1. Scenario
The xFusionCorp Industries data science team requires a standardized Python environment for their new machine learning project. Set up a virtual environment on the controlplane host that includes all necessary ML libraries.

The work is done on the controlplane host under `/root/code/`.
The end state must satisfy the following:
- a Python virtual environment named `ml-env` exists under `/root/code/`;
- the environment has `numpy`, `pandas`, `scikit-learn`, and `matplotlib` installed;
- a `requirements.txt` capturing the installed packages is saved at `/root/code/requirements.txt`.

---

## 2. Memorable Technique: The "VAIF" Sequence

To memorize the workflow perfectly, remember the acronym **VAIF**:
1. **V** - **Venv**: Create it (`python3 -m venv ml-env`)
2. **A** - **Activate**: Turn it on (`source ml-env/bin/activate`)
3. **I** - **Install**: Add the packages (`pip install numpy pandas scikit-learn matplotlib`)
4. **F** - **Freeze**: Save the state (`pip freeze > /root/code/requirements.txt`)

---

## 3. Step-by-Step Solution

Run these commands on the `controlplane` host:

```bash
# 1. Create and enter the working directory
mkdir -p /root/code
cd /root/code

# 2. Create the virtual environment
python3 -m venv ml-env

# 3. Activate the virtual environment
source ml-env/bin/activate

# 4. Install the required ML packages
pip install numpy pandas scikit-learn matplotlib

# 5. Capture installed packages into the requirements file
pip freeze > /root/code/requirements.txt
