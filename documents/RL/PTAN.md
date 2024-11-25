- $Agent$: a class that knows how to convert a batch of observations to a batch of actions to be executed.
- `ptan.agent.`$BaseAgent$: self-define
- $ActionSelector$: choose action from some specific output

使用step_count來顯示或者調用多少資訊
- $ExperienceSource$: 實時數據生成，用來追蹤以及調用經驗
- $ExperienceSourceBuffer$: 大量數據的調用
- $TargetNet$: 確保穩定性，一次只更新一個NN的權重，對目標經過週期進行深拷貝，所以會不一致的更新速度
	- `sync()`->`alpha_sync()`:用來給cont. actions

```python
import numpy as np >>> import ptan
q_vals = np.array([[1, 2, 3], [1, -1, 0]]) 
q_vals array([[ 1, 2, 3], [ 1, -1, 0]])
selector = ptan.actions.ArgmaxActionSelector() 
selector(q_vals)
array([2, 0])
```
$Q-values$ 是指在s下的actions期望值，所以經過selector返回特定index

$EndOfEpisodeHandler$: 可視化工具，紀錄訓練狀況
$PeriodicEvents$: 在特定階段執行動作

MuJoCo(付費), PyBullet(https://github.com/bulletphysics/bullet3), 用來進行模擬
`buffer.populate(1)`：將資料添加進ExpRelayBuffer
`rewards_steps = exp_source.pop_rewards_steps()`：調用剛剛添加的那筆資料

一個完整的追蹤流程：
```python
buffer.populate(1)
                rewards_steps = exp_source.pop_rewards_steps()
                if rewards_steps:
                    rewards, steps = zip(*rewards_steps)
                    tb_tracker.track("episode_steps", steps[0], frame_idx)
                    tracker.reward(rewards[0], frame_idx)
```