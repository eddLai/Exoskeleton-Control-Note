`i_slow_n["R"] == R_locs_possible_min_n`

`frame_R_heel_sground = np.concatenate(i_slow_n["R"][:1],i_slow_p["R"])`
$$speed\_midpoint=sort(lground_R \bigcup lground_L)$$
$$mean\_gap=round(\frac{1}{N-1}\sum^{N-1}_{i=1}{speed\_midpoint[i+1]-speed\_midpoint[i]}{})$$
if $$speed\_midpoint[0] - mean\_gap > 1$$ and
$$speed\_midpoint[-1] + mean\_gap < len(V\_abs)$$:
expand margin
### interpolation
for i in speed_midpoint:
$$temp\_interp = sort(V_{abs[i]}:V_{abs[i+2]})$$
一個時間段的速度變化，若不滿足==速度下降==，執行相反flipud
$$temp\_interp\_section =[speed\_midpoint[i+1]-speed\_midpoint[i]]$$
組合成$$interp\_speed\_sections$$
對其進行`PchipInterpolator`
$$\text{Threshold}_{\text{steady}} = 0.7 \cdot (\max(v_{\text{mean}}) - \min(v_{\text{mean}})) + \min(v_{\text{mean}})$$

$$\text{bound} = \{t \, | \, v_{\text{mean}}(t) > \text{Threshold}_{\text{steady}} \}$$

$$

\text{Threshold}_{\text{start/end}} = 0.2 \cdot (\max(v_{\text{mean}}) - \min(v_{\text{mean}})) + \min(v_{\text{mean}})

$$

  

$$

\text{bound}_{\text{start/end}} = \{t \, | \, v_{\text{mean}}(t) > \text{Threshold}_{\text{start/end}} \}

$$

計算兩者的速度的RMS
$$\text{RMS}_{[a,b]} = \sqrt{\frac{1}{b-a+1} \sum_{i=a}^b x_i^2}$$

