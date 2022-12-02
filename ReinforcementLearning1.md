## [CS 188 Lecture 9: Reinforcement Learning I](https://www.youtube.com/watch?v=aTcIQWMPmJY&list=PL4fsLMhBK1A2oeH__2bXbZC8oH87lsQpe&index=10&t=1s)

### Basics 
* Agent receives feedback in the form of rewards 
* Agent's utility is defined by the reward function 
* Must learn to do things that maximizes expected rewards
* Agent does certain actions upon environment, environment gives agent a reward based on state 
* Still assume MDP and that we are looking for a policy $\pi(s)$
* However, now we are unaware of what T or R is, meaning we don't know the transition model or reward function is 

### Offline vs. Online Planning 
#### Offline 
* Agents have full knowledge of both transition function and reward functiion 
* Optimal actions are already computed without even having to take actions 

#### Online 
* Agent may not know either the reward function or transition model
* Agent tries out actions and states out to learn and get feedback
* Feedback is then used to estimate an optimal policy through a process called reinforcement learning 

### Model Based Reinforcement Learning 
* Learn an approximate model based on experiences 
* Solve for values as if the learned model is correct 

* Step 1: Learn empirical MDP model
  * Count outcomes s' for each s,a 
  * Normalize to give an estimate of $\hat{T}(s,a,s')$ 
  * Discover each $\hat{R}(s,a,s')$ when we experience (s,a,s')
* Step 2: Solve the learned MDP
  * Possibly use value iteration

### Model-free Reinforcement Learning  
* Bypass needing to learn the $T$ or $R$ at all 
* Instead use either direct evaluation or temporal difference learning to evaluate $U^\pi$, the utility function for policy $\pi$
* Derive optimal policy $\pi$ without learning the model
* Q-learning can be conducted to learn $\pi$, $Q$\*, $V$\* without knowing $T$ and $R$ 

### Example of Model Based Learning 

### Passive Reinforcement Learning 
* Agent doesn't have control of itself, it is kind of looking at itself performing and learning 
* Goal is to learn the state values 
* Learner/Agent is "along for the ride" 
* No choices for actions, just execute policy and learn from experience
* Online planning  
* Direct Evaluation or Temporal Difference Learning 

### Direct Evaluation 
* Goal is to compute values for each state under $\pi$
* Idea: Avg. together observed sample values
  * Act according to policy $\pi$
  * Use observed policies to determine states that are visited
  * Each time a state is visited, write down the sum of discounted rewards turned out to be 
  * Avg. the samples by dividing the sum by number of times the state is visited
* Good: No need to know T, R
* Good: Eventually computes correct avg. values, using just sample transitions 
* Bad: Wastes info about state connections 
* Bad: Each state must be learned separately so it takes a long time to learn

### Bellman Equation
$U_i(s)=\sum_{s'}P(s'|s,\pi_i(s))[R(s,\pi_i(s),s') + \gamma U_i(s')]$

### Temporal Difference Learning 
* Update $V(s)$ each time we experience a transition, $(s,a,s',r)$
* Likely outcomes $s'$ will contribute updates more often than direct evaluation
* policy is still fixed 
* Values move toward value of whatever successor occurs 
  * running average 

* $\alpha$ is learning rate 
#### Exponential Moving Average 
* Decreasing learning rate of alpha can give converging averages 
* $\alpha=\frac{1}{n}$
* $U^\pi(s)\leftarrow (1-\alpha)U^\pi(s)+\alpha[R(s,\pi(s), s')+\gamma U^\pi(s')$
  * $\alpha$ and $\gamma$ are usually given by the problem
  * $U^\pi(s)$ is the estimated utility at the current state $s$
  * $R(s,\pi(s),s')$ is the observed reward for going from state $s$ to state $s'$
  * $U^\pi(s)$ is the estimated value at the transition state $s'$

### Active Reinforcement Learning 
* Agent actually has to decide what actions to take in order to learn the policy
* Agent doesn't know what the actions do
* Once againt transition model and reward function is unknown
* Actions are being chosen by the agent / learner
* Goal is to learn optimal policy / values 
* Not offline planning because you're actually taking actions in the world 