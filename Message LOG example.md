## 開啟GUI
```
SCONE version 2.3.1.2903
SCONE Tutorials and Examples are up-to-date
Successfully initialized OpenSim3 version 3.3-2021-01-28
```
## 先按了evaluation
```
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
Loaded Tutorial 4a - Gait - OpenSim.scone; dim=53; time=0.061
get_thread_priority() is not implemented for this platform
Terminating simulation at 2.705
Result             = 95.0951
  Gait             = 92.9274 <- 100 * (0.929274 > 0.05)
    step_velocity  = 0.0736412
    step_count     = 6
  Effort           = 0.756711 <- 0.1 * 7.56711
    effort         = 1399.88
    distance       = 2.4821
  MuscleActivation = 0.828293 <- 2000 * 0.000414146
    effort         = 1.37907
    distance       = 2.4821
  DofLimits        = 0.293592
    ankle_angle_l  = 0 <- 0.1 * 0
    ankle_angle_r  = 0 <- 0.1 * 0
    knee_angle_l   = 0.132264 <- 0.02 * (6.61322 > 1)
    knee_angle_r   = 0.161328 <- 0.02 * (8.0664 > 1)
  GRF              = 0.289106 <- 10 * 0.0289106
Evaluation took 1.82416s for 2.705s (1.48288x real-time)
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
Created model H0918v3; dofs=9 muscles=18 mass=74.5314
```

---
## 按下optimzation
```
Loaded Tutorial 4a - Gait - OpenSim.scone; dim=53; time=0.044
Reorganizing windows, columns=1 rows=1
Initialized optimization 241019.134522.H0918v3.RS2.S10WA3K1G14.D20
```