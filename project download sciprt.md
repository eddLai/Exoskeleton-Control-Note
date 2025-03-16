mocap_EMG_data: https://drive.google.com/drive/folders/1d8PC6TvaRWXRju_GHbBgCVanqYTLGN0C?usp=drive_link
policy weights tar file: https://drive.google.com/file/d/1Q020TqpAnvsIrE50PXTvgAyIQ_GksF4W/view?usp=sharing

先設定好git SSH
```
git clone https://github.com/eddLai/ExoskeletonPowerAsistance.git
cd ExoskeletonPowerAsistance
cd simulation
gdown --id 1jEMlAi7FMF9ZeB3SJ5YAlvDcV3I7zFv_ -O mocap_EMG_EEG_data.tar.xz
mkdir -p mocap_EMG_EEG_data
tar -xvJf mocap_EMG_EEG_data.tar.xz -C mocap_EMG_EEG_data && rm mocap_EMG_EEG_data.tar.xz
mamba env create -n inverse_analysis -f opensim_conda_env_setup.yml
sudo apt install ./simulation/SCONE_API/scone_2.4.0_amd64.deb -y
cd ..
mamba create -n forward_sim python=3.9 -y
conda activate forward_sim
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
mamba install conda-forge::poetry
git clone https://github.com/gnaixihZ/depRL.git
cd depRL
poetry install
cd baselines_DEPRL
gdown --id 1Q020TqpAnvsIrE50PXTvgAyIQ_GksF4W -O policy_weights.tar
tar -xvf policy_weights.tar
rm policy_weights.tar
cd ../..
git clone https://github.com/CEINMS/CEINMS.git
cd CEINMS
sudo apt update
sudo apt install libboost-filesystem-dev
wget https://www.codesynthesis.com/download/xsd/4.0/linux-gnu/x86_64/xsd_4.0.0-1_amd64.deb
sudo dpkg -i xsd_4.0.0-1_amd64.deb
mkdir build
cmake ..
make -j4
sudo make install
cd ../..
sudo apt install wine64 -y
sudo apt install wine32 -y
gdown --id 1VKVIoGIJhsN30GGOb3K5rqomcYUZb08a -O CEINMS_installer.exe
wine ./CEINMS_installer.exe
gdown --id 1mnYnl6BCFhDQBPrvsR3ZXEBAVQ80zDSR
wine OpenSim-3.3.0-win64VC13P.exe
alias WINE_CEINMS="wine $HOME/.wine/drive_c/Program\ Files/CEINMS\ 0.10/bin/CEINMS.exe"
source ~/.bashrc
WINE_CEINMS
```

`scp .\mocap_EMG_EEG_data.zip exo@120.126.94.127:~/Downloads`

`tar -cvJf sconewalk_h0918_osimv1_HPC.tar.xz -C . sconewalk_h0918_osimv1_HPC`

1. 還缺CEINMS編譯以及wine
2. opensim GUI是否必要


`tar -cvJf mocap_EMG_EEG_data.tar.xz -C mocap_EMG_EEG_data .`

按五下

