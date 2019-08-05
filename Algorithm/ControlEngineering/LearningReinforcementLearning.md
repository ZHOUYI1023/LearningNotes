# Reinforcement Learning
## CS229 Part XIII note 12
**Markov Decision Process**
A Markov decision process is a tuple $(S,A,P_{sa},\gamma,R)$, where
* S is a set of states
* A is a set of actions
* $P_{sa}$ are the state transition probabilities, which gives the distribution over what states we will transition to if we take action a in state s
* $\gamma \isin [0,1)$ is discount factor
* $ R: S \times A \mapsto \Reals$ is the reward function
* $\pi: S \mapsto A$ is the policy, following which we will take action $a=\pi(s)$ when we in state $s$

Goal: to choose actions over time so as to maximize the expected value of the total payoff:
$E[R(s_0)+\gamma R(s_1) + \gamma^2R(s_2)+\cdot\cdot\cdot]$

The value function for a policy $\pi$ is defined as
$V^\pi(s) = E[R(s_0) + \gamma R(s_1) + \gamma^2 R(s_2)+\cdot\cdot\cdot \mid s_0 = s,\pi]$ 
notice it starts from state s rather than end in it.

* Fully Observable environments: MDP
* Partial Oberservable: POMDP 

**Bellman Equation**
Given a fixed policy, its value function can be written in
$V^\pi(s) = R(s) + \gamma\displaystyle\sum_{s' \isin S} P_{s\pi(s)} (s')V^\pi(s')$
$R(s)$ is the immediate reward, the second term indicates the expected sum of future discounted rewards

In a finite-state MDP $|S| < \infty $, we can write down one such equation for every state $s$.

$\begin{bmatrix}V(s_1)\\\vdots\\V(s_n)\end{bmatrix} = \begin{bmatrix}R(s_1)\\\vdots\\R(s_n)\end{bmatrix} + \gamma\begin{bmatrix}P_{11}\cdots P_{1n}\\\vdots\qquad\vdots\\P_{n1} \cdots P_{nn}\end{bmatrix}\begin{bmatrix}V(s_1)\\\vdots\\V(s_n)\end{bmatrix}  $

It can be solved directly:
$v = R+\gamma Pv$ 
$v = (I-\gamma P)^{-1}R$
Direct solution only possible for small MRPs

The optimal value function is 
$V^*(s) = \displaystyle\max_\pi V^\pi(s) = R(s) + \displaystyle\max_{a\isin A}\gamma\displaystyle\sum_{s'\isin S}P_{sa}(s')V^*(s')$

The optimal policy is
$\pi^*(s) = \argmax_{a\isin A}\displaystyle\sum_{s'\isin S}P_{sa}(s')V^*(s')$

Thus,
$V^*(s) = V^{\pi^*}(s)\geqslant V^\pi(s)$

**Value Itertaion**
Repeatedly trying to update the estimated value function using Bellman Equations

For each state s, initilize ${V(s) := 0}$
Repeat until convergence{
&emsp;&emsp;For every state, update ${V(s) := R(s) + \displaystyle\max_\gamma\displaystyle\sum_{s'}P_{sa}(s')V(s')}$
}

**Policy Iteration**
Initialize $\pi$ randomly
Repeat until convergence{
&emsp;&emsp;Let $V:=V^{\pi}$
&emsp;&emsp;For each state s, let $\pi(s):=\displaystyle\argmax_{a\isin A}\sum_{s'}P_{sa}(s')V(s')$
}

* For MDPs with small state space, policy iteration is often fast and converges with very few iterations
* For MDPs with large state space, value iteration is preferred.

**Q Learning**

**Sarsa**

## On Value Functions and the Agent-Enironment Boundary