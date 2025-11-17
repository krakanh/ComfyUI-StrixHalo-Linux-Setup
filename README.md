# ComfyUI-StrixHalo-Linux-Setup
This repository provides a ready-to-use setup for running ComfyUI on Linux systems (tested on Mint and Ubuntu 22.04) with AMD GPUs, specifically for Strix Halo hardware.




Step 1: Create the Conda Environment

# Create a new Conda environment named "comfyui" with Python 3.12

       conda create -n comfy python=3.12

# Activate the environment

       conda activate comfy

Step 2: Upgrade pip and Download ROCm Wheel Files

First, upgrade pip and wheel inside the Conda environment:

      pip3 install --upgrade pip wheel
      
Then, download the ROCm-specific wheel files for PyTorch, TorchVision, Triton, and TorchAudio:

      wget https://repo.radeon.com/rocm/manylinux/rocm-rel-7.1/torch-2.8.0%2Brocm7.1.0.lw.git7a520360-cp312-cp312-linux_x86_64.whl
      wget https://repo.radeon.com/rocm/manylinux/rocm-rel-7.1/torchvision-0.23.0%2Brocm7.1.0.git824e8c87-cp312-cp312-linux_x86_64.whl 
      wget https://repo.radeon.com/rocm/manylinux/rocm-rel-7.1/triton-3.4.0%2Brocm7.1.0.gitf9e5bf54-cp312-cp312-linux_x86_64.whl 
      wget https://repo.radeon.com/rocm/manylinux/rocm-rel-7.1/torchaudio-2.8.0%2Brocm7.1.0.git6e1c7fe9-cp312-cp312-linux_x86_64.whl

 Finally, install them all at once:

     
       pip3 install torch-2.8.0+rocm7.1.0.lw.git7a520360-cp312-cp312-linux_x86_64.whl \
            torchvision-0.23.0+rocm7.1.0.git824e8c87-cp312-cp312-linux_x86_64.whl \
            torchaudio-2.8.0+rocm7.1.0.git6e1c7fe9-cp312-cp312-linux_x86_64.whl \
            triton-3.4.0+rocm7.1.0.gitf9e5bf54-cp312-cp312-linux_x86_64.whl


Step 3: Download ComfyUI and Install Requirements

Clone ComfyUI from GitHub:

     git clone https://github.com/comfyanonymous/ComfyUI.git

Navigate into the ComfyUI directory:

     cd ComfyUI

Edit the requirements.txt file

Open requirements.txt in your favorite editor (or use nano requirements.txt)

Delete the following lines:

   torch
   torchvision
   torchaudio

Save it

Install the remaining requirements:

     pip3 install -r requirements.txt

     
Step 4: Run ComfyUI with the Launch Script

Create a script on your Desktop (or anywhere you prefer) to launch ComfyUI easily. Make sure to update paths depending on where Conda and ComfyUI are installed.

Example run_comfyui.sh:

    #!/bin/bash

    # Activate Conda (path may vary depending on your installation)
    source ~/miniconda3/etc/profile.d/conda.sh

    # Activate the ComfyUI environment
    conda activate comfy

    # Disable cuDNN for AMD GPU performance
    export PYTORCH_CUDNN_ENABLED=0

    # Navigate to the ComfyUI directory
    cd /home/iva/ComfyUI

    # Launch ComfyUI
    python main.py


Instructions:

Save this script on your Desktop as run_comfyui.sh.

Make it executable:

    chmod +x ~/Desktop/run_comfyui.sh

And run it:

    ~/Desktop/run_comfyui.sh

> Note: This setup is inspired by guides and scripts shared by others in the community.  
> I adapted and tested it specifically for AMD GPUs (Strix Halo) on Linux Mint and Ubuntu 22.04.  
> Some parts have been modified to fix issues like `'NoneType' object has no attribute 'dtype'`.
