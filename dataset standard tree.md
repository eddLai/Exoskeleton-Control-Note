```
(opensim_scripting) (base) ntk@ntk:/media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/mocap_EMG_EEG_data/data_1009/path1_01$ tree
.
├── EMG
│   └── EMG_path1_01_155236-S.csv
├── opensim
│   ├── Balancing_for_IK_BODY.mot
│   ├── Empty_project_filt_0-30_IK.mot
│   ├── Empty_project_filt_0-30.trc
│   ├── _ik_marker_errors.sto
│   ├── IK_Setup_Pose2Sim_Body25_without_scaling.xml
│   ├── IK_Setup_Pose2Sim_Body25.xml
│   ├── IK_Setup_Pose2Sim_Halpe26.xml
│   ├── Model_Pose2Sim_Body25.osim
│   ├── Model_Pose2Sim_Halpe26.osim
│   ├── Model_Pose2Sim_Halpe26_scaled.osim
│   ├── opensim.log
│   ├── Scaling_Setup_Pose2Sim_Body25.xml
│   ├── Scaling_Setup_Pose2Sim_Halpe26.xml
│   └── sync_time_marker.npz
├── preprocessing
│   ├── gait_slicing
│   │   ├── big_toe_strike.png
│   │   ├── heel_strike.png
│   │   ├── plane_strike.png
│   │   └── small_toe_strike.png
│   ├── output
│   │   ├── cutted_EMG_data.csv
│   │   ├── filtered_trc_file.trc
│   │   ├── H0918
│   │   │   ├── inverse_dynamics.sto
│   │   │   ├── KA_Normal_data_1009_path1_01_Gait_Results
│   │   │   │   ├── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_dudt.sto
│   │   │   │   ├── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_q.sto
│   │   │   │   └── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_u.sto
│   │   │   ├── MA_Normal_data_1009_path1_01_Gait_Results
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_ActiveFiberForceAlongTendon.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_ActiveFiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberActivePower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberLength.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberPassivePower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Length.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_ankle_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_ankle_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_ankle_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_ankle_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_flexion_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_flexion_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_tilt.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_tx.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_ty.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_flexion_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_flexion_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_tilt.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_tx.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_ty.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MuscleActuatorPower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_NormalizedFiberLength.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_NormFiberVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PassiveFiberForceAlongTendon.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PassiveFiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PennationAngle.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PennationAngularVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonLength.sto
│   │   │   │   └── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonPower.sto
│   │   │   └── steady_MOCAP_walk_IK.mot
│   │   ├── RLU2023
│   │   │   ├── inverse_dynamics.sto
│   │   │   ├── KA_Normal_data_1009_path1_01_Gait_Results
│   │   │   │   ├── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_dudt.sto
│   │   │   │   ├── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_q.sto
│   │   │   │   └── Kinematics_Analysis_data_1009_path1_01_Gait_Kinematics_u.sto
│   │   │   ├── MA_Normal_data_1009_path1_01_Gait_Results
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_ActiveFiberForceAlongTendon.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_ActiveFiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberActivePower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberLength.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberPassivePower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_FiberVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Length.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_ankle_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_ankle_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_add_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_add_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_ankle_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_ankle_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_add_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_add_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_flex_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_flex_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_rot_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_arm_rot_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_elbow_flex_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_elbow_flex_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_flex_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_flex_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_adduction_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_adduction_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_flexion_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_flexion_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_rotation_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_hip_rotation_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_l_beta.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_r_beta.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_knee_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_lumbar_bending.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_lumbar_extension.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_lumbar_rotation.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_mtp_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_mtp_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_list.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_rotation.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_tilt.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_tx.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_ty.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pelvis_tz.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pro_sup_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_pro_sup_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_rot_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_arm_rot_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_subtalar_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MomentArm_subtalar_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_elbow_flex_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_elbow_flex_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_adduction_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_adduction_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_flexion_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_flexion_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_rotation_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_hip_rotation_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_l_beta.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_r_beta.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_knee_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_lumbar_bending.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_lumbar_extension.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_lumbar_rotation.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_mtp_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_mtp_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_list.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_rotation.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_tilt.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_tx.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_ty.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pelvis_tz.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pro_sup_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_pro_sup_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_subtalar_angle_l.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_Moment_subtalar_angle_r.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_MuscleActuatorPower.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_NormalizedFiberLength.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_NormFiberVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PassiveFiberForceAlongTendon.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PassiveFiberForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PennationAngle.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_PennationAngularVelocity.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonForce.sto
│   │   │   │   ├── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonLength.sto
│   │   │   │   └── Muscle_Analysis_data_1009_path1_01_Gait_MuscleAnalysis_TendonPower.sto
│   │   │   └── steady_MOCAP_walk_IK.mot
│   │   ├── steady_EMG_walk.sto
│   │   └── steady_MOCAP_walk.trc
│   ├── sync_outputLBF.png
│   ├── sync_outputLGL.png
│   ├── sync_outputLRF.png
│   ├── sync_outputLTA.png
│   ├── sync_outputRBF.png
│   ├── sync_outputRGL.png
│   ├── sync_outputRRF.png
│   └── sync_outputRTA.png
└── videos
    ├── 1.mp4
    ├── 2.mp4
    ├── 3.mp4
    └── 4.mp4
```