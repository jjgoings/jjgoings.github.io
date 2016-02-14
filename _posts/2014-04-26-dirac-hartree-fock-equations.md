---
layout: post 
title: Dirac Hartree Fock equations 
---

I wanted to try and understand more of how the physical picture changes going from non-relativistic theories to relativistic theories in electronic structure theory. So I figured a good place to start would be with the relativistic analog to the Hartree-Fock theory we know and love so well :)

Why do I care about relativistic electronic structure theory? It is the most fundamental theory of molecular science we have available! In particular, it is the most natural way to model and understand spin in molecules: molecular magnets, spin-orbit couplings, and high-energy spectroscopy all intrinsically depend on a theory of molecules that includes special relativity and a first principles treatment of spin. It also explains the reactivity (or lack thereof) of heavy metals, as well as their colors and properties. Did you know that if we did not include special relativity in our theories we'd predict gold to be silver instead of yellow? It's just one of the reasons I think the next decade or so will refine relativistic electronic structure theory into the de facto theory of molecules. Kind of like what coupled cluster did to the electron correlation problem over the past few decades, relativistic theories are maturing fast and should become standard in your favorite quantum chemistry packages. Anyway...

The Dirac-Hartree-Fock (DHF) operator for a single determinant wave function in terms of atomic spinors is identical to that in terms of atomic orbitals. The derivation is the same: you find the energetic stationary point with respect to spinor (orbital) rotations. Thus we start with the DHF operator:

$$   f_{pq} = h_{pq} + \sum\limits_{i}^{N} \left( pq \vert \vert  ii \right) \ \ \ \ \ (1) $$

The first term, $$ {h_{pq}} $$, is the one-electron part. The second term is the two-electron part. We will look at the one-electron part first. For $$ {h_{pq}} $$, we (obviously) cannot use the Schrödinger equation equivalent. Instead, we use the Dirac equation, which is the relativistic equation for a single electron. In two-spinor form, where

$$   \psi = \left( \begin{array}{c} \psi^{L} \\ \psi^{S} \end{array} \right) \ \ \ \ \ (2) $$

(Which is to say $$ {\psi^{L}} $$ is the large component and $$ {\psi^{S}} $$ is the small component.) We have the expression

$$   \left[\begin{array}{cc} V-E & c(\mathbf{\sigma}\cdot\mathbf{p}) \\ c(\mathbf{\sigma}\cdot\mathbf{p}) & V-E-2mc^2 \end{array} \right] \left[\begin{array}{c} \psi^{L} \\ \psi^{S} \end{array} \right] = 0 \ \ \ \ \ (3) $$

In this case $$ {c} $$ is the speed of light and $$ {m} $$ is the electron rest mass. $$ {V} $$ is the potential, which in the non-relativistic case is the point charge nucleus, though in general relativistic quantum chemistry assumes a finite nucleus. The bold operators are vectors, for example momentum $$ {\mathbf{p} = (p_x, p_y, p_z)} $$. Same with the Pauli operators. Now we will expand $$ {\psi^L} $$ and $$ {\psi^S} $$ in a basis. Again, the bold type means a vector.

$$   \psi^L = \vert \chi^L \rangle \mathbf{c}^L; \qquad \psi^S = \vert \chi^S \rangle \mathbf{c}^S \ \ \ \ \ (4) $$

The $$ {\mathbf{c}} $$ is a column vector containing the basis coefficients, just like in non-relativistic Hartree-Fock theory. Similarly, the $$ {\vert \chi \rangle} $$ ket is our basis. Inserting these expressions and multiplying on the left by $$ {\left[\langle \chi^L \vert  \quad \langle \chi^S \vert  \right]} $$ (compare with Szabo and Ostlund p. 137) we transform the integro-differential equations into a matrix equation.

$$   \left[\begin{array}{cc} \langle \chi^L \vert  V \vert  \chi^L \rangle - E\langle \chi^L \vert  \chi^L \rangle & c\langle \chi^L \vert  -i\hbar \mathbf{\sigma}\cdot\mathbf{\nabla} \vert  \chi^S \rangle \\ c\langle \chi^S \vert  -i\hbar \mathbf{\sigma}\cdot\mathbf{\nabla} \vert  \chi^L \rangle & \langle \chi^S \vert  V \vert  \chi^S \rangle - (2mc^2 +E) \langle \chi^S \vert  \chi^S \rangle \end{array} \right] \left[\begin{array}{c} \mathbf{c}^L \\ \mathbf{c}^S \end{array} \right] = 0 \ \ \ \ \ (5) $$

