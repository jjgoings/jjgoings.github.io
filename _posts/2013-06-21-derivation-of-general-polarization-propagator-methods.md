---
layout: post 
title: Derivation of general polarization propagator methods 
---


Most higher-order response methods use some form of the polarization [propagator](http://en.wikipedia.org/wiki/Propagator "Propagator"), which is what I intend to derive here. It can then be used to derive other methods, such as TDHF/RPA and SOPPA.

We have derived earlier a response function, or frequency dependent polarizability,

$$   \Pi(BA\vert  \omega) = \lim_{\eta \rightarrow 0} \left(\frac{1}{\hbar}\right) \sum\limits_{n\neq0} \left\{ \frac{\langle 0 \vert  B \vert  n\rangle\langle n \vert  A \vert 0\rangle}{\omega + i\eta - \omega_{0n}} - \frac{\langle 0 \vert  A \vert  n\rangle \langle n \vert  B \vert  0 \rangle}{\omega + i\eta + \omega_{0n}} \right\} \ \ \ \ \ (1) $$

where $$ {A} $$ is the applied perturbation, and $$ {B} $$ is the observable, and both are assumed to be Hermitian. $$ {\omega_{0n}} $$ is the excitation energy for the change between states $$ {0} $$ and $$ {n} $$. It should be clear that the response function has poles when $$ {\omega} $$ --- the applied field frequency -- equals to the excitation energy $$ {\omega_{0n}} $$. Finding these poles is precisely the goal of polarization propagator methods. In the polarization propagator approach, the above equation has $$ {\eta} $$ set to 0, and the response function (the `propagator'), defined as:  
$$   \langle \langle B;A \rangle \rangle_{\omega} \equiv \sum\limits_{n\neq0} \left\{ \frac{\langle 0 \vert  B \vert  n\rangle\langle n \vert  A \vert 0\rangle}{\hbar\omega - \hbar\omega_{0n}} + \frac{\langle 0 \vert  A \vert  n\rangle \langle n \vert  B \vert  0 \rangle}{-\hbar\omega - \hbar\omega_{0n}} \right\} \ \ \ \ \ (2) $$

Now we want to describe the propagator in terms of commutators between $$ {A} $$ and $$ {B} $$. Make the observation that $$ {\frac{ab}{c+d} = \frac{ab}{c} - \frac{d}{c}\left(\frac{ab}{c+d}\right)} $$, and applying to the first term of the above yields:  
$$   \sum\limits_{n\neq0} \frac{\langle 0 \vert  B \vert  n\rangle\langle n \vert  A \vert 0\rangle}{\hbar\omega - \hbar\omega_{0n}} = \sum\limits_{n\neq0} \frac{\langle 0 \vert  B \vert  n\rangle\langle n \vert  A \vert 0\rangle}{\hbar\omega} -\sum\limits_{n\neq0} \frac{-\hbar\omega_{0n}\langle 0 \vert  B \vert  n\rangle\langle n \vert  A \vert 0\rangle}{\hbar\omega\left(\hbar\omega - \hbar\omega_{0n}\right)} \ \ \ \ \ (3) $$

Do the same for the second term and combine, recognizing that the $$ {n=0} $$ term vanishes in the first part (thus we get a sum over all $$ {n} $$), and making use of the fact that $$ {1 = \sum\limits_{n}\vert n\rangle\langle n\vert } $$ and $$ {H\vert  n \rangle = E_n\vert n\rangle} $$ and $$ {\hbar\omega_{0n} = E_n - E_0} $$:  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \frac{1}{\hbar\omega} \langle 0 \vert  \left[B,A\right] \vert  0 \rangle + \frac{1}{\hbar\omega} \sum\limits_{n\neq0} \left\{\frac{\langle 0 \vert  B \vert  n\rangle\langle n \vert \left[H,A\right] \vert 0\rangle}{\hbar\omega - \hbar\omega_{0n}} + \frac{\langle 0 \vert  \left[H,A\right] \vert  n\rangle\langle n \vert  B \vert 0\rangle}{-\hbar\omega - \hbar\omega_{0n}}\right\} \ \ \ \ \ (4) $$

Which is to say that  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \frac{1}{\hbar\omega} \langle 0 \vert  \left[B,A\right] \vert  0 \rangle + \frac{1}{\hbar\omega}\langle \langle B;\left[H,A\right] \rangle \rangle_{\omega} \ \ \ \ \ (5) $$

Or, as we will use it:  
$$   \hbar\omega\langle \langle B;A \rangle \rangle_{\omega} = \langle 0 \vert  \left[B,A\right] \vert  0 \rangle - \langle \langle \left[H,B\right] A \rangle \rangle_{\omega} \ \ \ \ \ (6) $$

As you may have started to see, we can define the propagator iteratively in terms of commutator expectation values of ever-increasing complexity. This is what is known as the so-called ''moment expansion'' of the propagator. Thus by iteration:  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \frac{1}{\hbar\omega} \left\{ \langle 0 \vert  \left[B,A\right] \vert  0 \rangle + \left(\frac{-1}{\hbar\omega}\right)\langle 0 \vert  \left[\left[H,B\right],A\right] \vert  0 \rangle + \left(\frac{-1}{\hbar\omega}\right)^2\langle 0 \vert  \left[\left[H,\left[H,B\right]\right],A\right] \vert  0 \rangle + \cdots \right\} \ \ \ \ \ (7) $$

We introduce the ''superoperator'' (analogous to the [Liouville operator](http://en.wikipedia.org/wiki/Liouville%27s_theorem_%28Hamiltonian%29 "Liouville's theorem (Hamiltonian)") in Statistical Mechanics), which acts on operators to give their commutator:

$$   \hat{H}B = \left[H,B\right], \qquad \hat{H}^2B = \left[H,\left[H,B\right]\right], \qquad \hat{H}^3B = \left[H,\left[H,\left[H,B\right]\right]\right], \qquad \cdots \ \ \ \ \ (8) $$

With this definition, we have the power series  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \frac{1}{\hbar\omega} \sum\limits_{n=0}^{\infty} \left(\frac{-1}{\hbar\omega}\right)^n \langle 0 \vert  \left[\hat{H}^nB,A\right]\vert 0\rangle \ \ \ \ \ (9) $$

At this point we make two useful observations. First, recognize that  
$$   \langle 0 \vert  \left[\hat{H}B,A\right]\vert 0\rangle = -\langle0\vert \left[B,\hat{H}A\right]\vert 0\rangle \ \ \ \ \ (10) $$

and so $$ {\hat{H}} $$ can be applied to $$ {A} $$ instead of $$ {B} $$ insofar as we introduce a factor of $$ {(-1)^n} $$. Furthermore, note that the power series is equivalent to  
$$   \frac{1}{1-x} = 1 + x + x^2 + x^3 + \cdots \ \ \ \ \ (11) $$

Making use of these two observations (and using $$ {\hat{1}X = X} $$ and $$ {\hat{H}^0 = \hat{1}} $$, where $$ {\hat{1}} $$ is the unit superoperator), we have  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \langle 0 \vert  \left[B,\left(\hbar\omega\hat{1} - \hat{H}\right)^{-1}A\right]\vert 0\rangle \ \ \ \ \ (12) $$

Which is merely a cosmetic change at this point, as the superoperator resolvent is defined by the series expansion. We need to find a matrix representation of the resolvent, which implies that we find a complete basis set of operators. To do this, we are going to develop an operator space, where $$ {\hat{H}} $$ is defined by its effect on operators instead of vectors. Introducing the notation  
$$   \left(X\vert Y\right) = \langle 0 \vert  \left[X^{\dagger},Y\right] \vert  0 \rangle \ \ \ \ \ (13) $$

and it follows that $$ {\left(Y\vert X\right) = \left(X\vert Y\right)^*} $$. As defined, we now have  
$$   \langle \langle B;A \rangle \rangle_{\omega} = \left(B^{\dagger}\vert \left(\hbar\omega\hat{1} - \hat{H}\right)^{-1}\vert  A \right) \ \ \ \ \ (14) $$

Which is formally exact, albeit useless until we develop approximations. However, the form of the above equation does look similar to ordinary vector spaces in [Hartree-Fock](http://en.wikipedia.org/wiki/Hartree%E2%80%93Fock_method "Hartree–Fock method"), etc. methods. Truncation of a basis in linear vector space $$ {V} $$ to $$ {n} $$ elements produces a subspace $$ {V_n} $$, and truncation of a general vector corresponds to finding its projection onto the subspace. It follows, then, that we need to find a projection operator $$ {\rho} $$, associated with the truncated basis. If the basis ($$ {\mathbf{e}} $$, say) is orthonormal we write  
$$   \rho = \sum\limits_i e_ie_i^* = \mathbf{ee}^{\dagger} \ \ \ \ \ (15) $$

which in a complete basis gives:  
$$   \rho = \sum\limits_i \vert e_i\rangle \langle e_i\vert  = \mathbf{1} \ \ \ \ \ (16) $$

If it is not an orthonormal basis, we must include the metric matrix $$ {\mathbf{S} = \mathbf{e}^{\dagger}\mathbf{e}} $$ (or L\"{o}wdin basis $$ {\mathbf{\overline{e}}\mathbf{S}^{-1/2}} $$):  
$$   \rho = \mathbf{eS}^{-1}\mathbf{e}^{\dagger} = \sum\limits_{ij} e_i (S^{-1})_{ij}e_j^* \ \ \ \ \ (17) $$

When using a truncated basis in operator space, two kinds of projections are useful (Löwdin, 1977, 1982),  
$$   A' = \rho A \rho, \qquad A'' = A^{1/2} \rho A^{1/2} \ \ \ \ \ (18) $$

which are the outer projection and inner projection, respectively, onto space $$ {V_n} $$ defined by $$ {\rho} $$. Note that $$ AB = C$$ does not imply $$ A'B' = C'$$ does not imply $$ A''B'' = C''$$. Plugging the metric into $$ {A''} $$:  
$$   A'' = A^{1/2}\mathbf{eS}^{-1}\mathbf{e}^{\dagger}A^{1/2} \ \ \ \ \ (19) $$

and we define  
$$   \mathbf{f} \equiv A^{1/2}\mathbf{e} = \left(A^{1/2}\mathbf{e}_1 \quad A^{1/2}\mathbf{e}_1 \quad \cdots \right) \ \ \ \ \ (20) $$

We assume that $$ {A} $$ is Hermitian and positive-definite, so that $$ {A^{1/2}} $$ can be defined. Note that $$ {\mathbf{S} = \mathbf{e}^{\dagger}\mathbf{e} = \left(A^{-1/2}\mathbf{f}\right)^{\dagger}\left(A^{-1/2}\mathbf{f}\right) = \mathbf{f}^{\dagger}A^{-1}\mathbf{f} \implies A'' = \mathbf{f}\left(\mathbf{f}^{\dagger}A^{-1}\mathbf{f}\right)^{-1}\mathbf{f}^{\dagger}} $$. Because $$ {A} $$ is arbitrary, replace it with $$ {A^{-1}} $$, and since $$ {\mathbf{f}^{\dagger}A\mathbf{f} = \mathbf{A}} $$ with $$ {A_{ij} = \langle f_i \vert A\vert f_j\rangle} $$:  
$$   \left(\mathbf{A}^{-1}\right)'' = \mathbf{f}\left(\mathbf{f}^{\dagger}A\mathbf{f}\right)^{-1}\mathbf{f}^{\dagger} = \mathbf{fA}^{-1}\mathbf{f}^{\dagger} \ \ \ \ \ (21) $$

As the basis $$ {V_n \rightarrow V} $$, the inner projection $$ {\rightarrow \mathbf{A}^{-1}} $$, else it is simply a finite basis approximation to the inverse. This is the operator inverse in terms of a matrix inverse. Since $$ {\mathbf{e}} $$ was an arbitrary basis defining $$ {V_n} $$, let $$ {\mathbf{f}} $$ define n-dimensional subspace $$ {V_n'} $$. Thus:  
$$   \mathbf{A}^{-1} \approx \mathbf{eA}^{-1}\mathbf{e}^{\dagger} = \sum\limits_{ij} e_i(\mathbf{e}^{\dagger}\mathbf{Ae})^{-1}_{ij}\mathbf{e}^*_j \ \ \ \ \ (22) $$

Thus the inner projection leads to an approximation for the projector. Let us define the (as of yet undefined) operator basis:  
$$   \mathbf{n} = (\mathbf{n}_1 \quad \mathbf{n}_2 \quad \mathbf{n}_3 \quad \cdots) \ \ \ \ \ (23) $$

Given that the binary product (compare with $$ {\langle x\vert y\rangle = x^*y} $$ for vectors)  
$$   X^{\dagger} \cdot Y = (X\vert Y) = \langle 0 \vert  \left[X^{\dagger},Y\right] \vert  0 \rangle \ \ \ \ \ (24) $$

then for our resolvent superoperator we have  
$$   \hat{R}(\omega) = (\hbar\omega\hat{1} - \hat{H})^{-1} = \mathbf{n}R(\omega)\mathbf{n}^{\dagger} = \sum\limits_{r,s} \mathbf{n}_r[R(\omega)]_{rs}\mathbf{n}_{s}^{\dagger} \ \ \ \ \ (25) $$

where $$ {\mathbf{n}_r} $$ and $$ {\mathbf{n}_s^{\dagger}} $$ are the analogues of $$ {\mathbf{e}} $$ and $$ {\mathbf{e}^*} $$ in operator space. Finally, if  
$$   R(\omega) = M(\omega)^{-1}, \qquad M(\omega) = \mathbf{n}^{\dagger} (\hbar\omega\hat{1} - \hat{H})\mathbf{n} \ \ \ \ \ (26) $$

then we have  
$$   \langle \langle B;A \rangle \rangle_{\omega} = B\cdot R(\omega)\cdot A = B \cdot \mathbf{n} R(\omega) \mathbf{n}^{\dagger} \cdot A \ \ \ \ \ (27) $$

which is the key to calculating approximations to response properties. The matrix M is determined once we have chosen an operator basis. This approximation depends on two things: 1) the basis $$ {\mathbf{n}} $$ (and its truncations), and 2) the reference function, that is not the exact ground state. Any approximations to these two things are where we get out various response methods.


