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
高精度四捨五入
```python
from decimal import Decimal, ROUND_HALF_UP
int(Decimal(n).quantize(Decimal('1'), rounding=ROUND_HALF_UP))
```
## Define_COM

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

## find_foot_strike
為什麼不用加權才是質心速度阿
$$temp_{side}=\frac{\vec{P_{Heel\_side}}​+\vec{P_{SmallToe\_side}}​+\vec{P_{BigToe\_side}}​​}{3}$$
$$v_{side}=\sqrt{\sum{\Delta temp_{side}^2}}\times SR$$
$$TR_{side}=mean(v_{side})+std(v_{side})$$
- `find_peaks(V_side)`: 抬起的瞬間
- $TF_{side}$=`argrelmin(V_side)[0]`: index of 接觸地面的瞬間的$min\_pks\_value = v_{side}[TF_{side}]$
$$index_{min\_side}=TF_{side}[min\_pks\_value < mean(v_{side})-0.2 \times std(v_{side})]$$

$$\text{locs\_possible\_min\_L} = \{ i \mid \left| \frac{vL[i+1] - vL[i]}{\sigma(\Delta vL)} \right| < 0.3 \}$$
$$\text{locs\_possible\_min\_L} = \{ i \in \text{locs\_possible\_min\_L} \mid vL[i] < \mu(vL) - 0.2 \cdot \sigma(vL) \}$$
$$\text{locs\_possible\_min\_L} = \text{sort}(\text{locs\_minL} \cup \text{locs\_possible\_min\_L})$$

對該`locs_min` set進行交替驗證
- `frame_<side>_heel_sground`
- `frame_<side>_heel_lground`
