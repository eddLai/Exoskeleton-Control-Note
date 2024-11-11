為什麼不用加權才是質心速度阿
$$temp_{side}=\frac{\vec{P_{Heel\_side}}​+\vec{P_{SmallToe\_side}}​+\vec{P_{BigToe\_side}}​​}{3}$$
$$v_{side}=\sqrt{\sum{\Delta temp_{side}^2}}\times SR$$
---
### Peaks
- $i_{max\_side}$=`find_peaks(V_side)`: 抬起的瞬間 $max\_pks\_value = v_{side}[i_{max\_side}]$
- `final_temp_locs_side` = $i_{max\_side}[max\_pks\_value > TR_{side}==mean(v_{side})+std(v_{side})]$
- 篩選符合
$$min(v_{side\_i}, v_{side\_i+1})< mean(v_{side})-0.2 \times std(v_{side})$$
>需要處理最後的點，沒有值可以相減

---
### Minima
- $TF_{side}$=`argrelmin(V_side)[0]`: index of 接觸地面的瞬間的$min\_pks\_value = v_{side}[TF_{side}]$
- 對$min\_pks\_value$ 篩選
$$i_{min\_side}=TF_{side}[min\_pks\_value < mean(v_{side})-0.2 \times std(v_{side})]$$
$$\Delta v_{side}=v_{i+1}-v_{i}, i=1,2,...,n-1$$
$$i_{slow} = \{ i \mid \left| \frac{\Delta v}{\sigma(\Delta v)} \right| < 0.3 \}$$
$$i_{slow} = \{ i \in i_{slow} \mid v_{side}[i] < mean(v_{side})) - 0.2 \times std(v_{side}) \}$$
$$i_{slow} = \text{sort}(i_{min\_side} \cup i_{slow})$$
$$$$

---

對該`locs_min` set進行交替驗證
- `frame_<side>_heel_sground`
- `frame_<side>_heel_lground`
