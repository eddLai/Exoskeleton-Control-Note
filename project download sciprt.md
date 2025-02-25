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
wine

```

`scp .\mocap_EMG_EEG_data.zip exo@120.126.94.127:~/Downloads`

`tar -cvJf sconewalk_h0918_osimv1_HPC.tar.xz -C . sconewalk_h0918_osimv1_HPC`

1. 還缺CEINMS編譯以及wine
2. opensim GUI是否必要


`tar -cvJf mocap_EMG_EEG_data.tar.xz -C mocap_EMG_EEG_data .`

按五下