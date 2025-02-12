# Actor
Ref. [[Real-Time_NN_Gait_Phase_Estimation_Using_a_Robotic_Hip_Exoskeleton.pdf]]
目標：要擬合大腿步態週期
### 初始化
$Actor函數 \pi(s; \theta^\pi)$：
$W^{[l]} \sim \mathcal{N}(l-1, \sqrt{\frac{2}{n^{[l-1]}}})(He initialization)$
or
$W^{[l]} \sim \mathcal{U}(-\sqrt{\frac{6}{n^{[l-1]} + n^{[l]}}}, \sqrt{\frac{6}{n^{[l-1]} + n^{[l]}}})(Xavier initialization)$
Initial Biases：$b^{[l]} = \vec{0}$

---
### 模型架構
$\theta^{\hat{Q}} \leftarrow \theta^Q$
$\theta^{\hat{\pi}} \leftarrow \theta^\pi$
- 隱藏層：單隱藏層20個神經元，tanh激活函數
- 輸入輸出層：linear激活函數
- 優化器：使用帶Nesterov動量的SGD優化器，學習率為0.001

```python
HID_SIZE = 20

class DDPGActor(nn.Module):
    def __init__(self, obs_size, act_size):
        super(DDPGActor, self).__init__()

        self.net = nn.Sequential(
            nn.Linear(obs_size, HID_SIZE),  # 17 features to hidden layer with 20 neurons
            nn.Tanh(),          # tanh activation function for hidden layer 
            nn.Linear(20, act_size),   # Hidden layer to 2 output values
        )

    def forward(self, x):
        return self.net(x)
```

```python
optimizer = torch.optim.SGD(model.parameters(), lr=0.001, momentum=0.9, nesterov=True)
loss_function = nn.L1Loss()  # MAE loss
```
