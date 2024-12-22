ref. [[Estimation of musculotendon kinematics in large musculoskeletal models using multidimensional B-splines.pdf]]

---
## Terms
- Nominal value: 未個體化的，標準化的人體模型中每條肌腱單元的幾何屬性
- Peq: polynomial regression equations

## 傳統的model組成
- Generalized coordinates(GCs)
- their angular ranges of motion(ROM)(expressed in degrees)
- musculotendon actuators(MTAs)

---

## Summary of the paper
提出multidimensional B-splines function
spline 方法只需要 MTU 長度資訊，就可以估計 MTU 長度和力臂，相較之下，多項式迴歸法則需要不同的方程式來計算 MTU 長度和力臂
spline function per muscle

- 傳統上Peq：肌肉肌腱長度 $('mt)$ + 三維力臂 $(r)$ $\rightarrow$ 預測肌肉肌腱力 (Fmt)
>獨立的 'mt Peq 和 r Peq，需要手動輸入係數
- MB-spline:只用$'mt\ nominal\ value$

肌肉和肌腱的路徑並非簡單的直線，而是會繞過骨骼或其他組織結構。為了模擬這種情況，研究者會使用點或曲面來表示這些阻礙物。
- 不連續性，可能無法進行微分
- 多力臂