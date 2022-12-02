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
