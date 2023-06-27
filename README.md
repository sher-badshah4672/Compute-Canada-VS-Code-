# Using Compute Canada resources with VS Code for GPU programming

This guide will help you set up your Compute Canada environment with VS Code for GPU programming and job allocation.

## Prerequisites

- SSH Extension in VS Code
- Jupyter Notebook extension in VS Code
- An account on Compute Canada with access to GPU resources

## Steps

### 1. Connect to Compute Canada via SSH in VS Code

- Open VS Code.
- Click on the green bottom-left button (Remote - SSH).
- Enter your Compute Canada credentials (username@server.computecanada.ca).

### 2. Set up your virtual environment

- Once connected, open a terminal in VS Code.
- Create a new virtual environment (replace `my_venv` with your desired environment name): `python -m venv my_venv`
- Activate the environment: `source my_venv/bin/activate`
- Install necessary packages (like `torch`): `pip install pytorch`

### 3. Check for GPU availability

- Run the following command: `nvidia-smi`. 
  - If you get an error saying `NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.`, this means you are not on a GPU node.

### 4. Allocate GPU resources

- Run the following command to allocate GPU resources: `salloc --time=1:00:00 --gres=gpu:1 --cpus-per-task=1 --account=def-<YourComputeCanadaAccount> --mem=8G`. 
  - Replace `<YourComputeCanadaAccount>` with your Compute Canada account name.
  - Adjust time, GPU, CPU, and memory allocation as per your needs.

### 5. Run Jupyter Notebook server

- Once you have allocated resources and are on a GPU node, run the following command to start a Jupyter notebook server: `jupyter notebook --no-browser --ip=0.0.0.0 --port=8888`. 

### 6. Connect VS Code to the Jupyter server

- In VS Code, open the Command Palette (`F1` or `Ctrl+Shift+P`).
- Enter `Jupyter: Create New Blank Notebook`.
- Click on the "Select Kernel" button in the top-right of the notebook interface.
- Click on the "Add kernel" button at the bottom of the kernel selection list.
- You'll be asked for the URL of the Jupyter server. Enter the URL provided by the server when you started it.
- The new kernel should now appear in the kernel list. Select it to use it for your notebook.

### 7. Test GPU in Jupyter notebook

- In a new Jupyter notebook cell, run the following Python code to check if GPU is available: 

```python
import torch
torch.cuda.is_available()
```

- If it returns True, it means GPU is available in your Jupyter notebook.

