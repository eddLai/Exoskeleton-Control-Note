其他可能架構
- [[special Q-learning]]

---
### 傳統Q function
初始化$Q函數 ( Q(s, a; \theta^Q) )$：$\theta^Q \sim \mathcal{N}(0, \sigma^2)$ or $\theta^Q \sim \mathcal{U}(-\epsilon, \epsilon)$
- 避免梯度爆炸：高斯分布或均勻分布$\epsilon$ 確保初始化的參數不會太大。
- 早期的探索：確保策略有足夠的隨機性。
### Critic with DQN
$h_{obs} = f_{obs}(x)$
$h_{combined} = [h_{obs}; a]$
$y = f_{out}(h_{combined})$ 
`obs_net`：先用一些層處理$Env$的輸入
`out_net`：再與$actor$的輸出做整合，使用`torch.cat`
Single Neuron for Ouput：將`out_net`的`hidden layers`做壓縮輸出單一值(傳統DDPG的方法)

---
### D4PG DQN Critic
為了$distrubuted\ distributional$的性質，更好的探索性、穩定性
`distr_to_q`：轉回單一預期值，$Q = \sum_{i=1}^{N} p_i \cdot v_i, p_i為Atom, v_i為原子預期value$
>注意：需要`res.unsqueeze(dim=-1)`，增加一個Dim以匹配輸出的形狀
```python
class D4PGCritic(nn.Module):
    def __init__(self, obs_size, act_size,
                 n_atoms, v_min, v_max):
        super(D4PGCritic, self).__init__()

        self.obs_net = nn.Sequential(
            nn.Linear(obs_size, 400),
            nn.ReLU(),
        )

        self.out_net = nn.Sequential(
            nn.Linear(400 + act_size, 300),
            nn.ReLU(),
            nn.Linear(300, n_atoms)
        )

        delta = (v_max - v_min) / (n_atoms - 1)
        self.register_buffer("supports", torch.arange(
            v_min, v_max + delta, delta))

    def forward(self, x, a):
        obs = self.obs_net(x)
        return self.out_net(torch.cat([obs, a], dim=1))

    def distr_to_q(self, distr):
        weights = F.softmax(distr, dim=1) * self.supports
        res = weights.sum(dim=1)
        return res.unsqueeze(dim=-1)
```
`register_buffer`用於紀錄訓練過程中非模型的參數(不用梯度傳播)但又需要保存的內容

