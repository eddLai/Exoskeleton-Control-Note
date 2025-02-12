### Statistics Method

ref. [[Characterization of muscle fatigue in the lower limb by sEMG and angular position using the WFD protocol.pdf]]
為了對抗個體差異，因此必須考慮統計方法。方可得到人類的常模（母體均值）。

---
### Recall生物統計

{0, 5, 9, 14}和{5, 6, 8, 9}其平均值都是7，但第二個集合具有較小的標準差。
表述「相差$k$個標準差」，即在 $\bar{X}±kS$ 的[樣本](https://zh.wikipedia.org/wiki/%E6%A8%A3%E6%9C%AC_(%E7%B5%B1%E8%A8%88%E5%AD%B8) "樣本 (統計學)")（sample）範圍內考量。

樣本均值鄉對於母體均值的波動變化
SD樣本標準差，$\bar{x}$ 樣本均值
$$SE=\frac{SD}{\sqrt{n}}$$
SE越小就越接近母體
$$CI=\bar{x}+Z_{0.95} \cdot SE$$
Tukey檢驗
單因素ANOVA後使用
$$\Delta \bar{Y}_{ij} = \bar{Y}_i - \bar{Y}_j$$
$$SE(\Delta \bar{Y}_{ij}) = \sqrt{\frac{S^2}{n_i} + \frac{S^2}{n_j}}$$
$$q_\alpha透過顯著水平\alpha定義臨界值$$
$$|\Delta \bar{Y}_{ij}| > q_\alpha \cdot SE(\Delta \bar{Y}_{ij})則認為有顯著差異$$
