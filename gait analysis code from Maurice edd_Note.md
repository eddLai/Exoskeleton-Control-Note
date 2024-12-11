# Lib
openpyxl讀excel檔案

# Files
`root = NTKCAP\Patient_data`
`.trc`
`.mot`
IK data
# Constant
body_parts

---
## Data Structure
- 有用.mot
- .trc讀取應該用pandas優化，寫法有夠醜
>已知maurice用的trc column序列比我少1
18 -> RSmallToe_Y
20 -> RHeel_X
36 -> LSmallToe_Y
38 -> LHeel_X
# Funcs
- $i$: index
- $SR$: sample rate
- $v$: velocity

高精度四捨五入
```python
from decimal import Decimal, ROUND_HALF_UP
int(Decimal(n).quantize(Decimal('1'), rounding=ROUND_HALF_UP))
```
## Define_COM
1. Foot_R為什麼算法不一樣
2. Apose scaling每個人不一樣
$$\text{Segment} = \left( \vec{P}_{\text{Start}} + (\vec{P}_{\text{End}} - \vec{P}_{\text{Start}}) \times \text{Position Ratio} \right) \times \text{Mass Ratio}$$

| Segment       | Start     | End                     | Position Ratio | Mass Ratio |
| ------------- | --------- | ----------------------- | -------------- | ---------- |
| Upper\_arm\_R | RShoulder | RElbow                  | 0.436          | 0.028      |
| Upper\_arm\_L | LShoulder | LElbow                  | 0.436          | 0.028      |
| Forearm\_R    | RElbow    | RWrist                  | 0.682          | 0.022      |
| Forearm\_L    | LElbow    | LWrist                  | 0.682          | 0.022      |
| Foot\_R       | Rankle    | Avg(RBigToe, RSmallToe) | 0.5            | 0.0145     |
| Foot\_L       | Lankle    | Avg(LBigToe, LSmallToe) | 0.5            | 0.0145     |
| Leg\_R        | RKnee     | Rankle                  | 0.433          | 0.0465     |
| Leg\_L        | LKnee     | Lankle                  | 0.433          | 0.0465     |
| Thigh\_R      | RHip      | RKnee                   | 0.433          | 0.1        |
| Thigh\_L      | LHip      | LKnee                   | 0.433          | 0.1        |
| Head          | Neck      | Nose                    | 1              | 0.081      |
| Trunk\_R      | RHip      | RShoulder               | 0.5            | 0.2485     |
| Trunk\_L      | LHip      | LShoulder               | 0.5            | 0.2485     |
總COM = 全部COM_parts加總
## Down sample
```python 
def downsample(data, factor):
	return data[::factor]
```
$$down\_index = SR/SR_d$$
## heel_v_xy_plane
$$v_x = x_n-x_{n-1}$$
$$v_y = y_n-y_{n-1}$$
$$|\vec{v}| = \sqrt{v_x^2+v_y^2} \times SR(f_s = 1/s, scaling2real)$$
使用`find_peaks`找到$local\ minima$
## gaitspeedcm
改用$SR_d$
## [[find_foot_strike]]
## COM_analysis
用投影方法計算步態的穩定度
1. 質心數據投影至平面，並進行旋轉校正。
2. 使用濾波和平滑計算質心的包絡線與波動。
3. 計算左右步態的面積與速度特徵。
4. 輸出步態穩定性的特徵值，包括 RMS 和步態區間特徵。
## [[Speed_analysis]]：用於判斷stable步態

## flexion_analysis
為什麼有兩種，hip用flexion