---

---
### python與matlab都可以用則需要opensim GUI

---
### 使用conda獨立環境則使用
https://github.com/opensim-org/conda-opensim
conda install -c opensim-org opensim=4.5=py39np120


---
### C++核心功能開發，可能會用到Docker
[opensim_Build-Instructions](https://github.com/opensim-org/opensim-core/wiki/Build-Instructions#build-instructions-1)
[opensim-core-linux-build-script.sh](https://github.com/opensim-org/opensim-core/blob/main/scripts/build/opensim-core-linux-build-script.sh) 編譯core會產生：
- **`opensim-workspace/`**：
- **`swig/`**：
    - 這個目錄是在腳本下載並編譯 [[SWIG（Simplified Wrapper and Interface Generator）]]時創建的。SWIG 是用來生成 OpenSim 的 Python 綁定的重要工具。
- **`.cmake/`**：

運行以下：
```
# Test opensim-core.
echo "LOG: TESTING OPENSIM-CORE..."
cd ~/opensim-workspace/opensim-core-build
# TODO: Temporary for python to find Simbody libraries.
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/opensim-workspace/opensim-core-dependencies-install/simbody/lib
ctest --parallel $NUM_JOBS --output-on-failure
```
### Error
```bash
Number of objective function evaluations             = 397
Number of objective gradient evaluations             = 334
Number of equality constraint evaluations            = 397
Number of inequality constraint evaluations          = 0
Number of equality constraint Jacobian evaluations   = 334
Number of inequality constraint Jacobian evaluations = 0
Number of Lagrangian Hessian evaluations             = 0
Total seconds in IPOPT                               = 433.513

EXIT: Optimal Solution Found.
[info] Set log level to Info.

Active or violated continuous variable bounds
L and U indicate which bound is active; '*' indicates a bound is violated. 
The case of lower==upper==value is ignored.

State bounds: no bounds active or violated

Control bounds: no bounds active or violated

Adjunct bounds: no bounds active or violated

Diffuse bounds: no bounds active or violated

Active or violated parameter bounds
L and U indicate which bound is active; '*' indicates a bound is violated. 
The case of lower==upper==value is ignored.

Time bounds: no bounds active or violated

Parameter bounds: no bounds active or violated

Total number of constraints: 1000.

Differential equation defects:
  L2 norm across mesh, max abs value (L1 norm), time of max abs
/jointset/j0/q0/value        7.89e-12       2.25e-12       0.276947
/jointset/j1/q1/value        6.86e-11       5.22e-11       0.231731
/jointset/j0/q0/speed        1.20e-09       6.38e-10       0.262817
/jointset/j1/q1/speed        2.74e-09       1.47e-09       0.262817

Path constraints: none
[info] ------------------------------------------------------------------------
[info] Elapsed real time: 471 second(s) (7 minute(s), 51 second(s))
[info] Wed Oct  9 18:13:44 2024
[info] MocoTropterSolver succeeded!
[info] ========================================================================
[info] ========================================================================
[info] MocoTropterSolver starting.
[info] Wed Oct  9 18:13:44 2024
[info] ------------------------------------------------------------------------
[info] Costs: (total: 1)
[info]   goal. MocoStateTrackingGoal, enabled: true, mode: cost, weight: 1.0
[info]         state: /jointset/j0/q0/value, weight: 1.0
[info]         state: /jointset/j1/q1/value, weight: 1.0
[info]         state: /jointset/j0/q0/speed, weight: 1.0
[info]         state: /jointset/j1/q1/speed, weight: 1.0
[info] Endpoint constraints: none
[info] Kinematic constraints: none
[info] Path constraints: none
[info] States: (total: 4)
[info]   /jointset/j1/q1/value. bounds: [-10, 10] initial: 0
[info]   /jointset/j1/q1/speed. bounds: [-50, 50] initial: 0
[info]   /jointset/j0/q0/speed. bounds: [-50, 50] initial: 0
[info]   /jointset/j0/q0/value. bounds: [-10, 10] initial: 0
[info] Controls: (total: 2)
[info]   /tau1. bounds: [-150, 150]
[info]   /tau0. bounds: [-150, 150]
[info] Input controls: none
[info] Parameters: none
python3: /root/opensim-workspace/opensim-core-source/dependencies/simbody/SimTKmath/Geometry/include/simmath/internal/GCVSPLUtil.h:95: static SimTK::Vec<MM, double, 1> SimTK::GCVSPLUtil::splder(int, int, SimTK::Real, const SimTK::Vector&, const SimTK::Vector_<SimTK::Vec<MM, double, 1> >&) [with int K = 1; SimTK::Real = double; SimTK::Vector = SimTK::Vector_<double>]: Assertion `t >= x[0] && t <= x[x.size()-1]' failed.


50% tests passed, 2 tests failed out of 4

Total Test time (real) = 531.61 sec

The following tests FAILED:
	  3 - python_tests (Failed)
	  4 - python_examples (Subprocess aborted)
Errors while running CTest

```

---

### 嘗試
依據[Compilation and ctest on Linux](https://github.com/opensim-org/opensim-core/issues/2664)
~/opensim-workspace/opensim-core-build
make -j8 install
切換swig的版本
看錯誤說明，關掉conda
```
======================================================================
ERROR: test_states_trajectory (unittest.loader._FailedTest.test_states_trajectory)
----------------------------------------------------------------------
ImportError: Failed to import test module: test_states_trajectory
Traceback (most recent call last):
  File "/home/eddlai/miniconda3/lib/python3.12/unittest/loader.py", line 396, in _find_test_path
    module = self._get_module_from_name(name)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/eddlai/miniconda3/lib/python3.12/unittest/loader.py", line 339, in _get_module_from_name
    __import__(name)
  File "/home/eddlai/opensim-workspace/opensim-core-source/Bindings/Python/tests/test_states_trajectory.py", line 4, in <module>
    import opensim as osim
  File "/home/eddlai/opensim-workspace/opensim-core-build/Bindings/Python/RelWithDebInfo/opensim/__init__.py", line 18, in <module>
    from .simbody import *
  File "/home/eddlai/opensim-workspace/opensim-core-build/Bindings/Python/RelWithDebInfo/opensim/simbody.py", line 10, in <module>
    from . import _simbody
ImportError: /home/eddlai/miniconda3/lib/libstdc++.so.6: version `GLIBCXX_3.4.32' not found (required by /home/eddlai/opensim-workspace/opensim-core-build/Bindings/Python/RelWithDebInfo/opensim/_simbody.so)
```
conda 降級
並且conda install libgcc-ng=9.3.0
需要GLIBCXX_3.4.**32**，如果沒有改變swig中就不會有這個問題
1. 嘗試在終端中使用(failed)
```
export PATH=~/opensim-workspace/Python-3.6.9-source/Python-3.6.9:$PATH
export LD_LIBRARY_PATH=~/opensim-workspace/opensim-core-dependencies-install/simbody/lib:$LD_LIBRARY_PATH
```

2. 嘗試在.sh中加入(failed)
```
# 強制使用腳本下載的 Python 和 Simbody
export PATH=~/opensim-workspace/Python-3.6.9-source/Python-3.6.9/bin:$PATH
export LD_LIBRARY_PATH=~/opensim-workspace/opensim-core-dependencies-install/simbody/lib:$LD_LIBRARY_PATH

# 確保不使用 Conda 的 Python
unset PYTHONHOME
unset PYTHONPATH
```
3. 嘗試繼續使用conda，並修正問題
```
conda install -c conda-forge gcc=12 
```
沒有解決==但應該有下載阿==
4. 關閉conda bash自動開啟，`~/.bashrc`

注意.sh的使用方法，不能這樣debug