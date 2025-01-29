# Recall Power Series
For an ordinary Differential Equation: 
$$y'' + p(x)y' + q(x)y = 0$$
存在解
$$y(x) = \sum_{n=0}^{\infty} a_n x^n$$
帶入
$$\frac{dy}{dx} = \sum_{n=1}^{\infty} n a_n x^{n-1}$$
$$\frac{d^2y}{dx^2} = \sum_{n=2}^{\infty} n(n-1) a_n x^{n-2}
$$
$$\sum_{n=2}^{\infty} n(n-1) a_n x^{n-2} + p(x) \sum_{n=1}^{\infty} n a_n x^{n-1} + q(x) \sum_{n=0}^{\infty} a_n x^n = 0
$$
$$=\sum_{m=0}^{\infty} (m+2)(m+1) a_{m+2} x^m + \sum_{m=0}^{\infty} p(x)(m+1) a_{m+1} x^m + \sum_{m=0}^{\infty} q(x) a_m x^m = 0$$
$$=\sum_{m=0}^{\infty} \left[ (m+2)(m+1) a_{m+2} + p(x)(m+1) a_{m+1} + q(x) a_m \right] x^m = 0
$$
$$可以找出a_m之解，(m+2)(m+1) a_{m+2} + p(x)(m+1) a_{m+1} + q(x) a_m=0$$

---
## Fourier Series
對於一週期為p之函數，可拆解成cos and sin。
$$f(x+2\pi)=f(x)$$
$$f(x) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos\frac{n\pi x}{p} + b_n \sin\frac{n\pi x}{p} \right), \, n \in \mathbb{N}$$
Known in a period:
$$\int_{-p}^p f(x) \, dx=\int_{-p}^p[\frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos\frac{n\pi x}{p} + b_n \sin\frac{n\pi x}{p} \right)], \, n \in \mathbb{N}$$
$$a_0 = a_0p+\sum_{n=1}^{\infty}[\int_{-p}^p a_ncos(\frac{n\pi x}{p})\, dx+\int_{-p}^p b_nsin(\frac{n\pi x}{p})\, dx]$$
週期內cos, sin積分=0
$$a_0 = \frac{1}{p} \int_{-p}^p f(x) \, dx
$$

---
求$a_n$
求$b_n$
