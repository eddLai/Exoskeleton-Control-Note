```
git clone https://github.com/eddLai/ExoskeletonPowerAsistance.git
scp .\mocap_EMG_EEG_data.zip exo@120.126.94.127:~/Downloads
mv mocap_EMG_EEG_data ./ExoskeletonPowerAsistance/simulation/
mamba env create -n inverse_analysis -f opensim_conda_env_setup.yml
mamba create -n forward_sim python=3.9 -y
conda activate forward_sim

```