Which, we will simplify to

$$   \left[\begin{array}{cc} \mathbf{V}^{LL} - E\mathbf{S}^{LL} & c\mathbf{\Pi}^{LS} \\ c\mathbf{\Pi}^{SL} & \mathbf{V}^{SS} - (2mc^2 +E) \mathbf{S}^{SS} \end{array} \right] \left[\begin{array}{c} \mathbf{c}^L \\ \mathbf{c}^S \end{array} \right] = 0 \ \ \ \ \ (6) $$

Hopefully, it is obvious we made the notational replacements

$$   \mathbf{V}^{LL} = \langle \chi^L \vert  V \vert  \chi^L \rangle; \quad \mathbf{S}^{LL} = \langle \chi^L \vert  \chi^L \rangle; \quad \mathbf{\Pi}^{LS} = \langle \chi^L \vert  -i\hbar \mathbf{\sigma}\cdot\mathbf{\nabla} \vert  \chi^S \rangle; ~\hbox{etc.} \ \ \ \ \ (7) $$

For the DHF equations, we will slide the parts containing energy $$ {E} $$ over to the right hand side to recover the eigenvalue equation. We must now consider the analog to the Coulomb and exchange integrals in the non-relativistic HF equations to the relativistic Dirac equations. There are a few extra things to consider. The first is made clearest if we recall the definition of the two electron integrals (in Mulliken notation) for the non relativistic case. In general, we have

$$   (pq\vert rs) = \int\int \psi^{*}_p(\mathbf{r}_1) \psi_q(\mathbf{r}_1) \frac{1}{r_{12}} \psi^{*}_r(\mathbf{r}_2) \psi_s(\mathbf{r}_2)d\mathbf{r}_1d\mathbf{r}_2 \ \ \ \ \ (8) $$

In the relativistic case, we swap the orbitals $$ {\psi} $$ with their four-component spinors. We will have the same equation as above, except instead of the complex conjugate, we have the adjoint.

$$   (pq\vert rs) = \int\int \psi^{\dagger}_p(\mathbf{r}_1) \psi_q(\mathbf{r}_1) \frac{1}{r_{12}} \psi^{\dagger}_r(\mathbf{r}_2) \psi_s(\mathbf{r}_2)d\mathbf{r}_1d\mathbf{r}_2 \ \ \ \ \ (9) $$

This slight change is just because we aren't dealing with scalar functions anymore. For the most part things stay the same (at least in appearance), and we deal with charge distributions between two four spinors (in two spinor form) like so:

$$   \psi_p^{\dagger}\psi_q = \left( \psi_p^{L\dagger} \psi_p^{S\dagger} \right) \left( \begin{array}{c} \psi_q^{L} \\ \psi_q^S \end{array} \right) = \psi_p^{L\dagger}\psi_q^{L} + \psi_p^{S\dagger}\psi_q^{S} \ \ \ \ \ (10) $$

So it is ever so slightly more involved, but nothing too out of the ordinary. Extending this idea to the two electron integrals gives

$$   (pq\vert rs) = (p^{L}q^{L}\vert r^{L}s^{L}) + (p^{L}q^{L}\vert r^{S}s^{S}) + (p^{S}q^{S}\vert r^{L}s^{L}) + (p^{S}q^{S}\vert r^{S}s^{S}) \ \ \ \ \ (11) $$

Okay. Now implicit to all of this so far is that the interaction between two charge densities is just Coulombic and hasn't changed going from non relativistic to relativistic theories. This is not really the case, because the Coulombic interaction assumes an instantaneous response between electrons. QED tells us that this interaction is mediated by photons and therefore the interaction cannot occur any faster than the speed of light. In other words, there is a retardation effect between electrons that we must account for. This correction to the Coulomb interaction is called the Breit interaction, given by

$$   V^{C}(0,r_{ij}) = \frac{1}{r_{ij}} - \frac{\mathbf{\alpha_i}\cdot\mathbf{\alpha}_j}{r_{ij}} + \frac{(\mathbf{\alpha}_i \times r_{ij})(\mathbf{\alpha}_j \times r_{ij})}{r_{ij}^3} \ \ \ \ \ (12) $$

We will ignore this for the rest of the derivation (thus ultimately giving the Dirac-Coulomb-Hartree-Fock equations), but to see how the interaction may be accounted for, consider that you now have new integrals that take the form

