## 目標
核心採用Pathwise Derivative PG或稱Deep Deterministic Policy Gradient，並以最新的D4PG方法修改進行優化以提高穩定度
參考：[[Deep Reinforcement Learning Hands-On Apply modern RL.pdf]]的ch17
詳見[[principle of RL]], [[python tips]]

---
### models in pytorch
善用[[PTAN]] lib
- [[DDPGActor code]]
- [[D4PGCritic code]]
- [[Agent]]

---
### 環境輸入
- 考慮用OpenAI gym建立一個[[模擬環境]]
- [[嵌入式系統]]作輸入的串接code


### 疊代訓練
對於Actor DNN：單純的Gradient Decending
- [ ] SEMI relative importance of the specific user data compared to the other subjects, 80:1 is the best ratio
- [ ] epochs_max = 200
- [ ] stopping early if the loss is not improving in 5 epochs
- [ ] 10-fold cross validation as well as leave-one-subject-out validation to remove bias across users
對於Critic
- [ ] 使用soft sync，每次加入一點的新權重

D4PG的其他訓練案例：
![[RL trainning exampke.png]]

[[ModelTraining code]]
[[ModelInferencing code]]

---
### 顯示
如果是透過視覺進行Input則需要依據FPS進行調適
```python
if args.vis:
	delta = 1/FPS - (time.time() - start_ts) 
	if delta > 0:
		time.sleep(delta)
```