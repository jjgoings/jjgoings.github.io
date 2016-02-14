--- 
layout: post 
title: Derivation of Time Dependent Hartree-Fock (TDHF) Equations 
---


This derivation is largely based off the TD-DFT derivation (TDDFT and TDHF are very similar), found in the wonderful review, "Single-Reference ab Initio Methods for the Calculation of Excited States of Large Molecules" by Dreuw and Head-Gordon (Chem Reviews, 2005).

We start with the [time-dependent Schrödinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation"), given in [Hartree-Fock](http://en.wikipedia.org/wiki/Hartree%E2%80%93Fock_method "Hartree–Fock method") form, along with its adjoint:

$$   i \frac{\partial}{\partial t} \mathbf{C} = \mathbf{FC} \ \ \ \ \ (1) $$

$$   - i\frac{\partial}{\partial t}\mathbf{C}^{\dagger}= \mathbf{C}^{\dagger}\mathbf{F}\ \ \ \ \ (2) $$

Now,

$$   i \frac{\partial}{\partial t} \left(\mathbf{CC}^{\dagger}\right) = i \left(\frac{\partial}{\partial t} \mathbf{C}\right)\mathbf{C}^{\dagger} + i\mathbf{C}\left(\frac{\partial}{\partial t} \mathbf{C}^{\dagger}\right) \ \ \ \ \ (3) $$

Substituting the first two expressions into the right hand side, these two expressions yields the Dirac form of the time-dependent Hartree-Fock equations,

$$   i \frac{\partial}{\partial t} \mathbf{CC}^{\dagger} = i \frac{\partial}{\partial t} \mathbf{P}\ \ \ \ \ (4) $$

$$ i \frac{\partial}{\partial t} \mathbf{P} = i \left( -i\mathbf{FCC}^{\dagger} + i\mathbf{C}\mathbf{C}^{\dagger}\mathbf{F}\right)\ \ \ \ \ \ (5) $$

$$   \mathbf{FP} - \mathbf{PF} = i \frac{\partial}{\partial t} \mathbf{P} \ \ \ \ \ (6) $$

where $$ {\mathbf{F}} $$ is the [Fock matrix](http://en.wikipedia.org/wiki/Fock_matrix "Fock matrix") and $$ {\mathbf{P} = \mathbf{CC}^{\dagger}} $$ is the [density matrix](http://en.wikipedia.org/wiki/Density_matrix "Density matrix"), same as in the time independent Hartree-Fock equations. Before a time dependent perturbation is applied, we assume that the system is in its electronic ground state, such that

$$   \mathbf{F}^{(0)}\mathbf{P}^{(0)} - \mathbf{P}^{(0)}\mathbf{F}^{(0)} = 0 \ \ \ \ \ (7) $$

and

$$   \mathbf{P}^{(0)}\mathbf{P}^{(0)} = \mathbf{P}^{(0)} \ \ \ \ \ (8) $$

with $$ {\mathbf{P}^{(0)}} $$ and $$ {\mathbf{F}^{(0)}} $$ as the unperturbed density and Fock matrix, respectively. The first condition comes from the fact that commuting matrices share a common set of eigenvectors, and the second comes from the fact that at convergence the eigenvectors of the Fock matrix are orthonormal. (Recall that the density matrix may be written as $$ {\mathbf{P} = \mathbf{CC}^{\dagger}} $$, where the columns of $$ {\mathbf{C}} $$ form an orthonormal set, e.g. $$ {\mathbf{C}^{\dagger}\mathbf{C} = \mathbf{1}} $$). The Fock matrix elements are given by

$$   F_{pq}^{(0)} = H_{pq}^{core} + \sum\limits_{rs} P_{rs}[(pq\vert sr) - (pr\vert sq)] \ \ \ \ \ (9) $$

Note the Fock matrix dependence on the density matrix. At convergence, the Fock matrix is diagonal, with the elements corresponding to the orbital energies $$ {\epsilon} $$.

$$   F_{pq}^{(0)} = \delta_{pq}\epsilon_{p} \ \ \ \ \ (10) $$

Furthermore, the density matrix enjoys the following relations:

$$   P_{ij}^{(0)} = \delta_{ij} \ \ \ \ \ (11) $$

$$   P_{ia}^{(0)} = P_{ai}^{(0)} = P_{ab}^{(0)} = 0 \ \ \ \ \ (12) $$

Following convention, indices $$ {\{i,j,...\}} $$ correspond to occupied orbitals, $$ {\{a,b,...\}} $$ correspond to unoccupied orbitals, and $$ {\{p,q,...\}} $$ correspond to general orbitals. In general [perturbation theory](http://en.wikipedia.org/wiki/Perturbation_theory "Perturbation theory"), a perturbed wavefunction (or density matrix, for our purposes) can be decomposed, to first order, as

$$   \mathbf{P} = \mathbf{P}^{(0)} + \mathbf{P}^{(1)} \ \ \ \ \ (13) $$

and likewise for the density-dependent Fock matrix

$$   \mathbf{F} = \mathbf{F}^{(0)} + \mathbf{F}^{(1)} \ \ \ \ \ (14) $$

where the superscript (1) indicates the first-order time dependent change. Inserting the expressions 13 and 14 into the time-dependent equation 6 and collecting only the first order terms yields

$$   \mathbf{F}^{(0)}\mathbf{P}^{(1)} - \mathbf{P}^{(1)}\mathbf{F}^{(0)} + \mathbf{F}^{(1)}\mathbf{P}^{(0)} - \mathbf{P}^{(0)}\mathbf{F}^{(1)} = i \frac{\partial}{\partial t} \mathbf{P}^{(1)} \ \ \ \ \ (15) $$

The time-dependent perturbation can be described by a single Fourier component,

$$   g_{pq} = \frac{1}{2} [f_{pq}e^{-i\omega t} + f_{qp}^{*}e^{i\omega t}] \ \ \ \ \ (16) $$

The matrix $$ {f} $$ is a one-electron operator, which describes the applied perturbation. This perturbation acts on the electron density, resulting in a first order Fock matrix response

$$   \Delta F_{pq}^{(0)} = \sum\limits_{st} \frac{\partial F_{pq}^{(0)}}{\partial P_{st}} P_{st}^{(1)} \ \ \ \ \ (17) $$

so that the overall first order change in the Fock matrix is

$$   F_{pq}^{(1)} = g_{pq} + \Delta F_{pq}^{(0)} \ \ \ \ \ (18) $$

Similarly, the first order density response is given as

$$   P_{pq}^{(1)} = \frac{1}{2} [d_{pq}e^{-i\omega t} + d_{qp}^{*}e^{i\omega t}] \ \ \ \ \ (19) $$

with $$ {d_{pq}} $$ as the perturbation densities. Plugging the above expressions for $$ {\mathbf{F}^{(1)}} $$ and $$ {\mathbf{P}^{(1)}} $$ into the first order TDHF equation 15, and collecting the terms containing $$ {e^{-i\omega t}} $$ gives (after some algebra):

$$   \sum\limits_q F_{pq}^{(0)}d_{qr} - d_{pq}F_{qr}^{(0)} + \left(f_{pq} + \sum\limits_{st} \frac{\partial F_{pq}^{(0)}}{\partial P_{st}}d_{st}\right)P_{qr}^{(0)} - P_{pq}^{(0)}\left(f_{qr} + \sum\limits_{st} \frac{\partial F_{qr}^{(0)}}{\partial P_{st}}d_{st}\right) = \omega d_{pr} \ \ \ \ \ (20) $$

The terms multiplied by $$ {e^{i \omega t}} $$ give the complex conjugate of the above expression. Because the density matrix must be idempotent, we can show that

$$   \sum\limits_q \{P_{pq}^{(0)}P_{qr}^{(1)} + P_{pq}^{(1)}P_{qr}^{(0)}\} = P_{pr}^{(1)} \ \ \ \ \ (21) $$

If $$ {\mathbf{PP} = \mathbf{P}} $$, and we expand $$ {\mathbf{P}} $$ as a perturbation with arbitrary scalar $$ {\lambda} $$, we have:

$$   (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots)(\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) = (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) \ \ \ \ \ (22) $$

$$   (\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots)(\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(1)} + \dots) = (\mathbf{P}^{(0)}\mathbf{P}^{(0)} + \lambda\mathbf{P}^{(0)}\mathbf{P}^{(1)} + \lambda\mathbf{P}^{(1)}\mathbf{P}^{(0)} + \dots) \ \ \ \ \ (23) $$

Equating like powers of $$ {\lambda} $$ yields the expression 21, as well as our original expression 8. Using 21 allows us to restrict the elements of $$ {d_{pq}} $$, utilizing the nature of the zeroth order density matrix given in 11. As an example, consider the element $$ {d_{ii}} $$:

$$   d_{ii} \propto P_{ii}^{(1)} = \sum\limits_q \{P_{iq}^{(0)}P_{qi}^{(1)} + P_{iq}^{(1)}P_{qi}^{(0)}\} \ \ \ \ \ (24) $$

$$   P_{ii}^{(1)} = P_{ii}^{(0)}P_{ii}^{(1)} + P_{ii}^{(1)}P_{ii}^{(0)} \ \ \ \ \ (25) $$

$$   P_{ii}^{(1)} = P_{ii}^{(1)} + P_{ii}^{(1)} \ \ \ \ \ (26) $$

which is only true if $$ {P_{ii}^{(1)} = 0} $$. Similar arguments show that the only contributing blocks of $$ {d_{pq}} $$ are $$ {d_{ia}} $$ and $$ {d_{ai}} $$. In other words, the only contributions to the TDHF equations are the occupied-virtual and virtual-occupied blocks. All virtual-virtual and occupied-occupied blocks are necessarily zero. With this in mind, along with the diagonal nature of the unperturbed Fock matrix, yields

$$   F_{aa}^{(0)}x_{ai} - x_{ai}F_{ii}^{(0)} + \left(f_{ai} + \sum\limits_{bj} \left[\frac{\partial F_{ai}^{(0)}}{\partial P_{bj}}x_{bj} + \frac{\partial F_{ai}^{(0)}}{\partial P_{jb}}y_{bj}\right]\right)P_{ii}^{(0)} = \omega x_{ai} \ \ \ \ \ (27) $$

and

$$   F_{ii}^{(0)}y_{ai} - y_{ai}F_{aa}^{(0)} - P_{ii}^{(0)}\left(f_{ia} + \sum\limits_{bj} \left[\frac{\partial F_{ia}^{(0)}}{\partial P_{bj}}x_{bj} + \frac{\partial F_{ia}^{(0)}}{\partial P_{jb}}y_{bj}\right]\right) = \omega y_{ai} \ \ \ \ \ (28) $$

with $$ {x_{ai} = d_{ai}} $$ and $$ {y_{ai} = d_{ia}} $$, as is convention. The derivatives inside the expression evaluate as follows:

$$   \sum\limits_{rs}\frac{\partial F_{pq}}{\partial P_{rs}} = \sum\limits_{rs}\frac{\partial}{\partial P_{rs}} \left( H_{pq}^{core} + P_{rs}[(pq\vert sr) - (pr\vert sq)]\right) \ \ \ \ \ (29) $$

$$   = (pq\vert sr) - (pr\vert sq) = (pq\vert \vert sr) \ \ \ \ \ (30) $$

Finally, we make the assumption that the perturbation is infinitely small, which sends $$ {f_{ai} = f_{ia} \rightarrow 0} $$, and we recover (recognizing that $$ {F_{pp}^{(0)} = \epsilon_p} $$ and $$ {P_{ii}^{(0)} = 1} $$):

$$   \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{-B} & \mathbf{-A} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \ (31) $$

Which is the non-Hermitian eigenvalue TDHF equation. The elements of $$ {\mathbf{A}} $$ and $$ {\mathbf{B}} $$ are

$$   A_{ia,jb} = \delta_{ij}\delta_{ab}(\epsilon_a - \epsilon_i) + (ai\vert \vert jb) \ \ \ \ \ (32) $$

and

$$   B_{ia,jb} = (ai\vert \vert bj) \ \ \ \ \ (33) $$


