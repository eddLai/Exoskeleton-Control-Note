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
