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

# 
# Ours
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