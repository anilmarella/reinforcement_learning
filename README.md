# **Definitions**

**Markov Property:** State $S_{t}$ is Markov if and only if
$$ P[S_{t+1} | S_{t}] = P[S_{t+1} | S_{1}, S_{2}, ..., S_{t}] $$

---

**State transition matrix:** Gives the probability of going from one state $S$ to $S^{'}$
$$ P_{SS^{'}} = P[S_{t+1} = s^{'} | S_{t} = s]  $$
This above function is represented as a matrix which defines the dynamics of the Markov process
$$ P = \begin{bmatrix}P_{11} & ... & P_{1n}\\.\\.\\. \\P_{n1}&...& P_{nn}\end{bmatrix} $$

---

**Markov Process**
Can be defined by a tuple $\langle S, P \rangle $ Where,  
$S$ - is a finite set of all states  
$P$ - is the transition matrix  

---

**Markov Reward Process**
Can be defined by a tuple $\langle S, P, R, \gamma \rangle$ Where,  
$S$ - is a finite set of all states  
$P$ - is the transition dynamics  
$R$ - is the reward function. It is the reward you get when you exit a state $S$ [note: for time steps, $R$ is indexed $(t+1)$ if $S$ is indexed $t$]
$$ R_{s} = E[R_{t+1} | S_{t} = s]$$
$\gamma$ - is the discount factor  

---

**Markov Decision Process**
Markov decision process is Markov reward process with actions or decisions.  
Can be defined by a tuple $\langle S, A, P, R, \gamma \rangle$ Where,  
$S$ - is a finite set of all states  
$A$ - is a finite set of actions  
$P$ - is the transition dynamics  
$$ P_{SS^{'}}^{a} = P[S_{t+1} = s^{'} | S_{t} = s, A_{t} = a]  $$
note: This is to imply one separate transcition matrix for each action  
$R$ - is the reward function. It is the reward you get when you exit a state $S$ [note: for time steps, $R$ is indexed $(t+1)$ if $S$ is indexed $t$]
$$ R_{s}^{a} = E[R_{t+1} | S_{t} = s, A_{t}=a] $$
$\gamma$ - is the discount factor [0,1]  

---

**Total discounted reward:** for time-step $t$  
$$ G_{t} = R_{t+1} + \gamma R_{t+2} + \gamma^{2} R_{t+3} + ... = \sum_{k=0}^{\infty}\gamma^{k} R_{t+k+1} $$
Discounting is done mainly to have mathematical convenience and there is a lot of uncertainity in the future compared to the present

---

**Value function**
The state value function of a Markov reward process is the expected return starting from the state $S$
$$ v(s)  = E[G_{t} | S_{t} = s] $$

Bellman Equation for value function:  
Consists of two parts  
1. Immediate reward $R_{t+1}$ and   
2. Discounted value of successor state $\gamma v(S_{t+1})$

$$ v(s) = E[G_{t} | S_{t}=s] $$
$$ v(s) = E[R_{t+1} + \gamma R_{t+2} + \gamma^{2} R_{t+3} + ... | S_{t}=s] $$
$$ v(s) = E[R_{t+1} + \gamma G_{t+1} | S_{t}=s] $$
$$ v(s) = E[R_{t+1} + \gamma v(S_{t+1}) | S_{t}=s] $$  

$$ v(s) = R_{s} + \gamma \sum_{s^{'}\epsilon S} P_{SS^{'}}v(S^{'}) $$

Bellman Equation in Matrix form
$$ \begin{bmatrix}v(1) \\ . \\.\\.\\v(n) \end{bmatrix} = \begin{bmatrix}R_{1} \\ . \\.\\.\\R_{n} \end{bmatrix}  +  \gamma \begin{bmatrix}P_{11} & ... & P_{1n}\\.\\.\\. \\P_{n1}&...& P_{nn}\end{bmatrix}   \begin{bmatrix}v(1) \\ . \\.\\.\\v(n) \end{bmatrix}$$

---

**Policy function**
A policy is a distribution over actions given state.
$$ \pi(a|s) = P[A_{t}=a | S_{t}=s] $$
Policies are not time dependent. A policy is same no matter what time step.

---

**State value function:** $v_{\pi}(s)$ of an MDP is the expected return starting from state $s$ and following policy $\pi$
$$ v_{\pi}(s) = E_{\pi}[G_{t} | S_{t}=s] $$

**Policy value function:** $q_{\pi}(s,a)$ of an MDP is the expected return starting from state $s$, taking action $a$ and following policy $\pi$
$$ q_{\pi}(s,a) = E_{\pi}[G_{t} | S_{t}=s,A_{t}=a] $$

Also, to write v and q in terms of each other,  
$$ v_{\pi}(s) = \sum_{a \epsilon A} \pi(a|s)q_{\pi}(s,a) $$
$$ q_{\pi}(s,a) = R_{s}^{a} + \gamma \sum_{s^{'} \epsilon S} P_{SS^{'}}^{a}v_{\pi}(s^{'}) $$
By putting them together we get,
$$ v_{\pi}(s) = \sum_{a \epsilon A}\pi(a|s)(R_{s}^{a} + \gamma \sum_{s^{'} \epsilon S} P_{SS^{'}}^{a}v_{\pi}(s^{'})) $$
$$ q_{\pi}(s,a) = R_{s}^{a} + \gamma \sum_{s^{'} \epsilon S} P_{SS^{'}}^{a}\sum_{a^{'} \epsilon A} \pi(a^{'}|s^{'})q_{\pi}(s^{'},a) $$

**Using Bellman equation for State & Policy value functions**  
Both the State and Policy value functions can be decomposed into immediate reward plus discounted value for successor state.
$$ v_{\pi}(s) = E_{\pi}[R_{t+1} + \gamma v_{\pi}(S_{t+1})| S_{t}=s] $$
$$ q_{\pi}(s,a) = E_{\pi}[R_{t+1} + \gamma q_{\pi}(S_{t+1}, A_{t+1}) | S_{t}=s,A_{t}=a] $$

---