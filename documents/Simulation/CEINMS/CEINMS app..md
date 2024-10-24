EMG-informed method
ref.
- [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]]
- https://github.com/CEINMS/CEINMS

---
## Data Description
- preprocessing 得到 _geometrical_ state
- _musculo-tendon lengths_ 肌腱-肌肉單位的長度
	- By opensim scaling流程
- _moment arms_ 肌肉力矩臂
- _muscle excitations_ sEMG signals
	- 現有已經濾波過

file type: `.mot`, `.sto`

---
### Data input:
- `endheader`
- `nColumns=15` or `dataColumns 15`
- `nRows=1264` or `dataRows 1264`
多列stamps，第一列是`time`
格式要求: 
- muscle names <- `subjectDescFile`
- muscle activation <- excitationsDescFile`inputSignals

`<prefix>_Length.sto`
`<prefix>_MomentArm_<dof_name>.sto`
MuscleAnalysis
`compute_moments`, 
`muscle_list`:需要include all muscles
`moment_arm_coordinate_list`

需要透過MATLAB MOtoNMS轉檔

---
### File hierarchy
background: [[XML file]]
toc
.. toctree::
   :maxdepth: 2

   xsd/ceinmsCalibrationSetup.xsd
   xsd/calibration.xsd

   xsd/subject.xsd
   xsd/inputData.xsd
   xsd/excitationGenerator.xsd

XSD用於驗證XML可否使用

---
### CEINMS modes
objective function weightings alpha, beta and gamma
### optimization algorithm goal: 
`trackedMuscles在實驗中測量的肌肉  || predictedMusclesao沒有在實驗中測量的肌肉`

- _openLoop_: means _full-predictive_ 不需要外部反饋e.g. joint moments file
- _Hybrid mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle without experimental excitations

- _EMG-assisted mode_
> alpha = 1, beta > 1, gamma > 1
> 
> trackedMuscles = every muscle with experimental excitations
> 
> predictedMuscles = remaining muscles

- _Full optimization-driven closed-loop mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle


tendon setting: equilibriumElastic more acc. but stiff less comput. time