EMG-informed method
ref.
- [[CEINMS - a toolbox to investigate the influence of differentneural control solutions on the prediction of muscle excitationand joint moments during dynamic motor tasks Note]]
- https://github.com/CEINMS/CEINMS

---
- preprocessing 得到 _geometrical_ state
- _musculo-tendon lengths_ 肌腱-肌肉單位的長度
	- By opensim scaling流程
- _moment arms_ 肌肉力矩臂
- _muscle excitations_ sEMG signals
	- 現有已經濾波過

`.mot`, `.sto`

Data input:
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

需要透過MOtoNMS轉檔