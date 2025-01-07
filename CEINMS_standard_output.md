- Trial的次數
- 或者CEINMS_setup迭代的設定

```
algorithm_params = {
        "noEpsilon": 3,
        "rt": 0.3,
        "T": 200000,
        "NS": 30,
        "NT": 20,
        "epsilon": 1.E-4,
        "maxNoEval": 800000,
    }
```

T大，會在初期廣泛搜尋
$r_t: 0.1 \rightarrow 0.3$ 需要減小
maxNoEval: 800000，需要加大

# On windows
```
PS D:\CEINMS_TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1> CEINMScalibrate -S .\calibrationSetup_1.xml

+-+-+-+-+-+-+
|C|E|I|N|M|S|
+-+-+-+-+-+-+-+-+-+-+
|C|a|l|i|b|r|a|t|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+
|E|M|G|-|I|n|f|o|r|m|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|N|e|u|r|o|m|u|s|c|u|l|o|s|k|e|l|e|t|a|l|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|T|o|o|l|b|o|x|
+-+-+-+-+-+-+-+

Calibration

Copyright (C) 2024
Claudio Pizzolato, Monica Reggiani, Massimo Sartori, David Lloyd

Software developers: Claudio Pizzolato, Monica Reggiani
readNMSmodelCfg
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
Contact model  not found
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
activeForceLength
passiveForceLength
forceVelocity
tendonForceStrain
Assuming bifemlh_r pennation angle in radians: 0
Assuming bifemsh_r pennation angle in radians: 0.401426
Assuming grac_r pennation angle in radians: 0.0523599
Assuming lat_gas_r pennation angle in radians: 0.139626
Assuming med_gas_r pennation angle in radians: 0.296706
Assuming per_brev_r pennation angle in radians: 0.0872665
Assuming per_long_r pennation angle in radians: 0.174533
Assuming per_tert_r pennation angle in radians: 0.226893
Assuming rect_fem_r pennation angle in radians: 0.0872665
Assuming sar_r pennation angle in radians: 0
Assuming semimem_r pennation angle in radians: 0.261799
Assuming semiten_r pennation angle in radians: 0.0872665
Assuming soleus_r pennation angle in radians: 0.436332
Assuming tib_ant_r pennation angle in radians: 0.0872665
Assuming vas_int_r pennation angle in radians: 0.0523599
Assuming vas_lat_r pennation angle in radians: 0.0872665
Assuming vas_med_r pennation angle in radians: 0.0872665
No OpenSim model associated to the subject

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og3\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_smooth4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/calTrials/..\..\..\dynamicElaborations\calibrationTrials\calibrationTrials_DM_calfrise1\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE
CalibrationStepCfg 100
 --- DoFs: knee_angle_r ankle_angle_r
 --- Objective Function: Minimize Torque Error

 ---- Parameter: c1
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: c2
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: shapeFactor
 ---- Global
 ----- Absolute Range -2.999 -0.001

 ---- Parameter: tendonSlackLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: optimalFibreLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: strengthCoefficient
 ---- Grouped:
 ----- Group: bifemlh_r bifemsh_r semimem_r semiten_r
 ----- Group: grac_r
 ----- Group: sar_r
 ----- Group: lat_gas_r med_gas_r soleus_r
 ----- Group: per_brev_r per_long_r
 ----- Group: per_tert_r tib_ant_r
 ----- Group: rect_fem_r vas_int_r vas_lat_r vas_med_r
 ----- Absolute Range 0.5 3.5

knee_angle_r
ankle_angle_r
Return false
fLatest_.at(0) - fOpt_ = 640.412 - 54.0381 > 0.001
Joint moments RMSE
...
Fobj = 2.73018
Return false
fLatest_.at(3) - fOpt_ = 2.73356 - 2.73017 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7644 Nm
ankle_angle_r 7.0829 Nm

Trial #2
knee_angle_r 9.71743 Nm
ankle_angle_r 9.25537 Nm

Trial #3
knee_angle_r 9.0735 Nm
ankle_angle_r 8.08553 Nm

Trial #4
knee_angle_r 7.2015 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Return true!
fOpt_ = 2.73017
Joint moments RMSE
Trial #1
knee_angle_r 10.7642 Nm
ankle_angle_r 7.08367 Nm

Trial #2
knee_angle_r 9.71729 Nm
ankle_angle_r 9.25521 Nm

Trial #3
knee_angle_r 9.07343 Nm
ankle_angle_r 8.08559 Nm

Trial #4
knee_angle_r 7.20163 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
Calibration time: 2477072ms
```

