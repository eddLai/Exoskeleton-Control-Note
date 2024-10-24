![[Coordinate Systems.png|300]]
# Data collection
tool list: [Tools for Preparing Motion Data - OpenSim Documentation - OpenSim](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53089096/Tools+for+Preparing+Motion+Data)
### Terms
- anthropometry:人體測量學
- **PCSA** 是 **Physiological Cross-Sectional Area（生理橫截面積）**
### file and data structure
1. `.trc`: Marker trajectories
2. `.sto`: GRF, COP(center of pressure), EMG data
	1. 代表storage
	2. 第一行一定要是time
	3. 由opensim開發極似`.mot`
3. `.mot`: GRF, COP, Joints angle, EMG data
	1. 會有endheader
	2. 基本用途:SIMM (Software for Interactive Musculoskeletal Modeling)
4. `.osim`: Load model
5. `.mot`: Load motion
6.  [C3D (.c3d) Files](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53090837/C3D+.c3d+Files)，Mocap, OpenSim 4.0可以轉檔成`.trc`, `.mot`

### Caution
force file: NaNs often occur when computing COP，這是不行的