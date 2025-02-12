兩個問題，為什麼沒有用GPU，以及解決以下gym版本更新造成的問題，(D:\conda_envs\scone) PS D:\depRL> python -m deprl.main .\experiments\hyfydy\scone_run_h0918.yaml

MyoSuite:> Registering Myo Envs

No CUDA or MPS detected, running on CPU

{'tonic': {'after_training': '', 'header': 'import deprl, gym, sconegym', 'agent': 'deprl.custom_agents.dep_factory(3, deprl.custom_mpo_torch.TunedMPO())(replay=deprl.replays.buffers.Buffer(return_steps=1, batch_size=256, steps_between_batches=1000, batch_iterations=30, steps_before_batches=1e6))', 'before_training': '', 'checkpoint': 'last', 'environment': "deprl.environments.Gym('sconerun_h0918-v1', scaled_actions=False)", 'full_save': 1, 'name': 'sconerun_h0918_v1', 'resume': True, 'seed': 0, 'parallel': 20, 'sequential': 10, 'test_environment': None, 'trainer': 'deprl.custom_trainer.Trainer(steps=int(5e8), epoch_steps=int(2e5), save_steps=int(1e6))'}, 'working_dir': 'IGNORED_FOR_HYFYDY', 'env_args': {'clip_actions': False, 'grf_coeff': -0.07281, 'joint_limit_coeff': -0.1307, 'nmuscle_coeff': -1.57929, 'smooth_coeff': -0.097, 'self_contact_coeff': -10.0, 'vel_coeff': 10.0, 'step_size': 0.025, 'run': True, 'init_activations_mean': 0.01, 'init_activations_std': 0}, 'DEP': {'bias_rate': 0.002, 'buffer_size': 200, 'intervention_length': 8, 'intervention_proba': 0.00371, 'kappa': 1000, 'normalization': 'independent', 'q_norm_selector': 'l2', 'regularization': 32, 's4avg': 2, 'sensor_delay': 1, 'tau': 40, 'test_episode_every': 3, 'time_dist': 5, 'with_learning': True}}

22:48:56 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:48:56 Successfully initialized OpenSim4 version 4.4

22:48:56 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:48:56 Successfully initialized Hyfydy version 1.8.3.1183

22:48:56 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

Stochastic Switch-DEP. Paper version.

Found earlier run, continuing training: Path is: C:/SCONE/results\sconerun_h0918_v1

Script file saved to C:\SCONE\results\sconerun_h0918_v1\250122.224810.H0918v2j\script.py

Config file saved to C:\SCONE\results\sconerun_h0918_v1\250122.224810.H0918v2j\config.yaml

Checkpoint path is not valid: C:\SCONE\results\sconerun_h0918_v1\250122.224810.H0918v2j\checkpoints

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

MyoSuite:> Registering Myo Envs

22:49:04 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:04 Successfully initialized OpenSim4 version 4.4

22:49:04 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:04 Successfully initialized Hyfydy version 1.8.3.1183

22:49:04 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:04 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:04 Successfully initialized OpenSim4 version 4.4

22:49:04 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:04 Successfully initialized Hyfydy version 1.8.3.1183

22:49:04 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 22:49:05 Successfully initialized OpenSim4 version 4.4

Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:05 22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 22:49:05 Successfully initialized OpenSim4 version 4.4

Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

Successfully initialized OpenSim3 version 3.3-2021-01-28D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim4 version 4.4

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

Successfully initialized OpenSim4 version 4.4D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 22:49:05 D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

Successfully initialized OpenSim4 version 4.4

Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

Successfully initialized Hyfydy version 1.8.3.1183

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:05 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:05 Successfully initialized OpenSim4 version 4.4

22:49:05 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:06 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:06 Successfully initialized OpenSim4 version 4.4

22:49:06 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

22:49:06 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:06 Successfully initialized OpenSim4 version 4.4

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:06 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

22:49:06 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:06 22:49:06 Successfully initialized OpenSim4 version 4.4

Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:06 Successfully initialized OpenSim4 version 4.4

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

22:49:06 22:49:06 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zmlLoaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:06 22:49:06 Successfully initialized Hyfydy version 1.8.3.1183

Successfully initialized Hyfydy version 1.8.3.1183

22:49:06 22:49:06 Successfully initialized Hyfydy version 1.8.3.1183 Double PrecisionSuccessfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

22:49:06 Successfully initialized OpenSim3 version 3.3-2021-01-28

22:49:06 Successfully initialized OpenSim4 version 4.4

22:49:06 Loaded settings from C:/Users/ed2di/AppData/Local/SCONE/scone-settings.zml

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183

22:49:06 Successfully initialized Hyfydy version 1.8.3.1183 Double Precision

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_episode_steps to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_episode_steps` for environment variables or `env.get_attr('max_episode_steps')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.horizon to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.horizon` for environment variables or `env.get_attr('horizon')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.name to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.name` for environment variables or `env.get_attr('name')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.max_muscle to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.max_muscle` for environment variables or `env.get_attr('max_muscle')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.time to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.time` for environment variables or `env.get_attr('time')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

D:\conda_envs\scone\lib\site-packages\gymnasium\core.py:297: UserWarning: WARN: env.step_size to get variables from other wrappers is deprecated and will be removed in v1.0, to get this variable you can do `env.unwrapped.step_size` for environment variables or `env.get_attr('step_size')` that will search the reminding wrappers.

logger.warn(

trainer failed. Exception: could not broadcast input array from shape (10,121) into shape (10,2,121)

File "D:\depRL\deprl\main.py", line 118, in train

trainer.run(config, **time_dict)

File "D:\depRL\deprl\custom_trainer.py", line 77, in run

observations, muscle_states, info = self.environment.step(actions)

File "D:\depRL\deprl\custom_distributed.py", line 234, in step

self.next_observations_list[index] = infos["observations"]

Process SpawnProcess-2: