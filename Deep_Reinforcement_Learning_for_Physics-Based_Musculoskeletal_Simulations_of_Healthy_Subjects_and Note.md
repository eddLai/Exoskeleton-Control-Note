[[Deep_Reinforcement_Learning_for_Physics-Based_Musculoskeletal_Simulations_of_Healthy_Subjects_and.pdf]]

先從熟悉的RL架構進場

Deciaion variables in analogous
opensim端等於做了一層濾波

RL relatively sparse
解決了cont. action space的問題
learning from demostration
joint angle rather than muscle activation
但還是由上而下
no knowledge with the env.

4層PPO
214＋312×2＋18
tanh做標準化
