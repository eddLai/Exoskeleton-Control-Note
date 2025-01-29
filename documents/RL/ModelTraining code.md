- [x] Target network

optimizer.backward()：計算梯度
optimizer.step()：==以優化器==進行權重更新

## Trainning of Q functions
1. 隨機sample出一個batch
>所以能夠使用off-policy的特性才重要，但也因此需要進行done_mask的處理
>```python
`states_v, actions_v, rewards_v, dones_mask, last_states_v = ddpg.unpack_batch_ddpg(batch, device)`：last_states_v是預測結果而非states_v的平移
>```
[[unpack_batch_ddpg code]]

2. 將batch輸入net中
>並沒有順序性的一次輸入全部(so-called tensor平行運算)
>```python
>q_v = crt_net(states_v, actions_v)
>```
1. 使用`target_model()`取得$actions$ and $Q_{value}$，對於D4PG來說是一個distribution
>而非直接從當前正在訓練的actor, critic model去取得，以達到穩定的效果
>```
>last_act_v = tgt_act_net.target_model(last_states_v)
>q_last_v = tgt_crt_net.target_model(last_states_v, last_act_v)
>```

1. 計算新Q對於舊的Q的更新方向
># DDPG
>TD的算法只要前後兩個，參見[[principle of RL]]中的**why target net**，
>$Q_{\text{target}} = r + \gamma \cdot Q(s', a') \cdot (1 - \text{done})$, done是用來處理終止狀態
>計算$\text{Loss} = \text{MSE}(Q(s, a), Q_{\text{target}})$，用以確保Q的更新方向正確
>$\text{Loss} = \frac{1}{N} \sum_{i=1}^{N} \left( Q(s_i, a_i) - \left( r_i + \gamma \cdot Q(s'_i, a'_i) \cdot (1 - \text{done}_i) \right) \right)^2$
>```python
># DDPG
q_last_v[dones_mask] = 0.0
q_ref_v = rewards_v.unsqueeze(dim=-1) + q_last_v * GAMMA
critic_loss_v = F.mse_loss(q_v, q_ref_v.detach())
critic_loss_v.backward()
crt_opt.step()
>```
># D4PG
>$L(P, Q) = -\sum_{i} Q(i) \log P(i)$
>$P = \text{softmax}(\text{crt\_net}(s, a))$，雖然已經離散化，但還是要確保總合為1
>$Q = \text{distr\_projection}(r + \gamma Q(s', a'), \text{done})$，[[distr_projection的詳細內容]]
>```python
>last_distr_v = F.softmax(tgt_crt_net.target_model(ast_states_v, last_act_v), dim=1)
>proj_distr_v = distr_projection(last_distr_v, rewards_v, dones_mask,gamma=GAMMA**REWARD_STEPS, device=device)
>prob_dist_v = -F.log_softmax(crt_distr_v, dim=1) * proj_distr_v
>critic_loss_v = prob_dist_v.sum(dim=1).mean()
>```
>備註：[[log_softmax與softmax的差異]]
>

## Training of the actor
1. 清空之前Critic訓練殘存的Actor梯度
2. 最大化Q值，以得到最佳的Reward，因此加上負號
>$L_{\text{Actor}} = -Q(s, \text{cur\_actions\_v})$
>$\nabla_{\text{Actor}} = \frac{\partial L_{\text{Actor}}}{\partial \text{params}}$

## Sync tgt
```python
tgt_act_net.alpha_sync(alpha=1 - 1e-3)
tgt_crt_net.alpha_sync(alpha=1 - 1e-3)
```