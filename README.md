# ENPM667 - Control of Robotic Systems - Project 1

## Pratik Acharya   
## 117513615  

# Paper : [Robust Predictable Control](https://arxiv.org/pdf/2109.03214v1.pdf)  

This repository contains the code for the above-mentioned research paper. Installation and other instructions have been mentioned below.

## Installation
These instructions were tested with Ubuntu version 18.04.


### 1. Install Mujoco
Mujoco can be downloaded from [here](https://mujoco.org/download).


After download, move the downloaded folder to `.mujoco` folder in the home directory, and execute the following command line code.
```
echo "export LD_LIBRARY_PATH=\$LD_LIBRARY_PATH:$HOME/.mujoco/mujoco210/bin" >> ~/.bashrc
```

### 2. Install Anaconda
```
wget https://repo.anaconda.com/miniconda/Miniconda2-latest-Linux-x86_64.sh
chmod +x Miniconda2-latest-Linux-x86_64.sh
chmod +x ./Miniconda2-latest-Linux-x86_64.sh
```
Restart your terminal so the changes take effect.


### 3. Create an Anaconda environment and install the remaining dependencies
```
conda create --name rpc python=3.6
conda activate rpc
pip install tensorflow==2.6.0
pip install tf_agents==0.7.1
pip install git+https://github.com/openai/gym.git@9dea81b48a2e1d8f7e7a81211c0f09f627ee61a9
pip install mujoco-py==2.0.2.10
```



## Running Experiments

The following lines replicate the RPC experiments and baselines on the HalfCheetah-v2.

* RPC:
```
python train_eval.py --root_dir=~/rpc/rpc --gin_bindings='train_eval.env_name="HalfCheetah-v2"' -- gin_bindings='train_eval.log_prob_reward_scale="auto"' --gin_bindings='train_eval.predict_prior=True' -- gin_bindings='train_eval.use_recurrent_actor=False' --gin_bindings='train_eval.kl_constraint=0.3'
```
  
* VIB (Igl 2019):
```
python train_eval.py --root_dir=~/rpc/vib --gin_bindings='train_eval.env_name="HalfCheetah-v2"' --gin_bindings='train_eval.log_prob_reward_scale=0.0' --gin_bindings='train_eval.predict_prior=False' --gin_bindings='train_eval.use_recurrent_actor=False' --gin_bindings='train_eval.kl_constraint=0.3'
```

* VIB + reward (Lu 2020):
```
python train_eval.py --root_dir=~/rpc/vib_reward --gin_bindings='train_eval.env_name="HalfCheetah-v2"' --gin_bindings='train_eval.log_prob_reward_scale="auto"' --gin_bindings='train_eval.predict_prior=False' --gin_bindings='train_eval.use_recurrent_actor=False' --gin_bindings='train_eval.kl_constraint=0.3'
```

* VIB + RNN 
```
python train_eval.py --root_dir=~/rpc/vib_rnn --gin_bindings='train_eval.env_name="HalfCheetah-v2"' --gin_bindings='train_eval.log_prob_reward_scale=0.0' --gin_bindings='train_eval.predict_prior=False' --gin_bindings='train_eval.use_recurrent_actor=True' --gin_bindings='train_eval.kl_constraint=0.3'
```

* Latent-space model
```
python train_eval.py --root_dir=~/rpc/latent_space --gin_bindings='train_eval.env_name="HalfCheetah-v2"' --gin_bindings='train_eval.log_prob_reward_scale=0.0' --gin_bindings='train_eval.predict_prior=True' --gin_bindings='train_eval.use_recurrent_actor=False' --gin_bindings='train_eval.kl_constraint=100000.0'
```

### References
* Eysenbach, , et.al. "Robust Predictable Control" arXiv preprint arXiv:2109.03214 (2021)

* Lu, Xingyu, et al. "Dynamics Generalization via Information Bottleneck in Deep Reinforcement Learning." arXiv preprint arXiv:2008.00614 (2020).
* Igl, Maximilian, et al. "Generalization in Reinforcement Learning with Selective Noise Injection and Information Bottleneck." Advances in Neural Information Processing Systems 32 (2019): 13978-13990.
