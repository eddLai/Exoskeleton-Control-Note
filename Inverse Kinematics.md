用途:計算同化既有模型與實驗資料
==輸出的是.mot==
Units: m, radians
所以如果要用degrees，權重要乘以$\frac{180}{\pi}^2$
## Settings:
tips: 
- 優先增加「運動」段標記（例如放置於大腿段的三角架標記）的權重，因為這些標記通常較為穩定，不易受到軟組織位移的影響
- 相對權重 vs 絕對權重

## Process
weighted least squares problem
IK solver可以只依賴marker運算，但也可以提供實驗值
會得到: 
非預設座標的值會變動
$$\min_{\mathbf{q}} \left[
\sum_{i=\text{markers}} w_i \left\| \mathbf{x}_i^{\text{exp}} - \mathbf{x}_i (\mathbf{q}) \right\|^2
+ \sum_{j=\text{unprescribed coords}} \omega_j \left( q_j^{\text{exp}} - q_j \right)^2
\right]$$
## Command
`ik -S subject01_Setup_IK.xml`

### XML setup
`<InverseKinemtaticsTool>`
marker, coordinate各自權重
```
<IKTaskSet name="gait2354_IK">
	<objects>
		<!-- Markers -->
		<IKMarkerTask name="Sternum"> <weight>1</weight> </IKMarkerTask>
	
		<!-- Coordinates -->會直接使用這個固定值
		<IKCoordinateTask name="subtalar_angle_r"> <value> 0 </value></IKCoordinateTask>
```
`<weight>`
`<IKCoordinateTask>: <weight>, <from_file>, and <value>`, `<locked>`
`<default_value>`可以選擇`.osim`中的`<SimmCoordinate>` or `<default_value> `

需要
- marker_file
- coordinate_file
- time_range
- output_motion_file
- constraint_weight
- accuracy
## Result Evaluation
官方建議: 
- Maximum marker error should generally be less than 2-4 cm
- RMS under 2 cm
- similar experiment should within one standard deviation



