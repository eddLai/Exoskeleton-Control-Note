mocap_EMG_data: https://drive.google.com/drive/folders/1d8PC6TvaRWXRju_GHbBgCVanqYTLGN0C?usp=drive_link
policy weights tar file: https://drive.google.com/file/d/1Q020TqpAnvsIrE50PXTvgAyIQ_GksF4W/view?usp=sharing

```
git clone https://github.com/eddLai/ExoskeletonPowerAsistance.git
mv mocap_EMG_EEG_data ./ExoskeletonPowerAsistance/simulation/
mamba env create -n inverse_analysis -f opensim_conda_env_setup.yml
mamba create -n forward_sim python=3.9 -y
conda activate forward_sim
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
mamba install conda-forge::poetry
scone_2.4.0_amd64.deb
git clone 
cd /depRL
poetry install
sudo apt install ./scone_2.4.0_amd64.deb -y
```

`scp .\mocap_EMG_EEG_data.zip exo@120.126.94.127:~/Downloads`

`tar -cvJf sconewalk_h0918_osimv1_HPC.tar.xz -C . sconewalk_h0918_osimv1_HPC`