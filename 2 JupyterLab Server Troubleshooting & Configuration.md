# Lab 2: JupyterLab Server Troubleshooting & Configuration

## 1. Scenario
A teammate has configured a JupyterLab server for the xFusionCorp Industries data science team; however, the server is not functioning as expected. Inspect the configuration, diagnose any issues, and start the server.

JupyterLab is already installed in the virtual environment at `/root/code/ml-env/`. The team's configuration file is at `/root/code/jupyter_lab_config.py` and is visible in the file explorer. Start the server with the config (e.g. `/root/code/ml-env/bin/jupyter lab --config /root/code/jupyter_lab_config.py`) and observe how it comes up so you can see what is misconfigured.

**End State Requirements:**
- The running server listens on port **8888**;
- It binds on **0.0.0.0**;
- The notebook root directory is **`/root/notebooks/`**, and that directory exists on disk.
- With the configuration corrected and JupyterLab running, the Jupyter UI button at the top of the lab opens the notebook interface.

---

## 2. Memorable Technique: The "BIN-Root" Checklist

To quickly spot and fix Jupyter configuration and startup issues, remember **"BIN-Root"**:
* **B** - **B**ind IP (`c.ServerApp.ip = '0.0.0.0'`) and Port (`c.ServerApp.port = 8888`)
* **I** - **I**nstall missing dependencies (`pip install notebook`)
* **N** - **N**otebook Directory (`c.ServerApp.root_dir = '/root/notebooks/'`)
* **Root** - Run with `--allow-root`

---

## 3. Step-by-Step Solution
---
### Step 1: Fix the Configuration File
Open `/root/code/jupyter_lab_config.py` using your preferred editor (like `vi` or `nano`) and ensure these specific lines exist and are uncommented:
```python
c.ServerApp.ip = '0.0.0.0'
c.ServerApp.port = 8888
c.ServerApp.root_dir = '/root/notebooks/'
c.ServerApp.open_browser = False

---

### Step 2: Prepare the Environment
Ensure the target notebook directory exists on disk and that the required notebook package is installed to prevent the ExtensionModuleNotFound error:
# Create the notebook directory
mkdir -p /root/notebooks

# Activate environment and install the missing notebook package
source /root/code/ml-env/bin/activate
pip install notebook

---

### Step 3: Start the JupyterLab Server
Run the server using the virtual environment binary, the configuration file, and the required flag to allow execution as the root user:
/root/code/ml-env/bin/jupyter lab --config /root/code/jupyter_lab_config.py --allow-root

---
4. Active Recall Review
Test yourself: Read the prompt, write down the exact fix or command from memory, then verify against the answers below.

Python
c.ServerApp.ip = '0.0.0.0'
c.ServerApp.port = 8888
Bash
pip install notebook
Command:

Bash
mkdir -p /root/notebooks
Config:

Python
c.ServerApp.root_dir = '/root/notebooks/'
Append the --allow-root flag to the startup command:

Bash
/root/code/ml-env/bin/jupyter lab --config /root/code/jupyter_lab_config.py --allow-root
