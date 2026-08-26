# 问题

1. g1_29dof模型站不稳

   到6月3日为止改动过哪里？

   1. unitree.py文件的usd文件路径
   2. unitree.py文件中的init_state中的joint_pos参数，替换了leg、arms的包含关节，以及具体关节的stiffness（刚度）和damping（摩擦系数）
   3. rough_env_cfg.py中的joint_deviation_arms的奖励项关节设置、joint_deviation_torso中增加了waist\_.*\_link的参数
   4. rsl_rl\_ppo\_cfg.py中的entropy\_coef，让策略的熵尽可能大
   5. 在rought\_env\_cfg.py中增加了碰撞重置的部位，防止机器人全部倒地而不再重置
   6. flat\_env\_cfg.py中修改了track_ang_vel_z_exp.weight=2.0、action_rate_l2.weight=-0.01、feet_air_time.weight=2、feet_air_time.params['threshold']=0.5

   为什么出现这样的问题：

    1. 配置奖励函数出了问题

    2. 模型转换有问题，即模型本身有问题（待确定）

       每次加载usd资产的时候都会出现Calling getBypassRenderSkelMeshProcessing for prim /World/envs/env_0/Robot/torso_link/visuals.proto_mesh_id2 that has not been populated

       或者 Calling getBypassRenderSkelMeshProcessing for prim /World/G1/right_ankle_pitch_link/visuals.proto_mesh_id0 that has not been populated

    3. 靖华提到的，环境数量的问题，通过更多的环境数量，更快、更多地去接触到更多不同的场景数据

       将flat_env_cfg.py文件中的self.scene.num_envs的值更改为了4096

       > 1. 更改环境数量过后 代价函数损失（mean value_function loss）很小，但是，奖励值以及其他损失在震荡，mean_reward奖励缓慢减小、track_lin_vel_xy_exp缓慢增长
       >    第770轮mean_reward奖励转正
       >
       > ```
       > ################################################################################
       >                       Learning iteration 210/1500                       
       > 
       >                        Computation: 13895 steps/s (collection: 6.968s, learning 0.107s)
       >              Mean action noise std: 0.92
       >           Mean value_function loss: 0.0011
       >                Mean surrogate loss: -0.0142
       >                  Mean entropy loss: 32.8413
       >                        Mean reward: -2.25
       >                Mean episode length: 435.43
       > Episode_Reward/track_lin_vel_xy_exp: 0.0342
       > Episode_Reward/track_ang_vel_z_exp: 0.0664
       >        Episode_Reward/lin_vel_z_l2: -0.0034
       >       Episode_Reward/ang_vel_xy_l2: -0.0209
       >      Episode_Reward/dof_torques_l2: -0.0012
       >          Episode_Reward/dof_acc_l2: -0.0223
       >      Episode_Reward/action_rate_l2: -0.0574
       >       Episode_Reward/feet_air_time: 0.0044
       >  Episode_Reward/undesired_contacts: -0.0000
       > Episode_Reward/flat_orientation_l2: -0.0112
       >      Episode_Reward/dof_pos_limits: -0.0003
       > Episode_Reward/termination_penalty: -0.0500
       >          Episode_Reward/feet_slide: -0.0051
       > Episode_Reward/joint_deviation_hip: -0.0047
       > Episode_Reward/joint_deviation_arms: -0.0119
       > Episode_Reward/joint_deviation_torso: -0.0308
       > Metrics/base_velocity/error_vel_xy: 0.1696
       > Metrics/base_velocity/error_vel_yaw: 0.1958
       >       Episode_Termination/time_out: 0.0000
       >   Episode_Termination/base_contact: 11.5000
       > --------------------------------------------------------------------------------
       >                    Total timesteps: 20742144
       >                     Iteration time: 7.07s
       >                       Time elapsed: 00:28:30
       >                                ETA: 02:54:15
       > 
       > ################################################################################
       > 
       > 
       >                       Learning iteration 1013/1500                      
       > 
       >                        Computation: 16473 steps/s (collection: 5.873s, learning 0.095s)
       >              Mean action noise std: 0.94
       >           Mean value_function loss: 0.0009
       >                Mean surrogate loss: -0.0098
       >                  Mean entropy loss: 27.2960
       >                        Mean reward: 1.61
       >                Mean episode length: 980.04
       > Episode_Reward/track_lin_vel_xy_exp: 0.1334
       > Episode_Reward/track_ang_vel_z_exp: 0.2873
       >        Episode_Reward/lin_vel_z_l2: -0.0064
       >       Episode_Reward/ang_vel_xy_l2: -0.0221
       >      Episode_Reward/dof_torques_l2: -0.0016
       >          Episode_Reward/dof_acc_l2: -0.0203
       >      Episode_Reward/action_rate_l2: -0.1341
       >       Episode_Reward/feet_air_time: 0.0014
       >  Episode_Reward/undesired_contacts: -0.0000
       > Episode_Reward/flat_orientation_l2: -0.0102
       >      Episode_Reward/dof_pos_limits: -0.0005
       > Episode_Reward/termination_penalty: -0.0496
       >          Episode_Reward/feet_slide: -0.0092
       > Episode_Reward/joint_deviation_hip: -0.0070
       > Episode_Reward/joint_deviation_arms: -0.0275
       > Episode_Reward/joint_deviation_torso: -0.0523
       > Metrics/base_velocity/error_vel_xy: 0.2204
       > Metrics/base_velocity/error_vel_yaw: 0.1845
       >       Episode_Termination/time_out: 0.0417
       >   Episode_Termination/base_contact: 3.5417
       > --------------------------------------------------------------------------------
       >                    Total timesteps: 99680256
       >                     Iteration time: 5.97s
       >                       Time elapsed: 01:54:52
       >                       
       >                       
       >                       
       >                       
       >                                   
       >                       ################################################################################
       >                       Learning iteration 1499/1500                      
       > 
       >                        Computation: 13886 steps/s (collection: 6.982s, learning 0.097s)
       >              Mean action noise std: 0.98
       >           Mean value_function loss: 0.0013
       >                Mean surrogate loss: -0.0106
       >                  Mean entropy loss: 28.5486
       >                        Mean reward: 2.55
       >                Mean episode length: 1351.11
       > Episode_Reward/track_lin_vel_xy_exp: 0.2217
       > Episode_Reward/track_ang_vel_z_exp: 0.3999
       >        Episode_Reward/lin_vel_z_l2: -0.0130
       >       Episode_Reward/ang_vel_xy_l2: -0.0331
       >      Episode_Reward/dof_torques_l2: -0.0027
       >          Episode_Reward/dof_acc_l2: -0.0322
       >      Episode_Reward/action_rate_l2: -0.2038
       >       Episode_Reward/feet_air_time: 0.0026
       >  Episode_Reward/undesired_contacts: -0.0000
       > Episode_Reward/flat_orientation_l2: -0.0114
       >      Episode_Reward/dof_pos_limits: -0.0022
       > Episode_Reward/termination_penalty: -0.0500
       >          Episode_Reward/feet_slide: -0.0143
       > Episode_Reward/joint_deviation_hip: -0.0112
       > Episode_Reward/joint_deviation_arms: -0.0374
       > Episode_Reward/joint_deviation_torso: -0.0767
       > Metrics/base_velocity/error_vel_xy: 0.2523
       > Metrics/base_velocity/error_vel_yaw: 0.2701
       >       Episode_Termination/time_out: 0.0000
       >   Episode_Termination/base_contact: 3.7917
       > --------------------------------------------------------------------------------
       >                    Total timesteps: 147456000
       >                     Iteration time: 7.08s
       >                       Time elapsed: 02:49:54
       >                                ETA: 00:00:06
       > ```
       >
       > 发现训练了一千多轮track_ang_vel_z_exp.weight和track_lin_vel_xy_exp.weight都是很低

       > 2. 修改flat_env_cfg.py中的feet_air_time=1.5, threshold=0.4，
       >    #修改rsl_rl_ppo_cfg.py中的训练轮次为5000
       >    修改rough_env_cfg.py中的joint_deviation_arms的惩罚值为-0.2
       >    修改flat_env_cfg.py中的track_ang_vel_z_exp.weight=3.0
       >    修改rough_env_cfg.py中的track_lin_vel_xy_exp=3.0
       >
       >    ```
       >    +-------+-----------------------+--------+
       >    | Index | Name                  | Weight |
       >    +-------+-----------------------+--------+
       >    |   0   | track_lin_vel_xy_exp  |    3.0 |
       >    |   1   | track_ang_vel_z_exp   |    3.0 |
       >    |   2   | lin_vel_z_l2          |   -2.0 |
       >    |   3   | ang_vel_xy_l2         |  -0.05 |
       >    |   4   | dof_torques_l2        | -2e-06 |
       >    |   5   | dof_acc_l2            | -1e-07 |
       >    |   6   | action_rate_l2        |  -0.01 |
       >    |   7   | feet_air_time         |    1.5 |
       >    |   8   | undesired_contacts    |   -1.0 |
       >    |   9   | flat_orientation_l2   |   -1.0 |
       >    |   10  | dof_pos_limits        |   -1.0 |
       >    |   11  | termination_penalty   | -200.0 |
       >    |   12  | feet_slide            |   -0.1 |
       >    |   13  | joint_deviation_hip   |   -0.2 |
       >    |   14  | joint_deviation_arms  |   -0.2 |
       >    |   15  | joint_deviation_torso |   -0.1 |
       >    +-------+-----------------------+--------+
       >    
       >    
       >    ################################################################################
       >                          Learning iteration 150/5000                       
       >    
       >                           Computation: 13987 steps/s (collection: 6.915s, learning 0.113s)
       >                 Mean action noise std: 1.03
       >              Mean value_function loss: 0.0031
       >                   Mean surrogate loss: -0.0127
       >                     Mean entropy loss: 37.2584
       >                           Mean reward: -0.47
       >                   Mean episode length: 298.83
       >    Episode_Reward/track_lin_vel_xy_exp: 0.1482
       >    Episode_Reward/track_ang_vel_z_exp: 0.0458
       >           Episode_Reward/lin_vel_z_l2: -0.0074
       >          Episode_Reward/ang_vel_xy_l2: -0.0207
       >         Episode_Reward/dof_torques_l2: -0.0012
       >             Episode_Reward/dof_acc_l2: -0.0248
       >         Episode_Reward/action_rate_l2: -0.0503
       >          Episode_Reward/feet_air_time: 0.0009
       >     Episode_Reward/undesired_contacts: -0.0000
       >    Episode_Reward/flat_orientation_l2: -0.0091
       >         Episode_Reward/dof_pos_limits: -0.0004
       >    Episode_Reward/termination_penalty: -0.0500
       >             Episode_Reward/feet_slide: -0.0041
       >    Episode_Reward/joint_deviation_hip: -0.0059
       >    Episode_Reward/joint_deviation_arms: -0.0191
       >    Episode_Reward/joint_deviation_torso: -0.0288
       >    Metrics/base_velocity/error_vel_xy: 0.0648
       >    Metrics/base_velocity/error_vel_yaw: 0.2106
       >          Episode_Termination/time_out: 0.0000
       >      Episode_Termination/base_contact: 13.7500
       >    --------------------------------------------------------------------------------
       >                       Total timesteps: 14843904
       >                        Iteration time: 7.03s
       >                          Time elapsed: 00:18:10
       >                                   ETA: 09:43:34
       >    
       >    ################################################################################
       >    ```
       >
       >    会有好转，但是抬腿积极性依旧不高

       >  3. 在上一步的基础上将feet_air_time=2.25
       >
       >     	1. 754轮转正
       >
       >     ```
       >     +----------------------------------------+
       >     |          Active Reward Terms           |
       >     +-------+-----------------------+--------+
       >     | Index | Name                  | Weight |
       >     +-------+-----------------------+--------+
       >     |   0   | track_lin_vel_xy_exp  |    3.0 |
       >     |   1   | track_ang_vel_z_exp   |    3.0 |
       >     |   2   | lin_vel_z_l2          |   -2.0 |
       >     |   3   | ang_vel_xy_l2         |  -0.05 |
       >     |   4   | dof_torques_l2        | -2e-06 |
       >     |   5   | dof_acc_l2            | -1e-07 |
       >     |   6   | action_rate_l2        |  -0.01 |
       >     |   7   | feet_air_time         |   2.25 |
       >     |   8   | undesired_contacts    |   -1.0 |
       >     |   9   | flat_orientation_l2   |   -1.0 |
       >     |   10  | dof_pos_limits        |   -1.0 |
       >     |   11  | termination_penalty   | -200.0 |
       >     |   12  | feet_slide            |   -0.1 |
       >     |   13  | joint_deviation_hip   |   -0.2 |
       >     |   14  | joint_deviation_arms  |   -0.2 |
       >     |   15  | joint_deviation_torso |   -0.1 |
       >     +-------+-----------------------+--------+
       >     
       >     
       >     
       >     ################################################################################
       >                            Learning iteration 20/5000                       
       >     
       >                            Computation: 14283 steps/s (collection: 6.796s, learning 0.086s)
       >                  Mean action noise std: 0.94
       >               Mean value_function loss: 0.0028
       >                    Mean surrogate loss: -0.0152
       >                      Mean entropy loss: 38.8345
       >                            Mean reward: -2.91
       >                    Mean episode length: 176.56
       >     Episode_Reward/track_lin_vel_xy_exp: 0.0565
       >     Episode_Reward/track_ang_vel_z_exp: 0.0111
       >            Episode_Reward/lin_vel_z_l2: -0.0052
       >           Episode_Reward/ang_vel_xy_l2: -0.0467
       >          Episode_Reward/dof_torques_l2: -0.0019
       >              Episode_Reward/dof_acc_l2: -0.0572
       >          Episode_Reward/action_rate_l2: -0.0240
       >           Episode_Reward/feet_air_time: 0.0005
       >      Episode_Reward/undesired_contacts: -0.0000
       >     Episode_Reward/flat_orientation_l2: -0.0089
       >          Episode_Reward/dof_pos_limits: -0.0001
       >     Episode_Reward/termination_penalty: -0.0500
       >              Episode_Reward/feet_slide: -0.0042
       >     Episode_Reward/joint_deviation_hip: -0.0035
       >     Episode_Reward/joint_deviation_arms: -0.0053
       >     Episode_Reward/joint_deviation_torso: -0.0098
       >     Metrics/base_velocity/error_vel_xy: 0.0612
       >     Metrics/base_velocity/error_vel_yaw: 0.3074
       >           Episode_Termination/time_out: 0.0000
       >       Episode_Termination/base_contact: 56.7083
       >     --------------------------------------------------------------------------------
       >                        Total timesteps: 2064384
       >                         Iteration time: 6.88s
       >                           Time elapsed: 00:02:28
       >                                    ETA: 09:48:51
       >                                    
       >                                    
       >     ################################################################################
       >                           Learning iteration 980/5000                       
       >     
       >                            Computation: 14836 steps/s (collection: 6.533s, learning 0.093s)
       >                  Mean action noise std: 1.22
       >               Mean value_function loss: 0.0031
       >                    Mean surrogate loss: -0.0118
       >                      Mean entropy loss: 37.3848
       >                            Mean reward: 0.53
       >                    Mean episode length: 369.28
       >     Episode_Reward/track_lin_vel_xy_exp: 0.1867
       >     Episode_Reward/track_ang_vel_z_exp: 0.1086
       >            Episode_Reward/lin_vel_z_l2: -0.0090
       >           Episode_Reward/ang_vel_xy_l2: -0.0157
       >          Episode_Reward/dof_torques_l2: -0.0012
       >              Episode_Reward/dof_acc_l2: -0.0120
       >          Episode_Reward/action_rate_l2: -0.0819
       >           Episode_Reward/feet_air_time: 0.0037
       >      Episode_Reward/undesired_contacts: -0.0000
       >     Episode_Reward/flat_orientation_l2: -0.0160
       >          Episode_Reward/dof_pos_limits: -0.0023
       >     Episode_Reward/termination_penalty: -0.0500
       >              Episode_Reward/feet_slide: -0.0039
       >     Episode_Reward/joint_deviation_hip: -0.0073
       >     Episode_Reward/joint_deviation_arms: -0.0353
       >     Episode_Reward/joint_deviation_torso: -0.0486
       >     Metrics/base_velocity/error_vel_xy: 0.0774
       >     Metrics/base_velocity/error_vel_yaw: 0.1392
       >           Episode_Termination/time_out: 0.0000
       >       Episode_Termination/base_contact: 10.5417
       >     --------------------------------------------------------------------------------
       >                        Total timesteps: 96436224
       >                         Iteration time: 6.63s
       >                           Time elapsed: 01:46:41
       >                                    ETA: 07:17:13                               
       >                                    
       >      
       >     ```
       >
       >     依旧不理想，且熵值并没有减小

       > 4. 修改flat_env_cfg.py中的track_ang_vel_z_exp.weight=3.0
       >    修改rough_env_cfg.py中的track_lin_vel_xy_exp=3.0
       >    修改flat_env_cfg.py中的feet_air_time=1.5, threshold=0.4
       >
       >    ```
       >    ################################################################################
       >                          Learning iteration 4999/5000                      
       >                         
       >                           Computation: 14917 steps/s (collection: 6.466s, learning 0.123s)
       >                 Mean action noise std: 1.11
       >              Mean value_function loss: 0.0019
       >                   Mean surrogate loss: -0.0050
       >                     Mean entropy loss: 33.9105
       >                           Mean reward: 14.04
       >                   Mean episode length: 2332.05
       >    Episode_Reward/track_lin_vel_xy_exp: 0.7634
       >    Episode_Reward/track_ang_vel_z_exp: 0.5466
       >           Episode_Reward/lin_vel_z_l2: -0.0163
       >          Episode_Reward/ang_vel_xy_l2: -0.0237
       >         Episode_Reward/dof_torques_l2: -0.0068
       >             Episode_Reward/dof_acc_l2: -0.0416
       >         Episode_Reward/action_rate_l2: -0.3556
       >          Episode_Reward/feet_air_time: 0.0145
       >     Episode_Reward/undesired_contacts: -0.0001
       >    Episode_Reward/flat_orientation_l2: -0.0162
       >         Episode_Reward/dof_pos_limits: -0.0031
       >    Episode_Reward/termination_penalty: -0.0403
       >             Episode_Reward/feet_slide: -0.0208
       >    Episode_Reward/joint_deviation_hip: -0.0165
       >    Episode_Reward/joint_deviation_arms: -0.0886
       >    Episode_Reward/joint_deviation_torso: -0.1610
       >    Metrics/base_velocity/error_vel_xy: 0.3027
       >    Metrics/base_velocity/error_vel_yaw: 0.4400
       >          Episode_Termination/time_out: 0.4583
       >      Episode_Termination/base_contact: 1.6250
       >    --------------------------------------------------------------------------------
       >                       Total timesteps: 491520000
       >                        Iteration time: 6.59s
       >                          Time elapsed: 09:31:28
       >                                   ETA: 00:00:06
       >    ```
       >
       > 5. 



