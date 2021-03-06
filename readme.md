# Diversity-Augmented Intrinsic Motivation for Deep Reinforcement Learning

# Setup
```bash
pip install -e .
pip install -r requirements.txt
```


#  Mujoco with Proximal Policy Optimization (PPO)
Please first 
```commandline
cd rl_algorithms/ppo
```
then follow the following instruction.

## Instructions
1. Train the agents - **Atari Env**:
```bash
python train.py --env-name='<env-name>' --cuda (if you have a GPU) --env-type='atari' --lr-decay
```
2. Train the agents - **Mujoco Env** (we also support beta distribution, can use `--dist` flag):
```bash
python train.py --env-name='<env-name>' --cuda (if you have a GPU) --env-type='mujoco' --num-workers=1 --nsteps=2048 --clip=0.2 --batch-size=32 --epoch=10 --lr=3e-4 --ent-coef=0 --total-frames=1000000 --vloss-coef=1 
```
3. Train the intrinsic agents:
```bash
python -u train.py --env-name='HalfCheetah-v2' --cuda --reward-delay-freq=40 --dpp-batch-size=1 --r-ext-coef=1 --log-dir='logs_dpp_reward_delay_20_seed_123' --seed=123 2>&1 | tee exp_dpp_reward_delay_20_halfcheetah.log
```

4. Play the demo - Please use the same `--env-type` and `--dist` flag used in the training.
```bash
python demo.py --env-name='<env name>' --env-type='<env type>' --dist='<dist-type>'
```


# Atari with Synchronous Advantage Actor-Critic (A2C)
Please first 
```commandline
cd rl_algorithms/a2c
```
then follow the following instruction.

## Instructions
1. Train the agents:
```bash
python train.py --env-name='<env-name>' --cuda (if you have a GPU)
```
2. Play the demo:
```bash
python demo.py --env-name='<env name>'
```
## Results
* DAIM with different kernel sizes 
![](figures/mujoco_multi_frames.png)
* DAIM with different choices of `$\lambda^in$`
![](./figures/mario_results.png)
