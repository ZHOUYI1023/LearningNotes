# Analysis and Control of Multi-Robot Systems

**Multi-Robot Systems** are systems composed of multiple interacting dynamics unit.
- Biologically inspired by honeybees and fireflies.
- Synchronization: An agreement by multiple systems on a common state
- Coordination: Managing of multiple interacting systems to achieve a team objective.

## Passivity
Something that does not produce internel energy.

$\begin{cases}
\dot{x} = f(x) + g(x)u \\
y = h(x)
\end{cases}$

is said to be passive if there exists a **storage function**

$V(x) \isin C: R^n \rarr R^+$

such that $ \dot{V} \leqslant y^Tu $ or equivalently

$V(x(t)) \leqslant V(x(t_{0})) + \int_{t_0}^{t} y^T(s)u(s)ds $

**Current energy is at most equal to the inital energy + supplied energy from outside, 
i.e. no internal generation of energy.**

Proper interconnections of passive systems are passive.

port-based network modelling

# Formation Control: A Review and A New Consideration

## Stability Notions
* String Stability
* Mesh Stability
* Leader-to-Formation Stability

## Controllability Analysis
* Via Graph Theory
* Via Lyapunov Function

## Control Strategy
* Via Behaviour-based Approach and Potential Field Approach
* Via Leader-Follower Approach
* Via Generalized Coordinates
* Via Virtual Structure Method




