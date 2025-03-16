`CEINMS -S <path to main XML setup file>`
### optimization algorithm goal: 
`trackedMuscles在實驗中測量的肌肉  || predictedMusclesao沒有在實驗中測量的肌肉`
objective function weightings alpha, beta and gamma

---
- _openLoop_: means _full-predictive_ 不需要外部反饋e.g. joint moments file
- _Hybrid mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle without experimental excitations

---
- _EMG-assisted mode_
> alpha = 1, beta > 1, gamma > 1
> 
> trackedMuscles = every muscle with experimental excitations
> 
> predictedMuscles = remaining muscles

---
- _Full optimization-driven closed-loop mode_
> alpha = 1, beta = 0, gamma > 0
> 
> trackedMuscles = none
> 
> predictedMuscles = every muscle
