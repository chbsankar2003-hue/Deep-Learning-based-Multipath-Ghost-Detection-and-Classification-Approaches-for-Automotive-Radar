# Lab environment verification checklist

Run these commands on the university lab PC. They inspect the environment; they do not install or modify packages.

```bash
# Operating system and compiler
cat /etc/os-release
uname -a
gcc --version
g++ --version

# NVIDIA driver and GPU
nvidia-smi

# CUDA compiler, if installed/available
nvcc --version

# Conda environment
conda info --envs
conda activate <YOUR_EXISTING_WORKING_ENV>
python --version
which python
python -m pip --version

# Python packages
conda list
python -m pip show torch torchvision torchaudio numpy numba llvmlite spconv-cu118

# PyTorch CUDA visibility
python - <<'PY'
import sys
print("Python:", sys.version)
try:
    import torch
    print("PyTorch:", torch.__version__)
    print("PyTorch CUDA runtime:", torch.version.cuda)
    print("CUDA available:", torch.cuda.is_available())
    print("cuDNN:", torch.backends.cudnn.version())
    if torch.cuda.is_available():
        print("GPU:", torch.cuda.get_device_name(0))
        x = torch.randn(1024, 1024, device="cuda")
        print("GPU tensor test:", (x @ x).mean().item())
except Exception as e:
    print("PyTorch/CUDA check failed:", repr(e))
PY
```

Save the terminal output in your private lab notes. Before changing a working environment, capture its package list:

```bash
conda list --explicit > lab-conda-explicit.txt
python -m pip freeze > lab-pip-freeze.txt
```

These environment export files are machine-specific; do not commit them until reviewed and cleaned of local/private paths or credentials.

## Important compatibility notes

- The supervisor's example is PyTorch 2.6.0 + torchvision 0.21.0 + torchaudio 2.6.0 using the CUDA 11.8 wheel index, with `spconv-cu118`.
- The PyTorch CUDA wheel supplies its own CUDA runtime libraries. The locally installed NVIDIA driver must support that runtime. `nvidia-smi` reports driver capability; `torch.version.cuda` reports the CUDA runtime against which the installed PyTorch was built. They are different things.
- CUDA toolkit/compiler, PyTorch CUDA runtime, and spconv build must be compatible. Do not blindly install a second CUDA toolkit or upgrade packages in an environment that already works.
- The supervisor's suggested NumPy 1.23.0 and Numba 0.57 are a legacy-compatible set. The exact Python version and dependency resolver outcome matter; inspect `conda list` and pip output.
- Build OpenPCDet's CUDA extensions in the target environment using a compatible GCC/G++ toolchain. If compilation fails, preserve the complete error and diagnose the first failing compiler/build message rather than randomly changing packages.