方法论：如何让别人一看我这个文档就能够学会这整个unitree G1从仿真搭建、到最后训练、部署到实体上面这个流程呢

具体的sim2real的实机部署计划

代码上传到gitlab

12dof训练









# 6月9日

> 1. 将网络的层数从512， 256， 128调整为256，128， 128 
>    将track_lin_vel_xy_exp调整为2.0
>        track_ang_vel_z_exp调整为2.0
>        feet_air_time 调整为2.0
>
>    85轮转正
>
> 2. 将track_lin_vel_xy_exp调整为1.0
>        track_ang_vel_z_exp调整为1.0
>        feet_air_time 不变
>    427轮回正
>
>    ```
>    ################################################################################
>                          Learning iteration 427/1500                       
>          
>                           Computation: 20291 steps/s (collection: 4.730s, learning 0.114s)
>                 Mean action noise std: 0.60
>              Mean value_function loss: 0.0009
>                   Mean surrogate loss: -0.0071
>                     Mean entropy loss: 8.8894
>                           Mean reward: 0.20
>                   Mean episode length: 414.27
>    Episode_Reward/track_lin_vel_xy_exp: 0.0507
>    Episode_Reward/track_ang_vel_z_exp: 0.0721
>           Episode_Reward/lin_vel_z_l2: -0.0037
>          Episode_Reward/ang_vel_xy_l2: -0.0067
>         Episode_Reward/dof_torques_l2: -0.0015
>             Episode_Reward/dof_acc_l2: -0.0061
>         Episode_Reward/action_rate_l2: -0.0114
>          Episode_Reward/feet_air_time: 0.0023
>     Episode_Reward/undesired_contacts: -0.0000
>    Episode_Reward/flat_orientation_l2: -0.0082
>         Episode_Reward/dof_pos_limits: -0.0023
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0031
>    Episode_Reward/joint_deviation_hip: -0.0076
>    Episode_Reward/joint_deviation_torso: -0.0230
>    Metrics/base_velocity/error_vel_xy: 0.1194
>    Metrics/base_velocity/error_vel_yaw: 0.0549
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 11.3333
>    --------------------------------------------------------------------------------
>                       Total timesteps: 42074112
>                        Iteration time: 4.84s
>                          Time elapsed: 00:35:36
>                                   ETA: 01:29:16
>    ```
>
> 3. 将track_lin_vel_xy_exp调整为1.0
>        track_ang_vel_z_exp调整为1.0
>        feet_air_time 调整为1.0
>
>    ```
>          
>    ```
>
>    



