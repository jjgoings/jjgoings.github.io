---
layout: post 
title: Equation of Motion (EOM) derivation of RPA
--- 


The Equation of Motion derivations of [excited state](http://en.wikipedia.org/wiki/Excited_state "Excited state") and response properties are elegant, and (in my opinion) very direct. Here I'll give an example of how it can be used to derive TDHF/RPA. We've already done it two other ways, and the agreement between them is important if we wish to extend these methods further.

Given an exact [ground state](http://en.wikipedia.org/wiki/Ground_state "Ground state"), we can say that

$$   H \vert  n \rangle = E_n \vert  n \rangle \ \ \ \ \  $$

Define operator $$ {Q_n^{\dagger}} $$ and $$ {Q_n} $$:  
$$   \vert  n \rangle = Q_n^{\dagger} \vert  0 \rangle, \qquad Q_n\vert  0 \rangle = 0 \implies Q_n^{\dagger} = \vert  n \rangle \langle 0 \vert  \ \ \ \ \  $$

These operators generate excited states from the ground state (not excited determinants, as in the case of post-HF correlation methods). So it is clear that, when acting on an exact ground state:

$$ [H, Q_n^{\dagger}]\vert  0 \rangle = (E_n - E_0)Q_n^{\dagger} \vert  0 \rangle = \hbar\omega_{0n} Q_n^{\dagger} \vert  0 \rangle $$

Multiply on left by arbitrary state of form $$ {\langle 0 \vert  \delta Q} $$, giving  
$$   \langle 0 \vert  [\delta Q, [H, Q_n^{\dagger}]]\vert  0 \rangle = \hbar\omega_{0n} \langle 0 \vert  [\delta Q, Q_n^{\dagger}] \vert  0 \rangle \ \ \ \ \  $$

Where we have made use of the fact that $$ {\langle 0 \vert Q_n^{\dagger} = \langle 0 \vert HQ_n^{\dagger} = 0} $$. Note that is we express $$ {Q} $$ by particle-hole operators $$ {a_p^{\dagger}a_q} $$, $$ {a_p^{\dagger}a_q^{\dagger}a_r a_s} $$ with coefficients $$ {C_{pq}} $$ and $$ {C_{pqrs}} $$, then $$ {\delta Q} $$ is given by $$ {\frac{\partial Q}{\partial C} \delta C} $$ for arbitrary variations $$ {\delta C} $$. These are in principle exact, since $$ {\delta Q \vert  0 \rangle} $$ exhausts the whole [Hilbert space](http://en.wikipedia.org/wiki/Hilbert_space "Hilbert space"), such that the above equation corresponds to the full [Schrödinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation"). Tamm-Dancoff (or [Configuration Interaction Singles](http://en.wikipedia.org/wiki/Configuration_interaction "Configuration interaction")) can be obtained by approximating $$ {\vert  0 \rangle \rightarrow \vert  \hbox{HF} \rangle} $$ and the operator $$ {Q_n^{\dagger} = \sum\limits_{ia} C_{ia} a_a^{\dagger}a_i} $$, restricting ourselves to 1p-1h excitations. Thus $$ {\delta Q \vert  0 \rangle = \sum_{ia} a_a^{\dagger}a_i \vert \hbox{HF} \rangle \delta C_{ai}} $$, ($$ {\delta C_{ai}} $$ cancels), and  
$$   \sum\limits_{bj} \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, [H, a_b^{\dagger}a_j]]\vert  \hbox{HF} \rangle C_{jb} = \hbar\omega \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, a_a^{\dagger}a_i] \vert  \hbox{HF} \rangle C_{ia} \ \ \ \ \  $$

These are the CIS equations. Put another way:  
$$   \sum\limits_{bj} \left\{(\epsilon_a - \epsilon_i)\delta_{ab}\delta_{ij} + \langle aj \vert \vert  ib \rangle \right\} C_{bj} = E^{CIS}C_{ai} \ \ \ \ \  $$

Similarly, for RPA/TDHF, if we consider a ground state containing 2p-2h correlations, we can not only create a p-h pair, but also destroy one. Thus (choosing the minus sign for convenience):  
$$   Q_n^{\dagger} = \sum\limits_{ia} X_{ia} a_a^{\dagger}a_i - \sum\limits_{ia} Y_{ia} a_i^{\dagger}a_a, \qquad \hbox{and} Q_n \vert  RPA \rangle = 0 \ \ \ \ \  $$

So instead of the basis of only single excitations, and therefore one matrix $$ {C_{ia}} $$, we work in a basis of single excitations and single de-excitations, and have two matrices $$ {X_{ia}} $$ and $$ {Y_{ia}} $$. We also have two kinds of variations $$ {\delta Q \vert  0 \rangle} $$, namely $$ {a_a^{\dagger}a_i \vert  0 \rangle} $$ and $$ {a_i^{\dagger}a_a \vert  0 \rangle} $$. This gives us two sets of equations:  
$$   \langle \hbox{RPA} \vert  [a_i^{\dagger}a_a, [H,Q_n^{\dagger}]]\vert \hbox{RPA} \rangle = \hbar \omega \langle \hbox{RPA} \vert  [a_i^{\dagger}a_a, Q_n^{\dagger}] \vert \hbox{RPA} \rangle \notag \ \ \ \ \  $$

$$   \langle \hbox{RPA} \vert  [a_a^{\dagger}a_i, [H,Q_n^{\dagger}]]\vert \hbox{RPA} \rangle = \hbar \omega \langle \hbox{RPA} \vert  [a_a^{\dagger}a_i, Q_n^{\dagger}] \vert \hbox{RPA} \rangle \ \ \ \ \  $$

These contain only expectation values of our four Fermion operators, which cannot be calculated since we still do not know $$ {\vert \hbox{RPA} \rangle} $$. Thus we assume $$ {\vert \hbox{RPA} \rangle \rightarrow \vert \hbox{HF} \rangle} $$. This gives  
$$   \langle \hbox{RPA} \vert  [a_i^{\dagger}a_a, a_b^{\dagger}a_j] \vert \hbox{RPA} \rangle = \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, a_b^{\dagger}a_j] \vert \hbox{HF} \rangle = \delta_{ij}\delta_{ab} \ \ \ \ \  $$

