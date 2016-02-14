---
layout: post 
title: Derivation of general polarization propagator methods 
---

[PDF copy of below](http://joshuagoings.files.wordpress.com/2013/06/polarizationpropagatorpart1.pdf)

Most higher-order response methods use some form of the polarization [propagator](http://en.wikipedia.org/wiki/Propagator "Propagator"), which is what I intend to derive here. It can then be used to derive other methods, such as TDHF/RPA and SOPPA.

We have [derived earlier](http://joshuagoings.wordpress.com/2013/04/27/linear-response-td-dft-the-density-density-response-function/ "Linear Response TD-DFT: The density-density response function") a response function, or frequency dependent polarizability,

$$ \displaystyle \Pi(BA| \omega) = \lim\_{\eta \rightarrow 0} \left(\frac{1}{\hbar}\right) \sum\limits\_{n\neq0} \left\{ \frac{\langle 0 | B | n\rangle\langle n | A |0\rangle}{\omega + i\eta - \omega\_{0n}} - \frac{\langle 0 | A | n\rangle \langle n | B | 0 \rangle}{\omega + i\eta + \omega\_{0n}} \right\} \ \ \ \ \ (1)&fg=000000$$

where $$ {A}&fg=000000$$ is the applied perturbation, and $$ {B}&fg=000000$$ is the observable, and both are assumed to be Hermitian. $$ {\omega\_{0n}}&fg=000000$$ is the excitation energy for the change between states $$ {0}&fg=000000$$ and $$ {n}&fg=000000$$. It should be clear that the response function has poles when $$ {\omega}&fg=000000$$ --- the applied field frequency -- equals to the excitation energy $$ {\omega\_{0n}}&fg=000000$$. Finding these poles is precisely the goal of polarization propagator methods. In the polarization propagator approach, the above equation has $$ {\eta}&fg=000000$$ set to 0, and the response function (the `propagator'), defined as:  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} \equiv \sum\limits\_{n\neq0} \left\{ \frac{\langle 0 | B | n\rangle\langle n | A |0\rangle}{\hbar\omega - \hbar\omega\_{0n}} + \frac{\langle 0 | A | n\rangle \langle n | B | 0 \rangle}{-\hbar\omega - \hbar\omega\_{0n}} \right\} \ \ \ \ \ (2)&fg=000000$$

Now we want to describe the propagator in terms of commutators between $$ {A}&fg=000000$$ and $$ {B}&fg=000000$$. Make the observation that $$ {\frac{ab}{c+d} = \frac{ab}{c} - \frac{d}{c}\left(\frac{ab}{c+d}\right)}&fg=000000$$, and applying to the first term of the above yields:  
$$ \displaystyle \sum\limits\_{n\neq0} \frac{\langle 0 | B | n\rangle\langle n | A |0\rangle}{\hbar\omega - \hbar\omega\_{0n}} = \sum\limits\_{n\neq0} \frac{\langle 0 | B | n\rangle\langle n | A |0\rangle}{\hbar\omega} -\sum\limits\_{n\neq0} \frac{-\hbar\omega\_{0n}\langle 0 | B | n\rangle\langle n | A |0\rangle}{\hbar\omega\left(\hbar\omega - \hbar\omega\_{0n}\right)} \ \ \ \ \ (3)&fg=000000$$

Do the same for the second term and combine, recognizing that the $$ {n=0}&fg=000000$$ term vanishes in the first part (thus we get a sum over all $$ {n}&fg=000000$$), and making use of the fact that $$ {1 = \sum\limits\_{n}|n\rangle\langle n|}&fg=000000$$ and $$ {H| n \rangle = E\_n|n\rangle}&fg=000000$$ and $$ {\hbar\omega\_{0n} = E\_n - E\_0}&fg=000000$$:  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \frac{1}{\hbar\omega} \langle 0 | \left[B,A\right] | 0 \rangle + \frac{1}{\hbar\omega} \sum\limits\_{n\neq0} \left\{\frac{\langle 0 | B | n\rangle\langle n |\left[H,A\right] |0\rangle}{\hbar\omega - \hbar\omega\_{0n}} + \frac{\langle 0 | \left[H,A\right] | n\rangle\langle n | B |0\rangle}{-\hbar\omega - \hbar\omega\_{0n}}\right\} \ \ \ \ \ (4)&fg=000000$$

Which is to say that  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \frac{1}{\hbar\omega} \langle 0 | \left[B,A\right] | 0 \rangle + \frac{1}{\hbar\omega}\langle \langle B;\left[H,A\right] \rangle \rangle\_{\omega} \ \ \ \ \ (5)&fg=000000$$

Or, as we will use it:  
$$ \displaystyle \hbar\omega\langle \langle B;A \rangle \rangle\_{\omega} = \langle 0 | \left[B,A\right] | 0 \rangle - \langle \langle \left[H,B\right] A \rangle \rangle\_{\omega} \ \ \ \ \ (6)&fg=000000$$

As you may have started to see, we can define the propagator iteratively in terms of commutator expectation values of ever-increasing complexity. This is what is known as the so-called ``moment expansion'' of the propagator. Thus by iteration:  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \frac{1}{\hbar\omega} \left\{ \langle 0 | \left[B,A\right] | 0 \rangle + \left(\frac{-1}{\hbar\omega}\right)\langle 0 | \left[\left[H,B\right],A\right] | 0 \rangle + \left(\frac{-1}{\hbar\omega}\right)^2\langle 0 | \left[\left[H,\left[H,B\right]\right],A\right] | 0 \rangle + \cdots \right\} \ \ \ \ \ (7)&fg=000000$$

We introduce the ``superoperator'' (analogous to the [Liouville operator](http://en.wikipedia.org/wiki/Liouville%27s_theorem_%28Hamiltonian%29 "Liouville's theorem (Hamiltonian)") in Statistical Mechanics), which acts on operators to give their commutator:

$$ \displaystyle \hat{H}B = \left[H,B\right], \qquad \hat{H}^2B = \left[H,\left[H,B\right]\right], \qquad \hat{H}^3B = \left[H,\left[H,\left[H,B\right]\right]\right], \qquad \cdots \ \ \ \ \ (8)&fg=000000$$

With this definition, we have the power series  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \frac{1}{\hbar\omega} \sum\limits\_{n=0}^{\infty} \left(\frac{-1}{\hbar\omega}\right)^n \langle 0 | \left[\hat{H}^nB,A\right]|0\rangle \ \ \ \ \ (9)&fg=000000$$

At this point we make two useful observations. First, recognize that  
$$ \displaystyle \langle 0 | \left[\hat{H}B,A\right]|0\rangle = -\langle0|\left[B,\hat{H}A\right]|0\rangle \ \ \ \ \ (10)&fg=000000$$

and so $$ {\hat{H}}&fg=000000$$ can be applied to $$ {A}&fg=000000$$ instead of $$ {B}&fg=000000$$ insofar as we introduce a factor of $$ {(-1)^n}&fg=000000$$. Furthermore, note that the power series is equivalent to  
$$ \displaystyle \frac{1}{1-x} = 1 + x + x^2 + x^3 + \cdots \ \ \ \ \ (11)&fg=000000$$

Making use of these two observations (and using $$ {\hat{1}X = X}&fg=000000$$ and $$ {\hat{H}^0 = \hat{1}}&fg=000000$$, where $$ {\hat{1}}&fg=000000$$ is the unit superoperator), we have  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \langle 0 | \left[B,\left(\hbar\omega\hat{1} - \hat{H}\right)^{-1}A\right]|0\rangle \ \ \ \ \ (12)&fg=000000$$

Which is merely a cosmetic change at this point, as the superoperator resolvent is defined by the series expansion. We need to find a matrix representation of the resolvent, which implies that we find a complete basis set of operators. To do this, we are going to develop an ``operator space'', where $$ {\hat{H}}&fg=000000$$ is defined by its effect on operators instead of vectors. Introducing the notation  
$$ \displaystyle \left(X|Y\right) = \langle 0 | \left[X^{\dagger},Y\right] | 0 \rangle \ \ \ \ \ (13)&fg=000000$$

and it follows that $$ {\left(Y|X\right) = \left(X|Y\right)^\*}&fg=000000$$. As defined, we now have  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = \left(B^{\dagger}|\left(\hbar\omega\hat{1} - \hat{H}\right)^{-1}| A \right) \ \ \ \ \ (14)&fg=000000$$

Which is formally exact, albeit useless until we develop approximations. However, the form of the above equation does look similar to ordinary vector spaces in [Hartree-Fock](http://en.wikipedia.org/wiki/Hartree%E2%80%93Fock_method "Hartree–Fock method"), etc. methods. Truncation of a basis in linear vector space $$ {V}&fg=000000$$ to $$ {n}&fg=000000$$ elements produces a subspace $$ {V\_n}&fg=000000$$, and truncation of a general vector corresponds to finding its projection onto the subspace. It follows, then, that we need to find a projection operator $$ {\rho}&fg=000000$$, associated with the truncated basis. If the basis ($$ {\mathbf{e}}&fg=000000$$, say) is orthonormal we write  
$$ \displaystyle \rho = \sum\limits\_i e\_ie\_i^\* = \mathbf{ee}^{\dagger} \ \ \ \ \ (15)&fg=000000$$

which in a complete basis gives:  
$$ \displaystyle \rho = \sum\limits\_i |e\_i\rangle \langle e\_i| = \mathbf{1} \ \ \ \ \ (16)&fg=000000$$

If it is not an orthonormal basis, we must include the metric matrix $$ {\mathbf{S} = \mathbf{e}^{\dagger}\mathbf{e}}&fg=000000$$ (or L\"{o}wdin basis $$ {\mathbf{\overline{e}}\mathbf{S}^{-1/2}}&fg=000000$$):  
$$ \displaystyle \rho = \mathbf{eS}^{-1}\mathbf{e}^{\dagger} = \sum\limits\_{ij} e\_i (S^{-1})\_{ij}e\_j^\* \ \ \ \ \ (17)&fg=000000$$

When using a truncated basis in operator space, two kinds of projections are useful (Löwdin, 1977, 1982),  
$$ \displaystyle A' = \rho A \rho, \qquad A'' = A^{1/2} \rho A^{1/2} \ \ \ \ \ (18)&fg=000000$$

which are the outer projection and inner projection, respectively, onto space $$ {V\_n}&fg=000000$$ defined by $$ {\rho}&fg=000000$$. Note that $$ AB = C$$ does not imply $$ A'B' = C'$$ does not imply $$ A''B'' = C''$$. Plugging the metric into $$ {A''}&fg=000000$$:  
$$ \displaystyle A'' = A^{1/2}\mathbf{eS}^{-1}\mathbf{e}^{\dagger}A^{1/2} \ \ \ \ \ (19)&fg=000000$$

and we define  
$$ \displaystyle \mathbf{f} \equiv A^{1/2}\mathbf{e} = \left(A^{1/2}\mathbf{e}\_1 \quad A^{1/2}\mathbf{e}\_1 \quad \cdots \right) \ \ \ \ \ (20)&fg=000000$$

We assume that $$ {A}&fg=000000$$ is Hermitian and positive-definite, so that $$ {A^{1/2}}&fg=000000$$ can be defined. Note that $$ {\mathbf{S} = \mathbf{e}^{\dagger}\mathbf{e} = \left(A^{-1/2}\mathbf{f}\right)^{\dagger}\left(A^{-1/2}\mathbf{f}\right) = \mathbf{f}^{\dagger}A^{-1}\mathbf{f} \implies A'' = \mathbf{f}\left(\mathbf{f}^{\dagger}A^{-1}\mathbf{f}\right)^{-1}\mathbf{f}^{\dagger}}&fg=000000$$. Because $$ {A}&fg=000000$$ is arbitrary, replace it with $$ {A^{-1}}&fg=000000$$, and since $$ {\mathbf{f}^{\dagger}A\mathbf{f} = \mathbf{A}}&fg=000000$$ with $$ {A\_{ij} = \langle f\_i |A|f\_j\rangle}&fg=000000$$:  
$$ \displaystyle \left(\mathbf{A}^{-1}\right)'' = \mathbf{f}\left(\mathbf{f}^{\dagger}A\mathbf{f}\right)^{-1}\mathbf{f}^{\dagger} = \mathbf{fA}^{-1}\mathbf{f}^{\dagger} \ \ \ \ \ (21)&fg=000000$$

As the basis $$ {V\_n \rightarrow V}&fg=000000$$, the inner projection $$ {\rightarrow \mathbf{A}^{-1}}&fg=000000$$, else it is simply a finite basis approximation to the inverse. This is the operator inverse in terms of a matrix inverse. Since $$ {\mathbf{e}}&fg=000000$$ was an arbitrary basis defining $$ {V\_n}&fg=000000$$, let $$ {\mathbf{f}}&fg=000000$$ define n-dimensional subspace $$ {V\_n'}&fg=000000$$. Thus:  
$$ \displaystyle \mathbf{A}^{-1} \approx \mathbf{eA}^{-1}\mathbf{e}^{\dagger} = \sum\limits\_{ij} e\_i(\mathbf{e}^{\dagger}\mathbf{Ae})^{-1}\_{ij}\mathbf{e}^\*\_j \ \ \ \ \ (22)&fg=000000$$

Thus the inner projection leads to an approximation for the projector. Let us define the (as of yet undefined) operator basis:  
$$ \displaystyle \mathbf{n} = (\mathbf{n}\_1 \quad \mathbf{n}\_2 \quad \mathbf{n}\_3 \quad \cdots) \ \ \ \ \ (23)&fg=000000$$

Given that the binary product (compare with $$ {\langle x|y\rangle = x^\*y}&fg=000000$$ for vectors)  
$$ \displaystyle X^{\dagger} \cdot Y = (X|Y) = \langle 0 | \left[X^{\dagger},Y\right] | 0 \rangle \ \ \ \ \ (24)&fg=000000$$

then for our resolvent superoperator we have  
$$ \displaystyle \hat{R}(\omega) = (\hbar\omega\hat{1} - \hat{H})^{-1} = \mathbf{n}R(\omega)\mathbf{n}^{\dagger} = \sum\limits\_{r,s} \mathbf{n}\_r[R(\omega)]\_{rs}\mathbf{n}\_{s}^{\dagger} \ \ \ \ \ (25)&fg=000000$$

where $$ {\mathbf{n}\_r}&fg=000000$$ and $$ {\mathbf{n}\_s^{\dagger}}&fg=000000$$ are the analogues of $$ {\mathbf{e}}&fg=000000$$ and $$ {\mathbf{e}^\*}&fg=000000$$ in operator space. Finally, if  
$$ \displaystyle R(\omega) = M(\omega)^{-1}, \qquad M(\omega) = \mathbf{n}^{\dagger} (\hbar\omega\hat{1} - \hat{H})\mathbf{n} \ \ \ \ \ (26)&fg=000000$$

then we have  
$$ \displaystyle \langle \langle B;A \rangle \rangle\_{\omega} = B\cdot R(\omega)\cdot A = B \cdot \mathbf{n} R(\omega) \mathbf{n}^{\dagger} \cdot A \ \ \ \ \ (27)&fg=000000$$

which is the key to calculating approximations to response properties. The matrix M is determined once we have chosen an operator basis. This approximation depends on two things: 1) the basis $$ {\mathbf{n}}&fg=000000$$ (and its truncations), and 2) the reference function, that is not the exact ground state. Any approximations to these two things are where we get out various response methods.

\*typeset with [latex2wp](http://sourceforge.net/projects/latex2wp/)

