下面將詳細推導從線性時不變(LTI)系統的狀態方程出發，得到狀態 x(t)x(t) 的封閉形式解的過程。此推導將包含較多的數學細節與概念說明。

---

### 1. 問題設定

我們考慮一個線性時不變系統(LTI System)的狀態空間描述如下：

$$x˙(t)=Ax(t)+Bu(t),x(t0)=x0\dot{x}(t) = A x(t) + B u(t), \quad x(t_0) = x_0 y(t)=Cx(t)y(t) = C x(t)$$

其中：

- x(t)∈Rnx(t) \in \mathbb{R}^n 是狀態向量。
- u(t)∈Rmu(t) \in \mathbb{R}^m 是輸入向量。
- y(t)∈Rpy(t) \in \mathbb{R}^p 是輸出向量。
- A∈Rn×nA \in \mathbb{R}^{n \times n} 是系統矩陣，B∈Rn×mB \in \mathbb{R}^{n \times m} 是輸入矩陣，C∈Rp×nC \in \mathbb{R}^{p \times n} 是輸出矩陣。
- 初始條件為 x(t0)=x0x(t_0) = x_0。

系統方程為一組耦合的一階線性微分方程，可寫成向量-矩陣形式。

---

### 2. 基本概念與工具

要解此微分方程，我們會用到以下概念和步驟：

1. **同質方程(Homogeneous equation)** 的解：  
    若不考慮輸入 u(t)u(t)，則系統簡化為同質(齊次)方程：
    
    x˙(t)=Ax(t).\dot{x}(t) = A x(t).
    
    該方程的解形式為：
    
    xh(t)=eA(t−t0)x0.x_h(t) = e^{A(t-t_0)} x_0.
    
    此處 eA(t−t0)e^{A(t-t_0)} 稱為 **狀態轉移矩陣**(State Transition Matrix, STM)，其定義為：
    
    eAτ=I+Aτ+A2τ22!+A3τ33!+⋯ ,e^{A\tau} = I + A\tau + \frac{A^2 \tau^2}{2!} + \frac{A^3 \tau^3}{3!} + \cdots,
    
    並具有滿足微分方程：
    
    ddteA(t−t0)=AeA(t−t0),eA(t0−t0)=I.\frac{d}{dt}e^{A(t-t_0)} = A e^{A(t-t_0)}, \quad e^{A(t_0 - t_0)} = I.
2. **特徵方程與對角化(選擇性)**：  
    若 AA 可對角化，可將 A=VΛV−1A = V \Lambda V^{-1} (假設簡化情況)，則：
    
    eA(t−t0)=VeΛ(t−t0)V−1,e^{A(t-t_0)} = V e^{\Lambda(t-t_0)} V^{-1},
    
    此為矩陣指數的解析意義。但是本步驟並非必要，一般的狀態轉移矩陣定義即足以使用。
    
3. **變量變換(Variation of Parameters)求解非齊次方程**：  
    考慮原非齊次方程：
    
    x˙(t)=Ax(t)+Bu(t).\dot{x}(t) = A x(t) + B u(t).
    
    解非齊次線性方程常用的方法之一是「參數變動法」(variation of parameters)。具體作法是：
    
    - 我們已知同質方程的解為 xh(t)=eA(t−t0)x0x_h(t) = e^{A(t-t_0)} x_0。
    - 對於非齊次項 Bu(t)B u(t)，我們將嘗試找到一個特殊解 xp(t)x_p(t)。
    
    我們假設總解為：
    
    x(t)=eA(t−t0)x0+xp(t).x(t) = e^{A(t-t_0)} x_0 + x_p(t).
    
    將此代入原方程以求得 xp(t)x_p(t)。
    

---

### 3. 推導非齊次解的過程

令：

x(t)=eA(t−t0)x0+xp(t).x(t) = e^{A(t-t_0)} x_0 + x_p(t).

將此代入非齊次方程：

x˙(t)=Ax(t)+Bu(t).\dot{x}(t) = A x(t) + B u(t).

計算左手邊的導數：

x˙(t)=ddt(eA(t−t0)x0+xp(t))=AeA(t−t0)x0+x˙p(t).\dot{x}(t) = \frac{d}{dt}\bigl(e^{A(t-t_0)} x_0 + x_p(t)\bigr) = A e^{A(t-t_0)} x_0 + \dot{x}_p(t).

右手邊為：

Ax(t)+Bu(t)=A(eA(t−t0)x0+xp(t))+Bu(t)=AeA(t−t0)x0+Axp(t)+Bu(t).A x(t) + B u(t) = A \bigl(e^{A(t-t_0)} x_0 + x_p(t)\bigr) + B u(t) = A e^{A(t-t_0)} x_0 + A x_p(t) + B u(t).

將兩者相等：

AeA(t−t0)x0+x˙p(t)=AeA(t−t0)x0+Axp(t)+Bu(t).A e^{A(t-t_0)} x_0 + \dot{x}_p(t) = A e^{A(t-t_0)} x_0 + A x_p(t) + B u(t).

