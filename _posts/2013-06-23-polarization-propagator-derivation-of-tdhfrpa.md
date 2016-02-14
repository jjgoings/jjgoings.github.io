---
layout: post
title: Polarization Propagator Derivation of TDHF/RPA 
---


Following immediately where we left off last time, when $$ {A} $$ and $$ {B} $$ are one-electron number conserving, e.g. creation/annihilation operators are in pairs, we have

$$   A = \sum\limits_{rs} A_{rs}a_r^{\dagger}a_s, \qquad B = \sum\limits_{rs} B_{rs}a^{\dagger}_ra_s \ \ \ \ \ (28) $$

which allow us to define the general polarization [propagator](http://en.wikipedia.org/wiki/Propagator "Propagator"). If the elements did not conserve the number of electrons, we could use the same formalism to get the electron propagator, which can describe the attachment/detachment of electrons from a system, thus describing processes such as ionization. In general, it is sufficient to consider the typical elements $$ {A \rightarrow a_r^{\dagger}a_s} $$ and $$ {B \rightarrow a_t^{\dagger}a_u} $$. If [spin-orbitals](http://en.wikipedia.org/wiki/Atomic_orbital "Atomic orbital") of reference are $$ {\psi_i, \psi_j} $$,..., then a particle-hole basis includes only excitation and de-excitation operators $$ {a_a^{\dagger}a_i} $$ and $$ {a_i^{\dagger}a_a} $$, respectively. Thus the basis and its dual:  
$$   \mathbf{n} = (\mathbf{e} \quad \mathbf{d}), \qquad \mathbf{n}^{\dagger} = (\mathbf{e} \quad \mathbf{d})^{\dagger} \ \ \ \ \  $$  
$$   e_{ia} = a_a^{\dagger}a_i = E_{ia}, \qquad d_{ai} = a_i^{\dagger}a_a = E_{ia}^{\dagger} \ \ \ \ \ (29) $$

This gives, for our resolvent,  
$$   R(\omega) = \left[\mathbf{n}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{n}\right]^{-1} = \begin{bmatrix} \mathbf{e}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{e} & \mathbf{e}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{d} \\ \mathbf{d}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{e} & \mathbf{d}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{d} \\ \end{bmatrix}^{-1} \ \ \ \ \ (30) $$

As an example, we give the elements of the first block:  
$$   E^{\dagger}_{ia}(\hbar\omega\hat{1} - \hat{H})E_{jb} = \hbar\omega E^{\dagger}_{ia} E_{jb} - E^{\dagger}_{ia} \left[H,E_{jb}\right] \ \ \ \ \ (31) $$

with scalar products  
$$   E^{\dagger}_{ia} E_{jb} = \langle \psi_0 \vert  [E^{\dagger}_{ia},E_{jb}]\vert  \psi_0 \rangle, \qquad E^{\dagger}_{ia} \left[H,E_{jb}\right] = \langle \psi_0 \vert  [E^{\dagger}_{ia},[H,E_{jb}]]\vert  \psi_0 \rangle \ \ \ \ \ (32) $$

Evaluating these products gives  
$$   E^{\dagger}_{ia} E_{jb} = \langle \psi_0 \vert  [E^{\dagger}_{ia},E_{jb}]\vert  \psi_0 \rangle = \langle \psi_0 \vert  E^{\dagger}_{ia}E_{jb}\vert  \psi_0 \rangle - \langle \psi_0 \vert  E_{jb}E^{\dagger}_{ia}\vert  \psi_0 \rangle = \langle \psi_0 \vert  E^{\dagger}_{ia}E_{jb}\vert  \psi_0 \rangle = \delta_{ia,jb} \ \ \ \ \ (33) $$

and

$$   E^{\dagger}_{ia} \left[H,E_{jb}\right] = \langle \psi_0 \vert  [E^{\dagger}_{ia},[H,E_{jb}]]\vert  \psi_0 \rangle \ \ \ \ \  $$  
$$   E^{\dagger}_{ia} \left[H,E_{jb}\right] = \langle \psi_0 \vert  E^{\dagger}_{ia} H E_{jb}\vert  \psi_0 \rangle - \langle \psi_0 \vert  E^{\dagger}_{ia}E_{jb} H\vert  \psi_0 \rangle - \langle \psi_0 \vert  H E_{jb} E^{\dagger}_{ia}\vert  \psi_0 \rangle + \langle \psi_0 \vert  E_{jb} H E^{\dagger}_{ia} \vert  \psi_0 \rangle \ \ \ \ \  $$  
$$   E^{\dagger}_{ia} \left[H,E_{jb}\right] = \langle \psi^a_i \vert  H \vert  \psi_j^b \rangle - \delta_{ia}\delta_{jb}\langle \psi_0 \vert  H \vert  \psi_0 \rangle \ \ \ \ \  $$  
$$   E^{\dagger}_{ia} \left[H,E_{jb}\right] = E_0\delta_{ij}\delta_{ab} + F_{ab}\delta_{ij} - F_{ij}\delta_{ab} + \langle aj \vert \vert  ib \rangle - \delta_{ia}\delta{jb}E_0 \ \ \ \ \  $$  
$$   E^{\dagger}_{ia} \left[H,E_{jb}\right] = (\epsilon_a - \epsilon_i)\delta_{ia}\delta_{ab} + \langle aj \vert \vert  ib \rangle = \mathbf{A} \ \ \ \ \  $$  
Which is precisely the same elements as we have derived earlier for TDHF. Completing the rest, we have:  
$$   R(\omega) = M(\omega)^{-1} = \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \\ \end{bmatrix} - \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \ \ \ \ \ (34) $$

With $$ {\mathbf{B} = \langle ab \vert \vert  ij \rangle} $$. Now, we saw from the definition of the resolvent that $$ {R(\omega) \rightarrow \infty} $$ at $$ {\omega \rightarrow \omega_{0n}} $$, which are the poles of $$ {R(\omega)} $$. Therefore, $$ {R(\omega)^{-1} \rightarrow 0} $$ and  
$$   \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \ (35) $$

which are the RPA/TDHF equations. The eigencolumns determine the [linear combinations](http://en.wikipedia.org/wiki/Linear_combination "Linear combination") of excitation and de-excitation operators that produce corresponding approximate [excited states](http://en.wikipedia.org/wiki/Excited_state "Excited state") when working on the reference state $$ {\vert \psi_0 \rangle} $$.


