- [ ] [[relay buffer]]
- [ ] double DQN
- [x] noisy net
- [ ] deuling DQN
- [x] Exploration by [[OU process]]

寫net的code與輸入的Agent應該要分開。使用DDPG才需要使用OU
```python
class AgentD4PG(ptan.agent.BaseAgent):
    """
    Agent implementing noisy agent
    """
    def __init__(self, net, device="cpu", epsilon=0.3):
        self.net = net
        self.device = device
        self.epsilon = epsilon

    def __call__(self, states, agent_states):
        states_v = ptan.agent.float32_preprocessor(states)
        states_v = states_v.to(self.device)
        mu_v = self.net(states_v)
        actions = mu_v.data.cpu().numpy()
        actions += self.epsilon * np.random.normal(
            size=actions.shape)
        actions = np.clip(actions, -1, 1)
        return actions, agent_states
```

clip：可以用於防護，+/-75度