## windows detailed(1)
```
(base) PS D:\CEINMS_TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1> CEINMScalibrate -S .\calibrationSetup_1.xml

+-+-+-+-+-+-+
|C|E|I|N|M|S|
+-+-+-+-+-+-+-+-+-+-+
|C|a|l|i|b|r|a|t|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+
|E|M|G|-|I|n|f|o|r|m|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|N|e|u|r|o|m|u|s|c|u|l|o|s|k|e|l|e|t|a|l|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|T|o|o|l|b|o|x|
+-+-+-+-+-+-+-+

Calibration

Copyright (C) 2025
Claudio Pizzolato, Monica Reggiani, Massimo Sartori, David Lloyd

Software developers: Claudio Pizzolato, Monica Reggiani
readNMSmodelCfg
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
Contact model  not found
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
activeForceLength
passiveForceLength
forceVelocity
tendonForceStrain
Assuming bifemlh_r pennation angle in radians: 0
Assuming bifemsh_r pennation angle in radians: 0.401426
Assuming grac_r pennation angle in radians: 0.0523599
Assuming lat_gas_r pennation angle in radians: 0.139626
Assuming med_gas_r pennation angle in radians: 0.296706
Assuming per_brev_r pennation angle in radians: 0.0872665
Assuming per_long_r pennation angle in radians: 0.174533
Assuming per_tert_r pennation angle in radians: 0.226893
Assuming rect_fem_r pennation angle in radians: 0.0872665
Assuming sar_r pennation angle in radians: 0
Assuming semimem_r pennation angle in radians: 0.261799
Assuming semiten_r pennation angle in radians: 0.0872665
Assuming soleus_r pennation angle in radians: 0.436332
Assuming tib_ant_r pennation angle in radians: 0.0872665
Assuming vas_int_r pennation angle in radians: 0.0523599
Assuming vas_lat_r pennation angle in radians: 0.0872665
Assuming vas_med_r pennation angle in radians: 0.0872665
No OpenSim model associated to the subject

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og3\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_smooth4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file....\../../Cfg/Rstance1/../../../trials/calTrials/..\..\..\dynamicElaborations\calibrationTrials\calibrationTrials_DM_calfrise1\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE
CalibrationStepCfg 100
 --- DoFs: knee_angle_r ankle_angle_r
 --- Objective Function: Minimize Torque Error

 ---- Parameter: c1
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: c2
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: shapeFactor
 ---- Global
 ----- Absolute Range -2.999 -0.001

 ---- Parameter: tendonSlackLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: optimalFibreLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: strengthCoefficient
 ---- Grouped:
 ----- Group: bifemlh_r bifemsh_r semimem_r semiten_r
 ----- Group: grac_r
 ----- Group: sar_r
 ----- Group: lat_gas_r med_gas_r soleus_r
 ----- Group: per_brev_r per_long_r
 ----- Group: per_tert_r tib_ant_r
 ----- Group: rect_fem_r vas_int_r vas_lat_r vas_med_r
 ----- Absolute Range 0.5 3.5

knee_angle_r
ankle_angle_r
Return false
fLatest_.at(0) - fOpt_ = 640.412 - 54.0381 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 36.2077 Nm
ankle_angle_r 220.1 Nm

Trial #2
knee_angle_r 42.6964 Nm
ankle_angle_r 207.594 Nm

Trial #3
knee_angle_r 55.7904 Nm
ankle_angle_r 187.197 Nm

Trial #4
knee_angle_r 38.0966 Nm
ankle_angle_r 193.736 Nm

Fobj = 640.412
Return false
fLatest_.at(0) - fOpt_ = 2111.06 - 38.1714 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 191.148 Nm
ankle_angle_r 322.87 Nm

Trial #2
knee_angle_r 222.481 Nm
ankle_angle_r 290.037 Nm

Trial #3
knee_angle_r 259.532 Nm
ankle_angle_r 291.918 Nm

Trial #4
knee_angle_r 201.302 Nm
ankle_angle_r 195.385 Nm

Fobj = 2111.06
Return false
fLatest_.at(0) - fOpt_ = 452.614 - 25.9363 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 105.876 Nm
ankle_angle_r 81.8706 Nm

Trial #2
knee_angle_r 125.838 Nm
ankle_angle_r 72.9519 Nm

Trial #3
knee_angle_r 164.156 Nm
ankle_angle_r 75.4825 Nm

Trial #4
knee_angle_r 91.3024 Nm
ankle_angle_r 69.7034 Nm

Fobj = 452.614
Return false
fLatest_.at(0) - fOpt_ = 140.954 - 13.5397 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 48.0518 Nm
ankle_angle_r 71.4121 Nm

Trial #2
knee_angle_r 51.2763 Nm
ankle_angle_r 64.2763 Nm

Trial #3
knee_angle_r 72.4255 Nm
ankle_angle_r 62.804 Nm

Trial #4
knee_angle_r 29.0202 Nm
ankle_angle_r 72.8846 Nm

Fobj = 140.954
Return false
fLatest_.at(0) - fOpt_ = 43.1891 - 13.326 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 55.3567 Nm
ankle_angle_r 14.2976 Nm

Trial #2
knee_angle_r 62.7453 Nm
ankle_angle_r 18.2313 Nm

Trial #3
knee_angle_r 74.7244 Nm
ankle_angle_r 15.4354 Nm

Trial #4
knee_angle_r 43.9775 Nm
ankle_angle_r 14.2406 Nm

Fobj = 101.025
Return false
fLatest_.at(0) - fOpt_ = 11.5633 - 5.13097 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 19.6873 Nm
ankle_angle_r 10.7808 Nm

Trial #2
knee_angle_r 21.2491 Nm
ankle_angle_r 11.233 Nm

Trial #3
knee_angle_r 26.4146 Nm
ankle_angle_r 13.1386 Nm

Trial #4
knee_angle_r 12.6108 Nm
ankle_angle_r 10.8522 Nm

Fobj = 11.5633
Return false
fLatest_.at(0) - fOpt_ = 4.78919 - 4.0689 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 100.01 Nm
ankle_angle_r 3.91535 Nm

Trial #2
knee_angle_r 111.345 Nm
ankle_angle_r 14.8876 Nm

Trial #3
knee_angle_r 132.123 Nm
ankle_angle_r 10.4868 Nm

Trial #4
knee_angle_r 110.907 Nm
ankle_angle_r 7.07429 Nm

Fobj = 375.998
Return false
fLatest_.at(0) - fOpt_ = 3.13153 - 2.99324 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 11.3174 Nm
ankle_angle_r 9.03905 Nm

Trial #2
knee_angle_r 10.571 Nm
ankle_angle_r 8.07521 Nm

Trial #3
knee_angle_r 10.0566 Nm
ankle_angle_r 8.73544 Nm

Trial #4
knee_angle_r 7.19333 Nm
ankle_angle_r 5.49727 Nm

Fobj = 3.13153
Return false
fLatest_.at(0) - fOpt_ = 2.79069 - 2.76898 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.9779 Nm
ankle_angle_r 7.30923 Nm

Trial #2
knee_angle_r 10.1047 Nm
ankle_angle_r 9.36873 Nm

Trial #3
knee_angle_r 9.50101 Nm
ankle_angle_r 8.473 Nm

Trial #4
knee_angle_r 6.85664 Nm
ankle_angle_r 4.43642 Nm

Fobj = 2.79424
Return false
fLatest_.at(0) - fOpt_ = 2.74224 - 2.74104 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.6681 Nm
ankle_angle_r 7.60007 Nm

Trial #2
knee_angle_r 9.70276 Nm
ankle_angle_r 9.65135 Nm

Trial #3
knee_angle_r 9.11319 Nm
ankle_angle_r 8.39732 Nm

Trial #4
knee_angle_r 7.18712 Nm
ankle_angle_r 4.2821 Nm

Fobj = 2.74331
Return false
fLatest_.at(1) - fOpt_ = 2.74224 - 2.73352 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7131 Nm
ankle_angle_r 7.28468 Nm

Trial #2
knee_angle_r 9.67844 Nm
ankle_angle_r 9.41547 Nm

Trial #3
knee_angle_r 9.05603 Nm
ankle_angle_r 8.21512 Nm

Trial #4
knee_angle_r 7.23558 Nm
ankle_angle_r 4.24283 Nm

Fobj = 2.73356
Return false
fLatest_.at(1) - fOpt_ = 2.73356 - 2.73033 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 19.6101 Nm
ankle_angle_r 7.11038 Nm

Trial #2
knee_angle_r 21.2527 Nm
ankle_angle_r 9.26522 Nm

Trial #3
knee_angle_r 21.5435 Nm
ankle_angle_r 8.09075 Nm

Trial #4
knee_angle_r 12.6989 Nm
ankle_angle_r 4.25768 Nm

Fobj = 9.47745
Return false
fLatest_.at(2) - fOpt_ = 2.73356 - 2.73018 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7642 Nm
ankle_angle_r 7.08372 Nm

Trial #2
knee_angle_r 9.7173 Nm
ankle_angle_r 9.25412 Nm

Trial #3
knee_angle_r 9.07335 Nm
ankle_angle_r 8.08514 Nm

Trial #4
knee_angle_r 7.20175 Nm
ankle_angle_r 4.25991 Nm

Fobj = 2.73018
Return false
fLatest_.at(3) - fOpt_ = 2.73356 - 2.73017 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7644 Nm
ankle_angle_r 7.0829 Nm

Trial #2
knee_angle_r 9.71743 Nm
ankle_angle_r 9.25537 Nm

Trial #3
knee_angle_r 9.0735 Nm
ankle_angle_r 8.08553 Nm

Trial #4
knee_angle_r 7.2015 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Return true!
fOpt_ = 2.73017
Joint moments RMSE
Trial #1
knee_angle_r 10.7642 Nm
ankle_angle_r 7.08367 Nm

Trial #2
knee_angle_r 9.71729 Nm
ankle_angle_r 9.25521 Nm

Trial #3
knee_angle_r 9.07343 Nm
ankle_angle_r 8.08559 Nm

Trial #4
knee_angle_r 7.20163 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Reading subject file: .\../../uncalibrated/DM_uncalibrated.xml .
Calibration time: 3153698ms
```
## windows detailed(2)
```
PS C:\Users\sean9> CEINMScalibrate -S C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\calibrationSetup_1.xml

+-+-+-+-+-+-+
|C|E|I|N|M|S|
+-+-+-+-+-+-+-+-+-+-+
|C|a|l|i|b|r|a|t|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+
|E|M|G|-|I|n|f|o|r|m|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|N|e|u|r|o|m|u|s|c|u|l|o|s|k|e|l|e|t|a|l|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|T|o|o|l|b|o|x|
+-+-+-+-+-+-+-+

Calibration

Copyright (C) 2025
Claudio Pizzolato, Monica Reggiani, Massimo Sartori, David Lloyd

Software developers: Claudio Pizzolato, Monica Reggiani
readNMSmodelCfg
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
Contact model  not found
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
activeForceLength
passiveForceLength
forceVelocity
tendonForceStrain
Assuming bifemlh_r pennation angle in radians: 0
Assuming bifemsh_r pennation angle in radians: 0.401426
Assuming grac_r pennation angle in radians: 0.0523599
Assuming lat_gas_r pennation angle in radians: 0.139626
Assuming med_gas_r pennation angle in radians: 0.296706
Assuming per_brev_r pennation angle in radians: 0.0872665
Assuming per_long_r pennation angle in radians: 0.174533
Assuming per_tert_r pennation angle in radians: 0.226893
Assuming rect_fem_r pennation angle in radians: 0.0872665
Assuming sar_r pennation angle in radians: 0
Assuming semimem_r pennation angle in radians: 0.261799
Assuming semiten_r pennation angle in radians: 0.0872665
Assuming soleus_r pennation angle in radians: 0.436332
Assuming tib_ant_r pennation angle in radians: 0.0872665
Assuming vas_int_r pennation angle in radians: 0.0523599
Assuming vas_lat_r pennation angle in radians: 0.0872665
Assuming vas_med_r pennation angle in radians: 0.0872665
No OpenSim model associated to the subject

EMG: Reading emg file...C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og3\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file...C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file...C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_smooth4\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE

EMG: Reading emg file...C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../Cfg/Rstance1/../../../trials/calTrials/..\..\..\dynamicElaborations\calibrationTrials\calibrationTrials_DM_calfrise1\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE
CalibrationStepCfg 100
 --- DoFs: knee_angle_r ankle_angle_r
 --- Objective Function: Minimize Torque Error

 ---- Parameter: c1
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: c2
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: shapeFactor
 ---- Global
 ----- Absolute Range -2.999 -0.001

 ---- Parameter: tendonSlackLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: optimalFibreLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: strengthCoefficient
 ---- Grouped:
 ----- Group: bifemlh_r bifemsh_r semimem_r semiten_r
 ----- Group: grac_r
 ----- Group: sar_r
 ----- Group: lat_gas_r med_gas_r soleus_r
 ----- Group: per_brev_r per_long_r
 ----- Group: per_tert_r tib_ant_r
 ----- Group: rect_fem_r vas_int_r vas_lat_r vas_med_r
 ----- Absolute Range 0.5 3.5

knee_angle_r
ankle_angle_r
Return false
fLatest_.at(0) - fOpt_ = 640.412 - 54.0381 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 36.2077 Nm
ankle_angle_r 220.1 Nm

Trial #2
knee_angle_r 42.6964 Nm
ankle_angle_r 207.594 Nm

Trial #3
knee_angle_r 55.7904 Nm
ankle_angle_r 187.197 Nm

Trial #4
knee_angle_r 38.0966 Nm
ankle_angle_r 193.736 Nm

Fobj = 640.412
Return false
fLatest_.at(0) - fOpt_ = 2111.06 - 38.1714 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 191.148 Nm
ankle_angle_r 322.87 Nm

Trial #2
knee_angle_r 222.481 Nm
ankle_angle_r 290.037 Nm

Trial #3
knee_angle_r 259.532 Nm
ankle_angle_r 291.918 Nm

Trial #4
knee_angle_r 201.302 Nm
ankle_angle_r 195.385 Nm

Fobj = 2111.06
Return false
fLatest_.at(0) - fOpt_ = 452.614 - 25.9363 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 105.876 Nm
ankle_angle_r 81.8706 Nm

Trial #2
knee_angle_r 125.838 Nm
ankle_angle_r 72.9519 Nm

Trial #3
knee_angle_r 164.156 Nm
ankle_angle_r 75.4825 Nm

Trial #4
knee_angle_r 91.3024 Nm
ankle_angle_r 69.7034 Nm

Fobj = 452.614
Return false
fLatest_.at(0) - fOpt_ = 140.954 - 13.5397 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 48.0518 Nm
ankle_angle_r 71.4121 Nm

Trial #2
knee_angle_r 51.2763 Nm
ankle_angle_r 64.2763 Nm

Trial #3
knee_angle_r 72.4255 Nm
ankle_angle_r 62.804 Nm

Trial #4
knee_angle_r 29.0202 Nm
ankle_angle_r 72.8846 Nm

Fobj = 140.954
Return false
fLatest_.at(0) - fOpt_ = 43.1891 - 13.326 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 55.3567 Nm
ankle_angle_r 14.2976 Nm

Trial #2
knee_angle_r 62.7453 Nm
ankle_angle_r 18.2313 Nm

Trial #3
knee_angle_r 74.7244 Nm
ankle_angle_r 15.4354 Nm

Trial #4
knee_angle_r 43.9775 Nm
ankle_angle_r 14.2406 Nm

Fobj = 101.025
Return false
fLatest_.at(0) - fOpt_ = 11.5633 - 5.13097 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 19.6873 Nm
ankle_angle_r 10.7808 Nm

Trial #2
knee_angle_r 21.2491 Nm
ankle_angle_r 11.233 Nm

Trial #3
knee_angle_r 26.4146 Nm
ankle_angle_r 13.1386 Nm

Trial #4
knee_angle_r 12.6108 Nm
ankle_angle_r 10.8522 Nm

Fobj = 11.5633
Return false
fLatest_.at(0) - fOpt_ = 4.78919 - 4.0689 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 100.01 Nm
ankle_angle_r 3.91535 Nm

Trial #2
knee_angle_r 111.345 Nm
ankle_angle_r 14.8876 Nm

Trial #3
knee_angle_r 132.123 Nm
ankle_angle_r 10.4868 Nm

Trial #4
knee_angle_r 110.907 Nm
ankle_angle_r 7.07429 Nm

Fobj = 375.998
Return false
fLatest_.at(0) - fOpt_ = 3.13153 - 2.99324 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 11.3174 Nm
ankle_angle_r 9.03905 Nm

Trial #2
knee_angle_r 10.571 Nm
ankle_angle_r 8.07521 Nm

Trial #3
knee_angle_r 10.0566 Nm
ankle_angle_r 8.73544 Nm

Trial #4
knee_angle_r 7.19333 Nm
ankle_angle_r 5.49727 Nm

Fobj = 3.13153
Return false
fLatest_.at(0) - fOpt_ = 2.79069 - 2.76898 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.9779 Nm
ankle_angle_r 7.30923 Nm

Trial #2
knee_angle_r 10.1047 Nm
ankle_angle_r 9.36873 Nm

Trial #3
knee_angle_r 9.50101 Nm
ankle_angle_r 8.473 Nm

Trial #4
knee_angle_r 6.85664 Nm
ankle_angle_r 4.43642 Nm

Fobj = 2.79424
Return false
fLatest_.at(0) - fOpt_ = 2.74224 - 2.74104 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.6681 Nm
ankle_angle_r 7.60007 Nm

Trial #2
knee_angle_r 9.70276 Nm
ankle_angle_r 9.65135 Nm

Trial #3
knee_angle_r 9.11319 Nm
ankle_angle_r 8.39732 Nm

Trial #4
knee_angle_r 7.18712 Nm
ankle_angle_r 4.2821 Nm

Fobj = 2.74331
Return false
fLatest_.at(1) - fOpt_ = 2.74224 - 2.73352 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7131 Nm
ankle_angle_r 7.28468 Nm

Trial #2
knee_angle_r 9.67844 Nm
ankle_angle_r 9.41547 Nm

Trial #3
knee_angle_r 9.05603 Nm
ankle_angle_r 8.21512 Nm

Trial #4
knee_angle_r 7.23558 Nm
ankle_angle_r 4.24283 Nm

Fobj = 2.73356
Return false
fLatest_.at(1) - fOpt_ = 2.73356 - 2.73033 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 19.6101 Nm
ankle_angle_r 7.11038 Nm

Trial #2
knee_angle_r 21.2527 Nm
ankle_angle_r 9.26522 Nm

Trial #3
knee_angle_r 21.5435 Nm
ankle_angle_r 8.09075 Nm

Trial #4
knee_angle_r 12.6989 Nm
ankle_angle_r 4.25768 Nm

Fobj = 9.47745
Return false
fLatest_.at(2) - fOpt_ = 2.73356 - 2.73018 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7642 Nm
ankle_angle_r 7.08372 Nm

Trial #2
knee_angle_r 9.7173 Nm
ankle_angle_r 9.25412 Nm

Trial #3
knee_angle_r 9.07335 Nm
ankle_angle_r 8.08514 Nm

Trial #4
knee_angle_r 7.20175 Nm
ankle_angle_r 4.25991 Nm

Fobj = 2.73018
Return false
fLatest_.at(3) - fOpt_ = 2.73356 - 2.73017 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 10.7644 Nm
ankle_angle_r 7.0829 Nm

Trial #2
knee_angle_r 9.71743 Nm
ankle_angle_r 9.25537 Nm

Trial #3
knee_angle_r 9.0735 Nm
ankle_angle_r 8.08553 Nm

Trial #4
knee_angle_r 7.2015 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Return true!
fOpt_ = 2.73017
Joint moments RMSE
Trial #1
knee_angle_r 10.7642 Nm
ankle_angle_r 7.08367 Nm

Trial #2
knee_angle_r 9.71729 Nm
ankle_angle_r 9.25521 Nm

Trial #3
knee_angle_r 9.07343 Nm
ankle_angle_r 8.08559 Nm

Trial #4
knee_angle_r 7.20163 Nm
ankle_angle_r 4.25968 Nm

Fobj = 2.73017
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
Calibration time: 6393019ms
```