# 6月16日

# 

> 1. 将网络的层数从256， 128， 128调整为256，256， 128 
>    将track_lin_vel_xy_exp调整为1.0
>        track_ang_vel_z_exp调整为1.0
>        feet_air_time 调整为0.75
>        lin_vel_z_l2 调整为-0.2
>
>    ```
>    ################################################################################
>                          Learning iteration 287/1500                       
>       
>                           Computation: 22858 steps/s (collection: 4.206s, learning 0.094s)
>                 Mean action noise std: 0.63
>              Mean value_function loss: 0.0012
>                   Mean surrogate loss: -0.0079
>                     Mean entropy loss: 9.6247
>                           Mean reward: 0.03
>                   Mean episode length: 454.72
>    Episode_Reward/track_lin_vel_xy_exp: 0.0442
>    Episode_Reward/track_ang_vel_z_exp: 0.0792
>           Episode_Reward/lin_vel_z_l2: -0.0011
>          Episode_Reward/ang_vel_xy_l2: -0.0041
>         Episode_Reward/dof_torques_l2: -0.0015
>             Episode_Reward/dof_acc_l2: -0.0117
>         Episode_Reward/action_rate_l2: -0.0149
>          Episode_Reward/feet_air_time: 0.0010
>     Episode_Reward/undesired_contacts: -0.0001
>    Episode_Reward/flat_orientation_l2: -0.0109
>         Episode_Reward/dof_pos_limits: -0.0003
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0043
>    Episode_Reward/joint_deviation_hip: -0.0048
>    Episode_Reward/joint_deviation_torso: -0.0184
>    Metrics/base_velocity/error_vel_xy: 0.1549
>    Metrics/base_velocity/error_vel_yaw: 0.0748
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 7.1667
>    --------------------------------------------------------------------------------
>                       Total timesteps: 28311552
>                        Iteration time: 4.30s
>                          Time elapsed: 00:21:24
>                                   ETA: 01:30:08
>       
>    ################################################################################
>       
>                          Learning iteration 892/1500                       
>       
>                           Computation: 24007 steps/s (collection: 4.005s, learning 0.090s)
>                 Mean action noise std: 0.57
>              Mean value_function loss: 0.0010
>                   Mean surrogate loss: -0.0084
>                     Mean entropy loss: 7.6300
>                           Mean reward: 1.52
>                   Mean episode length: 622.47
>    Episode_Reward/track_lin_vel_xy_exp: 0.0868
>    Episode_Reward/track_ang_vel_z_exp: 0.1236
>           Episode_Reward/lin_vel_z_l2: -0.0009
>          Episode_Reward/ang_vel_xy_l2: -0.0043
>         Episode_Reward/dof_torques_l2: -0.0019
>             Episode_Reward/dof_acc_l2: -0.0111
>         Episode_Reward/action_rate_l2: -0.0186
>          Episode_Reward/feet_air_time: 0.0012
>     Episode_Reward/undesired_contacts: -0.0001
>    Episode_Reward/flat_orientation_l2: -0.0117
>         Episode_Reward/dof_pos_limits: -0.0006
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0055
>    Episode_Reward/joint_deviation_hip: -0.0042
>    Episode_Reward/joint_deviation_torso: -0.0175
>    Metrics/base_velocity/error_vel_xy: 0.1678
>    Metrics/base_velocity/error_vel_yaw: 0.0784
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 5.2917
>    --------------------------------------------------------------------------------
>                       Total timesteps: 87785472
>                        Iteration time: 4.09s
>                          Time elapsed: 01:06:11
>                                   ETA: 00:45:03
>    
>    
>    ```
>
>    287轮转正，且愿意冻腿，转弯愿意冻腿，但是直行不愿意冻腿，并且是先调整了重心，然后再冻腿进行移动
>    892轮track_lin_vel_xy/z_exp稳定0.1，此时瘸腿走
>    1000轮track_lin_vel_xy/z_exp稳定0.2,跨步不够大
>
>    ```
>    ################################################################################
>                          Learning iteration 1388/1500                      
>    
>                           Computation: 21858 steps/s (collection: 4.400s, learning 0.098s)
>                 Mean action noise std: 0.61
>              Mean value_function loss: 0.0011
>                   Mean surrogate loss: -0.0088
>                     Mean entropy loss: 8.5098
>                           Mean reward: 11.71
>                   Mean episode length: 2314.33
>    Episode_Reward/track_lin_vel_xy_exp: 0.4951
>    Episode_Reward/track_ang_vel_z_exp: 0.4632
>           Episode_Reward/lin_vel_z_l2: -0.0045
>          Episode_Reward/ang_vel_xy_l2: -0.0145
>         Episode_Reward/dof_torques_l2: -0.0111
>             Episode_Reward/dof_acc_l2: -0.0535
>         Episode_Reward/action_rate_l2: -0.0854
>          Episode_Reward/feet_air_time: 0.0109
>     Episode_Reward/undesired_contacts: -0.0001
>    Episode_Reward/flat_orientation_l2: -0.0166
>         Episode_Reward/dof_pos_limits: -0.0043
>    Episode_Reward/termination_penalty: -0.0383
>             Episode_Reward/feet_slide: -0.0238
>    Episode_Reward/joint_deviation_hip: -0.0223
>    Episode_Reward/joint_deviation_torso: -0.0789
>    Metrics/base_velocity/error_vel_xy: 0.2914
>    Metrics/base_velocity/error_vel_yaw: 0.3077
>          Episode_Termination/time_out: 0.6250
>      Episode_Termination/base_contact: 1.8750
>    --------------------------------------------------------------------------------
>                       Total timesteps: 136544256
>                        Iteration time: 4.50s
>                          Time elapsed: 01:42:51
>                                   ETA: 00:08:17
>    
>    ################################################################################
>                          Learning iteration 1389/1500                      
>    
>                           Computation: 21238 steps/s (collection: 4.537s, learning 0.092s)
>                 Mean action noise std: 0.61
>              Mean value_function loss: 0.0011
>                   Mean surrogate loss: -0.0093
>                     Mean entropy loss: 8.5080
>                           Mean reward: 11.44
>                   Mean episode length: 2273.54
>    Episode_Reward/track_lin_vel_xy_exp: 0.4877
>    Episode_Reward/track_ang_vel_z_exp: 0.4510
>           Episode_Reward/lin_vel_z_l2: -0.0043
>          Episode_Reward/ang_vel_xy_l2: -0.0141
>         Episode_Reward/dof_torques_l2: -0.0107
>             Episode_Reward/dof_acc_l2: -0.0516
>         Episode_Reward/action_rate_l2: -0.0830
>          Episode_Reward/feet_air_time: 0.0110
>     Episode_Reward/undesired_contacts: -0.0001
>    Episode_Reward/flat_orientation_l2: -0.0152
>         Episode_Reward/dof_pos_limits: -0.0036
>    Episode_Reward/termination_penalty: -0.0355
>             Episode_Reward/feet_slide: -0.0228
>    Episode_Reward/joint_deviation_hip: -0.0206
>    Episode_Reward/joint_deviation_torso: -0.0744
>    Metrics/base_velocity/error_vel_xy: 0.2699
>    Metrics/base_velocity/error_vel_yaw: 0.2967
>          Episode_Termination/time_out: 0.8333
>      Episode_Termination/base_contact: 1.7917
>    --------------------------------------------------------------------------------
>                       Total timesteps: 136642560
>                        Iteration time: 4.63s
>                          Time elapsed: 01:42:55
>                                   ETA: 00:08:13
>    ```
>
>    1389轮稳定track_lin_vel_xy/z_exp=0.4, 但左腿依旧不过右腿，且有僵尸跳的痕迹
>
>    ```
>    ################################################################################
>                          Learning iteration 1499/1500                      
>    
>                           Computation: 21325 steps/s (collection: 4.500s, learning 0.110s)
>                 Mean action noise std: 0.60
>              Mean value_function loss: 0.0010
>                   Mean surrogate loss: -0.0076
>                     Mean entropy loss: 8.2650
>                           Mean reward: 12.75
>                   Mean episode length: 2458.41
>    Episode_Reward/track_lin_vel_xy_exp: 0.5491
>    Episode_Reward/track_ang_vel_z_exp: 0.5219
>           Episode_Reward/lin_vel_z_l2: -0.0042
>          Episode_Reward/ang_vel_xy_l2: -0.0160
>         Episode_Reward/dof_torques_l2: -0.0123
>             Episode_Reward/dof_acc_l2: -0.0589
>         Episode_Reward/action_rate_l2: -0.0945
>          Episode_Reward/feet_air_time: 0.0125
>     Episode_Reward/undesired_contacts: -0.0002
>    Episode_Reward/flat_orientation_l2: -0.0166
>         Episode_Reward/dof_pos_limits: -0.0033
>    Episode_Reward/termination_penalty: -0.0309
>             Episode_Reward/feet_slide: -0.0266
>    Episode_Reward/joint_deviation_hip: -0.0194
>    Episode_Reward/joint_deviation_torso: -0.0747
>    Metrics/base_velocity/error_vel_xy: 0.3249
>    Metrics/base_velocity/error_vel_yaw: 0.3384
>          Episode_Termination/time_out: 0.7083
>      Episode_Termination/base_contact: 1.2500
>    --------------------------------------------------------------------------------
>                       Total timesteps: 147456000
>                        Iteration time: 4.61s
>                          Time elapsed: 01:51:00
>                                   ETA: 00:00:04
>    ```
>
>    
>

