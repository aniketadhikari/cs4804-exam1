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

![](discounting.PNG)
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