```
#!/bin/bash
# Downloaded files should be placed in ~/Downloads or somewhere that can store at least three folders.
# ======================================================
# Exoskeleton Environment Setup Script
# ======================================================
# This script automates the setup of an exoskeleton
# simulation environment. It includes:
# - Installing Miniconda and Mamba
# - Cloning necessary GitHub repositories
# - Setting up Conda/Mamba environments
# - Installing dependencies such as CUDA, Boost, and Wine
# - Downloading and extracting required datasets
# - Configuring and compiling CEINMS
# - Running the CEINMS installer via Wine
# ======================================================

# Ensure the user has GitHub SSH access to the required repositories
echo "Make sure you have GitHub SSH access to the necessary repositories."
read -p "Press Enter to begin installation..."

# ======================================================
# Install Miniconda and Mamba
# ======================================================
echo "Installing Miniconda..."
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh

# Add Conda to PATH
source ~/miniconda3/bin/activate
conda init --all

# Install Mamba
echo "Installing Mamba..."
conda install -n base -c conda-forge mamba -y

# ======================================================
# Clone ExoskeletonPowerAsistance and extract dataset
# ======================================================
echo "Cloning ExoskeletonPowerAsistance repository..."
git clone git@github.com:eddLai/ExoskeletonPowerAsistance.git
pip install --upgrade gdown
cd ExoskeletonPowerAsistance/simulation
#!/bin/bash
cd ExoskeletonPowerAsistance/simulation
echo "Checking for existing mocap_EMG_EEG_data.tar.xz..."

# check file existence
if [ -f "mocap_EMG_EEG_data.tar.xz" ]; then
    echo "File mocap_EMG_EEG_data.tar.xz already exists. Skipping download."
else
    echo "File not found. Downloading mocap_EMG_EEG_data.tar.xz..."
    gdown --id 1jEMlAi7FMF9ZeB3SJ5YAlvDcV3I7zFv_ -O mocap_EMG_EEG_data.tar.xz
    if [ $? -ne 0 ]; then
        echo "Download failed!"
        exit 1
    fi
fi
if [ -f "mocap_EMG_EEG_data.tar.xz" ]; then
    echo "Extracting mocap_EMG_EEG_data.tar.xz..."
    mkdir -p mocap_EMG_EEG_data
    tar -xvJf mocap_EMG_EEG_data.tar.xz -C mocap_EMG_EEG_data && rm mocap_EMG_EEG_data.tar.xz
    echo "Extraction complete!"
else
    echo "Error: Downloaded file not found!"
    exit 1
fi

# ======================================================
# Create and activate the inverse_analysis conda environment
# ======================================================
echo "Creating Conda environment: inverse_analysis..."
mamba env create -n inverse_analysis -f opensim_conda_env_setup.yml

# ======================================================
# Install SCONE API
# ======================================================
echo "Installing SCONE API..."
sudo apt install ./SCONE_API/scone_2.4.0_amd64.deb -y

# ======================================================
# Create and activate the forward_sim environment
# ======================================================
echo "Creating Conda environment: forward_sim..."
mamba create -n forward_sim python=3.9 -y
conda activate forward_sim

# ======================================================
# Install CUDA Toolkit
# ======================================================
cd ..
echo "Installing CUDA Toolkit..."
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3

# ======================================================
# Install Poetry package manager
# ======================================================
echo "Installing Poetry..."
mamba install conda-forge::poetry -y

# ======================================================
# Clone and setup depRL
# ======================================================
echo "Cloning depRL repository..."
git clone git@github.com:gnaixihZ/depRL.git
cd depRL
poetry install

# Download and extract policy weights
mkdir -p baselines_DEPRL
cd baselines_DEPRL
echo "Downloading and extracting policy weights..."
gdown --id 1Q020TqpAnvsIrE50PXTvgAyIQ_GksF4W -O policy_weights.tar
tar -xvf policy_weights.tar && rm policy_weights.tar
cd ../..

# ======================================================
# Clone, build, and install CEINMS
# ======================================================
echo "Cloning CEINMS repository..."
git clone git@github.com:CEINMS/CEINMS.git
cd CEINMS

echo "Installing Boost and other dependencies..."
sudo apt update
sudo apt install libboost-filesystem-dev -y

echo "Downloading and installing CodeSynthesis XSD..."
wget https://www.codesynthesis.com/download/xsd/4.0/linux-gnu/x86_64/xsd_4.0.0-1_amd64.deb
sudo dpkg -i xsd_4.0.0-1_amd64.deb

echo "Building CEINMS..."
mkdir build && cd build
cmake ..
make -j4
sudo make install
cd ../..

# ======================================================
# Install Wine and setup CEINMS
# ======================================================
echo "Installing Wine..."
sudo apt install wine64 wine32 -y

# ======================================================
# Install CEINMS via Wine
# ======================================================
echo "Downloading CEINMS Installer..."
gdown --id 1VKVIoGIJhsN30GGOb3K5rqomcYUZb08a -O CEINMS_installer.exe
wine ./CEINMS_installer.exe

# ======================================================
# Install OpenSim
# ======================================================
echo "Downloading OpenSim Installer..."
gdown --id 1mnYnl6BCFhDQBPrvsR3ZXEBAVQ80zDSR -O OpenSim-3.3.0-win64VC13P.exe
wine OpenSim-3.3.0-win64VC13P.exe

# ======================================================
# Set up alias for CEINMS execution
# ======================================================
echo "Setting up CEINMS alias..."
CEINMS_PATH="$HOME/.wine/drive_c/Program Files/CEINMS 0.10/bin/CEINMS.exe"

if [ -f "$CEINMS_PATH" ]; then
    chmod +x "$CEINMS_PATH"
else
    echo "Error: CEINMS.exe not found at $CEINMS_PATH!"
    exit 1
fi

# for shell
export WINE_CEINMS="wine \"$CEINMS_PATH\""

# for setup permanently
if ! grep -q "alias WINE_CEINMS=" ~/.bashrc; then
    echo "alias WINE_CEINMS='wine \"$CEINMS_PATH\"'" >> ~/.bashrc
    echo "export WINE_CEINMS='wine \"$CEINMS_PATH\"'" >> ~/.bashrc
    echo "CEINMS alias added to ~/.bashrc"
fi

source ~/.bashrc
# ======================================================
# Run CEINMS
# ======================================================
echo "Running CEINMS..."
eval $WINE_CEINMS


```