左、右手邊的 AeA(t−t0)x0A e^{A(t-t_0)} x_0 相互抵消後，得到：

x˙p(t)=Axp(t)+Bu(t).\dot{x}_p(t) = A x_p(t) + B u(t).

現在，我們將焦點放在此方程：

x˙p(t)−Axp(t)=Bu(t).\dot{x}_p(t) - A x_p(t) = B u(t).

這是一個以 xp(t)x_p(t) 為未知的非齊次方程。我們可以再利用一個技巧來簡化：考慮引入「積分因子」的概念。在矩陣狀態空間中，此概念透過狀態轉移矩陣來實現。

為了消去左側的 Axp(t)A x_p(t) 項，我們左乘 e−A(t−t0)e^{-A(t-t_0)}：

e−A(t−t0)x˙p(t)−e−A(t−t0)Axp(t)=e−A(t−t0)Bu(t).e^{-A(t-t_0)} \dot{x}_p(t) - e^{-A(t-t_0)} A x_p(t) = e^{-A(t-t_0)} B u(t).

利用矩陣微分法則：ddt[e−A(t−t0)xp(t)]=e−A(t−t0)x˙p(t)−e−A(t−t0)Axp(t)\frac{d}{dt}[e^{-A(t-t_0)} x_p(t)] = e^{-A(t-t_0)}\dot{x}_p(t) - e^{-A(t-t_0)} A x_p(t)，故上式可重寫為：

ddt[e−A(t−t0)xp(t)]=e−A(t−t0)Bu(t).\frac{d}{dt}[e^{-A(t-t_0)} x_p(t)] = e^{-A(t-t_0)} B u(t).

對 tt 從 t0t_0 積分到 tt:

e−A(t−t0)xp(t)−e−A(t0−t0)xp(t0)=∫t0te−A(τ−t0)Bu(τ) dτ.e^{-A(t-t_0)} x_p(t) - e^{-A(t_0 - t_0)} x_p(t_0) = \int_{t_0}^{t} e^{-A(\tau - t_0)} B u(\tau) \, d\tau.

注意在 t=t0t = t_0 時，e−A(t0−t0)=e0=Ie^{-A(t_0 - t_0)} = e^0 = I。通常我們選擇 xp(t0)=0x_p(t_0) = 0 作為特解的初始條件，因為我們最終的總解中會考慮初始條件的影響在 eA(t−t0)x0e^{A(t-t_0)} x_0 中處理。若 xp(t0)=0x_p(t_0) = 0，則：

e−A(t−t0)xp(t)=∫t0te−A(τ−t0)Bu(τ) dτ.e^{-A(t-t_0)} x_p(t) = \int_{t_0}^{t} e^{-A(\tau - t_0)} B u(\tau) \, d\tau.

兩邊再右乘 eA(t−t0)e^{A(t-t_0)}：

xp(t)=∫t0teA(t−τ)Bu(τ) dτ.x_p(t) = \int_{t_0}^{t} e^{A(t-\tau)} B u(\tau) \, d\tau.

因此，我們得到了特解：

xp(t)=∫t0teA(t−τ)Bu(τ) dτ.x_p(t) = \int_{t_0}^{t} e^{A(t-\tau)} B u(\tau) \, d\tau.

將特解與同質解相加，即為原系統的總解：

x(t)=eA(t−t0)x0+∫t0teA(t−τ)Bu(τ) dτ.x(t) = e^{A(t-t_0)} x_0 + \int_{t_0}^{t} e^{A(t-\tau)} B u(\tau) \, d\tau.

---

### 4. 解的意義與狀態轉移矩陣

上式中，eA(t−t0)e^{A(t-t_0)} 稱為「狀態轉移矩陣」，它描述了狀態從時間 t0t_0 演化到時間 tt 的方式，不受輸入影響，純屬系統本身的特性決定。  
完整解包含兩個部分：

1. **自然響應(natural response)**： eA(t−t0)x0e^{A(t-t_0)}x_0，僅仰賴初始條件。
2. **強制響應(forced response)**： ∫t0teA(t−τ)Bu(τ) dτ\int_{t_0}^{t} e^{A(t-\tau)} B u(\tau) \, d\tau ，由輸入 u(t)u(t) 所引入。

當我們有了 x(t)x(t)，輸出 y(t)y(t) 則直接由下式求得：

y(t)=Cx(t).y(t) = Cx(t).

---

### 5. 結論

透過以上推導，我們完整地呈現了狀態方程解的由來，從同質方程的解出發，再利用變參數法將輸入的影響整合進來，最終得到：

x(t)=eA(t−t0)x0+∫t0teA(t−τ)Bu(τ) dτ.x(t) = e^{A(t-t_0)}x_0 + \int_{t_0}^{t} e^{A(t-\tau)}B u(\tau) \, d\tau.

此結果清楚地區分了由初始條件引起的自然響應與由外部輸入所引起的強制響應。對任意給定的輸入函數 u(t)u(t) 及初始狀態 x0x_0，此公式即可求得任意時間 tt 的狀態 x(t)x(t) 。

---

若有其他細節或進一步證明的需求，請隨時提出！