>
>
>1. 将网络的层数从256，256， 128调整为 256， 128， 128
>     将track_lin_val_z_exp为0.5
>
>   ```
>   ################################################################################
>                          Learning iteration 38/3000                       
>   
>                          Computation: 21544 steps/s (collection: 4.465s, learning 0.098s)
>                Mean action noise std: 0.81
>             Mean value_function loss: 0.0006
>                  Mean surrogate loss: -0.0069
>                    Mean entropy loss: 14.2885
>                          Mean reward: -1.68
>                  Mean episode length: 236.83
>   Episode_Reward/track_lin_vel_xy_exp: 0.0238
>   Episode_Reward/track_ang_vel_z_exp: 0.0079
>          Episode_Reward/lin_vel_z_l2: -0.0014
>         Episode_Reward/ang_vel_xy_l2: -0.0046
>        Episode_Reward/dof_torques_l2: -0.0020
>            Episode_Reward/dof_acc_l2: -0.0200
>        Episode_Reward/action_rate_l2: -0.0105
>         Episode_Reward/feet_air_time: 0.0003
>    Episode_Reward/undesired_contacts: -0.0001
>   Episode_Reward/flat_orientation_l2: -0.0101
>        Episode_Reward/dof_pos_limits: -0.0001
>   Episode_Reward/termination_penalty: -0.0500
>            Episode_Reward/feet_slide: -0.0041
>   Episode_Reward/joint_deviation_hip: -0.0023
>   Episode_Reward/joint_deviation_torso: -0.0105
>   Metrics/base_velocity/error_vel_xy: 0.0805
>   Metrics/base_velocity/error_vel_yaw: 0.1222
>         Episode_Termination/time_out: 0.0000
>     Episode_Termination/base_contact: 31.1667
>   --------------------------------------------------------------------------------
>                      Total timesteps: 3833856
>                       Iteration time: 4.56s
>                         Time elapsed: 00:02:58
>                                  ETA: 03:46:05
>   ```
>



