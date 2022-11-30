# Markov Decision Processes I
## [Markov Decision Processes - Georgia Tech - Machine Learning](https://www.youtube.com/watch?v=Jk2V9yA82YU&list=PLdT4hf-aFsmnKBOJQXQ7P30bHloCePaNg&index=6)

* States: S
  * Set of possible states that are agent can be in
  * Ex. Possible grid positions 
  * Initial state, goal state, etc.

## [Markov Decision Processes - Computerphile](https://www.youtube.com/watch?v=2iF9PRriA7w&list=PLdT4hf-aFsmnKBOJQXQ7P30bHloCePaNg&index=4)
* How do robots make decisions 

## [CS 188 Lecture 7: MDPs I](https://www.youtube.com/watch?v=wIloocUqL-E&list=PL4fsLMhBK1A2oeH__2bXbZC8oH87lsQpe&index=9&t=231s)
* MDPs are used for non-deterministic search problems, meaning ***we do not know the cost of reaching our goal state***
* Probabilities that correspond to actions 
* Maze-like 
* Agent receives reward on each step
  * Reward can be negative, meaning that the step taken was bad

![](images/deterministicvsctochastic.png)

### Definition of MDP
* Set of states, $s \in S$
* Set of actions $a \in A$
* A transition function $T(s, a, s')$
  * Also translated to *the probability of landing in $s'$ when starting from $s$ and taking action $a$*
* A reward function $R(s, a, s')$
* A start state
* (Possibly) a terminal state


### Markov Meaning 
* ***Action outcomes depend only on the current state and NOT on past decisions/states***

### Policies 
* A policy refers to a plan, or sequence of actions, from start to goal
* Function that maps states to actions ($S\rarr A$) = $\pi$ 
* Optimal function that maps states to actions ($S\rarr A$) = $\pi$* 
  * maximizes expected utility

### MDP Search Trees 
* Each MDP state projects an expectimax-like search tree 

### Utilities of Sequences 
* More or less? 
  * [1, 2, 2] or [2, 3, 4]
  * Obviously [2, 3, 4] because the sum of values in this array is more than the other one
* Now or later? 
  * [0, 0, 1] or [1, 0, 0]
  * We would want our reward now rather than later so [1, 0, 0] is preferable
  * Think about money: we want money now rather than later on as the value of money decays 

### Discounting 
* Reasonable to maximize the sum of rewards BUT it's also reasonable to prefer rewards now rather than later 
* ***Value of rewards decay exponentially***
#### How to Discount?
* Each time we descend a level, discount is multiplied in once 

#### Why Discount?
* Sooner rewards probably do have higher utility than later rewards  
* Helps for algorithms to converge 

## Chapter 17.1 - 17.3
* **Optimal policy** is a policy that yields the highest expected utility 
  * Denoted with $\pi$*
* Finite horizon means that there is a fixed time $N$ after which nothing matters and the game is over
  * Optimal actions may actually depend on how much time is left (bigger risks toward end of life cycle)
* Discount factor
  * $0<\gamma<1$
  * Closer to 0 means rewards in future are viewed as insignificant (lives in the moment)
  * Closer to 1 means agent will wait for rewards (forward-thinking)



# Markov Decision Processes II
## [CS 188 Lecture 7: MDPs I](https://www.youtube.com/watch?v=S0jvKddQdUU&list=PL4fsLMhBK1A2oeH__2bXbZC8oH87lsQpe&index=9)
### Bellman Equations 
$V$*$(s) = max(a)Q$\*$(s,a)$

$V$*$(s)=max(a)\sum_{s}T(s,a,s')[R(s,a,s')+\gamma V$\* $(s')]$

* Bellman equations are characterizing equations for the optimal values and q-values 
### Stationary vs. Nonstationary 
* Stationary policies
  * Optimal policy that optimal action depends only on the current state 
* Nonstationary policies 
  * A policy that depends on time 

### Value Iteration 
* Start with $V_0(s)=0$
  * If there are no time steps left, that means there is an expected reward sum of zero
* Given vector of $V_k(s)$ values, do one ply of expectimax from each state:
  * $V_{k+1}(s)=max_{a}\sum_{s'}T(s,a,s')[R(s,a,s')+\gamma V_k(s')]$
* Repeat until convergence 
* Time complexity of each iteration $O(S^2A)$
* Value iteration is guaranteed to converge 
* Value iteration will converge to the same vector of values (V*) no matter what values we use to initialize V.
* For an infinite horizon MDP with a finite number of states and actions and with a discount factor γ that satisfies 0<$\gamma$<1, value iteration is guaranteed to converge.
*  If one is using value iteration and the values have converged, the policy must have converged as well. 


### Issues with Value Iteration 
1. It is slow 
   * $O(S^2A)$ per iteration
2. The max at each stage rarely changes 
3. The policy often converges long before the values 

# Reinforcement Learning I
## [CS 188 Lecture 9: Reinforcement Learning I](https://www.youtube.com/watch?v=aTcIQWMPmJY&list=PL4fsLMhBK1A2oeH__2bXbZC8oH87lsQpe&index=10&t=1s)

### Basics 
* Agent receives feedback in the form of rewards 
* Agent's utility is defined by the reward function 
* Must learn to do things that maximizes expected rewards
* Agent does certain actions upon environment, environment gives agent a reward based on state 
* Still assume MDP and that we are looking for a policy $\pi(s)$
* However, now we are unaware of what T or R is, meaning we don't know the transition model or reward function is 

### Model Based Learning 
* Learn an approximate model based on experiences 
* Solve for values as if the learned model is correct 

* Step 1: Learn empirical MDP model
  * Count outcomes s' for each s,a 
  * Normalize to give an estimate of $\hat{T}(s,a,s')$ 
  * Discover each $\hat{R}(s,a,s')$ when we experience (s,a,s')
* Step 2: Solve the learned MDP
  * Possibly use value iteration