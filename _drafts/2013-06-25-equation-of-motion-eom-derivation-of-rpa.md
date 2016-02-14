---
layout: post 
title: Equation of Motion (EOM) derivation of RPA
--- 

[PDF copy of below](http://joshuagoings.files.wordpress.com/2013/06/eomrpa.pdf)

The Equation of Motion derivations of [excited state](http://en.wikipedia.org/wiki/Excited_state "Excited state") and response properties are elegant, and (in my opinion) very direct. Here I'll give an example of how it can be used to derive TDHF/RPA. We've already done it [two](http://joshuagoings.wordpress.com/2013/05/03/derivation-of-time-dependent-hartree-fock-tdhf-equations/ "Derivation of Time Dependent Hartree-Fock (TDHF) Equations") other ways, and the agreement between them is important if we wish to extend these methods further.

Given an exact [ground state](http://en.wikipedia.org/wiki/Ground_state "Ground state"), we can say that

$latex \displaystyle H | n \rangle = E\_n | n \rangle \ \ \ \ \ &fg=000000$

Define operator $latex {Q\_n^{\dagger}}&fg=000000$ and $latex {Q\_n}&fg=000000$:  
$latex \displaystyle | n \rangle = Q\_n^{\dagger} | 0 \rangle, \qquad Q\_n| 0 \rangle = 0 \implies Q\_n^{\dagger} = | n \rangle \langle 0 | \ \ \ \ \ &fg=000000$

These operators generate excited states from the ground state (not excited determinants, as in the case of post-HF correlation methods). So it is clear that, when acting on an exact ground state:

$latex [H, Q\_n^{\dagger}]| 0 \rangle = (E\_n - E\_0)Q\_n^{\dagger} | 0 \rangle = \hbar\omega\_{0n} Q\_n^{\dagger} | 0 \rangle $

Multiply on left by arbitrary state of form $latex {\langle 0 | \delta Q}&fg=000000$, giving  
$latex \displaystyle \langle 0 | [\delta Q, [H, Q\_n^{\dagger}]]| 0 \rangle = \hbar\omega\_{0n} \langle 0 | [\delta Q, Q\_n^{\dagger}] | 0 \rangle \ \ \ \ \ &fg=000000$

Where we have made use of the fact that $latex {\langle 0 |Q\_n^{\dagger} = \langle 0 |HQ\_n^{\dagger} = 0}&fg=000000$. Note that is we express $latex {Q}&fg=000000$ by particle-hole operators $latex {a\_p^{\dagger}a\_q}&fg=000000$, $latex {a\_p^{\dagger}a\_q^{\dagger}a\_r a\_s}&fg=000000$ with coefficients $latex {C\_{pq}}&fg=000000$ and $latex {C\_{pqrs}}&fg=000000$, then $latex {\delta Q}&fg=000000$ is given by $latex {\frac{\partial Q}{\partial C} \delta C}&fg=000000$ for arbitrary variations $latex {\delta C}&fg=000000$. These are in principle exact, since $latex {\delta Q | 0 \rangle}&fg=000000$ exhausts the whole [Hilbert space](http://en.wikipedia.org/wiki/Hilbert_space "Hilbert space"), such that the above equation corresponds to the full [Schrödinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation"). Tamm-Dancoff (or [Configuration Interaction Singles](http://en.wikipedia.org/wiki/Configuration_interaction "Configuration interaction")) can be obtained by approximating $latex {| 0 \rangle \rightarrow | \hbox{HF} \rangle}&fg=000000$ and the operator $latex {Q\_n^{\dagger} = \sum\limits\_{ia} C\_{ia} a\_a^{\dagger}a\_i}&fg=000000$, restricting ourselves to 1p-1h excitations. Thus $latex {\delta Q | 0 \rangle = \sum\_{ia} a\_a^{\dagger}a\_i |\hbox{HF} \rangle \delta C\_{ai}}&fg=000000$, ($latex {\delta C\_{ai}}&fg=000000$ cancels), and  
$latex \displaystyle \sum\limits\_{bj} \langle \hbox{HF} | [a\_i^{\dagger}a\_a, [H, a\_b^{\dagger}a\_j]]| \hbox{HF} \rangle C\_{jb} = \hbar\omega \langle \hbox{HF} | [a\_i^{\dagger}a\_a, a\_a^{\dagger}a\_i] | \hbox{HF} \rangle C\_{ia} \ \ \ \ \ &fg=000000$

These are the CIS equations. Put another way:  
$latex \displaystyle \sum\limits\_{bj} \left\{(\epsilon\_a - \epsilon\_i)\delta\_{ab}\delta\_{ij} + \langle aj || ib \rangle \right\} C\_{bj} = E^{CIS}C\_{ai} \ \ \ \ \ &fg=000000$

Similarly, for RPA/TDHF, if we consider a ground state containing 2p-2h correlations, we can not only create a p-h pair, but also destroy one. Thus (choosing the minus sign for convenience):  
$latex \displaystyle Q\_n^{\dagger} = \sum\limits\_{ia} X\_{ia} a\_a^{\dagger}a\_i - \sum\limits\_{ia} Y\_{ia} a\_i^{\dagger}a\_a, \qquad \hbox{and} Q\_n | RPA \rangle = 0 \ \ \ \ \ &fg=000000$

So instead of the basis of only single excitations, and therefore one matrix $latex {C\_{ia}}&fg=000000$, we work in a basis of single excitations and single de-excitations, and have two matrices $latex {X\_{ia}}&fg=000000$ and $latex {Y\_{ia}}&fg=000000$. We also have two kinds of variations $latex {\delta Q | 0 \rangle}&fg=000000$, namely $latex {a\_a^{\dagger}a\_i | 0 \rangle}&fg=000000$ and $latex {a\_i^{\dagger}a\_a | 0 \rangle}&fg=000000$. This gives us two sets of equations:  
$latex \displaystyle \langle \hbox{RPA} | [a\_i^{\dagger}a\_a, [H,Q\_n^{\dagger}]]|\hbox{RPA} \rangle = \hbar \omega \langle \hbox{RPA} | [a\_i^{\dagger}a\_a, Q\_n^{\dagger}] |\hbox{RPA} \rangle \notag \ \ \ \ \ &fg=000000$

$latex \displaystyle \langle \hbox{RPA} | [a\_a^{\dagger}a\_i, [H,Q\_n^{\dagger}]]|\hbox{RPA} \rangle = \hbar \omega \langle \hbox{RPA} | [a\_a^{\dagger}a\_i, Q\_n^{\dagger}] |\hbox{RPA} \rangle \ \ \ \ \ &fg=000000$

These contain only expectation values of our four Fermion operators, which cannot be calculated since we still do not know $latex {|\hbox{RPA} \rangle}&fg=000000$. Thus we assume $latex {|\hbox{RPA} \rangle \rightarrow |\hbox{HF} \rangle}&fg=000000$. This gives  
$latex \displaystyle \langle \hbox{RPA} | [a\_i^{\dagger}a\_a, a\_b^{\dagger}a\_j] |\hbox{RPA} \rangle = \langle \hbox{HF} | [a\_i^{\dagger}a\_a, a\_b^{\dagger}a\_j] |\hbox{HF} \rangle = \delta\_{ij}\delta\_{ab} \ \ \ \ \ &fg=000000$

The probability of finding states $latex {a\_a^{\dagger}a\_i | 0 \rangle}&fg=000000$ and $latex {a\_i^{\dagger}a\_a | 0 \rangle}&fg=000000$ in excited state $latex {|n\rangle}&fg=000000$, that is, the p-h and h-p matrix elements of transition density matrix $latex {\rho^{(1)}}&fg=000000$ are:  
$latex \displaystyle \rho^{(1)}\_{ai} = \langle 0 | a\_i^{\dagger}a\_a | n \rangle \simeq \langle \hbox{HF} | [a\_i^{\dagger}a\_a, Q\_n^{\dagger}] |\hbox{HF} \rangle = X\_{ia} \ \ \ \ \ &fg=000000$

$latex \displaystyle \rho^{(1)}\_{ia} = \langle 0 | a\_a^{\dagger}a\_i | n \rangle \simeq \langle \hbox{HF} | [a\_a^{\dagger}a\_i, Q\_n^{\dagger}] |\hbox{HF} \rangle = Y\_{ia} \ \ \ \ \ &fg=000000$

Thus altogether  
$latex \displaystyle \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B}^\* & \mathbf{A}^\* \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \hbar\omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{-1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} \ \ \ \ \ &fg=000000$

with  
$latex \displaystyle A\_{ia,jb} = \langle \hbox{HF} | [a\_i^{\dagger}a\_a, [H,a\_b^{\dagger}a\_j]]|\hbox{HF} \rangle \ \ \ \ \ &fg=000000$

and  
$latex \displaystyle B\_{ia,jb} = - \langle \hbox{HF} | [a\_i^{\dagger}a\_a, [H,a\_j^{\dagger}a\_b]]|\hbox{HF} \rangle \ \ \ \ \ &fg=000000$

which are the TDHF/RPA equations.

\*typeset using [latex2wp](http://sourceforge.net/projects/latex2wp/?source=dlp)

