---
layout: post
title: Polarization Propagator Derivation of TDHF/RPA 
---

[PDF copy of below](http://joshuagoings.files.wordpress.com/2013/06/polarizationpropagatorrpa.pdf)

 

Following immediately where we [left off last time](http://joshuagoings.wordpress.com/2013/06/21/derivation-of-general-polarization-propagator-methods/ "Derivation of general polarization propagator methods"), when $$ {A}&fg=000000$$ and $$ {B}&fg=000000$$ are one-electron number conserving, e.g. creation/annihilation operators are in pairs, we have

$$ \displaystyle A = \sum\limits\_{rs} A\_{rs}a\_r^{\dagger}a\_s, \qquad B = \sum\limits\_{rs} B\_{rs}a^{\dagger}\_ra\_s \ \ \ \ \ (28)&fg=000000$$

which allow us to define the general polarization [propagator](http://en.wikipedia.org/wiki/Propagator "Propagator"). If the elements did not conserve the number of electrons, we could use the same formalism to get the electron propagator, which can describe the attachment/detachment of electrons from a system, thus describing processes such as ionization. In general, it is sufficient to consider the typical elements $$ {A \rightarrow a\_r^{\dagger}a\_s}&fg=000000$$ and $$ {B \rightarrow a\_t^{\dagger}a\_u}&fg=000000$$. If [spin-orbitals](http://en.wikipedia.org/wiki/Atomic_orbital "Atomic orbital") of reference are $$ {\psi\_i, \psi\_j}&fg=000000$$,..., then a ``particle-hole'' basis includes only ``excitation'' and ``de-excitation'' operators $$ {a\_a^{\dagger}a\_i}&fg=000000$$ and $$ {a\_i^{\dagger}a\_a}&fg=000000$$, respectively. Thus the basis and its dual:  
$$ \displaystyle \mathbf{n} = (\mathbf{e} \quad \mathbf{d}), \qquad \mathbf{n}^{\dagger} = (\mathbf{e} \quad \mathbf{d})^{\dagger} \ \ \ \ \ &fg=000000$$  
$$ \displaystyle e\_{ia} = a\_a^{\dagger}a\_i = E\_{ia}, \qquad d\_{ai} = a\_i^{\dagger}a\_a = E\_{ia}^{\dagger} \ \ \ \ \ (29)&fg=000000$$

This gives, for our resolvent,  
$$ \displaystyle R(\omega) = \left[\mathbf{n}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{n}\right]^{-1} = \begin{bmatrix} \mathbf{e}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{e} & \mathbf{e}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{d} \\ \mathbf{d}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{e} & \mathbf{d}^{\dagger}(\hbar\omega\hat{1} - \hat{H})\mathbf{d} \\ \end{bmatrix}^{-1} \ \ \ \ \ (30)&fg=000000$$

As an example, we give the elements of the first block:  
$$ \displaystyle E^{\dagger}\_{ia}(\hbar\omega\hat{1} - \hat{H})E\_{jb} = \hbar\omega E^{\dagger}\_{ia} E\_{jb} - E^{\dagger}\_{ia} \left[H,E\_{jb}\right] \ \ \ \ \ (31)&fg=000000$$

with scalar products  
$$ \displaystyle E^{\dagger}\_{ia} E\_{jb} = \langle \psi\_0 | [E^{\dagger}\_{ia},E\_{jb}]| \psi\_0 \rangle, \qquad E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = \langle \psi\_0 | [E^{\dagger}\_{ia},[H,E\_{jb}]]| \psi\_0 \rangle \ \ \ \ \ (32)&fg=000000$$

Evaluating these products gives  
$$ \displaystyle E^{\dagger}\_{ia} E\_{jb} = \langle \psi\_0 | [E^{\dagger}\_{ia},E\_{jb}]| \psi\_0 \rangle = \langle \psi\_0 | E^{\dagger}\_{ia}E\_{jb}| \psi\_0 \rangle - \langle \psi\_0 | E\_{jb}E^{\dagger}\_{ia}| \psi\_0 \rangle = \langle \psi\_0 | E^{\dagger}\_{ia}E\_{jb}| \psi\_0 \rangle = \delta\_{ia,jb} \ \ \ \ \ (33)&fg=000000$$

and

$$ \displaystyle E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = \langle \psi\_0 | [E^{\dagger}\_{ia},[H,E\_{jb}]]| \psi\_0 \rangle \ \ \ \ \ &fg=000000$$  
$$ \displaystyle E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = \langle \psi\_0 | E^{\dagger}\_{ia} H E\_{jb}| \psi\_0 \rangle - \langle \psi\_0 | E^{\dagger}\_{ia}E\_{jb} H| \psi\_0 \rangle - \langle \psi\_0 | H E\_{jb} E^{\dagger}\_{ia}| \psi\_0 \rangle + \langle \psi\_0 | E\_{jb} H E^{\dagger}\_{ia} | \psi\_0 \rangle \ \ \ \ \ &fg=000000$$  
$$ \displaystyle E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = \langle \psi^a\_i | H | \psi\_j^b \rangle - \delta\_{ia}\delta\_{jb}\langle \psi\_0 | H | \psi\_0 \rangle \ \ \ \ \ &fg=000000$$  
$$ \displaystyle E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = E\_0\delta\_{ij}\delta\_{ab} + F\_{ab}\delta\_{ij} - F\_{ij}\delta\_{ab} + \langle aj || ib \rangle - \delta\_{ia}\delta{jb}E\_0 \ \ \ \ \ &fg=000000$$  
$$ \displaystyle E^{\dagger}\_{ia} \left[H,E\_{jb}\right] = (\epsilon\_a - \epsilon\_i)\delta\_{ia}\delta\_{ab} + \langle aj || ib \rangle = \mathbf{A} \ \ \ \ \ &fg=000000$$  
Which is precisely the same elements as we have derived earlier for TDHF. Completing the rest, we have:  
$$ \displaystyle R(\omega) = M(\omega)^{-1} = \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^\* & \mathbf{A}^\* \\ \end{bmatrix} - \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \ \ \ \ \ (34)&fg=000000$$

With $$ {\mathbf{B} = \langle ab || ij \rangle}&fg=000000$$. Now, we saw from the definition of the resolvent that $$ {R(\omega) \rightarrow \infty}&fg=000000$$ at $$ {\omega \rightarrow \omega\_{0n}}&fg=000000$$, which are the poles of $$ {R(\omega)}&fg=000000$$. Therefore, $$ {R(\omega)^{-1} \rightarrow 0}&fg=000000$$ and  
$$ \displaystyle \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^\* & \mathbf{A}^\* \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \ (35)&fg=000000$$

which are the RPA/TDHF equations. The eigencolumns determine the [linear combinations](http://en.wikipedia.org/wiki/Linear_combination "Linear combination") of excitation and de-excitation operators that produce corresponding approximate [excited states](http://en.wikipedia.org/wiki/Excited_state "Excited state") when working on the reference state $$ {|\psi\_0 \rangle}&fg=000000$$.

\*typeset with  [latex2wp](http://sourceforge.net/projects/latex2wp/)