## Trialset減少
```
PS C:\Users\sean9> CEINMScalibrate -S C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\calibrationSetup_1.xml

+-+-+-+-+-+-+
|C|E|I|N|M|S|
+-+-+-+-+-+-+-+-+-+-+
|C|a|l|i|b|r|a|t|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+
|E|M|G|-|I|n|f|o|r|m|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|N|e|u|r|o|m|u|s|c|u|l|o|s|k|e|l|e|t|a|l|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|T|o|o|l|b|o|x|
+-+-+-+-+-+-+-+

Calibration

Copyright (C) 2025
Claudio Pizzolato, Monica Reggiani, Massimo Sartori, David Lloyd

Software developers: Claudio Pizzolato, Monica Reggiani
readNMSmodelCfg
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
Contact model  not found
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
activeForceLength
passiveForceLength
forceVelocity
tendonForceStrain
Assuming bifemlh_r pennation angle in radians: 0
Assuming bifemsh_r pennation angle in radians: 0.401426
Assuming grac_r pennation angle in radians: 0.0523599
Assuming lat_gas_r pennation angle in radians: 0.139626
Assuming med_gas_r pennation angle in radians: 0.296706
Assuming per_brev_r pennation angle in radians: 0.0872665
Assuming per_long_r pennation angle in radians: 0.174533
Assuming per_tert_r pennation angle in radians: 0.226893
Assuming rect_fem_r pennation angle in radians: 0.0872665
Assuming sar_r pennation angle in radians: 0
Assuming semimem_r pennation angle in radians: 0.261799
Assuming semiten_r pennation angle in radians: 0.0872665
Assuming soleus_r pennation angle in radians: 0.436332
Assuming tib_ant_r pennation angle in radians: 0.0872665
Assuming vas_int_r pennation angle in radians: 0.0523599
Assuming vas_lat_r pennation angle in radians: 0.0872665
Assuming vas_med_r pennation angle in radians: 0.0872665
No OpenSim model associated to the subject

EMG: Reading emg file...C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../Cfg/Rstance1/../../../trials/Rstance1/..\..\..\dynamicElaborations\Rstance1_allTrials_all\OvergroundGaitTrials_DM_ngait_og3\emg.mot
Muscle excitations to muscle mapping:
bifemlh_r -> bifemlh_r
bifemsh_r -> bifemsh_r
grac_r -> grac_r
lat_gas_r -> lat_gas_r
med_gas_r -> med_gas_r
per_brev_r -> per_brev_r
per_long_r -> per_long_r
per_tert_r -> per_tert_r
rect_fem_r -> rect_fem_r
sar_r -> sar_r
semimem_r -> semimem_r
semiten_r -> semiten_r
soleus_r -> soleus_r
tib_ant_r -> tib_ant_r
vas_int_r -> vas_int_r
vas_lat_r -> vas_lat_r
vas_med_r -> vas_med_r

externalTorque DONE

EMG: EMG DONE

LmtMa: lmtMa DONE
CalibrationStepCfg 100
 --- DoFs: knee_angle_r ankle_angle_r
 --- Objective Function: Minimize Torque Error

 ---- Parameter: c1
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: c2
 ---- Global
 ----- Absolute Range -0.95 -0.05

 ---- Parameter: shapeFactor
 ---- Global
 ----- Absolute Range -2.999 -0.001

 ---- Parameter: tendonSlackLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: optimalFibreLength
 ---- Single
 ----- Relative Range 0.95 1.05

 ---- Parameter: strengthCoefficient
 ---- Grouped:
 ----- Group: bifemlh_r bifemsh_r semimem_r semiten_r
 ----- Group: grac_r
 ----- Group: sar_r
 ----- Group: lat_gas_r med_gas_r soleus_r
 ----- Group: per_brev_r per_long_r
 ----- Group: per_tert_r tib_ant_r
 ----- Group: rect_fem_r vas_int_r vas_lat_r vas_med_r
 ----- Absolute Range 0.5 3.5

knee_angle_r
ankle_angle_r
Return false
fLatest_.at(0) - fOpt_ = 271.649 - 9.15878 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 132.086 Nm
ankle_angle_r 305.782 Nm

Fobj = 271.649
Return false
fLatest_.at(0) - fOpt_ = 181.356 - 6.1161 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 58.3985 Nm
ankle_angle_r 292.404 Nm

Fobj = 181.356
Return false
fLatest_.at(0) - fOpt_ = 34.2848 - 5.99371 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 35.9402 Nm
ankle_angle_r 103.45 Nm

Fobj = 34.2848
Return false
fLatest_.at(0) - fOpt_ = 45.7977 - 5.99371 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 86.1428 Nm
ankle_angle_r 31.6782 Nm

Fobj = 45.7977
Return false
fLatest_.at(0) - fOpt_ = 15.1832 - 1.93012 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 34.076 Nm
ankle_angle_r 71.3264 Nm

Fobj = 15.1832
Return false
fLatest_.at(0) - fOpt_ = 1.8963 - 1.5764 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 32.569 Nm
ankle_angle_r 15.7808 Nm

Fobj = 6.70694
Return false
fLatest_.at(0) - fOpt_ = 2.09669 - 0.817633 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 19.3571 Nm
ankle_angle_r 13.3655 Nm

Fobj = 2.50687
Return false
fLatest_.at(0) - fOpt_ = 0.54642 - 0.468914 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 94.9036 Nm
ankle_angle_r 4.93591 Nm

Fobj = 53.7739
Return false
fLatest_.at(0) - fOpt_ = 0.317005 - 0.303768 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 6.90082 Nm
ankle_angle_r 4.88669 Nm

Fobj = 0.320391
Return false
fLatest_.at(1) - fOpt_ = 0.317005 - 0.275563 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 70.0489 Nm
ankle_angle_r 4.44937 Nm

Fobj = 29.3059
Return false
fLatest_.at(1) - fOpt_ = 0.27655 - 0.271448 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 6.37931 Nm
ankle_angle_r 4.37054 Nm

Fobj = 0.271813
Return false
fLatest_.at(2) - fOpt_ = 0.27655 - 0.270989 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 6.36042 Nm
ankle_angle_r 4.41898 Nm

Fobj = 0.271024
Return false
fLatest_.at(3) - fOpt_ = 0.27655 - 0.270948 > 0.001
Joint moments RMSE
Trial #1
knee_angle_r 6.3541 Nm
ankle_angle_r 4.44905 Nm

Fobj = 0.27095
Return true!
fOpt_ = 0.270943
Joint moments RMSE
Trial #1
knee_angle_r 6.35429 Nm
ankle_angle_r 4.44744 Nm

Fobj = 0.270943
Reading subject file: C:\Users\sean9\Desktop\project\TestData\ElaboratedData\sixthGC\ceinms\calibration\Setup\Rstance1\../../uncalibrated/DM_uncalibrated.xml .
Calibration time: 267135ms
```