The probability of finding states $$ {a_a^{\dagger}a_i \vert  0 \rangle} $$ and $$ {a_i^{\dagger}a_a \vert  0 \rangle} $$ in excited state $$ {\vert n\rangle} $$, that is, the p-h and h-p matrix elements of transition density matrix $$ {\rho^{(1)}} $$ are:  
$$   \rho^{(1)}_{ai} = \langle 0 \vert  a_i^{\dagger}a_a \vert  n \rangle \simeq \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, Q_n^{\dagger}] \vert \hbox{HF} \rangle = X_{ia} \ \ \ \ \  $$

$$   \rho^{(1)}_{ia} = \langle 0 \vert  a_a^{\dagger}a_i \vert  n \rangle \simeq \langle \hbox{HF} \vert  [a_a^{\dagger}a_i, Q_n^{\dagger}] \vert \hbox{HF} \rangle = Y_{ia} \ \ \ \ \  $$

Thus altogether  
$$   \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^* & \mathbf{A}^* \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \  $$

with  
$$   A_{ia,jb} = \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, [H,a_b^{\dagger}a_j]]\vert \hbox{HF} \rangle \ \ \ \ \  $$

and  
$$   B_{ia,jb} = - \langle \hbox{HF} \vert  [a_i^{\dagger}a_a, [H,a_j^{\dagger}a_b]]\vert \hbox{HF} \rangle \ \ \ \ \  $$

which are the TDHF/RPA equations.


