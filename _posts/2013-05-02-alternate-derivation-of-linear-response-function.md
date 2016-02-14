--- 
layout: post 
title: Alternate derivation of linear response function 
---

I've given a derivation before of the density-density response function, but today I want to give an alternate derivation of the more general [linear-response function](http://en.wikipedia.org/wiki/Linear_response_function "Linear response function"), which will prove to be useful in the derivation of the time-dependent Hartree-Fock equations (TDHF), also known in the nuclear physics community as the [Random Phase Approximation](http://en.wikipedia.org/wiki/Random_phase_approximation "Random phase approximation") (RPA). This derivation is largely taken from McWeeny (1989).

In order to derive the response function --- also called frequency-dependent polarizability --- we must first partition the Hamiltonian into two parts: the time-independent Hamiltonian, and the time dependent response:

$$   H = H_0 + H'(t) \ \ \ \ \ (1) $$

Furthermore, the time-dependent [Schrodinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation") is given as:

$$   H\Psi = i\hbar\frac{\partial \Psi}{\partial t} \ \ \ \ \ (2) $$

In the interaction picture, $$ {\Psi'_0(t) = \Psi'_0e^{-iE_0t/\hbar}} $$. Thus we can partition the time-dependent wavefunction (expanding over basis of complete eigenstates) as

$$   \Psi'_0(t) = \sum\limits_n c_n(t)\Psi_n \notag \ \ \ \ \ (3) $$

$$   \Psi'_0e^{-iE_0t/\hbar } =\sum\limits_n c_n(t)e^{-iE_0t/\hbar}\Psi_n \ \ \ \ \ (4) $$

$$   \Psi'_0 = \Psi_0 + \sum\limits_{n\neq0} c_n(t)e^{-i\omega_{0n}t}\Psi_n \ \ \ \ \ (5) $$

Where

$$   \omega_{0n} = (E_n - E_0)/\hbar \ \ \ \ \ (6) $$

are real, positive, _exact_ excitation frequencies of unperturbed system. Note that $$ {c_0(t) = 1} $$. We are assuming that $$ {H'(t)} $$ is turned on slowly at time $$ {t \rightarrow -\infty} $$. Substitute 1 and 3 into 2, separate the orders, and impose the boundary conditions that $$ {c_0 = 1} $$ and $$ {c_m = 0} $$ $$ {(n\neq0)} $$ at $$ {t \rightarrow -\infty} $$. This gives

$$   i\hbar\dot{c}_n = \langle n \vert  H'(t) \vert  0 \rangle e^{i\omega_{0n}t} \ \ \ \ \ (7) $$

If we let

$$   H'(t) = F(t)A \ \ \ \ \ (8) $$

Where a 'fixed' [Hermitian operator](http://en.wikipedia.org/wiki/Self-adjoint_operator "Self-adjoint operator") $$ {A} $$ determines the `shape' of the perturbation, while time dependence is confined to the (real) 'strength' factor $$ {F(t)} $$. For a perturbation beginning at time $$ {t \rightarrow -\infty} $$ up to time $$ {t} $$,

$$   c_n(t) = (i\hbar)^{-1}\int\limits_{-\infty}^{t} \langle n \vert  A \vert  0 \rangle F(t') e^{i\omega_{0n}t'}dt' \ \ \ \ \ (9) $$

Which, to first order, determines the perturbed wavefunction. Now we are interested not in the perturbed wavefunction _per se_, but rather in the response of an observable $$ {O} $$ to the perturbation.

$$   \delta\langle O \rangle = \langle O \rangle - \langle O \rangle_0 = \int\limits_{-\infty}^{t} K(OA\vert t-t')F(t')dt' \ \ \ \ \ (10) $$

where

$$   K(OA\vert t-t') = (i\hbar)^{-1} \sum\limits_{n\neq0} [\langle 0 \vert  O \vert  n \rangle\langle n \vert  A \vert  0 \rangle e^{-i\omega_{0n}(t-t')} - \langle 0 \vert  A \vert  n \rangle\langle n \vert  O \vert  0 \rangle e^{i\omega_{0n}(t-t')}] \ \ \ \ \ (11) $$

This is a time correlation function, relating fluctuation of $$ {\langle O \rangle} $$ at time t to the strength of the perturbation $$ {A} $$ at some earlier time $$ {t'} $$. $$ {K(OA\vert t-t')} $$ is defined only for $$ {t'<t} $$, in accordance with the principle of causality. Thus, it is a function only of the difference $$ {\tau = t - t'} $$. Recalling the definitions of the Fourier transform $$ {f(\omega)} $$:

$$   f(\omega) = \int\limits_{-\infty}^{\infty} F(t) e^{i\omega t} dt \ \ \ \ \ (12) $$

Then instead of 8, we have:

$$   H'(t) = \frac{1}{2\pi} \int\limits_{-\infty}^{\infty} f(\omega) A_{\omega} e^{-i\omega t} d\omega \ \ \ \ \ (13) $$

Requiring $$ {H'(t)} $$ to be Hermitian,

$$   H'(t) = H'(t)^{\dagger} \ \ \ \ \ (14) $$

$$   \frac{1}{2\pi} \int\limits_{-\infty}^{\infty} f(\omega) A_{\omega} e^{-i\omega t} d\omega = \frac{1}{2\pi} \int\limits_{-\infty}^{\infty} f(-\omega) A^{\dagger}_{\omega} e^{i\omega t} d\omega \notag \ \ \ \ \ (15) $$

Now,

$$   A_{-\omega} = A_{\omega}^{\dagger} \ \ \ \ \ (16) $$

$$   f(-\omega) = f(\omega) \ \ \ \ \ (17) $$

Which, upon combining the expressions for $$ {H'(t)} $$ so as to `Hermitize' the expression:

$$   2H'(t) = \frac{1}{2\pi} \int\limits_{-\infty}^{\infty} (f(\omega) A_{\omega} e^{-i\omega t} + f(\omega) A_{-\omega} e^{i\omega t}) d\omega \notag \ \ \ \ \ (18) $$

$$   H'(t) = \frac{1}{2\pi} \int\limits_{-\infty}^{\infty} f(\omega) \frac{1}{2} (A_{\omega} e^{-i\omega t} + A_{-\omega} e^{i\omega t}) d\omega \ \ \ \ \ (19) $$

Thus

$$   A = \frac{1}{2}(A_{\omega} + A_{-\omega}) \ \ \ \ \ (20) $$

with $$ {F(t)} $$ real. Instead of working in the [time domain](http://en.wikipedia.org/wiki/Time_domain "Time domain"), we may also consider the response in terms of a single oscillatory perturbation. This means that

$$   H'(\omega) = \frac{1}{2} (A_{\omega} e^{-i\omega t} + A_{-\omega} e^{i\omega t}) \ \ \ \ \ (21) $$

To ensure $$ {H'(\omega)} $$ builds smoothly from zero at $$ {t \rightarrow -\infty} $$, we can introduce a convergence factor $$ {e^{\eta t}} $$ with the initial condition $$ {c_0 = 1} $$ and $$ {c_n = 0} $$, which gives:

$$   c_n(t) = \lim_{\eta \rightarrow 0} \left(-\frac{1}{2\hbar}\right) \left\{ \frac{\langle n \vert  A_{\omega} \vert  0\rangle}{\omega_{0n} - \omega - i\eta} e^{i(\omega_{0n} - \omega - i\eta)t} + \frac{\langle n \vert  A_{-\omega} \vert  0\rangle}{\omega_{0n} + \omega - i\eta} e^{i(\omega_{0n} + \omega - i\eta)t} \right\} \ \ \ \ \ (22) $$

Then, collecting terms of $$ {\pm \omega} $$:

$$   \delta \langle O \rangle = \frac{1}{2} \left[\Pi(OA_{\omega}\vert \omega)e^{-i\omega t} + \Pi(OA_{-\omega}\vert -\omega)e^{i\omega t} \right] \ \ \ \ \ (23) $$

Finally:

$$   \Pi(OA_{\omega} \vert  \omega) = \lim_{\eta \rightarrow 0} \left(\frac{1}{\hbar}\right) \sum\limits_{n\neq0} \left\{ \frac{\langle 0 \vert  O \vert  n\rangle\langle n \vert  A_{\omega}\vert 0\rangle}{\omega + i\eta - \omega_{0n}} - \frac{\langle 0 \vert  A_{\omega} \vert  n\rangle \langle n \vert  O \vert  0 \rangle}{\omega + i\eta + \omega_{0n}} \right\} \ \ \ \ \ (24) $$

Which is the response function, or frequency-dependent polarizability.