# Ours 
## 最初的
```
knee_angle_l
knee_angle_r
mtp_angle_l
mtp_angle_r
pelvis_list
pelvis_rotation
pelvis_tilt
subtalar_angle_l
subtalar_angle_r
Return false
fLatest_.at(0) - fOpt_ = 62655.4 - 55570.2 > 1e-05
Joint moments RMSE
Trial #1
ankle_angle_l 4.53578 Nm
ankle_angle_r 7.60242 Nm
hip_adduction_l 8.31782 Nm
hip_adduction_r 19.1352 Nm
hip_flexion_l 17.3508 Nm
hip_flexion_r 39.451 Nm
hip_rotation_l 2.21987 Nm
hip_rotation_r 1.86852 Nm
knee_angle_l 17.7614 Nm
knee_angle_r 53.1255 Nm
mtp_angle_l 0.6215 Nm
mtp_angle_r 0.0584794 Nm
pelvis_list 15.0202 Nm
pelvis_rotation 5.35652 Nm
pelvis_tilt 40.324 Nm
subtalar_angle_l 2.45441 Nm
subtalar_angle_r 2.44517 Nm

Fobj = 62655.4
Reading subject file: d:\ExoskeletonPowerAsistance\simulation/XML_CEINMS_generator/CEINMS_calibration_XML\subject.xml .
Calibration time: 470326ms
```