# 6月18日

解决瘸腿走路问题

> 1. 将rough_env_cfg_G1_12dof.py文件中的dof_torques_l2相关的关节改为所有.*
>
>    ```
>    ################################################################################
>                           Learning iteration 1/3000                        
>    
>                           Computation: 17992 steps/s (collection: 5.338s, learning 0.126s)
>                 Mean action noise std: 1.00
>              Mean value_function loss: 0.0048
>                   Mean surrogate loss: -0.0039
>                     Mean entropy loss: 17.0483
>                           Mean reward: -0.12
>                   Mean episode length: 25.56
>    Episode_Reward/track_lin_vel_xy_exp: 0.0035
>    Episode_Reward/track_ang_vel_z_exp: 0.0019
>           Episode_Reward/lin_vel_z_l2: -0.0001
>          Episode_Reward/ang_vel_xy_l2: -0.0013
>         Episode_Reward/dof_torques_l2: -0.0006
>             Episode_Reward/dof_acc_l2: -0.0075
>         Episode_Reward/action_rate_l2: -0.0023
>          Episode_Reward/feet_air_time: 0.0000
>     Episode_Reward/undesired_contacts: 0.0000
>    Episode_Reward/flat_orientation_l2: -0.0000
>         Episode_Reward/dof_pos_limits: -0.0000
>    Episode_Reward/termination_penalty: 0.0000
>             Episode_Reward/feet_slide: -0.0008
>    Episode_Reward/joint_deviation_hip: -0.0003
>    Episode_Reward/joint_deviation_torso: -0.0009
>    Metrics/base_velocity/error_vel_xy: 0.0095
>    Metrics/base_velocity/error_vel_yaw: 0.0230
>          Episode_Termination/time_out: 1.5833
>      Episode_Termination/base_contact: 0.0000
>    --------------------------------------------------------------------------------
>                       Total timesteps: 196608
>                        Iteration time: 5.46s
>                          Time elapsed: 00:00:19
>                                   ETA: 08:16:55
>                                   
>                                   
>                                   
>                                   
>                                   
>    ################################################################################
>                          Learning iteration 122/3000                       
>    
>                           Computation: 19377 steps/s (collection: 4.989s, learning 0.084s)
>                 Mean action noise std: 0.69
>              Mean value_function loss: 0.0012
>                   Mean surrogate loss: -0.0085
>                     Mean entropy loss: 11.6353
>                           Mean reward: -1.07
>                   Mean episode length: 371.15
>    Episode_Reward/track_lin_vel_xy_exp: 0.0322
>    Episode_Reward/track_ang_vel_z_exp: 0.0525
>           Episode_Reward/lin_vel_z_l2: -0.0015
>          Episode_Reward/ang_vel_xy_l2: -0.0042
>         Episode_Reward/dof_torques_l2: -0.0018
>             Episode_Reward/dof_acc_l2: -0.0161
>         Episode_Reward/action_rate_l2: -0.0133
>          Episode_Reward/feet_air_time: 0.0004
>     Episode_Reward/undesired_contacts: -0.0001
>    Episode_Reward/flat_orientation_l2: -0.0105
>         Episode_Reward/dof_pos_limits: -0.0124
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0046
>    Episode_Reward/joint_deviation_hip: -0.0053
>    Episode_Reward/joint_deviation_torso: -0.0191
>    Metrics/base_velocity/error_vel_xy: 0.1334
>    Metrics/base_velocity/error_vel_yaw: 0.0847
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 9.5000
>    --------------------------------------------------------------------------------
>                       Total timesteps: 12091392
>                        Iteration time: 5.07s
>                          Time elapsed: 00:10:27
>                                   ETA: 04:04:52
>                                   
>    ################################################################################
>                          Learning iteration 300/3000                       
>    
>                           Computation: 21170 steps/s (collection: 4.512s, learning 0.131s)
>                 Mean action noise std: 0.64
>              Mean value_function loss: 0.0013
>                   Mean surrogate loss: -0.0082
>                     Mean entropy loss: 9.5404
>                           Mean reward: -0.20
>                   Mean episode length: 322.46
>    Episode_Reward/track_lin_vel_xy_exp: 0.0379
>    Episode_Reward/track_ang_vel_z_exp: 0.0526
>           Episode_Reward/lin_vel_z_l2: -0.0019
>          Episode_Reward/ang_vel_xy_l2: -0.0038
>         Episode_Reward/dof_torques_l2: -0.0010
>             Episode_Reward/dof_acc_l2: -0.0074
>         Episode_Reward/action_rate_l2: -0.0100
>          Episode_Reward/feet_air_time: 0.0005
>     Episode_Reward/undesired_contacts: -0.0002
>    Episode_Reward/flat_orientation_l2: -0.0053
>         Episode_Reward/dof_pos_limits: -0.0006
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0029
>    Episode_Reward/joint_deviation_hip: -0.0047
>    Episode_Reward/joint_deviation_torso: -0.0149
>    Metrics/base_velocity/error_vel_xy: 0.1003
>    Metrics/base_velocity/error_vel_yaw: 0.0539
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 12.5833
>    --------------------------------------------------------------------------------
>                       Total timesteps: 29589504
>                        Iteration time: 4.64s
>                          Time elapsed: 00:25:36
>                                   ETA: 03:49:39
>    ```
>
>    310轮mean_reward转正
>    500轮mean_reward==1.0
>    无效
>
> 
>
> 2. flat_env_cfg_G1_12dof.py文件中的commands.base_velocity.ranges.lin_vel_x = (0.0, 1.5)
>
>    ```
>    ################################################################################
>                           Learning iteration 57/3000                       
>    
>                           Computation: 18082 steps/s (collection: 5.312s, learning 0.125s)
>                 Mean action noise std: 0.78
>              Mean value_function loss: 0.0010
>                   Mean surrogate loss: -0.0089
>                     Mean entropy loss: 13.4978
>                           Mean reward: -1.79
>                   Mean episode length: 321.56
>    Episode_Reward/track_lin_vel_xy_exp: 0.0101
>    Episode_Reward/track_ang_vel_z_exp: 0.0327
>           Episode_Reward/lin_vel_z_l2: -0.0043
>          Episode_Reward/ang_vel_xy_l2: -0.0074
>         Episode_Reward/dof_torques_l2: -0.0023
>             Episode_Reward/dof_acc_l2: -0.0213
>         Episode_Reward/action_rate_l2: -0.0128
>          Episode_Reward/feet_air_time: 0.0004
>     Episode_Reward/undesired_contacts: -0.0002
>    Episode_Reward/flat_orientation_l2: -0.0094
>         Episode_Reward/dof_pos_limits: -0.0001
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0047
>    Episode_Reward/joint_deviation_hip: -0.0029
>    Episode_Reward/joint_deviation_torso: -0.0179
>    Metrics/base_velocity/error_vel_xy: 0.2028
>    Metrics/base_velocity/error_vel_yaw: 0.1315
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 9.9167
>    --------------------------------------------------------------------------------
>                       Total timesteps: 5701632
>                        Iteration time: 5.44s
>                          Time elapsed: 00:05:14
>                                   ETA: 04:26:07
>    ```
>
>    306轮转正，抬腿的积极性消失了，我认为是位置限制导致了，垃圾
>
>    
>
> 3. rough_env_cfg_G1_12dof.py文件的dof_pos_limits的joint_names改回[".\*_ankle\_pitch\_joint", ".\*\_ankle\_roll\_joint"]
>
>    ```
>    [INFO] Reward Manager:  <RewardManager> contains 15 active terms.
>    +----------------------------------------+
>    |          Active Reward Terms           |
>    +-------+-----------------------+--------+
>    | Index | Name                  | Weight |
>    +-------+-----------------------+--------+
>    |   0   | track_lin_vel_xy_exp  |    1.0 |
>    |   1   | track_ang_vel_z_exp   |    1.0 |
>    |   2   | lin_vel_z_l2          |   -0.2 |
>    |   3   | ang_vel_xy_l2         |  -0.05 |
>    |   4   | dof_torques_l2        | -2e-06 |
>    |   5   | dof_acc_l2            | -1e-07 |
>    |   6   | action_rate_l2        |  -0.01 |
>    |   7   | feet_air_time         |   0.75 |
>    |   8   | undesired_contacts    |   -1.0 |
>    |   9   | flat_orientation_l2   |   -1.0 |
>    |   10  | dof_pos_limits        |   -0.5 |
>    |   11  | termination_penalty   | -200.0 |
>    |   12  | feet_slide            |   -0.1 |
>    |   13  | joint_deviation_hip   |   -0.1 |
>    |   14  | joint_deviation_torso |   -0.1 |
>    +-------+-----------------------+--------+
>    ```
>
>    不动腿，垃圾
>    
>
> 4. 调整网络深度为【512，256， 128】
>    将scene调回50
>
>    ```
>    [INFO] Reward Manager:  <RewardManager> contains 15 active terms.
>    +----------------------------------------+
>    |          Active Reward Terms           |
>    +-------+-----------------------+--------+
>    | Index | Name                  | Weight |
>    +-------+-----------------------+--------+
>    |   0   | track_lin_vel_xy_exp  |    1.0 |
>    |   1   | track_ang_vel_z_exp   |    1.0 |
>    |   2   | lin_vel_z_l2          |   -0.2 |
>    |   3   | ang_vel_xy_l2         |  -0.05 |
>    |   4   | dof_torques_l2        | -2e-06 |
>    |   5   | dof_acc_l2            | -1e-07 |
>    |   6   | action_rate_l2        |  -0.01 |
>    |   7   | feet_air_time         |   0.75 |
>    |   8   | undesired_contacts    |   -1.0 |
>    |   9   | flat_orientation_l2   |   -1.0 |
>    |   10  | dof_pos_limits        |   -0.5 |
>    |   11  | termination_penalty   | -200.0 |
>    |   12  | feet_slide            |   -0.1 |
>    |   13  | joint_deviation_hip   |   -0.1 |
>    |   14  | joint_deviation_torso |   -0.1 |
>    +-------+-----------------------+--------+
>    
>    ################################################################################
>                           Learning iteration 50/3000                       
>    
>                           Computation: 14286 steps/s (collection: 6.750s, learning 0.131s)
>                 Mean action noise std: 0.81
>              Mean value_function loss: 0.0042
>                   Mean surrogate loss: -0.0032
>                     Mean entropy loss: 14.0771
>                           Mean reward: -1.70
>                   Mean episode length: 192.55
>    Episode_Reward/track_lin_vel_xy_exp: 0.0058
>    Episode_Reward/track_ang_vel_z_exp: 0.0180
>           Episode_Reward/lin_vel_z_l2: -0.0028
>          Episode_Reward/ang_vel_xy_l2: -0.0071
>         Episode_Reward/dof_torques_l2: -0.0016
>             Episode_Reward/dof_acc_l2: -0.0150
>         Episode_Reward/action_rate_l2: -0.0094
>          Episode_Reward/feet_air_time: 0.0004
>     Episode_Reward/undesired_contacts: -0.0002
>    Episode_Reward/flat_orientation_l2: -0.0052
>         Episode_Reward/dof_pos_limits: -0.0001
>    Episode_Reward/termination_penalty: -0.0500
>             Episode_Reward/feet_slide: -0.0032
>    Episode_Reward/joint_deviation_hip: -0.0043
>    Episode_Reward/joint_deviation_torso: -0.0124
>    Metrics/base_velocity/error_vel_xy: 0.1389
>    Metrics/base_velocity/error_vel_yaw: 0.0973
>          Episode_Termination/time_out: 0.0000
>      Episode_Termination/base_contact: 14.2500
>    --------------------------------------------------------------------------------
>                       Total timesteps: 5013504
>                        Iteration time: 6.88s
>                          Time elapsed: 00:05:20
>                                   ETA: 05:08:46
>    
>    ```
>
>    
>
>    5. 将flat_env_cfg_G1_12dof.py文件中的    self.commands.base_velocity.ranges.lin_vel_y = (-1.0, 1.0)    self.commands.base_velocity.ranges.ang_vel_z = (-1.0, 1.0)
>
>       rough_env_cfg_G1_12dof.py文件中的
>           params={"asset_cfg": SceneEntityCfg("robot", joint_names=[".*_ankle_pitch_joint", ".*_ankle_roll_joint", ".*_hip_pitch_joint"])},
>
>       ```
>       
>       ```
>
>       

