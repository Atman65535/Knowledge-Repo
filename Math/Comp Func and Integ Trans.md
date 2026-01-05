# Complex Function
contains real part and imagine part.
- argz 
	-  $\arctan{z} + \pi$ or $-\pi$ , $2k \pi$ 
	- not continuious on negative real axis
- Cauchy-Riemann
	- $\frac{\partial u}{\partial x} =\frac{\partial v}{\partial y} \ \frac{\partial u}{\partial y} = - \frac{\partial v}{\partial x}$  
	- $f'(x) = \frac{\partial f}{\partial x}$ 


# Cauchy Integral and High order Deviate
- if analytic:
$$
\int_C f(z)dz = 0
$$
$$
\int_c \frac{f(\zeta)}{\zeta - z}d\zeta = 2\pi i f(z)
$$
- then cauchy high order deviate
$$
f^{(n)}(z) = \frac{n!}{2 \pi i} \int_C \frac{f(\zeta)}{(\zeta - z)^{n+1}}d\zeta
$$

# Laurent and Residual
- Laurent: series presentation of function in ring regions. All.
	![[LaurentSeries.png]]
- Residuals $c_{-1}$

- Residual of $\infty$:$-c_{-1}$ of the Laurent Series.
$$
\Sigma Res[f(z), s_i] + Res[f(z), \infty] = 0
$$
- Solve Residuals:
	- when the numerator is not zero, denominator is One Order zero point:
$$
Res[f(z), s] = \frac{ \phi (z))}{\psi '(z)}
$$
		The denomenator can be $\sin z$ $\cos z$ and $\tan z$
	- High order deriviate 
$$
Res[f(z), s_k] = \frac{1}{(k-1)!} [\frac{d^{(n-1)}(z-z_0)^kf(z)}{dz^{(n-1)}} ]
$$

>[!warning] The factorial
>When we use Gaussian Deriviate Formula, the factorial term is on numerator, while it is on denominator when solving residuals.


# Fourier and Laplacian Transformation
>*Those Fucking Traits and integral results are never used!*
>*Forget them after the exam.*

- Basic concept:
	- When a function contains finit one class break point, $\int_{-\infty}^{+\infty} |f(t)|dt$ is convergent.
	- we can get its Fourier Transformation and inverse Fourier. ***Break point*** take $\frac{(f(b^+) + f(b^-)}{2}$ !
- some integral charts
$$
u(t)e^{-kt} = \frac{1}{s + k} \ \ \ or \ \ \ = \frac{1}{iw + k}
$$
$$
F[u(t)] = \frac{1}{i\omega} + \pi\delta(w)
$$
	All are add.
$$
\int_{-\infty}^{+\infty} e^{-i(\omega + \omega_0)t}dt = 2 \pi \delta(w+w_0) 
$$
$$
\int_{-\infty}^{+\infty}e^{i\omega(t+t_0)}d\omega = 2\pi\delta(t+t_0)
$$
$$
\int_0^{+\infty} \frac{\sin ax}{x} = \frac \pi 2 \ if (a> 0)
$$
>[!warning] This is not Fourier Inverse !

- fucking traits.

|                   | Fourier                                                         | Laplacian                                      | Relationship                              |
| ----------------- | --------------------------------------------------------------- | ---------------------------------------------- | ----------------------------------------- |
| Trans             | $F[e^{i \omega_0 t}f(t)] = F(\omega - \omega_0)$                | $F[e^{\alpha t}f(t)] = F(s - \alpha)$          | exponential to linear                     |
| Delay             | $F[f(t - t_0)] = e^{-i\omega t_0}F(\omega)$                     | $F[f(t-t_0)u(t-t_0) = e^{-st_0F(s)}$           | $i\omega$ is $s$, never early             |
| Diff              | $F[f'(t)] = i\omega F(\omega)$                                  | $F[f'(t)] = sF(s) - f(0)$                      | Integ by part rathe                       |
|                   | $F'(\omega) = F[-itf(t)]$                                       | $F'(s) = F[-tf(t)]$                            | cuz no $i$ in Laplacian                   |
| Integ             | $F[\int_{-\infty}^t f(\tau)d\tau] = \frac{1}{i\omega}F(\omega)$ | $F[\int_{0}^t f(\tau)d\tau] = \frac{1}{s}F(s)$ | $i\omega$ to $s$                          |
| $u(t)$            | $F[u(t)] = \frac 1 {i\omega} + \pi\delta(w)$                    | $F[u(t)] = \frac 1 s$                          | $i\omega$ to $s$                          |
| $\delta^{(n)}(t)$ | $F[\delta^{(n)}(t)] = (i\omega)^n$                              | $F[\delta^{(n)}(t)] = (s)^n$                   | $\int \delta^{(n)}(t)f(t) = - f^{(n)}(0)$ |
<p align="center">A piece of shit</p>

---

<p align="right"><em>Complex Variable Function Review Stops Here</em></p>