$$   \psi_p^{\dagger}\mathbf{\alpha}\psi_q = \left( \psi_p^{L\dagger} \psi_p^{S\dagger} \right) \left( \begin{array}{cc} 0_2 & \mathbf{\sigma} \\ \mathbf{\sigma} & 0_2 \end{array} \right) \left( \begin{array}{c} \psi_q^{L} \\ \psi_q^S \end{array} \right) = \psi_p^{S\dagger}\mathbf{\sigma}\psi_q^{L} + \psi_p^{L\dagger}\mathbf{\sigma}\psi_q^{S} \ \ \ \ \ (13) $$

Which basically adds some different coupling elements. The alpha is the dame as in the Dirac equation, and the sigma is again your Pauli matrices. Anyway, going back, we now have a form of the two-electron integrals in 2-spinor form. We can insert the same basis set expansion elements as before for the one-electron case, and we get, for example

$$   (p^L q^L \vert  r^L s^L) = \sum\limits_{\mu \nu \kappa \lambda} c^{L*}_{\mu p} c^{L}_{\nu q} c^{L*}_{\kappa r} c^{L}_{\lambda s} (\mu^L \nu^L \vert  \kappa^L \lambda^L) \ \ \ \ \ (14) $$

And similar expressions hold for the other terms. This should look nearly identical to the molecular-orbital/atomic-orbital relation in Hartree Fock theory.

And that's really all there is to it! To clean up our expressions, we introduce density matrix $$ {\mathbf{P}} $$, where, for example

$$   \mathbf{P} = \left[\begin{array} {cc} \mathbf{P}^{LL} & \mathbf{P}^{LS} \\ \mathbf{P}^{SL} & \mathbf{P}^{SS} \end{array} \right] \ \ \ \ \ (15) $$

with

$$   \mathbf{P}^{LL} = \mathbf{c}^{L}\mathbf{c}^{L\dagger}, ~\hbox{etc.} \ \ \ \ \ (16) $$

Then our Dirac-(Coulomb-) Hartree Fock matrix looks like

$$   \mathbf{F} = \left[\begin{array} {cc} \mathbf{F}^{LL} & \mathbf{F}^{LS} \\ \mathbf{F}^{SL} & \mathbf{F}^{SS} \end{array} \right] \ \ \ \ \ (17) $$

With

$$   F^{LL}_{\mu \nu} = V^{LL}_{\mu \nu} + \sum\limits_{\kappa \lambda} P^{LL}_{\kappa \lambda} \left[(\mu^L \nu^L \vert  \kappa^L \lambda^{L}) - (\mu^{L} \lambda^{L} \vert  \kappa^{L} \nu^{L})\right] + \sum\limits_{\kappa\lambda} P^{SS}_{\kappa \lambda} \left[(\mu^L \nu^L \vert  \kappa^S \lambda^S )\right] \ \ \ \ \ (18) $$

$$   F^{LS}_{\mu \nu} = c \Pi^{LS}_{\mu \nu} - \sum\limits_{\kappa \lambda} P_{\kappa \lambda}^{SL} (\mu^L \lambda^L \vert  \kappa^{S} \nu^{S} ) \ \ \ \ \ (19) $$

$$   F^{SS}_{\mu \nu} = V^{SS}_{\mu \nu} - 2c^2 S^{SS}_{\mu\nu} + \sum\limits_{\kappa \lambda} P_{\kappa \lambda}^{LL} (\mu^S \nu^S \vert  \kappa^L \lambda^L) + \sum\limits_{\kappa \lambda} P_{\kappa \lambda}^{SS} \left[(\mu^S \nu^S \vert  \kappa^S \lambda^S) - (\mu^S \lambda^S \vert  \kappa^S \nu^S ) \right] \ \ \ \ \ (20) $$

And of course the form of the DHF equations is the same as in the non-relativistic case (with $$ {\mathbf{C}} $$ the matrix of all eigenvectors $$ {\mathbf{c}} $$):

$$   \mathbf{FC} = \mathbf{SC}E \ \ \ \ \ (21) $$

The Dirac Fock matrix is Hermitian, and you can see that it depends on the density $$ {\mathbf{P}=\mathbf{CC^{\dagger}}} $$ as well, meaning we have to solve the equations iteratively.

Now, there is still a lot more to do with these equations, such as finding a suitable basis set and actually setting up the problem and integrals. It's not a trivial task, but I plan to explore these more in the future.

Questions, comments, or corrections? Let me know! I'd love to hear from you.

