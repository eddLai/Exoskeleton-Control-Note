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
$$(1) \quad i_{slow\_side} = \{ i \mid \left| \frac{\Delta v}{\sigma(\Delta v)} \right| < 0.3 \}$$
$$(2) \quad i_{slow\_side} = \{ i \in i_{slow\_side} \mid v_{side}[i] < mean(v_{side})) - 0.2 \times std(v_{side}) \}$$
$$(3) \quad i_{slow\_side} = \text{sort}(i_{min\_side} \cup i_{slow\_side})$$
$$loc_k\subset i_{min\_side}$$
`p = np.where(condition)[0]`
$$p_k=min(i \in i_{slow\_side}|i>loc_k), \rightarrow p_k, p_{k+1}...$$
$$n_k=min(i \in i_{slow\_side}|i<loc_k)\rightarrow n_k, n_{k-1}...$$
if $p_k$ existed (`p.size>0`): `p_x[0]` $\rightarrow p\_R, p\_L\ array$
if $n_k$ existed (`p.size>0`): `n_x[-1]` $\rightarrow n\_R, n\_L\ array$
$p_k[i]$跟$n_k[i]$是一對。

---

對該`locs_min` set進行交替驗證
- `frame_<side>_heel_sground`
- `frame_<side>_heel_lground`
