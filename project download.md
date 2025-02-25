```
git clone https://github.com/eddLai/ExoskeletonPowerAsistance.git
scp .\mocap_EMG_EEG_data.zip exo@120.126.94.127:~/Downloads
mv mocap_EMG_EEG_data ./ExoskeletonPowerAsistance/simulation/
mamba create -n inverse_analysis python=3.11 -y
mamba create -n forward_sim python=3.9 -y

```
