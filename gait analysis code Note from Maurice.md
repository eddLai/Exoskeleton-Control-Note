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
# Funcs
高精度四捨五入
```python
from decimal import Decimal, ROUND_HALF_UP
int(Decimal(n).quantize(Decimal('1'), rounding=ROUND_HALF_UP))
```

heel_v_xy_plane
$$v_x = x_n-x_{n-1}$$
$$v_y = y_n-y_{n-1}$$
$$|\vec{v}| = \sqrt{v_x^2+v_y^2} \times SR(f_s = 1/s, scaling2real)$$
使用`find_peaks`找到$local\ minima$

gaitspeedcm
改用SR