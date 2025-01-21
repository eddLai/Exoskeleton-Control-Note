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

## Environment setup
`conda install -n base -c conda-forge mamba`

```
conda config --add envs_dirs /home/eddlai/miniconda3/envs
conda config --add envs_dirs /media/eddlai/DATA/conda_envs

```
`mamba create --prefix /media/eddlai/DATA/conda_envs/simulation python=3.9`


---
# SCONEgym
ABC庫
```
class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        """每個動物都必須實作這個方法來發出聲音"""
        pass

    def sleep(self):
        """非抽象方法，可選擇性覆蓋"""
        print("Sleeping...")
```

- Progress
	- `self.episode`：當前的 episode 編號。
	- `self.total_reward`：當前 episode 的累計獎勵。
	- `self.total_steps / self.steps`：模擬的總步數和當前 episode 的步數。
	- `self.has_reset`：是否已經重置過環境。
	- `self.init_dof_pos_std` / `self.init_dof_vel_std`：關節初始位置和速度的標準差。
	- `self.init_load`
- 
	- `self.obs_type`：觀察空間類型。
	- `self.left_leg_idxs` / `self.right_leg_idxs`：左腿和右腿的關節索引。