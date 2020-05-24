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
$$x_{k + 1} = f_k(x_k， u_k), k = 0, 1, \ldots, N - 1 \tag{1.3}$$

on a time horizon of length $N$, with $N$ control input vectors $u_0, \ldots, u_{N-1}\in\mathbb{R}^{n_u}$ and ($N + 1$) state vectors $x_0, \ldots, x_N\in \mathbb{R}^{n_x}$.

if we know the inital state and all control input, we can obtain all other states, we call this a **forward simulation** of the system dynamics.

the forward simulation is the map:

$$f_sim: \mathbb{R}^{n_x + Nn_u} \to \mathbb{R}^{(N+ 1)n_x}, (x_0; u_0,\ldots, u_{N-1})\to (x_0,x_1,\ldots, x_N) $$ 

by solving the equation recursively for all $k = 0, 1, \ldots, N - 1$.

(1.3) 是dynamical optimization problem的核心问。 有没有初始值的约束不重要。

### Linear time invariant(LTI) system

In discrete time case, the  linear time invariant system is given:
$$x_{k + 1} = Ax_k + Bu_k, k = 0, 1,\ldots, N - 1$$

with fixed matrices $A^{n_x \times n_x}$ and $B\in\mathbb{R}^{n_x \times n_u}$.

Stable and asymptotically stable is same as general control course.

the forward simulation map for this system on a horizon with length N is given:

$\left[\begin{matrix} x_0\\ x_1 \\ x_2 \\ \vdots \\ x_N \end{matrix}\right]$  = $\left[\begin{matrix} x_0\\ Ax_0 + Bu_0 \\A^2x_0 + ABu_0 + Bu_1  \\ \vdots \\ A^Nx_0 + \sum_{k = 0}^{N - 1}A^{N - 1- k}Bu_k  \end{matrix}\right]$


### Affine system and linearizations along trajectory

affine time-varying system:
$$x_{k + 1} = A_k x_k + B_k u_k + c_k, k = 0, 1, \cdots, N - 1 \tag{1.4}$$

These often as linearization of nonlinear dynamic systems along a given reference trajectory. 

For some nonlinear system, the Taylor expansion of each function $f_k$ at the reference value $(\bar x_{k}, \bar u_{k})$ is given by:

$$(x_{k + 1} - \bar x_{k + 1}) \approx \frac{\partial f_k}{\partial x}(x_k, u_k)(x_k - \bar x_k) + \frac{\partial f_k}{\partial u}(x_k, u_k)(u_k - \bar u_k) + (f_k(\bar x_k, \bar u_k) - \bar x_{k + 1})$$

and this is the 1.4.

The simulation map of the affine system 1.4 is an affine function of the initial value and the controls. This affine map is for any $N \in \mathbb{N}$ given by:
$$x_N = (A_{N - 1}\cdots A_0)x_0 + \sum_{k = 0}^{N  - 1} (\prod_{j = k + 1}^{N - 1}A_j)(B_ku_k + c_k)$$

### 1.4 optimization problem classes

Discrete time optimal control problems fall into the first and continuous time optimal control problems into the second class. (e.g. finite or infinite dimensional optimization.)

If an inifinte number of inequality constraints while the decision variables is finite, it is called **semi-infinite optimization** problem, naturally arises in the context of **robust optimization.**

### convex and nonconvex optimization

convex optimization is a subclass of the continuous optimization problems and arise if the objective function is a convex function and the set of feasible points a convex set.