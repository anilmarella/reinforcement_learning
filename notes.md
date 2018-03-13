Markov Process
==============

**Markov Property:** State $S_{t}$ is Markov if and only if

​							$$ P[S_{t+1} | S_{t}] = P[S_{t+1} | S_{1}, S_{2}, ..., S_{t}] $$

**State transition matrix:** Gives the probability of going from one state $S$ to $S~{'}$

​							$$ P_{SS~{'}} = P[S_{t+1} = s~{'} | S_{t} = s]  $$

This above function is represented as a matrix which defines the dynamics of the Markov process

​							$$ P = \begin{bmatrix}P_{11} & ... & P_{1n}\\.\\.\\. \\P_{n1}&...& P_{nn}\end{bmatrix} $$

**Markov Process:** can be defined by a tuple $<S, P> $ Where,

​				$S$ - is set of all states

​				$P$ - is the transition matrix

# Markov Reward Process



