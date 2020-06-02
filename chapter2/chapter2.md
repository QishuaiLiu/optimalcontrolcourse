## Root finding with newton type method

consider a continuously differetiable function $R: \mathbb{R}^n\to\mathbb{R}^n, z\to R(z)$, aim is to solve the nonlinear equation system:
$$ R(z) = 0$$

start with a $z_0$, and recursively generate a sequence of iterates $\{z_k\}_{k = 0}^{\infty}$ by linearizing the equation at the current iterate:

$$R(z_k) + \frac{\partial R}{\partial z}(z - z_k) = 0$$

then,

$$z_{k + 1} = z_k - (\frac{\partial R}{\partial z}(z_k))^{-1}R(z_k)$$

assume here is that the Jacobian $J(z_k):= \frac{\partial R}{\partial z}$ is invertible.

More general, we can use an invertible approximation $M_k$ of the Jacobian $\frac{\partial R}{\partial z}(z_k)$. The general Newton type iteration is
$$z_{k + 1} = z_k - M_k^{-1}R(z_k)$$


### local convergence rate

- Q-linearly, $\lVert z_{k + 1} - \bar{z} \rVert $ <= $C \lVert z_k - \bar{z}\rVert$ with $C < 1$.
this is equivalent to: 
$$\lim \sup_{k\to\infty}\frac{\lVert z_{k+ 1} - \bar{z}\rVert}{\lVert z_{k} - \bar{z}\rVert} < 1$$
- Q-superlinearly, $\lVert z_{k + 1} - \bar{z} \rVert $ <= $C_k \lVert z_k - \bar{z}\rVert$ with $C_k \to 0$.

this is equivalent to: 
$$\lim \sup_{k\to\infty}\frac{\lVert z_{k+ 1} - \bar{z}\rVert}{\lVert z_{k} - \bar{z}\rVert} = 0$$

- Q-quadratically, $\lVert z_{k + 1} - \bar{z} \rVert $ <= $C \lVert z_k - \bar{z}\rVert$ with $C < \infty$.

this is equivalent to: 
$$\lim \sup_{k\to\infty}\frac{\lVert z_{k+ 1} - \bar{z}\rVert}{\lVert z_{k} - \bar{z}\rVert} < \infty$$


where $Q$ means quotient.

### local contraction theorem
suppose the sequence by newton type method is
$$\lVert z_{k + 1} - z^*\rVert \le \big(\kappa_k + \omega/2\lVert z_{k} - z^*\rVert\big) \lVert z_{k} - z^*\rVert$$

if there exist $\omega < \infty$ and $\kappa < 1$ such that for all $z_k$ and $z$ holds

$$\lVert M^{-1}_k(J(z_k) - J(z))\rVert \le \omega \lVert z_k - z\rVert$$ (lipschitz, or omega condition)


$$\lVert M^{-1}_k(J(z_k) - J(z))\rVert \le \kappa_k \le kappa$$ (compatibility, or kappa condition)

and if $\lVert z_0 - Z^*\rVert$ is sufficiently small, namely  $\lVert z_0 - Z^*\rVert < \frac{2(1 - \kappa)}{\omega}$
note $\kappa = 0$ for exact newton.

Proof:
The proof use the taylor expansion.

or use the weaker condition of $omega $ and $\kappa$.
### Affine Invariance

The ietration method to solve the root finding problem is called "affine invariant" if affine transformation of the equations or of the variables will not change the resulting iterations. 

Given two invertible matrices $A, B\in\mathbb{R}^{n\times n}$ and a vector $b\in\mathbb{R}^n$, the root finding problem:
$$\tilde R(y):= AR(b + By) = 0$$

clearly, if we have a solution $z^*$ with $R(z^*) = 0$, we can construct from it a $y^*$ such that $\tilde R(y^*) = 0$, by inverting the relation $z^* = b + By^*$, i.e. $y^* = B^{-1}(z^* - b)$
starting from a initial guess $z_0$, towards the solution of $R(z) = 0$. This method is called "affine invariant".


### Tight condition for local convergence
The local contraction theorem gives sufficient condition for local convergence. But the $\omega$ condition is not retrctive.

In this part, a sufficient condition for local convergence that is tight and even a necessary condition for local convergence of Newton-type methods. 
The only assumption is that the iteration matrices $M_k$ is continuously differentiable.

(LInear statbility analysis)
the iteration form $z_{k+ 1} = G(z_k)$, with $G$ is a continuously differentiable function in a neighborhood of a fixed point $G(z^*) = z^*$. if the Jacobian $\frac{\partial G}{\partial z}(z^*)$ have a modulus smaller than one, i.e., the spectral radius is smaller than one. then the fixed point is asymptotically stable and the iterates converge to $z^*$ with a $Q-linear$ convergence rate. if spectral radius >1, the fixed point is unstable.

### Globalization
