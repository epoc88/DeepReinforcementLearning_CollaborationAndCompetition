

# Project 3: Multi-Agent Collaboration & Competition

### Introduction 
DDPG stands for Deep Deterministic Policy Gradients, presented in 2015 in “Continuous Control With Deep Reinforcement Learning” (Lillicrap et al, 2015). DDPG builds on the actor-critic framework but differentiates itself by directly outputting action values instead of a probability distribution across discrete values. 

For this project, two agents must collaborate in this enviornment to maximize reward. According to the [MADDPG Paper](https://arxiv.org/abs/1706.02275) we need to make additional considerations when working with multiple agents. In the case of multi agent, both agents shared a common replay buffer as indicated in the MADDPG paper. After trying both, I found that the simpler DDPG should work.

Learning process started by initializing our four networks (critic, actor, target critic, target actor) and our replay buffer. In the training, for each episode to train, the state is initialized (to start again with a new environment), and for each time step, we select an action based on the current policy and exploration policy. We get an action from the actor network and add noise to it. Then performing the action in the environment, observe the reward, and new state of the environment (now we have s,a,r,s'). The experience (s,a,r,s') are stored in memory buffer. Depending on the training policy, we may sample a minibatch from this buffer and calculate an updated Q value. The updated Q-value is obtained by the Bellman Equation but we use the target value network to calculate the next state Q value and the target policy network to get the next action value.  
 
 
### Implementation details
#### actor network: 
The state observation is input and the action is output. 

Fully connected layer 1 - 400 nodes  
Fully connected layer 2 - 300 nodes  


#### critic network: 
Uses similar architecture as actor network, which takes both state observation and action as input and the scalar (_Q_ value) as the output.

Fully connected layer 1 - 400 nodes  
Fully connected layer 2 - 300 nodes  

#### Hyperparameters  

Hyperparameters | value
---|---
Batch size | 128
Gamma | 0.99
Tau | 1e-3
Actor learning rate | 1e-3 
Actor learning rate minimum | 1e-4 
Critic learning rate | 1e-3 
Critic learning rate minimum | 1e-4 
Steps / each Learn   | 1
Minibatches per learning step| 16 
OU sigma |0.2
OU theta | 0.15
Epsilon decay for noise process | 1e-6


### Plot of Scores
The environment is solved at **304** episodes. 
<img src="https://github.com/epoc88/DeepReinforcementLearning_CollaborationAndCompetition/blob/master/images/results.png?raw=true" width="60%" align="top-left" alt="" title="Results" />  
  
### Future work
##### Other solutions than DDPG
- D4PG: The paper by Barth-Maron et. al 2018 has achieved state of the art resutls on the continuous control problems.  
- MADDPG: Another solution is to implement by maddpg, i.e. multi agent deep deterministic policy gradient, similar to the one outlined and implemented in Lowe, Wu, et. al. The idea behind MADDPG is to leverage the successful ideas behind DDPG Lillicrap, Hunt, et. al., which itself builds up on deep q-learning networks DQN Mnih, Kavukcuoglu, Silver, et. al. 


##### Hyper parameter tuning
Current hyperparameters are the initial guess, and have not been optimized. A selection of hyperparameter mechanism or visualization could be done in the future.
 
