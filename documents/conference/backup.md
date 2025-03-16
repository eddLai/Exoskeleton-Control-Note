- [x] 段落全不不勾，最小行距
- [ ] [1] 要找有外骨骼以及疲乏的論文，討論為什麼要用RL，introduction，background review，RL配合review有一個清楚的為什麼要用這個架構，優勢?的說明
- [ ] 改成新的methods
- [x] AR要拿掉
- [x] Figure2 腳的圖

![[外骨骼兩張.png]]


[5]
[6] 哪幾項假設，哪幾項因素會導致不精準

This approach aims to overcome the traditional dynamics models encounter when handling rapid motion transitions.

Given the personalized characteristics of EMG signal, we have chosen a Deep Learning (DL) architecture, surpassing the performance of traditional dynamics models [5, 6]

欠驅動系統
傳統模型，需要一些精確的動作假設，為了滿足假設，有時需簡化被動關節，也需考慮馬達的機械系統方能使系統精確，RL的架構使得指導模型的過程自動化，deep learning 的引入讓RL不需要顯式的公式或者列表，而能保持架構的靈活性。

In exoskeleton technology development, achieving precise and adaptable interaction force control is critical, particularly as we plan to conduct experiments on actual underactuated exoskeleton platforms and extend our interaction force control algorithm to lower limb hydraulic exoskeletons with complex multi-phase dynamics during different gait phases. Traditional mathematical models often fall short in flexibility and adaptability, especially when facing these highly nonlinear and time-varying system dynamics. Reinforcement Learning (RL) emerges as a superior solution, offering the ability to dynamically learn and adjust strategies through continuous interaction with the environment. This capability is crucial as it allows for the adaptation to the unpredictability of real-world applications and enhances safety and operational efficiency in scenarios requiring load carrying and the prediction of short-term user intentions, such as with the HUALEX system. Thus, employing RL over traditional methods is essential for advancing exoskeleton technologies, ensuring more synchronized and responsive human-machine interactions.

We employ the Distributed Deep Deterministic Policy Gradient (D4PG) strategy to detect walking intentions and enhance Human-Machine Interaction (HMI) [4]. The Temporal Convolutional Network (TCN) acts as the actor, identifying time series and understanding user action intentions during muscle fatigue, subsequently commanding the motor controller. The Deep Q-Network (DQN) optimizes the actor's performance. This data-driven approach simplifies the training process by allowing the user to walk at multiple speeds while interacting with the environment. To test our hypothesis that the system provides precise control to reduce the burden on the Rectus Femoris and Biceps Femoris muscles during walking, we conducted experiments comparing integrated EMG (iEMG) with and without assistance (Figure 1).


==#Muslce fatigue is one of the harmful outcome of prolong physical activities.If it gets less concentration on it, the safety and healthy risk not only be the potential problem. Consequently, it inspire me to develop the  project , which is a system aims to reduce the  intensity of specific muscle usage and extend the duration of strenous acticities.#==