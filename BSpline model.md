ref. [[Estimation of musculotendon kinematics in large musculoskeletal models using multidimensional B-splines.pdf]]

## Terms
- Nominal value: 未個體化的，標準化的人體模型中每條肌腱單元的幾何屬性

multidimensional B-splines function
spline 方法只需要 MTU 長度資訊，就可以估計 MTU 長度和力臂，相較之下，多項式迴歸法則需要不同的方程式來計算 MTU 長度和力臂
spline function per muscle

- 傳統上：肌肉肌腱長度 $('mt)$ + 三維力臂 $(r)$ $\rightarrow$ 預測肌肉肌腱力 (Fmt)
- MB-spline:只用

肌肉和肌腱的路徑並非簡單的直線，而是會繞過骨骼或其他組織結構。為了模擬這種情況，研究者會使用點或曲面來表示這些阻礙物。