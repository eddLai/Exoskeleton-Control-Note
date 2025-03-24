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
	  %%text-transform: lowercase%%;
	  text-transform: capitalize;
	}
	.with-border{
		border: 1px solid red;
	}
</style>
<grid drag="70 10" drop="-3 40">
signal decomposition Note
<!-- element style="font-size: 40px;align: left; text-align: left;color: white"-->
</grid>

<grid drag="80 10" drop="-3 70">
賴宏達
</grid>

<!-- slide bg="../../NTKLab_white bg_cover_resize.png"-->

---
# Recall system and signals
- $h(t)_{系統衝擊響應}$，為$\delta(x)_{Dirac\ delta單位脈衝函數}$輸入$LTI$系統所得到的響應
- LTI系統：線性響應, 時不變性（系統輸出與響應有相同位移）
- 系統響應：標準信號的輸出
- 系統輸出是信號與系統函數的卷積
$$y(t) = x(t) \ast h(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau.
$$

[[instantaneous frequency-Analytic signal and Hilbert Transform]]，然而這個傳統的數學方法在複雜的波形會有巨大的飄移，他只能用在單純的波形上，透過使用在IMF使其有用武之地

---
科普文章連結 https://blog.csdn.net/ARM_qiao/article/details/108482457
>瞬時頻率：透過analytic signal，"本征模式函数(Intrinsic Mode Function，IMF)的新概念，基于这类函数的局部特性，使函数的任何一点瞬时频率都有意义。"

---
# Signal Decomposition
**目的**：用來改進如Fourier Transform需要的基底函數組成假設cos+sin的組合，因為原本的FT會將產生Harmonic
>可能導致錯誤的跨頻連結 (Cross-Frequency Coupling, CFC) 結果，例如將諧波錯誤地解釋為真實的跨頻交互。
>ref. 
>- [Brain Oscillations and the Importance of Waveform Shape - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1364661316302182?via%3Dihub)
>- [Non-Sinusoidal Activity Can Produce Cross-Frequency Coupling in Cortical Signals in the Absence of Functional Interaction between Neural Sources | PLOS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0167351)

---
![[nonsinusoidal waveforms harmonics.png]]
### intrinsic mode function:
定義：
- 局部極值，與過零點數量相等
- 上下包絡線對於時間軸對稱（平均值為零）

---
## Empirical Mode Decomposition, EMD
data-driven method，一個signal由多個IMF組成，IMF可以是線性或者非線性的
`emd.sift.，可以用這種方式修改設定
```python
ext_opts = config['extrema_opts']
ext_opts['method'] = 'numpypad'
ext_opts['pad_width'] = 5
max_locs, max_mag = emd.sift.get_padded_extrema(x, mode='peaks', **ext_opts)
```

$$r(t) = x(t), \quad i = 0, \quad k = 1, \quad \text{SD} < \delta, \quad \delta \in [0.2, 0.3]
$$

---
![[extreme padding method.png]]

---
用局部極值找到包絡線
`emd.sift.interp_envelope()`
$$e_{\text{max}}(t), \quad e_{\text{min}}(t)$$
$$m(t) = \frac{e_{\text{max}}(t) + e_{\text{min}}(t)}{2}$$

![[EMD step1,2.png|500]]

---
取得分量，減去均值包絡線，==這樣就能得到最快的分量==
$$p(t) = r(t) - m(t)\quad \text{(2)}$$
$$\text{SD} = \frac{1}{N} \sum_{t=1}^{N} \left| p(t) - m(t) \right|$$
![[EMD step3,4.png|500]]

---
<split no-margin>
![[emd example 1.png|450]]
![[emd example 2.png|450]]
</split>

多次迭代
$$r_k(n) = r_{k-1}(n) - \sum_{k=1}^{K} IMF_k(n)$$

---
兩個條件跳出迭代
1. $$\text{If } \text{SD} < \delta, \text{ proceed to next step, otherwise return to step (2)}$$
2. r必須是單方向的$$\text{If } r(t) \text{ is not monotonic, then go back to step (2) and set } k = k + 1$$
$$x(t) = c_1(t) + c_2(t) + \cdots + c_n(t) + r_n(t)$$


---
# Example
TCN透過多層擴張卷積來處理這些輸入，每層的擴張因子逐漸增加，使得隨著模型深度的增加，感受野隨之擴大，從而能夠捕捉更長範圍內的時間依賴性。 因果卷積確保模型的預測僅依賴當前及之前的時間點。擴張卷積則為因果卷積加上擴張因子做為權重的變體，如式(4) [33, 34]。

![](data:image/png;base64,R0lGODlhnAEeAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAAAwCcARsAhwAAAAAAAAEAAAEBAAEBAQIBAAIBAQAAOgEAOgEBOgAAZgAAZQEAZQEAZgAA/wA6OgA6ZgE7ZgA6ZQA6kAE6jwA6jwBmkABmtgBmtQBltQCqqgCq/wD//zoAADoBADsBATsBADoAOjo6ADs7ATs7kDs6kDpljzpmkDpmjzpmtjpmtTtmtjqQtjqQ2zqQ2jqP2jqP2TuQ2mYAAGYBAGcBAWcCAWY6AGc7AWc7OmZmAGVlOmaPZmaPtWaQ22eQ2ma222a12ma22mW12ma2/2a2/ma1/mW1/mW1/ZA6AJA6AZE7AZA7AZE7ApA6OpA7ZpBmAJBmOpBmZpBmkJCQOpCQZpC224+12pDb25Db/5Da/4/a/pDa/rZmALZlALdmALZnAbZmOrdnO7VmO7ZmZraQOreRO7aRO6qq/7bb27bb/7Xa/7ba/7Xa/rb//7X+/rX9/qr//7b+/9uQOtyQOtuROtuRO9uQZtuRZtu2Ztu3Z9u2kNu3kdvbkNv/ttv//9r+/tr//9r+/9n+/v+2Zv+3Zv+2Zf+2kP/bkP/bkf/ckP/btv//tv//t///2///3P7+2////wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwj/AAEIHEiwoMGDCBMqXMiwYcNGSAIEUNAGgByJAS44FIgnBJaNIEOKHEmypMmTKFOqXMmypUuTi2wo+CiQy4EeG/XYmFjx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)                                                  (4)

![](data:image/png;base64,R0lGODlhLQAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAEABQArABYAhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADqQ22YAAGY6AGa2/5A6AJA6OpBmkJCQZpC225Db/7ZmALZmOrbb/7b//9uQOtuQZtu2kNv///+2Zv/bkP/btv//tv//2wECAwX8ICCOZGliCmKSFgGtcAx4jPDKAFpkpBT8O9Hm8BNESJ1EECeiDSojWoAAHV0CNpKzyhQllwBNAAywGEti1UpyNlkCi1HyORrGtQy66cvbK/sAPndJaiRDBiseEwGIMGxHIm9qEo0lkm4/mQF6I5dCBzsWZCOCiTWQK2KVNAIPnHhtJXNcJkNgb7ElrKiGB5UrtoBvv7qnK54wwaQBhSa7a3AyyjPGMaWyCa8mqnUH2pbMtaCAx+EiYqMlh+JBHg60Io9NDFPwxdpDAxQcDc1efwCSZPpGIo2JC0QI8OoUrcs9ezL4OPSTDsaWiaay4MBwgArGGCjuwNDgwkQIADs=)是時間點 ![](data:image/png;base64,R0lGODlhCgAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAEACQAJAA4AhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADqQ22YAAGa2/5A6AJA6OpBmkJDb/7ZmALZmOrbb/7b//9uQOtuQZtv////bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwU6ICA+giOeWFJUJ5BBgdFOQW0PkruULZDiPctB1qMheoBHQNH75VrCVfAgzTRywkHkwjiKKIcAwSQKAQA7) 的預測輸出；![](data:image/png;base64,R0lGODlhLgAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABQAtABYAhQAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADo6ADqQ22YAAGY6AGZmAGa222a2/5A6AJA6OpBmkJC225Db/7ZmALZmOrbb/7b//9uQOtuQZtu2kNv/ttv///+2Zv+2kP/bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwb/QIBwSCwahZpF4jjEECTMqFT0EEClgGSBYxRVAuDBBfA5gAUTYkixxQ6p4iMlMLAMOwFBgwgfu4drbUV4ggAYAQ6DAUtyaEeHiUVrcQB4jG8PlJJsXEaBnUSQZAcGRmWlXV+ojWlFZQUbCquhi0aHYLiaQoeXmAIIhURzkUVUjkx4s010fsVVrZu6rgfBAFTMR8bQRKdSr6BCFAMMiNnPj7VR36FoyebHRcPe1KB4iZPNwuXR+UbuQt3C7SvCyxQ9KQUBfLoToNooZaPaiIjQDwAFR9eIVcqzTUifaXVAQOglZOECMATsAPBghqO/dEQymCHQcdfAP86kYVmI8whPFjcfezIxdkWKhgMEKgotkkSjvydGggAAOw==)是時間點 ![](data:image/png;base64,R0lGODlhCgAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAEACQAJAA4AhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADqQ22YAAGa2/5A6AJA6OpBmkJDb/7ZmALZmOrbb/7b//9uQOtuQZtv////bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwU6ICA+giOeWFJUJ5BBgdFOQW0PkruULZDiPctB1qMheoBHQNH75VrCVfAgzTRywkHkwjiKKIcAwSQKAQA7) 的輸入特徵向量；![](data:image/png;base64,R0lGODlhNAAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAEABQAzABYAhQAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADoAOjo6ADqQtjqQ22YAAGY6AGa222a2/5A6AJBmAJCQZpC225Db25Db/7ZmALaQOrb//9uQOtu2Ztu2kNvbkNv///+2Zv/bkP//tv//2wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwb/QIBwSCwaj8JNY4EEZAiTpnRKDEEEUamy0CFeAmBBZWgNPIafAzjAJIIYXCrAOsAQLQEx0QM+DzVgCl1kEHVHeG1Db3FCGQGMcxB9RGmQQnyJVVdjRY5+AHyQHwgJZkQZepqGcopwg6GDABYGeJ9vBkZpuKx3qbBCoxW1Qxarp2xGb2CZx22Vg7OypgBpzELDyQypRny7z9QIY9gWlkJW224MxkXf39GyemmfmuhoB+X2cc/B12JW+JHqXUKG5NuiDu/gVfAg0NymQ9OOGITDIRwxARQg7EKCTZUdJN2ELIqwEZ6EdUYcWfuGRKVIBnk4XVs2RRe3ACWNWEhVJiceOZRG6Hwc0i3EBWsHHUacOa8JpiJlBDiINcQTLzlCeSW9SmXrlKxcsV7J0mTDAQJDw8pR0nQPFCNBAAA7)是權重向量；![](data:image/png;base64,R0lGODlhDwAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABgAOABEAhQAAAAAAAAAAOgAAZgA6kABmtjoAADo6kDpmkDpmtjqQ22YAAGY6AGY6OmaQZma2/5A6AJA6ZpBmZpDb/7ZmALZmOraQOrbb27bb/7b//9uQOtuQZtu2Ztu2kNv///+2Zv/bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwZpQIBwOKQEAoMMcQnYBAgeJvETUEiJmsDjWhRMuIARBLoMNY4Ch6Gw5DwxAJChSpSTwxDvUKwXipNDVHcAIguDWVaBdEVaREZbfhCNQnJ9Qo9+EQyAigUeIRIXEEkdB1EAFUcIURZHCVFBADs=)是時間間隔，用於控制輸入特徵之間的時間延遲，以滿足時序性的需求；![](data:image/png;base64,R0lGODlhEQAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABwARABAAhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADpmtjqQ22YAAGY6AGa222a2/5A6AJBmAJDb/7ZmALbb/7b//9uQOtu2Ztv///+2Zv/bkP/btv//tv//2wECAwECAwECAwECAwVmICBeQRk0ImUGiShWJeNuTyDILkAWlqspBEkuFTDMHLyhKHISbRyGnvIpgAAyC4TShTnwKofWdrRqjgHMxIZpHFOt3er4N5gsWeOdVL9ViQFPZjmBKC4qbTlgeC4kcowrYj8lNy4hADs=)是權重向量的大小；![](data:image/png;base64,R0lGODlhDQAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABgAMABEAhAAAAAAAAAAAOgAAZgA6kABmtjoAADo6kDpmkDpmtjqQtjqQ22YAAGa2/5A6AJA6OpBmAJBmOpDb/7ZmALaQZrbbkLbb/7b//9uQOtv///+2Zv/bkP/btv//tv//2wECAwVbIAB4ThAUYpp6ULCo8CRI8OoMVy1uBqoDGtcPgJlxIqaEbVA5WEiBhqjDCBwyIsxpZ5ilgj6tL7sFyGipiZCKs3l5BKwoGAcG6iOH1xzwcvRSIw8KFAYmCBYpIQA7)是偏置項。

殘差連接（Residual Connections）塊則可以幫助資訊在深層網路中傳播，防止梯度消失問題。 殘差塊可以表示為式(5)：

![](data:image/png;base64,R0lGODlh7AAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABQDsABcAhQAAAAAAAAEAAAAAOgAAZgAA/wA6ZgA6kABmkABmtgD//zoAADoBADoAOjo6ADpmkDpmtjqQtjqQ2zqQ2mYAAGYAOmY6AGZmAGa222a2/2a2/pA6AJBmAJCQZpC225Db25Db/5Da/7ZmALZmOraQOraQZrbb27bb/7b/27b//9uQOtuROtu2Ztu2kNvbkNv/ttv//9r///+2Zv+3Zv+2kP/bkP/btv//tv//2////wECAwECAwECAwECAwECAwECAwb/QIBwSCwaiS2L5MgEqAyepnRKrRqTS6t2y2U+o92weIvbDMDb5AE2blvLZ/cRV3IEEnKiLDB4mIpqbHmDewGGGUI3FIZ3RYprRDgjjAQpADULhgMgQmWVg1SFjKObjhSQQ5KUlpianFOYAxhDJIylnRsBiEKthllFNrm/uJ+gRqqGnzUMmiFELIazQ4oBCILElkYiAQQnQ3uyRI/XxkfQxQA2FOgAntlF293ffNJSZbrwfK9ChbtC0AEikItkZl+iUwPLAYjnTcgMAeH0BECFC5/EYRIpqrBIZKM/hUX2UFw4cg/GeRo5SsHEzsnEa/dUYhppZONJj1rK0Jwi8toK/wEaajYSt+5duw0tpxXlF+AkgHEghWIUgScVUqNEi5m0MnNgzyE1Gtj5qOJWE5tGoFbRmVCKIq0CJhzZ9hHAV7ALqnrBh0mvNrNRhdCFlVcKzr5aWGK9uzDB4IN+9zoVAdjehp1TDhc+VrAI2o5NVy448IJCZM+hA2Pj1cCgkM9MZpY+7ZZC5bthQTxemFSbyiGwp7DlItt07AXs7tXdPceMA8zzaM8bRd2W6yJd23HYyZzzgOdtpXTP3nihRUxOi8C5bncoleFknEMXVR3w+szcsBohH5i+odP3GZZfF+ONxkZu5u0iAnQE9cafZQyeNSAT22DE2FGVqZdLb0Q8CP/SY4rUhSF7Vk2oRQubdWhgeQuVgomITOwh0H4rvndZeE3cw2GAwLmHS4ZEiEDABb/RGKEcAd5QwXU8zjVkkTkKc0RXCLYIAnxDCKnfJZnU5SFT1dVHYpZPwvjUUkH+1qRnm+whHV5HuvHWlgQB+VqbPlaBIgRpIURVlm1WhuU3eSX0ZXNxdoSndBcqkmF38yAypxRuUhqmmE1USgWkTEmKphaUufaIC60B+sEGb3LWm6Y2Jtrpmb0Fx2VSsvKSIqc9pgdKrUfwiphgUIr32yMc+EVZBxweMalUb9zI1a1FKocabb8SRdGF8Ng5iLRUVKvUtS+FlOePoi4C2DapgRbsbS4whtpsomq1d0AMRbCQyTD37OQOQSqBQ2K8INmbrmXJsSvRbePCitU9kcWzpQq9Vdinq4MywS1TAzgznS8VGbLTVkLYYIEhBjREQyb69BosIaPoetEQIpNsMsqAsaoiTRcDa+aCbdWK07s4hjxyACULcXIzSF7VBsCq5aR0GD9jV+PSFKQnK9MQBt20Ka6qSufWU2BNhSJ8KvvpGC9SqNK+YAcGBxonLmDA121bFscWKriMK95ALgsAinPX3XQSZsYIheBjEG6Mo/WIISQKI3wUsz8yHI745ZhnLgYddqTK0wIRtddHQ5pPEQQAOw==)                                                                 (5)

![](data:image/png;base64,R0lGODlhYAAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABQBgABcAhQAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADoAOjo6ADpmkDpmtjqQtjqQ22YAAGYAOmY6AGZmAGa222a2/5A6AJBmAJCQZpC225Db25Db/7ZmALZmOraQOraQZrbb27bb/7b/27b//9uQOtu2Ztu2kNvbkNv/ttv///+2Zv+2kP/bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwb/QIBwSCwahSRI48hsOp/QIiogUHiizxZFcMF6Aa1OImD4YleUwJI4DbjfbkGmyHIUTsTW5j0IAVQHcXNPgAISQxxvckNaARNDgG9rRlqLRCMBfUMrDpqMFJ5FGpkfQ1OGUI2PRKOWQm2rQpgBDHhMImpSAXesvKa5R1O+ALixToChQrjDjY5EgMNHuJPKwEMaZZ/JRHWeU9THB9EAwrZ/CGPGIq631kKjxkeA2e2P817Ifmy75tjwQ3XoNfmnTZ8KBIOITAtXwIQDgVDqsCPHT8jBDAQBaNhGaUvCP+LwtKgwTqOzJpUSlHyS0WLId2UIAgJ3REuyNnAggvH4BBdH/ygtQfK6aHKVhpVGptS6drJOvJ0TizT66YTEAZ3Q8GB7twjQ0yaRhFQaxOLBR7E8Bw6IcDJKI5pCTxDVKEfLuI362Fy11S0vk7FN1mWYovOJ1QVG6tzZynXwRLvm0IYiHCXor0d9zWiYqLgEwmsCMFAozCRzNbhGFhq5964tlqCKKwjcbIFqzTSrVEVhzc2OuXK6CgPuTeXjKHfVXDNdMyIQaqmg/Or+NZFy4k5+d5IRlSm7sp8LcSJn8m0TBDcESgFIEaj4vsJZoSu3/G6lajM7bfdU7hLplzqo0YeFYpEN6ABiR5iG3zMHfKXggpV08YUIzxW1YBGCGbHCeV/hlx9EhxdKdMiF7wwAwgarnKKAeiS26JYY212IwgGoOBEEADs=)是某函數以![](data:image/png;base64,R0lGODlhGwAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAEABwAZABUAhAAAAAAAAAAAOgAAZgA6kABmtjoAADoAOjo6ADqQtjqQ22YAAGa222a2/5A6AJBmAJCQZpDb25Db/7ZmALZmOraQOrb/27b//9uQOtu2ZtvbkNv///+2Zv/bkP//tv//2wWuYBWMggScnxM0J9AZY6C0wBSUNDeybTYmGxomQAiiVCvaq0gD6JinzgGRbGFwzaexVrDxAJ5FoXnSRg8Sb2syuJBdBuhkrIbP3sug1FSfQMl5XCcTOC9fgHEbe4MlKX+DbWALRXNrJRxYLY5BYQQaaJYRDmNvLZ0PpIwQkaUnYTcmayN3QjtHAamDAaxNGKwpVbKHNH5bra1htMethsvLV7HOpWwWFMPSZQYCDAAhADs=)為參數應用於輸入![](data:image/png;base64,R0lGODlhEAAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABwAQABAAhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADo6ADqQ22YAAGY6AGZmAGa222a2/5A6AJDb/7ZmALZmOrbb/7b//9uQOtv/ttv///+2Zv+2kP/bkP//tv//2wECAwECAwECAwVhIABwUmAOFKAdpgCJYhQME4wFQgOLd3HBlYBjJ9ooULxAgggUqg4GJmxVsCiiUhHnIUD4sk0kePSYpcaRAcMJrrhuWOltaBQTV3HZkGj8Jv1aZXtJLjsLJgQ1ABksOC8iIQA7)；![](data:image/png;base64,R0lGODlhEAAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABwAQABAAhAAAAAAAAAAAOgAAZgA6ZgA6kABmtjoAADo6ADqQ22YAAGY6AGZmAGa222a2/5A6AJDb/7ZmALZmOrbb/7b//9uQOtv/ttv///+2Zv+2kP/bkP//tv//2wECAwECAwECAwVhIABwUmAOFKAdpgCJYhQME4wFQgOLd3HBlYBjJ9ooULxAgggUqg4GJmxVsCiiUhHnIUD4sk0kePSYpcaRAcMJrrhuWOltaBQTV3HZkGj8Jv1aZXtJLjsLJgQ1ABksOC8iIQA7) 是原始的輸入，直接加到![](data:image/png;base64,R0lGODlhEAAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABwAPABAAhAAAAAAAAAAAOgAAZgA6kABmtjoAADoAOjqQ22YAAGYAOma2/5A6AJBmAJDb/7ZmALb//9uQOtu2Ztv///+2Zv/bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwECAwVUICBSQWmagiOKUjBAq5W8K0ASU/3gdRQgNcCjEHwEFsEkhkEDVA6qYMXAwzR4QdIpQEwakYBLAlxbpkQXRbQmbiZXpO575QPORcvjnWX47bUldm8hADs=) 的輸出上以形成![](data:image/png;base64,R0lGODlhNgAcAHcAMSH+GlNvZnR3YXJlOiBNaWNyb3NvZnQgT2ZmaWNlACH5BAEAAAAALAAABQA1ABYAhQAAAAAAAAAAOgAAZgA6ZgA6kABmkABmtjoAADo6ADqQ22YAAGY6AGZmAGa222a2/5A6AJC225Db/7ZmALZmOrbb/7b//9uQOtu2Ztu2kNv/ttv///+2Zv+2kP/bkP/btv//tv//2wECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwECAwb/QIBwSCwaiRmG4sgEXAiRplQaggiiU2OysDlyAuDAQwhahA/FMpcYooQHFoAHARZIhFX4EQN2EMsBBl1DeXFGEwEDFUNfAn5DaoNEX2uEEGJFX0teAZVOmEUXoESiaH8LepapRmWpmkeRRYhjk52ScgimTKJjc7qHdmxWd6QBm0Oix0dzBRoLv0bJRHOrAFWjQrNUVgmenL9fYeIBwZblTaLVywieiMoAlLdV50fX6kbMg/PEyAHQ+1ImDGiAbV2lVoaGaBNGL5SdL9DwsRsU71RDAAuNfBmDUArEfu+oJQS5TlfGI9KsXaLVLyKuiLGEVGQyoRwGOsquecMDodo1PpbwyPFLs2BNODCbroHZGfTYBwZgCCwC0IGOUJQFsxgppLVJzK5MvoLleW8sQyxjMyAgMNIskyRAs3CAYiQIADs=)。

輸入部分考量不同腦區的時間延遲可能達到解碼器的性能提升

---
## recall FT
頻譜科普： https://blog.maxkit.com.tw/2021/02/blog-post.html
假設兩信號
```python
x = np.cos(2*np.pi*freq*time_vect)
y = np.cos(2*np.pi*freq*time_vect) + 0.25*np.cos(2*np.pi*freq*2*time_vect-np.pi)
```

![[a signal spectrum.png|400]]
$$ppy[k] = \sum_{n=0}^{N-1} y[n] e^{-j \frac{2\pi}{K} k n}, \quad k = 0, 1, 2, \dots, N-1$$
```python
pyy = np.fft.fft(y) / len(x)
```

---
## Reconstruct the signal from freq. domain
$$f(x) =\sum_{n=-\infty}^\infty C_n \cdot e^{\frac{nx\pi}{p}j}=C_0 + \sum_{n=1}^\infty 2 |C_n| \cos\left( \frac{n\pi}{p} x + \phi_n \right)$$
$$|C_n| = \sqrt{\text{Re}(C_n)^2 + \text{Im}(C_n)^2}, \quad \phi_n = \arctan\left( \frac{\text{Im}(C_n)}{\text{Re}(C_n)} \right)$$

---
$$ppy_k=ppy[k], k=specific\ frequency,e.g.\ 50, 100Hz$$\

$$A=2\times |ppy|$$

$$\phi_{ppy_k}=tan^{-1}{\frac{Im(ppy_k)}{Rm(ppy_k)}}$$

$$comp(t)=Acos(2\pi k\cdot t+\phi)$$

```python
comp1 = comp1_amp * np.cos(2*np.pi*5*time_vect + comp1_phase)
```

---

FT decomposition

![[FT decomposition of a signal.png|400]]
EMD decomposition

![[EMD decomposition of a signal.png|400]]

---
但是FT會有低頻訊號被轉換為多個高頻**separate harmonics**的問題。
![[separate harmonics.png|600]]
影響到我們觀察高頻信號

---
### EMF hilbert
```python
IP, IF, IA = emd.spectra.frequency_transform(imf, sample_rate, 'hilbert')
plt.figure(figsize=(10, 6))
plt.subplots_adjust(hspace=0.4)
plt.subplot(211)
plt.plot(time_vect[:sample_rate], imf[:sample_rate, 0])
plt.title('IMF-1')
plt.subplot(212)
plt.plot(time_vect[:sample_rate], IF[:sample_rate, 0])
plt.title('IMF-1 Instantaneous Frequency')
plt.ylabel('Frequency (Hz)')
```
instantaneous frequency\
![[instantaneous frequency.png|450]]

---
```python
IP, IF, IA = emd.spectra.frequency_transform(imf, sample_rate, 'nht')
```
IP瞬時相位,、IF瞬時頻率、IA瞬時振幅，

以下對於只有一個IMF的結果
![[hilbert-huang transform.png|450]]
不同於FT，Hilbert-Huang用一個連續的波段就表示了這樣一個訊號。

---
![[hilbert-huang transform nearsight.png]]
>瞬時頻率的波動使 HHT 的能量分布擴展到該範圍內（spread the power within this range），不再集中於單一頻率，反應了非線性的要素

---
對於一個多IMF的訊號(bin是為了離散化頻譜，決定resolution)
```python
freq_edges, freq_centres = emd.spectra.define_hist_bins(0, 100, 128, 'linear')
# Amplitude weighted HHT per IMF
f, spec_weighted = emd.spectra.hilberthuang(IF, IA, freq_edges, sum_imfs=False)
# Unweighted HHT per IMF - we replace the instantaneous amplitude values with ones
f, spec_unweighted = emd.spectra.hilberthuang(IF, np.ones_like(IA), freq_edges, sum_imfs=False)
```
![[hilbert-huang transform more IMFs.png]]

---
2D-hilbert-huang transform

![[2D HHT.png|600]]
透過上圖可以嘗試理解IF瞬間頻率的意義

---
Bin determines the resolution

e.g., with a linear spacing: `define_hist_bins(1, 25, 24, 'log')`
![[bin resolution.png]]

---
### Application
對於一個週期性震盪的複雜訊號
我們需要不同的windows來比較出哪種resolution會比較好
![[STFT vs HHT 1.png|350]]![[STFT vs HHT 2.png|350]]
HHT可以把**同瞬間頻率的點連起來看**

---
Plotting
```python
emd.plotting.plot_hilberthuang(hht, time_centres, freq_centres)
emd.plotting.plot_hilberthuang(hht, time_centres, freq_centres,

                               cmap='viridis', time_lims=(750, 1500),  log_y=True)
```
![[HHT standard plotting.png]]

---
# EEMD
噪音和瞬態信號的結合可能導致 EMD 分解效果不佳，出現信號分散在多個 IMF 的問題
<split no-margin>
![[signal with manual bursting.png|450]]![[IMF of signal with manual bursting.png|450]]
</split>

---
![[flowchart of EEMD.png]]

---
![[result of EEMD.png|500]]
```python
emd.sift.ensemble_sift()
imf = emd.sift.ensemble_sift(burst+n, max_imfs=5, nensembles=24, nprocesses=6, ensemble_noise=1, imf_opts=imf_opts)
```
`noise_variance from `0.25` to `1`.

---
## Mask
加入一個想要分離的頻率，用以解決資料被seperate的問題
![[unmasked signal.png|300]]![[unmasked signal EMD.png|500]]

---
<split no-margin>
![[masked signal.png|400]]![[masked signal EMD.png|400]]
</split>

一個頻率為 $f Hz$ 的掩膜預期會去除低於 $0.7 \times fHz$ 的頻率成分。
```python
emd.sift.mask_sift(xy, mask_freqs=30/sample_rate, ret_mask_freq=True, max_imfs=4)
```
ref. http://arxiv.org/abs/1709.05547

---
automatic methods, use the first two modes as frequency
```python
emd.sift.iterated_mask_sift(x, sample_rate=sample_rate, max_imfs=3)
```
<split no-margin>
![[automatic masked test signal.png|400]]
![[automated masking spectrum.png|400]]
</split>

---
操作上
1. 先得到1-layer IMFs
2. 進行Mask $\rightarrow$ 2-layer IMFs，

---
# MEMD
ref. [nihms439498.pdf](https://pmc.ncbi.nlm.nih.gov/articles/PMC3831372/pdf/nihms439498.pdf)
multivariate data，用於local minimum不好找的情況。
projections along different directions in $(n−1)$dimensional spaces

$Hammersley$ 序列
$(n−1)$ 球面對應於 $n$ 維空間中的單位球面，$P_k (t)=v(t) \cdot x_{\theta_k}$
在特定投影上，主要特徵之極大值
$$m(t) = \frac{1}{K} \sum_{k=1}^K e_k(t)$$
$e_k(t)$為上邊界
$$d(t)=v(t)-m(t)$$

---
# CEEMDAN
透過加入噪聲，解決雜訊的問題。

原始論文：[[A_complete_ensemble_empirical_mode_decomposition_with_adaptive_noise.pdf]]
ref. 
- 科普：[CEEMDAN：一种优化的集合经验模态分解算法](https://cloud.baidu.com/article/3253447)
- 應用：
	- [[Denoising_electromyogram_and_electroencephalogram_.pdf]]
	- [[A Novel Noise Reduction Method of UAV Magnetic Survey Data Based on CEEMDAN, Permutation Entropy, Correlation Coefficient and Wavelet Threshold Denoising.pdf]]

---
<split even>
![[flowchart of EEMD.png|450]]
![[flowchart of CEEMDAN.png|500]]
</split>


---
# tools
- python庫解決方案: [PyEMD包安装导入踩坑 - 哔哩哔哩](https://www.bilibili.com/opus/781745878429859881)
- [EMD Tutorials — emd 0.6.2 documentation](https://emd.readthedocs.io/en/stable/emd_tutorials/index.html)
- [3.7 HHT ( Hilbert-Huang Transform)](http://www.ancad.com.tw/VS_Online_Help/ch03s07.html)

---
# Customised sifting with functools.partial
```python
import emd
# Create a mask sift config object and customise some options
config = emd.sift.get_config('mask_sift')
config['max_imfs'] = 5
config['mask_amp_mode'] = 'ratio_sig'
config['envelope_opts/interp_method'] = 'mono_pchip'

# Create a partial function - my_mask_sift is now a function with the arguments
# in config fixed as defaults.
from functools import partial
my_mask_sift = partial(emd.sift.mask_sift, **config)

# my_mask_sift can then be called with the input data as the only argument.
imfs = my_mask_sift(x)

```

---
```python
# Create a temporary file OR specify your own file path
import tempfile
config_file = tempfile.NamedTemporaryFile(prefix="ExampleSiftConfig_").name
# Or uncomment the following line and specify your own file
#config_file = '/path/to/my/file'

# Save the config into yaml format
config.to_yaml_file(config_file)
```