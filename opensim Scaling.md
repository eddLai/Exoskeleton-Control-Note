<div style="background-color: white; padding: 10px;">
  <img src="D:\Notes\Exoskeleton-Control-Note\documents\Simulation\opensim\Inputs and Outputs of the Scale Tool.png" alt="ID Tool" width="300"/></div>

## 目標
- ScaleTasks: 
	- 比較虛擬與實驗標記
	- 解決(他移動虛擬標記的演算法是?)反向動力學
	- 誤差->權重
- ScaleMeasurementSet: 實驗對象相關測量數據
- ScaleScaleSet: 手動縮放
- ScaleMarkerSet.xml: 虛擬標記位置

---
[sject01_Setup_Scale.xml](https://github.com/opensim-org/opensim-models/blob/master/Pipelines/Gait2354_Simbody/subject01_Setup_Scale.xml)
[Scale Setup File - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53090015/Scale+Setup+File)
Unit: mm, kg, year
### 通用:
`<notes>`:用於註記
`<apply>true</apply>`: 用於啟用
### `<ScaleTool name="subject01">`之定義
`<GenericModelMaker>`
- `<model_file>`
- `<marker_set_file>`: [Scale Marker File - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53090011/Scale+Marker+File)
##### `<model scaler>`
```
<ModelScaler>
	<apply>true</apply>
	<scaling_order> measurements manualScale</scaling_order>
```
用於[[Manual Scaling]]
- `<MeasurementSet>`:
	- `<MarkerPairSet>`
	- `<BodyScale>`:可以決定X, Y, Z
- `<ScaleSet>`:
	- `<marker_file>`
	- `<time_range>`

`<preserve_mass_distribution>`: 1 or 0 option
```
<output_model_file>subject01_scaledOnly.osim</output_model_file> <output_scale_file>subject01_scaleSet_applied.xml</output_scale_file>
```

##### `<MarkerPlacer>`
`<IKTaskSet>`: 含[[scaling IKTaskSet]]
#### `<MeasurementSet>`

---

#### Detail process of IK
1. Measurement-based Scaling
	1. $p_1 = \{ \text{R.ASIS}, \text{R.Knee.Lat} \}$
	2. $s_1 = \frac{e_1}{m_1}$
	3. $p_2 = \{ \text{L.ASIS}, \text{L.Knee.Lat} \}$
	4. ...
	5. $s = \frac{s_1 + s_2}{2}$
2. 幾何縮放
	1. 關節框架
	2. 質量中心
	3. 力作用點與肌肉附著點
	4. Wrapping Objects
3. 質量與慣性選項: Target Mass, TM + 保留質量分佈（Preserve Mass Distribution, PMD）
4. 肌肉及韌帶
	1. optimal_fiber_length
	2. tendon_slack_length
# Our Mocap integrated process
debug ref.:[Getting Started with Scaling - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089123/Getting+Started+with+Scaling)
