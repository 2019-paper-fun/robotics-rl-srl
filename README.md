# Reinforcement Learning (RL) and State Representation Learning (SRL) with robotic arms (Baxter and Kuka)

## Requirements:

- Python 3 (python 2 not supported because of OpenAI baselines)
- [OpenAI Baselines](https://github.com/openai/baselines) (latest version)
- [OpenAI Gym](https://github.com/openai/gym/) (latest version)
- Install the dependencies using `environment.yml` file (for conda users)

[PyBullet Documentation](https://docs.google.com/document/d/10sXEhzFRSnvFcl3XxNGhnD4N2SedqwdAvK3dsihxVUA)

```
git clone git@github.com:araffin/robotics-rl-srl.git --recursive
```

## Kuka Arm \w PyBullet

Launch visdom server:
```
python -m visdom.server
```

Pytorch Agent:
```
python train_pytorch.py --num-cpu 4 --num-stack 1 --env-name KukaButtonGymEnv-v0 --algo a2c --log-dir logs/
```

OpenAI Baselines Agent:
```
python -m rl_baselines.train --algo ppo2 --log-dir logs/
```


## Reinforcement Learning

Note: All CNN policies normalize input dividing by 255.

### OpenAI Baselines

Several algorithms from [Open AI baselines](https://github.com/openai/baselines) have been integrated along with a random agent and random search:

- DQN and variants (Double, Dueling, prioritized experience replay)
- ACER (Sample Efficient Actor-Critic with Experience Replay)
- A2C
- PPO2

To train an agent:
```
python -m rl_baselines.train --algo acer --log-dir logs/
```

### Pytorch Agents

This concerns the `train_pytorch.py` script.

We are using Pytorch Implementation of A2C, PPO and [ACKTR](https://blog.openai.com/baselines-acktr-a2c/) from [https://github.com/ikostrikov/pytorch-a2c-ppo-acktr](https://github.com/ikostrikov/pytorch-a2c-ppo-acktr) (see `pytorch_agents` folder):

- A2C - A synchronous, deterministic variant of Asynchronous Advantage Actor Critic (A3C) which gives equal performance.
- ACKTR (pronounced “actor”) Actor Critic using Kronecker-factored Trust Region ("Scalable trust-region method for deep reinforcement learning using Kronecker-factored approximation") is a more sample-efficient reinforcement learning algorithm than TRPO and A2C,
- PPO- Proximal Policy Optimization


## Baxter Robot \w Gazebo and ROS
Gym Wrapper for baxter environment + RL algorithms

```
roslaunch arm_scenario_simulator baxter_world.launch
rosrun arm_scenario_simulator spawn_objects_example

python -m gazebo.gazebo_server
python -m gazebo.teleop_client
```

```
sudo netstat -lpn | grep :7777
```

## Troubleshooting
If a submodule is not downloaded:
```
git submodule update --init
```
