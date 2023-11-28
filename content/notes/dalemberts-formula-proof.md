+++
title = "d'Alembert's Formula Proof"
description = "Proof for d'Alembert's Formula"
date = "2023-05-25"
aliases = ["d'Alembert's formula proof"]
author = "Benjamin Hong"
math = true
+++

For function $u(t,x)$ which has one temporal and one spacial dimension, the wave equation is of the form
$$\begin{equation}-u_{tt}+c^2u_{xx}=0\end{equation}$$
This can be rearranged to yield
$$u_{tt}-c^2u_{xx}=(\frac{\partial}{\partial t}-c\frac{\partial}{\partial x})(\frac{\partial}{\partial t}+c\frac{\partial}{\partial x})u = 0$$

### » Proof for the general solution of the 1-D wave equation

Let $\alpha=x+ct$ and $\beta=x-ct$. This gives us
$$x=\frac{1}{2}(\alpha+\beta), \qquad t=\frac{1}{2c}(\alpha-\beta)$$
By the chain rule,
$$\frac{\partial}{\partial x} = \frac{\partial \alpha}{\partial x}\frac{\partial}{\partial \alpha} + \frac{\partial\beta}{\partial x}\frac{\partial}{\partial\beta} = \frac{\partial}{\partial \alpha} + \frac{\partial}{\partial\beta}$$
$$\frac{\partial}{\partial t} = \frac{\partial \alpha}{\partial t}\frac{\partial}{\partial \alpha} + \frac{\partial\beta}{\partial t}\frac{\partial}{\partial\beta} = c(\frac{\partial}{\partial \alpha} - \frac{\partial}{\partial\beta})$$
Then,
$$\frac{\partial}{\partial t}-c\frac{\partial}{\partial x} = c(\frac{\partial}{\partial \alpha} - \frac{\partial}{\partial\beta}) - c(\frac{\partial}{\partial \alpha} + \frac{\partial}{\partial\beta}) = -2c\frac{\partial}{\partial\beta}$$
$$\frac{\partial}{\partial t}+c\frac{\partial}{\partial x} = c(\frac{\partial}{\partial \alpha} - \frac{\partial}{\partial\beta}) + c(\frac{\partial}{\partial \alpha} + \frac{\partial}{\partial\beta}) = 2c\frac{\partial}{\partial\alpha}$$
Substituting in these values, we get
$$u_{tt}-c^2u_{xx}=-4c^2\frac{\partial}{\partial\alpha} \frac{\partial}{\partial\beta}u$$
We can conclude that
$$u(\alpha,\beta)=A(\alpha) + B(\beta)$$
As a result, the general solution for $(1)$ is
$$u(x,t) = f(x+ct) + g(x-ct)$$

### » Proof for d'Alembert's formula

Assume we are provided with the initial conditions $u(x,0)=\phi(x)$ and $\partial_t u(x,0)=\psi(x)$. From these initial conditions, we know that
$$\phi(x)=f(x)+g(x)$$
$$\psi(x)=cf^\prime(x)-cg^\prime(x)$$
We find that
$$\phi^\prime(x)=f^\prime(x)+g^\prime(x)$$
$$\frac{\psi(x)}{c}=f^\prime(x)-g^\prime(x)$$
Solving for $f^\prime$ and $g^\prime$ gives us
$$f^\prime(x)=\frac{1}{2}(\phi^\prime(x)+\frac{\psi(x)}{c}$$
$$g^\prime(x)=\frac{1}{2}(\phi^\prime(x)-\frac{\psi(x)}{c}$$
After integration, we have
$$f(x)=\frac{1}{2}\phi(x) + \frac{1}{2c}\int_0^x \phi(s)\mathop{}\mathrm{d}s + C_1$$
$$g(x)=\frac{1}{2}\phi(x) - \frac{1}{2c}\int_0^x \phi(s)\mathop{}\mathrm{d}s + C_2$$
where $C_1$ and $C_2$ are constants. Since $\phi(x)=f(x)+g(x)$, we know that $C_1+C_2=0$.

Substitution and simplification gives us d'Alembert's formula.
$$\begin{aligned}
u(x,t) &= f(x+ct) + g(x-ct) \\\\ 
&= \frac{1}{2}\phi(x) + \frac{1}{2c}\int_0^x \phi(s)\mathop{}\mathrm{d}s + C_1 + \frac{1}{2}\phi(x) - \frac{1}{2c}\int_0^x \phi(s)\mathop{}\mathrm{d}s + C_2 \\\\
&= \frac{1}{2}[\phi(x+ct)+\phi(x-ct)]+\frac{1}{2c}\int_{x-ct}^{x+ct}\phi(s)\mathop{} \mathrm{d}s
\end{aligned}$$
