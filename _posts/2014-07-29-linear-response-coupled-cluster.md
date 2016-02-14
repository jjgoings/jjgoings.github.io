---
layout: post 
title: Linear Response Coupled Cluster
--- 

Linear response coupled cluster (LR-CC) is a way of getting electronic excitation energies at a coupled cluster level of theory. It's also a general way of getting many response properties, which basically answer the question of "what do molecules do when you poke them"?

Here is a simple derivation of LR-CC, which I like because it parallels the derivation of linear response time-dependent DFT and Hartree Fock. There are much more robust ways to get these results, for example, propagator approaches have been particularly successful when applied to coupled cluster response theory, but I think it can mask a lot of the physics if you aren't careful.

Anyway, here it is.

The coupled cluster ground state equations are given by

$$   \hat{H}^{(0)} e^{\hat{T}^{(0)}} \vert  \phi_0 \rangle = E_{CC}^{(0)} e^{T^{(0)}} \vert  \phi_0 \rangle \ \ \ \ \ (1) $$

Since this is, by definition, a stationary state the following is equivalent

$$   \hat{H}^{(0)} e^{\hat{T}^{(0)}} \vert  \phi_0 \rangle e^{-iE_{CC}^{(0)}t} = E_{CC}^{(0)} e^{T^{(0)}} \vert  \phi_0 \rangle e^{-iE_{CC}^{(0)}t} \ \ \ \ \ (2) $$

Since

$$   \vert \phi(t) \rangle = \vert \phi(0)\rangle e^{-i E t} \ \ \ \ \ (3) $$

Now, perturbing the system with monochromatic light of frequency $$ {\omega} $$ gives us the modified Hamiltonian (in the dipole approximation):

$$   \hat{H} = \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i\omega t} + \hat{f}^{(1)*}e^{i\omega t} \ \ \ \ \ (4) $$

This induces a response to the wavefunction, which is parameterized by the cluster operator $$ {\hat{T}} $$.

$$   \hat{T} = \hat{T}^{(0)} + \hat{R}^{(1)}e^{-i \omega t} + R^{(1)*}e^{i \omega t} + \cdots \ \ \ \ \ (5) $$

The extra terms are higher order responses in the cluster operator. I should also note that this means T and R are in the same excitation manifold: in other words, if T is a single excitation operator, so is R. Same for doubles, triples, etc. Anyway, we are only considering the linear response here. Furthermore, from here on out I won't write the complex conjugate parts. Though they are still there (and I will indicate them by dots), ultimately we collect terms of only $$ {e^{-i \omega t}} $$ to get our final equations. We could collect the conjugates as well, but would get the same equations in the end.

The time dependent Schrödinger equation is

$$   \hat{H}\vert  \psi \rangle = i \frac{\partial}{\partial t} \vert  \psi \rangle \ \ \ \ \ (6) $$

Plugging in the above perturbed expressions yields

$$   \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left( e^{\hat{T}^{(0)} + \hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left( e^{\hat{T}^{(0)} + \hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} \ \ \ \ \ (7) $$

Since $$ {\hat{T^{(0)}}} $$ and $$ {\hat{R}^{(1)}} $$ commute, we can rewrite as

$$   \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left( e^{\hat{T}^{(0)}}e^{\hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left( e^{\hat{T}^{(0)}}e^{\hat{R}^{(1)}e^{-i\omega t} + \cdots} \right) \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} \ \ \ \ \ (8) $$

Expanding the exponential containing $$ {\hat{R}^{(1)}} $$

$$   \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} = i \frac{\partial}{\partial t} \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} \ \ \ \ \ (9) $$

Finally perform the derivation, making sure not to forget the time dependent phase

$$   \left( \hat{H}^{(0)} + \hat{f}^{(1)}e^{-i \omega t} + \cdots \right) \left[e^{\hat{T}^{(0)}}\left(1 + \hat{R}^{(1)}e^{-i\omega t} + \cdots \right) \right] \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} = i e^{\hat{T}^{(0)}} \left(-i \omega {R}^{(1)}e^{-i\omega t} - i E_{CC}^{(0)} \hat{R}^{(1)} e^{-i \omega t} + \cdots \right) \vert \phi_0 \rangle e^{-i E_{CC}^{(0)} t} \ \ \ \ \ (10) $$

Collect terms with $$ {e^{-i\omega t}} $$, cancel out phase factors

$$   \hat{H}^{(0)}e^{\hat{T}^{(0)}} \hat{R}^{(1)} \vert  \phi_0 \rangle + \hat{f}^{(1)} e^{\hat{T}^{(0)}} \vert  \phi_0 \rangle = \omega e^{\hat{T}^{(0)}} \hat{R}^{(1)} \vert  \phi_0 \rangle + E_{CC}^{(0)} e^{\hat{T}^{(0)}} \hat{R}^{(1)} \vert  \phi_0 \rangle \ \ \ \ \ (11) $$

In linear response theory, we assume the perturbation is small and send $$ {\hat{f}^{(1)} \rightarrow 0} $$.

$$   \hat{H}^{(0)}e^{\hat{T}^{(0)}} \hat{R}^{(1)} \vert  \phi_0 \rangle = (\omega + E_{CC}^{(0)}) e^{\hat{T}^{(0)}} \hat{R}^{(1)} \vert  \phi_0 \rangle \ \ \ \ \ (12) $$

Thus the eigenvalues are just the ground state coupled cluster energy plus an excitation energy.

As an aside, it is possible (in fact, this is how LR-CC is done in practice) to get rid of the $$ {E_{CC}^{(0)}} $$ entirely, so that you solve for the excitation energies directly. How? The simplest way to think about it is that when you evaluate the left hand side, you find that it contains expressions for the ground state energy (times $$ {R} $$), so if we leave out these terms when solving the equations, we can solve for the excitation energies directly. In other words we force the ground state energies on both sides to cancel by being careful how we set up the equation. And so we get an equation like so:

$$   (e^{-\hat{T}^{(0)}}\hat{H}^{(0)}e^{\hat{T}^{(0)}})_c \hat{R}^{(1)} \vert  \phi_0 \rangle = \omega \hat{R}^{(1)} \vert  \phi_0 \rangle \ \ \ \ \ (13) $$

Here's the more jargony answer: if you apply Wick's theorem to the Hausdorff expansion of the similarity transformed coupled cluster Hamiltonian, you retain only terms that share a sum with each other. Diagrammatically, this means we keep only the connected diagrams. If you go ahead and derive all diagrams, connected and disconnected, you find that the disconnected diagrams correspond exactly to the terms you want to cancel on the right.

