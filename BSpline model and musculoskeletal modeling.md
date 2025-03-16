---
bg: "[[NTKLab_white bg.png]]"
---

<style>
    .reveal {
        font-family: 'Times New Roman', '標楷體';
        font-size: 30px;
        text-align: left;
        color: black;
        background-size: cover;
        background-position: center;
    }
	.reveal h1,
	.reveal h2,
	.reveal h3,
	.reveal h4,
	.reveal h5,
	.reveal h6 {
	  font-family: 'Times New Roman', '標楷體';
	  color: black;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="70 10" drop="-3 40">
BSpline model and  musculoskeletal modeling
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="70 10" drop="-3 70">
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
## Terms
ref. [[Estimation of musculotendon kinematics in large musculoskeletal models using multidimensional B-splines.pdf]]
- Nominal value: 未個體化的，標準化的人體模型中每條肌腱單元的幾何屬性
- Peq: polynomial regression equations

## 傳統的model組成
- Generalized coordinates(GCs)
- their angular ranges of motion(ROM)(expressed in degrees)
- musculotendon actuators(MTAs)

---

## Summary of the paper
提出multidimensional B-splines function，function per muscle
spline 方法只需要 MTU 長度資訊，就可以估計 MTU 長度和力臂，相較之下，Peq則需要不同的方程式來計算 MTU 長度和力臂
- 傳統上Peq：肌肉肌腱長度 $('mt)$ + 三維力臂 $(r)$ $\rightarrow$ 預測肌肉肌腱力 (Fmt)
>獨立的 'mt Peq 和 r Peq，需要手動輸入係數
- MB-spline:只用$$'mt\ nominal\ value$$

---
## 肌肉模擬的複雜性
肌肉和肌腱的路徑並非簡單的直線，而是會繞過骨骼或其他組織結構。為了模擬這種情況，研究者會使用點或曲面來表示這些阻礙物。
- 不連續性，可能無法進行微分
- 多力臂

---
## spline數學描述
$$S_1(x)=\sum_{i=1}^mc_iu_i(x)$$
$$m = \min(l + 3, n + 3)$$
- $x$對應到樣條節點的索引，用於確定插值的區域
$$l = \frac{x - a}{h} + 1$$
- 平衡插值精度與計算效率
$$N_c = \prod_{i=1}^{d} (n_i + 3), \quad N_d = \prod_{i=1}^{d} (m_i - l_i + 1) \leq 3^d
$$


---
- $s(x,z)$描述肌肉-肌腱長度 $l^{mt}$ 與多個關節角度 $q1,…,qd$​ 的關係。

$$\frac{\partial s_2(x, z)}{\partial x} = \sum_{i_1 = l_1}^{m_1} \sum_{i_2 = l_2}^{m_2} c_{i_1 i_2} u_{i_1}'(x) v_{i_2}(z)$$
- Moment arms:

$$r_{q_i} = \frac{\partial \ell^{mt}(q_1, \dots, q_d)}{\partial q_i} = \frac{\partial s_d(q_1, \dots, q_d)}{\partial q_i}
$$


---
performance index

$$\text{MFE} = \frac{1}{N} \sum_{i=1}^{N} |\hat{X}_i - X_i|,$$

$$\%\varepsilon_c = \frac{\text{MFE}}{\mathbb{E}[\hat{X}]} \times 100$$

- $\hat{X}\_i$​: 使用 OpenSim 生成的數據作為標準
- 肌腱單位長度 $l^mt$
- 力臂$r$
- 肌腱單位力$F^{mt}$

$\%\varepsilon_c$則用來計算一些統計分析

---
## 整合EMG-driven model
都是透過Hill-type muscle model
$$F^{mt} = F_t = F_m \cos(\phi(t)) = \left[a(t) f(l_m) f(v_m) + f_P(l_m)\right] F_{\text{max}} \cos(\phi(t)),
$$
- $F^{mt}$: 肌腱力（musculotendon force）
- $F_t$: 肌腱總力
- $F_m$: 肌肉產生的總力
- $\phi(t)$: 隨著纖維長度變化的羽角（pennation angle)
- $a(t)$: 肌肉激活信號
- $f(l_m)$: 力-長度關係函數
- $f(v_m)$: 力-速度關係函數
- $f_P(l_m)$: 被動力-長度關係函數
- $F_{\text{max}}$: 最大等長肌肉力

tool: [RehabEngGroup/mcbs: Multidimensional Cubic Bspline Library](https://github.com/RehabEngGroup/mcbs/tree/master)

---
ref. [[EMG-DrivenForward-DynamicEstimationofMuscle.pdf]]