## 把運算最大時間拉長
```
Return false
fLatest_.at(0) - fOpt_ = 63578.4 - 56937 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 62639.1 - 56863.1 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 61938.4 - 55778 > 1e-05
Reading subject file: /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/subject.xml .
Calibration time: 12000738ms

```

## Simpler model
```
(opensim_scripting) (base) ntk@ntk:/media/ntk/Exoskeleton/ExoskeletonPowerAsistance$ CEINMScalibrate -S /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/ceinmsCalibrationSetup.xml

+-+-+-+-+-+-+
|C|E|I|N|M|S|
+-+-+-+-+-+-+-+-+-+-+
|C|a|l|i|b|r|a|t|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+
|E|M|G|-|I|n|f|o|r|m|e|d|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|N|e|u|r|o|m|u|s|c|u|l|o|s|k|e|l|e|t|a|l|
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|T|o|o|l|b|o|x|
+-+-+-+-+-+-+-+

Copyright (C) 2010-2025 Griffith University and the Contributors

CEINMS Contributors: C. Pizzolato, M. Reggiani, M. Sartori
                     E. Ceseracciu, and D.G. Lloyd

Software developers: C. Pizzolato, E. Ceseracciu, and M. Reggiani


readNMSmodelCfg
Reading subject file: /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/subject.xml .
activeForceLength
passiveForceLength
forceVelocity
tendonForceStrain
Assuming bifemsh_l pennation angle in radians: 0.401426
Assuming bifemsh_r pennation angle in radians: 0.401426
Assuming gastroc_l pennation angle in radians: 0.296706
Assuming gastroc_r pennation angle in radians: 0.296706
Assuming glut_max_l pennation angle in radians: 0
Assuming glut_max_r pennation angle in radians: 0
Assuming hamstrings_l pennation angle in radians: 0
Assuming hamstrings_r pennation angle in radians: 0
Assuming iliopsoas_l pennation angle in radians: 0.139626
Assuming iliopsoas_r pennation angle in radians: 0.139626
Assuming rect_fem_l pennation angle in radians: 0.0872665
Assuming rect_fem_r pennation angle in radians: 0.0872665
Assuming soleus_l pennation angle in radians: 0.436332
Assuming soleus_r pennation angle in radians: 0.436332
Assuming tib_ant_l pennation angle in radians: 0.0872665
Assuming tib_ant_r pennation angle in radians: 0.0872665
Assuming vasti_l pennation angle in radians: 0.0523599
Assuming vasti_r pennation angle in radians: 0.0523599

EMG: Reading emg file.../media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/mocap_EMG_EEG_data/data_1009/path1_25/preprocessing/output/steady_EMG_walk.sto

ExtTorque: starting externalTorqueProduce, reading from external torque data file

 ExtTorque: external Torques available 

externalTorque DONE

LmtMa: lmtMa DONE

EMG: EMG DONE
CalibrationStepCfg 100
Return false
fLatest_.at(0) - fOpt_ = 35126.4 - 5140.84 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 19975.4 - 5095.73 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 5910.81 - 5031.67 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 5301.8 - 4850.82 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 4329.09 - 4099.03 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3950.45 - 3921.36 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3900.64 - 3898.26 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3895.5 - 3895.3 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3894.87 - 3894.81 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3894.77 - 3894.77 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3894.76 - 3894.76 > 1e-05
Return false
fLatest_.at(0) - fOpt_ = 3894.76 - 3894.76 > 1e-05
Return false
fLatest_.at(1) - fOpt_ = 3894.76 - 3894.76 > 1e-05
Return false
fLatest_.at(1) - fOpt_ = 3894.76 - 3894.76 > 1e-05
Return false
fLatest_.at(2) - fOpt_ = 3894.76 - 3894.76 > 1e-05
Reading subject file: /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/subject.xml .
Calibration time: 4762798ms
```