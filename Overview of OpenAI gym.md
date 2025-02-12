# Gym basic
需要用到swig來跟Env底層的C端口做互動
- [`TimeLimit`](https://gymnasium.farama.org/api/wrappers/misc_wrappers/#gymnasium.wrappers.TimeLimit "gymnasium.wrappers.TimeLimit")
- [`OrderEnforcing`](https://gymnasium.farama.org/api/wrappers/misc_wrappers/#gymnasium.wrappers.OrderEnforcing "gymnasium.wrappers.OrderEnforcing")
- [`PassiveEnvChecker`](https://gymnasium.farama.org/api/wrappers/misc_wrappers/#gymnasium.wrappers.PassiveEnvChecker "gymnasium.wrappers.PassiveEnvChecker").

TimeAwareObservation
`pprint_registry()`
環境維度可能跟Env資訊相關
- `_get_obs` 得到環境狀態，統一format
- `_get_info` 可以進行一些運算

gym.register(
    id="`namespcae/mandatory_name-version`",
    entry_point=GridWorldEnv,
)
多個環境：gymnasium.make_vec()
wrapper對現有結構進行新的封裝(不影響舊的)

錄製：`env = RecordVideo(env, video_folder="cartpole-agent", name_prefix="training",episode_trigger=lambda x: x % training_period == 0)`

`env = gym.make("OldV21Env-v0", apply_api_compatibility=True)`解決相容問題
([`gymnasium.utils.step_api_compatibility.convert_to_terminated_truncated_step_api()`](https://gymnasium.farama.org/api/utils/#gymnasium.utils.step_api_compatibility.convert_to_terminated_truncated_step_api "gymnasium.utils.step_api_compatibility.convert_to_terminated_truncated_step_api"))

0.21: 可以用env.seed(123)
0.26

Stable-Baselines3
- **`terminated=True`** 時應進行引導值回填（bootstrapping）。
- **`truncated=True`** 時則不進行回填。

---
## Environment setup
`conda install -n base -c conda-forge mamba`

```
conda config --add envs_dirs /home/eddlai/miniconda3/envs
conda config --add envs_dirs /media/eddlai/DATA/conda_envs

```
`mamba create --prefix /media/eddlai/DATA/conda_envs/simulation python=3.9`
`pip install poetry`

[[SCONE python based API and SCONE gym]]

`mamba create --prefix /media/eddlai/DATA/conda_envs/myocontrol python=3.10`
gesture detection for hand exoskeleton for my grandma's hand atrophy

`pip cache purge`
