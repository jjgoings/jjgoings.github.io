--- 
layout: post 
title: Alternate derivation of linear response function 
---

[PDF copy of below](http://joshuagoings.files.wordpress.com/2013/06/responsefunction.pdf)

I've given a derivation before of the [density-density response function](http://joshuagoings.wordpress.com/2013/04/27/linear-response-td-dft-the-density-density-response-function/ "Linear Response TD-DFT: The density-density response function"), but today I want to give an alternate derivation of the more general [linear-response function](http://en.wikipedia.org/wiki/Linear_response_function "Linear response function"), which will prove to be useful in the derivation of the time-dependent Hartree-Fock equations (TDHF), also known in the nuclear physics community as the [Random Phase Approximation](http://en.wikipedia.org/wiki/Random_phase_approximation "Random phase approximation") (RPA). This derivation is largely taken from McWeeny (1989).

In order to derive the response function --- also called frequency-dependent polarizability --- we must first partition the Hamiltonian into two parts: the time-independent Hamiltonian, and the time dependent response:

$$ \displaystyle H = H\_0 + H'(t) \ \ \ \ \ (1)&fg=000000$$

Furthermore, the time-dependent [Schrodinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation") is given as:

$$ \displaystyle H\Psi = i\hbar\frac{\partial \Psi}{\partial t} \ \ \ \ \ (2)&fg=000000$$

In the interaction picture, $$ {\Psi'\_0(t) = \Psi'\_0e^{-iE\_0t/\hbar}}&fg=000000$$. Thus we can partition the time-dependent wavefunction (expanding over basis of complete eigenstates) as

$$ \displaystyle \Psi'\_0(t) = \sum\limits\_n c\_n(t)\Psi\_n \notag \ \ \ \ \ (3)&fg=000000$$

$$ \displaystyle \Psi'\_0e^{-iE\_0t/\hbar } =\sum\limits\_n c\_n(t)e^{-iE\_0t/\hbar}\Psi\_n \ \ \ \ \ (4)&fg=000000$$

$$ \displaystyle \Psi'\_0 = \Psi\_0 + \sum\limits\_{n\neq0} c\_n(t)e^{-i\omega\_{0n}t}\Psi\_n \ \ \ \ \ (5)&fg=000000$$

Where

$$ \displaystyle \omega\_{0n} = (E\_n - E\_0)/\hbar \ \ \ \ \ (6)&fg=000000$$

are real, positive, _exact_ excitation frequencies of unperturbed system. Note that $$ {c\_0(t) = 1}&fg=000000$$. We are assuming that $$ {H'(t)}&fg=000000$$ is turned on slowly at time $$ {t \rightarrow -\infty}&fg=000000$$. Substitute 1 and 3 into 2, separate the orders, and impose the boundary conditions that $$ {c\_0 = 1}&fg=000000$$ and $$ {c\_m = 0}&fg=000000$$ $$ {(n\neq0)}&fg=000000$$ at $$ {t \rightarrow -\infty}&fg=000000$$. This gives

$$ \displaystyle i\hbar\dot{c}\_n = \langle n | H'(t) | 0 \rangle e^{i\omega\_{0n}t} \ \ \ \ \ (7)&fg=000000$$

If we let

$$ \displaystyle H'(t) = F(t)A \ \ \ \ \ (8)&fg=000000$$

Where a 'fixed' [Hermitian operator](http://en.wikipedia.org/wiki/Self-adjoint_operator "Self-adjoint operator") $$ {A}&fg=000000$$ determines the `shape' of the perturbation, while time dependence is confined to the (real) 'strength' factor $$ {F(t)}&fg=000000$$. For a perturbation beginning at time $$ {t \rightarrow -\infty}&fg=000000$$ up to time $$ {t}&fg=000000$$,

$$ \displaystyle c\_n(t) = (i\hbar)^{-1}\int\limits\_{-\infty}^{t} \langle n | A | 0 \rangle F(t') e^{i\omega\_{0n}t'}dt' \ \ \ \ \ (9)&fg=000000$$

Which, to first order, determines the perturbed wavefunction. Now we are interested not in the perturbed wavefunction _per se_, but rather in the response of an observable $$ {O}&fg=000000$$ to the perturbation.

$$ \displaystyle \delta\langle O \rangle = \langle O \rangle - \langle O \rangle\_0 = \int\limits\_{-\infty}^{t} K(OA|t-t')F(t')dt' \ \ \ \ \ (10)&fg=000000$$

where

$$ \displaystyle K(OA|t-t') = (i\hbar)^{-1} \sum\limits\_{n\neq0} [\langle 0 | O | n \rangle\langle n | A | 0 \rangle e^{-i\omega\_{0n}(t-t')} - \langle 0 | A | n \rangle\langle n | O | 0 \rangle e^{i\omega\_{0n}(t-t')}] \ \ \ \ \ (11)&fg=000000$$

This is a time correlation function, relating fluctuation of $$ {\langle O \rangle}&fg=000000$$ at time t to the strength of the perturbation $$ {A}&fg=000000$$ at some earlier time $$ {t'}&fg=000000$$. $$ {K(OA|t-t')}&fg=000000$$ is defined only for $$ {t'\<t}&fg=000000$$, in accordance with the principle of causality. Thus, it is a function only of the difference $$ {\tau = t - t'}&fg=000000$$. Recalling the definitions of the Fourier transform $$ {f(\omega)}&fg=000000$$:

$$ \displaystyle f(\omega) = \int\limits\_{-\infty}^{\infty} F(t) e^{i\omega t} dt \ \ \ \ \ (12)&fg=000000$$

Then instead of 8, we have:

$$ \displaystyle H'(t) = \frac{1}{2\pi} \int\limits\_{-\infty}^{\infty} f(\omega) A\_{\omega} e^{-i\omega t} d\omega \ \ \ \ \ (13)&fg=000000$$

Requiring $$ {H'(t)}&fg=000000$$ to be Hermitian,

$$ \displaystyle H'(t) = H'(t)^{\dagger} \ \ \ \ \ (14)&fg=000000$$

$$ \displaystyle \frac{1}{2\pi} \int\limits\_{-\infty}^{\infty} f(\omega) A\_{\omega} e^{-i\omega t} d\omega = \frac{1}{2\pi} \int\limits\_{-\infty}^{\infty} f(-\omega) A^{\dagger}\_{\omega} e^{i\omega t} d\omega \notag \ \ \ \ \ (15)&fg=000000$$

Now,

$$ \displaystyle A\_{-\omega} = A\_{\omega}^{\dagger} \ \ \ \ \ (16)&fg=000000$$

$$ \displaystyle f(-\omega) = f(\omega) \ \ \ \ \ (17)&fg=000000$$

Which, upon combining the expressions for $$ {H'(t)}&fg=000000$$ so as to `Hermitize' the expression:

$$ \displaystyle 2H'(t) = \frac{1}{2\pi} \int\limits\_{-\infty}^{\infty} (f(\omega) A\_{\omega} e^{-i\omega t} + f(\omega) A\_{-\omega} e^{i\omega t}) d\omega \notag \ \ \ \ \ (18)&fg=000000$$

$$ \displaystyle H'(t) = \frac{1}{2\pi} \int\limits\_{-\infty}^{\infty} f(\omega) \frac{1}{2} (A\_{\omega} e^{-i\omega t} + A\_{-\omega} e^{i\omega t}) d\omega \ \ \ \ \ (19)&fg=000000$$

Thus

$$ \displaystyle A = \frac{1}{2}(A\_{\omega} + A\_{-\omega}) \ \ \ \ \ (20)&fg=000000$$

with $$ {F(t)}&fg=000000$$ real. Instead of working in the [time domain](http://en.wikipedia.org/wiki/Time_domain "Time domain"), we may also consider the response in terms of a single oscillatory perturbation. This means that

$$ \displaystyle H'(\omega) = \frac{1}{2} (A\_{\omega} e^{-i\omega t} + A\_{-\omega} e^{i\omega t}) \ \ \ \ \ (21)&fg=000000$$

To ensure $$ {H'(\omega)}&fg=000000$$ builds smoothly from zero at $$ {t \rightarrow -\infty}&fg=000000$$, we can introduce a convergence factor $$ {e^{\eta t}}&fg=000000$$ with the initial condition $$ {c\_0 = 1}&fg=000000$$ and $$ {c\_n = 0}&fg=000000$$, which gives:

$$ \displaystyle c\_n(t) = \lim\_{\eta \rightarrow 0} \left(-\frac{1}{2\hbar}\right) \left\{ \frac{\langle n | A\_{\omega} | 0\rangle}{\omega\_{0n} - \omega - i\eta} e^{i(\omega\_{0n} - \omega - i\eta)t} + \frac{\langle n | A\_{-\omega} | 0\rangle}{\omega\_{0n} + \omega - i\eta} e^{i(\omega\_{0n} + \omega - i\eta)t} \right\} \ \ \ \ \ (22)&fg=000000$$

Then, collecting terms of $$ {\pm \omega}&fg=000000$$:

$$ \displaystyle \delta \langle O \rangle = \frac{1}{2} \left[\Pi(OA\_{\omega}|\omega)e^{-i\omega t} + \Pi(OA\_{-\omega}|-\omega)e^{i\omega t} \right] \ \ \ \ \ (23)&fg=000000$$

Finally:

$$ \displaystyle \Pi(OA\_{\omega} | \omega) = \lim\_{\eta \rightarrow 0} \left(\frac{1}{\hbar}\right) \sum\limits\_{n\neq0} \left\{ \frac{\langle 0 | O | n\rangle\langle n | A\_{\omega}|0\rangle}{\omega + i\eta - \omega\_{0n}} - \frac{\langle 0 | A\_{\omega} | n\rangle \langle n | O | 0 \rangle}{\omega + i\eta + \omega\_{0n}} \right\} \ \ \ \ \ (24)&fg=000000$$

Which is the response function, or frequency-dependent polarizability.

\*Typeset using [_latex2wp_](http://lucatrevisan.wordpress.com/latex-to-wordpress/)

