--- 
layout: post 
title: Derivation of Time Dependent Hartree-Fock (TDHF) Equations 
---

[PDF](https://joshuagoings.files.wordpress.com/2013/05/tdhf.pdf)

This derivation is largely based off the TD-DFT derivation (TDDFT and TDHF are very similar), found in the wonderful review, "Single-Reference ab Initio Methods for the Calculation of Excited States of Large Molecules" by Dreuw and Head-Gordon (Chem Reviews, 2005).

We start with the [time-dependent Schrödinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation"), given in [Hartree-Fock](http://en.wikipedia.org/wiki/Hartree%E2%80%93Fock_method "Hartree–Fock method") form, along with its adjoint:

$$ \displaystyle i \frac{\partial}{\partial t} \mathbf{C} = \mathbf{FC} \ \ \ \ \ (1)&fg=000000$$

$$ \displaystyle - i\frac{\partial}{\partial t}\mathbf{C}^{\dagger}= \mathbf{C}^{\dagger}\mathbf{F}\ \ \ \ \ (2)&fg=000000$$

Now,

$$ \displaystyle i \frac{\partial}{\partial t} \left(\mathbf{CC}^{\dagger}\right) = i \left(\frac{\partial}{\partial t} \mathbf{C}\right)\mathbf{C}^{\dagger} + i\mathbf{C}\left(\frac{\partial}{\partial t} \mathbf{C}^{\dagger}\right) \ \ \ \ \ (3)&fg=000000$$

Substituting the first two expressions into the right hand side, these two expressions yields the Dirac form of the time-dependent Hartree-Fock equations,

$$ \displaystyle i \frac{\partial}{\partial t} \mathbf{CC}^{\dagger} = i \frac{\partial}{\partial t} \mathbf{P}\ \ \ \ \ (4)&fg=000000$$

$$ i \frac{\partial}{\partial t} \mathbf{P} = i \left( -i\mathbf{FCC}^{\dagger} + i\mathbf{C}\mathbf{C}^{\dagger}\mathbf{F}\right)\ \ \ \ \ \ (5)&fg=000000$$

$$ \displaystyle \mathbf{FP} - \mathbf{PF} = i \frac{\partial}{\partial t} \mathbf{P} \ \ \ \ \ (6)&fg=000000$$

where $$ {\mathbf{F}}&fg=000000$$ is the [Fock matrix](http://en.wikipedia.org/wiki/Fock_matrix "Fock matrix") and $$ {\mathbf{P} = \mathbf{CC}^{\dagger}}&fg=000000$$ is the [density matrix](http://en.wikipedia.org/wiki/Density_matrix "Density matrix"), same as in the time independent Hartree-Fock equations. Before a time dependent perturbation is applied, we assume that the system is in its electronic ground state, such that

$$ \displaystyle \mathbf{F}^{(0)}\mathbf{P}^{(0)} - \mathbf{P}^{(0)}\mathbf{F}^{(0)} = 0 \ \ \ \ \ (7)&fg=000000$$

and

$$ \displaystyle \mathbf{P}^{(0)}\mathbf{P}^{(0)} = \mathbf{P}^{(0)} \ \ \ \ \ (8)&fg=000000$$

with $$ {\mathbf{P}^{(0)}}&fg=000000$$ and $$ {\mathbf{F}^{(0)}}&fg=000000$$ as the unperturbed density and Fock matrix, respectively. The first condition comes from the fact that commuting matrices share a common set of eigenvectors, and the second comes from the fact that at convergence the eigenvectors of the Fock matrix are orthonormal. (Recall that the density matrix may be written as $$ {\mathbf{P} = \mathbf{CC}^{\dagger}}&fg=000000$$, where the columns of $$ {\mathbf{C}}&fg=000000$$ form an orthonormal set, e.g. $$ {\mathbf{C}^{\dagger}\mathbf{C} = \mathbf{1}}&fg=000000$$). The Fock matrix elements are given by

$$ \displaystyle F\_{pq}^{(0)} = H\_{pq}^{core} + \sum\limits\_{rs} P\_{rs}[(pq|sr) - (pr|sq)] \ \ \ \ \ (9)&fg=000000$$

Note the Fock matrix dependence on the density matrix. At convergence, the Fock matrix is diagonal, with the elements corresponding to the orbital energies $$ {\epsilon}&fg=000000$$.

$$ \displaystyle F\_{pq}^{(0)} = \delta\_{pq}\epsilon\_{p} \ \ \ \ \ (10)&fg=000000$$

Furthermore, the density matrix enjoys the following relations:

$$ \displaystyle P\_{ij}^{(0)} = \delta\_{ij} \ \ \ \ \ (11)&fg=000000$$

$$ \displaystyle P\_{ia}^{(0)} = P\_{ai}^{(0)} = P\_{ab}^{(0)} = 0 \ \ \ \ \ (12)&fg=000000$$

Following convention, indices $$ {\{i,j,...\}}&fg=000000$$ correspond to occupied orbitals, $$ {\{a,b,...\}}&fg=000000$$ correspond to unoccupied orbitals, and $$ {\{p,q,...\}}&fg=000000$$ correspond to general orbitals. In general [perturbation theory](http://en.wikipedia.org/wiki/Perturbation_theory "Perturbation theory"), a perturbed wavefunction (or density matrix, for our purposes) can be decomposed, to first order, as

$$ \displaystyle \mathbf{P} = \mathbf{P}^{(0)} + \mathbf{P}^{(1)} \ \ \ \ \ (13)&fg=000000$$

and likewise for the density-dependent Fock matrix

$$ \displaystyle \mathbf{F} = \mathbf{F}^{(0)} + \mathbf{F}^{(1)} \ \ \ \ \ (14)&fg=000000$$

where the superscript (1) indicates the first-order time dependent change. Inserting the expressions 13 and 14 into the time-dependent equation 6 and collecting only the first order terms yields

$$ \displaystyle \mathbf{F}^{(0)}\mathbf{P}^{(1)} - \mathbf{P}^{(1)}\mathbf{F}^{(0)} + \mathbf{F}^{(1)}\mathbf{P}^{(0)} - \mathbf{P}^{(0)}\mathbf{F}^{(1)} = i \frac{\partial}{\partial t} \mathbf{P}^{(1)} \ \ \ \ \ (15)&fg=000000$$

The time-dependent perturbation can be described by a single Fourier component (see why [here](http://joshuagoings.wordpress.com/2013/05/02/alternate-derivation-of-linear-response-function/ "Alternate derivation of linear response function")),

$$ \displaystyle g\_{pq} = \frac{1}{2} [f\_{pq}e^{-i\omega t} + f\_{qp}^{\*}e^{i\omega t}] \ \ \ \ \ (16)&fg=000000$$

The matrix $$ {f}&fg=000000$$ is a one-electron operator, which describes the applied perturbation. This perturbation acts on the electron density, resulting in a first order Fock matrix response

$$ \displaystyle \Delta F\_{pq}^{(0)} = \sum\limits\_{st} \frac{\partial F\_{pq}^{(0)}}{\partial P\_{st}} P\_{st}^{(1)} \ \ \ \ \ (17)&fg=000000$$

so that the overall first order change in the Fock matrix is

$$ \displaystyle F\_{pq}^{(1)} = g\_{pq} + \Delta F\_{pq}^{(0)} \ \ \ \ \ (18)&fg=000000$$

Similarly, the first order density response is given as

$$ \displaystyle P\_{pq}^{(1)} = \frac{1}{2} [d\_{pq}e^{-i\omega t} + d\_{qp}^{\*}e^{i\omega t}] \ \ \ \ \ (19)&fg=000000$$

with $$ {d\_{pq}}&fg=000000$$ as the perturbation densities. Plugging the above expressions for $$ {\mathbf{F}^{(1)}}&fg=000000$$ and $$ {\mathbf{P}^{(1)}}&fg=000000$$ into the first order TDHF equation 15, and collecting the terms containing $$ {e^{-i\omega t}}&fg=000000$$ gives (after some algebra):

$$ \displaystyle \sum\limits\_q F\_{pq}^{(0)}d\_{qr} - d\_{pq}F\_{qr}^{(0)} + \left(f\_{pq} + \sum\limits\_{st} \frac{\partial F\_{pq}^{(0)}}{\partial P\_{st}}d\_{st}\right)P\_{qr}^{(0)} - P\_{pq}^{(0)}\left(f\_{qr} + \sum\limits\_{st} \frac{\partial F\_{qr}^{(0)}}{\partial P\_{st}}d\_{st}\right) = \omega d\_{pr} \ \ \ \ \ (20)&fg=000000$$

The terms multiplied by $$ {e^{i \omega t}}&fg=000000$$ give the complex conjugate of the above expression. Because the density matrix must be idempotent, we can show that

$$ \displaystyle \sum\limits\_q \{P\_{pq}^{(0)}P\_{qr}^{(1)} + P\_{pq}^{(1)}P\_{qr}^{(0)}\} = P\_{pr}^{(1)} \ \ \ \ \ (21)&fg=000000$$

If $$ {\mathbf{PP} = \mathbf{P}}&fg=000000$$, and we expand $$ {\mathbf{P}}&fg=000000$$ as a perturbation with arbitrary scalar $$ {\lambda}&fg=000000$$, we have:

$$ \displaystyle (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots)(\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) = (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) \ \ \ \ \ (22)&fg=000000$$

$$ \displaystyle (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots)(\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) = (\mathbf{P}^{(0)}\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(0)}\mathbf{P}^{(1)} + \lambda\mathbf{P}^{(1)}\mathbf{P}^{(0)} + \dots) \ \ \ \ \ (23)&fg=000000$$

Equating like powers of $$ {\lambda}&fg=000000$$ yields the expression 21, as well as our original expression 8. Using 21 allows us to restrict the elements of $$ {d\_{pq}}&fg=000000$$, utilizing the nature of the zeroth order density matrix given in 11. As an example, consider the element $$ {d\_{ii}}&fg=000000$$:

$$ \displaystyle d\_{ii} \propto P\_{ii}^{(1)} = \sum\limits\_q \{P\_{iq}^{(0)}P\_{qi}^{(1)} + P\_{iq}^{(1)}P\_{qi}^{(0)}\} \ \ \ \ \ (24)&fg=000000$$

$$ \displaystyle P\_{ii}^{(1)} = P\_{ii}^{(0)}P\_{ii}^{(1)} + P\_{ii}^{(1)}P\_{ii}^{(0)} \ \ \ \ \ (25)&fg=000000$$

$$ \displaystyle P\_{ii}^{(1)} = P\_{ii}^{(1)} + P\_{ii}^{(1)} \ \ \ \ \ (26)&fg=000000$$

which is only true if $$ {P\_{ii}^{(1)} = 0}&fg=000000$$. Similar arguments show that the only contributing blocks of $$ {d\_{pq}}&fg=000000$$ are $$ {d\_{ia}}&fg=000000$$ and $$ {d\_{ai}}&fg=000000$$. In other words, the only contributions to the TDHF equations are the occupied-virtual and virtual-occupied blocks. All virtual-virtual and occupied-occupied blocks are necessarily zero. With this in mind, along with the diagonal nature of the unperturbed Fock matrix, yields

$$ \displaystyle F\_{aa}^{(0)}x\_{ai} - x\_{ai}F\_{ii}^{(0)} + \left(f\_{ai} + \sum\limits\_{bj} \left[\frac{\partial F\_{ai}^{(0)}}{\partial P\_{bj}}x\_{bj} + \frac{\partial F\_{ai}^{(0)}}{\partial P\_{jb}}y\_{bj}\right]\right)P\_{ii}^{(0)} = \omega x\_{ai} \ \ \ \ \ (27)&fg=000000$$

and

$$ \displaystyle F\_{ii}^{(0)}y\_{ai} - y\_{ai}F\_{aa}^{(0)} - P\_{ii}^{(0)}\left(f\_{ia} + \sum\limits\_{bj} \left[\frac{\partial F\_{ia}^{(0)}}{\partial P\_{bj}}x\_{bj} + \frac{\partial F\_{ia}^{(0)}}{\partial P\_{jb}}y\_{bj}\right]\right) = \omega y\_{ai} \ \ \ \ \ (28)&fg=000000$$

with $$ {x\_{ai} = d\_{ai}}&fg=000000$$ and $$ {y\_{ai} = d\_{ia}}&fg=000000$$, as is convention. The derivatives inside the expression evaluate as follows:

$$ \displaystyle \sum\limits\_{rs}\frac{\partial F\_{pq}}{\partial P\_{rs}} = \sum\limits\_{rs}\frac{\partial}{\partial P\_{rs}} \left( H\_{pq}^{core} + P\_{rs}[(pq|sr) - (pr|sq)]\right) \ \ \ \ \ (29)&fg=000000$$

$$ \displaystyle = (pq|sr) - (pr|sq) = (pq||sr) \ \ \ \ \ (30)&fg=000000$$

Finally, we make the assumption that the perturbation is infinitely small, which sends $$ {f\_{ai} = f\_{ia} \rightarrow 0}&fg=000000$$, and we recover (recognizing that $$ {F\_{pp}^{(0)} = \epsilon\_p}&fg=000000$$ and $$ {P\_{ii}^{(0)} = 1}&fg=000000$$):

$$ \displaystyle \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{-B} & \mathbf{-A} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \ (31)&fg=000000$$

Which is the non-Hermitian eigenvalue TDHF equation. The elements of $$ {\mathbf{A}}&fg=000000$$ and $$ {\mathbf{B}}&fg=000000$$ are

$$ \displaystyle A\_{ia,jb} = \delta\_{ij}\delta\_{ab}(\epsilon\_a - \epsilon\_i) + (ai||jb) \ \ \ \ \ (32)&fg=000000$$

and

$$ \displaystyle B\_{ia,jb} = (ai||bj) \ \ \ \ \ (33)&fg=000000$$

\*Typeset using  [_latex2wp_](http://lucatrevisan.wordpress.com/latex-to-wordpress/)

