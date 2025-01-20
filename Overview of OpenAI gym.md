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