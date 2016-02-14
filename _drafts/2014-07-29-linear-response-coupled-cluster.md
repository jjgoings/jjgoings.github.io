---
layout: post 
title: Linear Response Coupled Cluster
--- 

Linear response coupled cluster (LR-CC) is a way of getting electronic excitation energies at a coupled cluster level of theory. It's also a general way of getting many response properties, which basically answer the question of "what do molecules do when you poke them"?

Here is a simple derivation of LR-CC, which I like because it parallels the derivation of linear response time-dependent DFT and Hartree Fock. There are much more robust ways to get these results, for example, propagator approaches have been particularly successful when applied to coupled cluster response theory, but I think it can mask a lot of the physics if you aren't careful.

Anyway, here it is.

Oh! And here is the [PDF](https://joshuagoings.files.wordpress.com/2014/07/lrcc.pdf). I forget to attach it sometimes.

The coupled cluster ground state equations are given by

$latex \displaystyle \hat{H}^{(0)} e^{\hat{T}^{(0)}} | \phi\_0 \rangle = E\_{CC}^{(0)} e^{T^{(0)}} | \phi\_0 \rangle \ \ \ \ \ (1)&fg=000000$

Since this is, by definition, a stationary state the following is equivalent

$latex \displaystyle \hat{H}^{(0)} e^{\hat{T}^{(0)}} | \phi\_0 \rangle e^{-iE\_{CC}^{(0)}t} = E\_{CC}^{(0)} e^{T^{(0)}} | \phi\_0 \rangle e^{-iE\_{CC}^{(0)}t} \ \ \ \ \ (2)&fg=000000$

Since

$latex \displaystyle |\phi(t) \rangle = |\phi(0)\rangle e^{-i E t} \ \ \ \ \ (3)&fg=000000$

Now, perturbing the system with monochromatic light of frequency $latex {\omega}&fg=000000$ gives us the modified Hamiltonian (in the dipole approximation):

$latex \displaystyle \hat{H} = \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i\omega t} + \hat{f}^{(1)\*}e^{i\omega t} \ \ \ \ \ (4)&fg=000000$

This induces a response to the wavefunction, which is parameterized by the cluster operator $latex {\hat{T}}&fg=000000$.

$latex \displaystyle \hat{T} = \hat{T}^{(0)} + \hat{R}^{(1)}e^{-i \omega t} + R^{(1)\*}e^{i \omega t} + \cdots \ \ \ \ \ (5)&fg=000000$

The extra terms are higher order responses in the cluster operator. I should also note that this means T and R are in the same excitation manifold: in other words, if T is a single excitation operator, so is R. Same for doubles, triples, etc. Anyway, we are only considering&nbsp;the linear response here. Furthermore, from here on out I won't write the complex conjugate parts. Though they are still there (and I will indicate them by dots), ultimately we collect terms of only $latex {e^{-i \omega t}}&fg=000000$ to get our final equations. We could collect the conjugates as well, but would get the same equations in the end.

The time dependent Schrödinger equation is

$latex \displaystyle \hat{H}| \psi \rangle = i \frac{\partial}{\partial t} | \psi \rangle \ \ \ \ \ (6)&fg=000000$

Plugging in the above perturbed expressions yields

$latex \displaystyle \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left( e^{\hat{T}^{(0)} + \hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left( e^{\hat{T}^{(0)} + \hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} \ \ \ \ \ (7)&fg=000000$

Since $latex {\hat{T^{(0)}}}&fg=000000$ and $latex {\hat{R}^{(1)}}&fg=000000$ commute, we can rewrite as

$latex \displaystyle \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left( e^{\hat{T}^{(0)}}e^{\hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left( e^{\hat{T}^{(0)}}e^{\hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} \ \ \ \ \ (8)&fg=000000$

Expanding the exponential containing $latex {\hat{R}^{(1)}}&fg=000000$

$latex \displaystyle \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} \ \ \ \ \ (9)&fg=000000$

Finally perform the derivation, making sure not to forget the time dependent phase

$latex \displaystyle \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} = i e^{\hat{T}^{(0)}} \left(-i \omega {R}^{(1)}e^{-i\omega t} - i E\_{CC}^{(0)} \hat{R}^{(1)} e^{-i \omega t} + \cdots \right) |\phi\_0 \rangle e^{-i E\_{CC}^{(0)} t} \ \ \ \ \ (10)&fg=000000$

Collect terms with $latex {e^{-i\omega t}}&fg=000000$, cancel out phase factors

$latex \displaystyle \hat{H}^{(0)}e^{\hat{T}^{(0)}} \hat{R}^{(1)} | \phi\_0 \rangle + \hat{f}^{(1)} e^{\hat{T}^{(0)}} | \phi\_0 \rangle = \omega e^{\hat{T}^{(0)}} \hat{R}^{(1)} | \phi\_0 \rangle + E\_{CC}^{(0)} e^{\hat{T}^{(0)}} \hat{R}^{(1)} | \phi\_0 \rangle \ \ \ \ \ (11)&fg=000000$

In linear response theory, we assume the perturbation is small and send $latex {\hat{f}^{(1)} \rightarrow 0}&fg=000000$.

$latex \displaystyle \hat{H}^{(0)}e^{\hat{T}^{(0)}} \hat{R}^{(1)} | \phi\_0 \rangle = (\omega + E\_{CC}^{(0)}) e^{\hat{T}^{(0)}} \hat{R}^{(1)} | \phi\_0 \rangle \ \ \ \ \ (12)&fg=000000$

Thus the eigenvalues are just the ground state coupled cluster energy plus an excitation energy.

As an aside, it is possible (in fact, this is how LR-CC is done in practice) to get rid of the $latex {E\_{CC}^{(0)}}&fg=000000$ entirely, so that you solve for the excitation energies directly. How? The simplest way to think about it is that when you evaluate the left hand side, you find that it contains expressions for the ground state energy (times $latex {R}&fg=000000$), so if we leave out these terms when solving the equations, we can solve for the excitation energies directly. In other words we force the ground state energies on both sides to cancel by being careful how we set up the equation. And so we get an equation like so:

$latex \displaystyle (e^{-\hat{T}^{(0)}}\hat{H}^{(0)}e^{\hat{T}^{(0)}})\_c \hat{R}^{(1)} | \phi\_0 \rangle = \omega \hat{R}^{(1)} | \phi\_0 \rangle \ \ \ \ \ (13)&fg=000000$

Here's the more jargony answer: if you apply Wick's theorem to the Hausdorff expansion of the similarity transformed coupled cluster Hamiltonian, you retain only terms that share a sum with each other. Diagrammatically, this means we keep only the connected diagrams. If you go ahead and derive all diagrams, connected and disconnected, you find that the disconnected diagrams correspond exactly to the terms you want to cancel on the right.

