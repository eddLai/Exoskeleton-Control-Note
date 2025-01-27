[Soft Actor Critic—Deep Reinforcement Learning with Real-World Robots – The Berkeley Artificial Intelligence Research Blog](https://bair.berkeley.edu/blog/2018/12/14/sac/#:~:text=Soft%20actor,a%20single%20set%20of%20hyperparameters)
[(145) Deep Reinforcement Learning, 2018 - YouTube](https://www.youtube.com/playlist?list=PLJV_el3uVTsODxQFgzMzPLa16h6B8kWM_)

---
### Q-function, from tabular $Q$ to $DQN$
已經證明$\pi'(s)=arg \max_a Q^\pi(s, a)$會使得$V^{\pi'}(s) \geq V^\pi(s)$
$Tabular\ Q\ function$

| State | A1 | A2 |
|-------|----|----|
| S1    | 0  | 0  |
| S2    | 0  | 0  |
| S3    | 0  | 0  |
| S4    | 0  | 0  |
$Q(S1, A1) \leftarrow 0 + \alpha (1 + \gamma \max_a Q(S2, a) - 0)$
$Assuming ( \alpha = 0.1 ) and ( \gamma = 0.9 )$,
The updated Q-table:

| State | A1  | A2 |
|-------|-----|----|
| S1    | 0.1 | 0  |
| S2    | 0   | 0  |
| S3    | 0   | 0  |
| S4    | 0   | 0  |

After many iterations, 

| State | A1  | A2 |
|-------|-----|----|
| S1    | 0.6 | 0.4|
| S2    | 0.7 | 0.5|
| S3    | 0.8 | 0.9|
| S4    | 1.0 | 0.2|
### DQN
所以要用NN架構去逼近表格
- Input：輸入一個State
- Output：一個多個Action的期望值，在此先假設Action為離散的。

所以變得跟本不用管Policy function
### Why Target Net?
目標的Q函數不會更新，而只有原本的Q函數更新
![[RL Target Nettwork.png|300]]

$\pi$ 是policy function
1. 代理在狀態 $( s_t )$ 選擇行動 $( a_t )$。
2. 行動導致代理接收即時獎勵 $( r_t )$ 並轉移到新狀態 $( s_{t+1} )$。
3. 計算目標 $( Q )$ 值，即 $( r_t )$ 加上 $( s_{t+1} )$ 下最佳行動的折扣 $( Q )$ 值。
4. 更新行為網絡的 $( Q )$ 值以減小目標 $( Q )$ 值和估計的 $( Q )$ 值之間的差異。
其中重複第四點，不斷進行多次更新，直到某個收斂標準被滿足（例如，損失函數的減少到一個閾值以下）。才開放Target Net進行更新，以避免同時有兩個NN在進行訓練
(因為是off-policy所以可以得到$s_{t+1}$等資訊)



---
### deep deterministic policy gradient
或稱為pathwise derivative policy gradient，其中只是強化了policy function的部分，本質上算是Q function的改良也是一種off-policy算法可以用比較少的軌跡資料
*"Deterministic PG makes it possible to apply the chain rule to the Q-value, and by maximizing the Q, the policy will be improved as well."*
*"Policy is deterministic, which means that it directly provides us with the action to take from the state."*

缺點：our policy is now deterministic, so we have to explore the environment somehow，相反的PPO本身就帶有sampling的過程所以產出的決定是隨機的。

### OU過程
奧恩斯坦-烏倫貝克（Ornstein-Uhlenbeck）過程是一種用來模擬具有時間相關性噪聲的隨機過程。它在數學上可以表示為一個隨機微分方程：
$dx_t = \theta (\mu - x_t) dt + \sigma dW_t$

其中:
- $x_t$ 是時間 \( t \) 的過程值。
- $\theta$ 是速度參數，控制過程回歸到平均值的速度。
- $\mu$ 是過程的長期平均值。
- $\sigma$ 是過程的波動性或標準差。
- $dW_t$ 是韋納過程（Wiener Process），代表隨機噪聲。

最後要確認動作的值，並進行範圍剪裁
`__call__`代表可以直接初始化這個物件即會執行
```python
def __call__(self, states, agent_states):
        states_v = ptan.agent.float32_preprocessor(states)
        states_v = states_v.to(self.device)
        mu_v = self.net(states_v)
        actions = mu_v.data.cpu().numpy()

        if self.ou_enabled and self.ou_epsilon > 0:
            new_a_states = []
            for a_state, action in zip(agent_states, actions):
                if a_state is None:
                    a_state = np.zeros(
                        shape=action.shape, dtype=np.float32)
                a_state += self.ou_teta * (self.ou_mu - a_state)
                a_state += self.ou_sigma * np.random.normal(
                    size=action.shape)

                action += self.ou_epsilon * a_state
                new_a_states.append(a_state)
        else:
            new_a_states = agent_states

        actions = np.clip(actions, -1, 1)
        return actions, new_a_states
```

---

### Distributed distributional DDPG
不同處：
- critic's output is N_ATOMS values，用於解決Q function輸出單一動作的期望值，而連續動作只會得到一個值這樣的問題
- simple random noise to the actions is OK

ATOMS：用於將連續轉離散
dones_mask：對於未來估值的$V$當任務結束應為0
### Terms
stateless DQN (Deep Q-Network) agent：是一種不保留(使用)以前狀態記憶的Agent
