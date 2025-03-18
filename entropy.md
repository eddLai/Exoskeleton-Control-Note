### Entropy
ref. 
- [Entropy Hub Guide](https://www.entropyhub.xyz/_downloads/40d9c1910993d9509e60865d940bb066/EntropyHubGuide.pdf)
- [[Approximate Entropy and Sample Entropy A Comprehensive Tutorial.pdf]]
- [[A Novel Noise Reduction Method of UAV Magnetic Survey Data Based on CEEMDAN, Permutation Entropy, Correlation Coefficient and Wavelet Threshold Denoising.pdf]]

Sample Entropy (SE)

得到一個對陣列中，所有可能計算評估
$$SE(m, \gamma, \tau) = -\log\left(\frac{A_{\tau}}{B_{\tau}}\right)$$
存在${x_1, x_2, ..., x_N}$，
- $m$: ~~可輸入之樣式長度~~，切分pattern是自動的，$m$ 的向量為 ${x_i, x_{i+1}, ..., x_{i+m-1}}$，其中 $1 \le i \le N-m+1$
- $r$: $|x_{i+k} - x_{j+k}| \le \gamma$，其中 $0 \le k \le m-1$
- $\tau$: 樣本長度N

B的序列再延伸一個值
$$A_{\tau}=B^{m+1}(\gamma)$$
$$B_{\tau}=B^m(\gamma)$$


---
>SE結果：$0<SE<\infty$, 用於量化時間序列的複雜度或規律性，亂度低表示越規律

粗粒化

用於不同尺度(粗度)的時間序列
$$y_j(\tau) = \frac{1}{\tau} \sum_{i = (j-1)\tau + 1}^{j\tau} x_i \quad \text{for} \quad 1 \leq j \leq \frac{N}{\tau}$$

$$MSE\ method(m,r)\rightarrow CI(Complexity\ Index) = \sum_{i=1}^{\tau_{\text{max}}} SE(i)$$

---
SE example
![[MSE example.png|500]]
白噪音較長時間尺度下較不複雜, 但1/f 噪音沒有


---
### intrinsic mode entropy (IMEn):
based on the recently developed multivariate empirical mode decomposition (MEMD) method
先把Data分解成IMF，再開始計算Sample Entropy
>IMF: 波動是0，上下差小於1?
