[模仿学习（Imitation Learning）介绍 - 知乎](https://zhuanlan.zhihu.com/p/25688750)也是一種RL
**Behavior Cloning**h存在compounding errors，執行越久，策略越偏差
大量的训练数据形成一个合适的状态概率分布，這個方案是不實際的

---
[李宏毅_ATDL_Lecture_18 - HackMD](https://hackmd.io/@shaoeChen/SJmNmF1ES)
Imitation Learning
- Behavior Cloning
>需要注意：
>- Actor的capacity是有限的
- Inverse Reinforcement Learning: 找出reward而不是policy
- Generative Adversarial network
$$R(\tau)=\sum_{t=1}^Tr(s_t,a_t)$$
尋找一個Reward function滿足上面的假設，即$\bar{R_{\hat{\pi}}}>\bar{R_{\pi}}$
$$r_t=w\cdot f(s_t,a_t)$$
對於一組trajectory
$$R(\tau^n)=\sum_{t=1}^Tr_t$$
我們預期會得到
$$\bar{R}_\pi=\dfrac{1}{N}\sum^N_{n=1}R(\tau^n)=w\cdot\dfrac{1}{N}\sum_{n=1}^N\sum_{t=1}^Tf(s_t,a_t)$$

