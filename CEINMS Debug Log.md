```

1. 可以一個分兩個：沒影響，但是意義==有待商榷==
```xml
<excitation id="bflh_l">
      <input weight="0.5">LBF</input>
</excitation>
<excitation id="bfsh_l">
      <input weight="0.5">LBF</input>
</excitation>
```

2. subject的mtu要對照到excitation的所有肌肉? -> 剩下的所有mtu可能都要有?，砍掉舊有的一部分做測試。對，必須要完全一樣
	1. 所以把mtu改成跟emg一樣(不行，dof對不上)
```xml
    <excitation id="vas_int_r"/>如果這行刪掉就會報錯
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
    <excitation id="vas_lat_r"/>
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
    <excitation id="vas_med_r"/>
        <!-- <input weight="1">vas_lat_r</input>
    </excitation> -->
```
1. 需要`.mot`檔案：no
2. 檔名要有_：no
3. 要用相對路徑：no沒有影響
4. subject中的mtu不能砍DOF對不上edl_l

`<trialSet>../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og3.xml ../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og4.xml ../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og5.xml</trialSet>`
`<externalTorquesFile>..\..\..\inverseDynamics\Rstance1_R2L1_6\OvergroundGaitTrials_DM_ngait_og5\inverse_dynamics.sto</externalTorquesFile>`

`<trialSet>../../../trials/Rstance1/OvergroundGaitTrials_DM_ngait_og3.xml</trialSet>`
`<externalTorquesFile>../../../inverseDynamics/Rstance1_R2L1_6/OvergroundGaitTrials_DM_ngait_og3/inverse_dynamics.sto</externalTorquesFile>`

可以跑但結果異常
```
LmtMa: lmtMa DONE
CalibrationStepCfg 100
Return false
fLatest_.at(0) - fOpt_ = 63777.4 - 55633.3 > 1e-05
Reading subject file: /media/ntk/Exoskeleton/ExoskeletonPowerAsistance/simulation/XML_CEINMS_generator/CEINMS_calibration_XML/subject.xml .
Calibration time: 3676435ms
```

`<excitationsFile>`的位置沒有影響