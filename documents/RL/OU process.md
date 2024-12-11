Ornstein-Uhlenbeck（OU）
$dx_t = \theta (\mu - x_t) dt + \sigma dW_t$

其中：
- \($x_t$\) 是当前的噪声值。
- \($\mu$\) 是长期平均值（`ou_mu`），噪声的中心向往回归的位置。
- \($\theta$\) （`ou_teta`）是回归率，决定了噪声回归到平均值的速度。
- \($\sigma$\) （`ou_sigma`）是噪声的标准差，决定了噪声的振幅。
- \($dW_t$\) 是维纳过程（Wiener process），表示随机扰动。
- \($dt$\) 是时间步长。

`ou_epsilon`可能会随着时间或训练的进程而动态调整，以平衡探索与利用。具体来说，`ou_epsilon`通常在训练开始时设为较大的值，以鼓励更多的探索，随着训练的进行，逐渐减小`ou_epsilon`的值，以减少噪声的影响，使策略更加稳定和精确。

```python
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
```