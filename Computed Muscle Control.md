IDEA:用模擬肌肉的激發來drive model於還原動作軌跡
用途: find out a set of muscle excitations (or, more generally, actuator controls) that will drive a dynamic musculoskeletal model to track a set of desired kinematics.
Input
- Desire Kinematics`.mot`
- Tracking Tasks`.xml`
- Actuator Constraints`.xml`
- **Set CMC look-ahead window.** A time window of 0.01 is generally sufficient for muscle activations to change enough to produce the desired accelerations.動作肌肉激活需要時間完成