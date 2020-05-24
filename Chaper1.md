### zero order hold and solution map

$$\dot{x} = f(x(t) , u_{const}) $$
$t\in [0, \Delta t]$ with $x(0) = x_0$.

在0到$\Delta t$的时间之内，可以当做连续系统。解可以写为：

$$x(t; x_0, u_{const})$$
for $t\in [0, \Delta t]$, 这个解map from $(x_0, u_{const})$ to the state trajectory is called **solution map**.

### solution map of linear time invariant systems

consider system:
$$\dot{x} = Ax + Bu$$
inital value is $x_0$ at $t = 0$, and constant control input $u = u_{const}$, the solution map is:

$$x(t; x_0, u_{const}) = \exp(At)x_0 + \int_0^{t}\exp(A(t - \tau))Bu_{cosnt}d\tau$$
The corresponding discrete time system with sampling time $\Delta t$ is given as:
$$f(x_k, u_k) = A_{dis}x_k + B_{dis}u_k$$
with  $A_{dis} = \exp(A\Delta t)$ and $B_{dis} = \int_0^{\Delta t} \exp(A(\Delta t - \tau))Bd\tau$

### sensitivities
restrcit the solution to a neighborhood $\mathcal{N}$ of fixed values $(x_0, u_{cosnt})$, for each fixed $t\in[0, \Delta t]$, solution map $x(t;\cdot):\mathcal{N}\to \mathbb{R}^{n_x}， (x_0, u_{const}) \to x(t;x_0, u_{const})$.

If $f$ is $m$ times continuously differential with respect to both $x$ and $u$, then the solution map $x(t;\cdot)$ for each $t\in [0,\Delta t]$ is also $m$ time continuously differetiable with respect to $(x_0, u_{const})$.


### numerical intergration methods
a numerical simulation routine that approximates the solution map is often called **integrator**. a simple way is to perform the linear extrapolation based on the time derivative $\dot{x} = f(x, u)$ at the inital time point:

$$\tilde{x}(t;x_0, u_{const}) = x_0 + t f(x_0, u_{const}), t\in [0, \Delta t]$$

This is called **Euler intergration step**. The error $\tilde {x}(\Delta t; x_0, u_{const}) - x(\Delta t; x_0, u_{const})$ is of second order in $\Delta t$. 

接下来介绍**euler ingegration method** and show it is stble, which means the propagation of local errors is bounded with a constant that is independent of the step size $h$. 
在接下来是 **Runge-Kutta method of order four**.

From here on, we control a discrete time system
$$x_{k + 1} = f_{dis}(x_k, u_k)$$.
the transition map $f_{dis}(x_k, u_k)$ is usually not given as an explicit expression but can instead be a relatively involved computer code.

## 1.3 Discrete time systems
consider the system with dynamics:
$$x_{k + 1} = f_k(x_k， u_k), k = 0, 1, \ldots, N - 1$$

on a time horizon of length $N$, with $N$ control input vectors $u_0, \ldots, u_{N-1}\in\mathbb{R}^{n_u}$ and ($N + 1$) state vectors $x_0, \ldots, x_N\in \mathbb{R}^{n_x}$.

if we know the inital state and all control input, we can obtain all other states, we call this a **forward simulation** of the system dynamics.

the forward simulation is the map:

$$f_sim: \mathbb{R}^{n_x + Nn_u} \to \mathbb{R}^{(N+ 1)n_x}, (x_0; u_0,\ldots, u_{N-1})\to (x_0,x_1,\ldots, x_N)$$

by solving the equation recursively for all $k = 0, 1, \ldots, N - 1$.

