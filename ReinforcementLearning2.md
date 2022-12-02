# Passive vs. Active Learning 
* Passive learning: Agent follows a policy and learns the underline MDP 
* Active learning: Agent decideds what actions to take and learns the underline MDP

# Q-learning 
* Active learning as the agent is attempting to find an optimal policy be exploring different actions in the world
* $Q_{k+1}(s, a)=(1-\alpha)Q(s,a)+\alpha[R(s,a)+ \gamma \ maxQ'(s', a')-Q(s,a)]$
  * $Q(s,a)$ is the current Q value
  * $maxQ'(s', a')$ is the expected value of the next state assuming our policy runs optimally 
* Q-learning engages in something called off-policy learning converges to optimal policy even if you're acting suboptimally 
  * To accomplish this amazing feat, it has to do A LOT of exploring 
  * Learning rate $\gamma$ must eventually be small but it can't decrease too quickly 

# Exploration vs. Exploitation 
* Tradeoff that agent decides betweein
* Exploring $\rightarrow$ Looking at the unknown possibility for bigger reward
* Exploitation $\rightarrow$  Win-now to maximize short-term rewards  
* Naive approach: randomly choose an action
* Greedy approach: always act greedy, but overestimate the potential for rewards in the unexplored
* Greedy in limit of infinite exploration (GLIE)

## GLIE Schemes 
* Simplest scheme is the have the agent choose a random action at time step $t$ with a probability of $\frac{1}{t}$ but then follow the greedy policy in other cases 
  * Slow 
* Better approach to GLIE would be to give weight to actions that the agent hasn't tried too often while at the same time trying to avoid actions that give low reward

## Approximating TD and TD Q-Learning 
* more generalized version of Q-learning and significantly more memory-efficient one 
* Only the weight vector needs to be stored 
* $U^\pi(s)\leftarrow U^\pi(s)+\alpha(R(s,\pi(s),s')+\gamma \ U^\pi(s')-U^\pi(s)$
* $Q(s,a)\leftarrow Q(s,a)+\alpha(R(s,a,s')+\gamma \ maxQ'(s', a')-Q(s,a)$

## Approximating TD Q-Learning 