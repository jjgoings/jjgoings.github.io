--- 
layout: post 
title: Understanding the Relativistic Dirac Equation for a Free Particle 
---

[![Dirac]({{ site.baseurl }}/assets/dirac_4.jpg?w=203)](http://joshuagoings.files.wordpress.com/2014/03/dirac_4.jpg)

A PDF of below, which is much prettier:  [Dirac Equation](http://joshuagoings.files.wordpress.com/2014/03/dirac.pdf)

According to Einstein's special theory of relativity, the relation between energy ($$ {E}&fg=000000$$) and momentum ($$ {\mathbf{p}}&fg=000000$$) is given by the expression  
$$ \displaystyle E^2 = \mathbf{p}^2 c^2 + m\_0^2 c^4 \ \ \ \ \ (1)&fg=000000$$

This relates a particle's rest mass ($$ {m\_0}&fg=000000$$, which we will call $$ {m}&fg=000000$$ from here on out), momentum, and total energy. This equation sets time and space coordinates on equal footing (a requirement for Lorentz invariance), and is a suitable starting point for developing a relativistic quantum mechanics. Now, when we derive non-relativistic quantum mechanics (the Schrödinger equation) we make use of the correspondence principle and replace classical momentum and energy with their quantum mechanical operators  
$$ \displaystyle E \rightarrow i\hbar \frac{\partial}{\partial t} \ \ \ \ \ (2)&fg=000000$$

and  
$$ \displaystyle \mathbf{p} \rightarrow -i \hbar \nabla \ \ \ \ \ (3)&fg=000000$$

It would make sense then, to extend this idea and substitute the operators into the relativistic energy-momentum expression. Doing so gives  
$$ \displaystyle \left(i\hbar \frac{\partial}{\partial t}\right)^2 = \left(-i\hbar \nabla \right)^2 c^2 + m^2 c^4 \ \ \ \ \ (4)&fg=000000$$

which reduces to (and is more commonly seen as)  
$$ \displaystyle \left( \frac{1}{c^2}\frac{\partial^2}{\partial t^2} - \nabla^2 + \frac{m^2 c^2}{\hbar^2} \right)\psi = 0 \ \ \ \ \ (5)&fg=000000$$

Where $$ {\psi}&fg=000000$$ is our wave function. This equation is known as the Klein-Gordon equation and was one of the first attempts to merge special relativity with the Schrödinger equation. A couple things you might note about the Klein-Gordon equation right off the bat: first, it treats time and position equally as second order derivatives. This was one of the flaws in the non-relativistic Schrödinger equation, in that time was first order but position was second order. To be Lorentz invariant, and therefore a proper relativistic theory, both coordinates must be treated equally. The second thing you might notice is that the equation is spinless. Now, it turns out that the Klein-Gordon equation fails as a fundamental equation on account of not having a positive definite probability density. Probability can be negative in the Klein-Gordon equation! (Why? It turns out that having a time second derivative is the culprit. When integrating with respect to time, you can choose two independent integration constants for the wave function and its time derivative, which allow for both positive and negative probability densities.) Now, Feynman later re-interpreted the Klein-Gordon equation as an equation of motion for a spinless particle, so it isn't completely useless. It also turns out that the Dirac equation (which is a fundamental equation) solutions will always be solutions for the Klein-Gordon equation, just not the other way around.  
Okay, so the first attempt at deriving a relativistic Schrödinger equation didn't quite work out. We still want to use the energy-momentum relation, and we still want to use the correspondence principle, so what do we try next? Since the second order time derivatives caused the problems for Klein-Gordon, so let's try an equation of the form

$$ \displaystyle E = \sqrt{\mathbf{p}^2 c^2 + m^2 c^4} = c\sqrt{\mathbf{p}^2 + m^2 c^2} \ \ \ \ \ (6)&fg=000000$$

If we then insert the corresponding operators, we get  
$$ \displaystyle i\hbar\frac{\partial}{\partial t} = c \sqrt{-\hbar^2 \nabla^2 + m^2c^2} \ \ \ \ \ (7)&fg=000000$$

Now as you might have guessed, this form presents some problems because we can't easily solve for the square root of the squared momentum operator. We could try a series expansion of the form  
$$ \displaystyle i\hbar\frac{\partial}{\partial t} = mc^2 \sqrt{1 - \left(\frac{\hbar \nabla}{mc}\right)^2} = mc^2 - \frac{\hbar^2 \nabla^2}{2m} + \frac{\hbar^4 \nabla^4}{8m^3c^2} + \cdots \ \ \ \ \ (8)&fg=000000$$

But this gets quite complicated. Moreover, to be soluble we have to truncate at some point, and any truncation will destroy our Lorentz invariance. So we must look elsewhere to solve this problem. Dirac's insight was to go back to the argument of the square root operator and assume that it could be written as a perfect square. In other words, determine $$ {\mathbf{\alpha}}&fg=000000$$ and $$ {\beta}&fg=000000$$ such that  
$$ \displaystyle \mathbf{p}^2 + m^2c^2 = \left(\mathbf{\alpha} \cdot \mathbf{p} + \beta m c\right)^2 \ \ \ \ \ (9)&fg=000000$$

If we do this, the square root goes away, and we get the Dirac equation for a free particle.  
$$ \displaystyle i\hbar\frac{\partial}{\partial t} \psi = c \alpha \cdot \left( - i \hbar \nabla \right) \psi + \beta mc^2 \psi \ \ \ \ \ (10)&fg=000000$$

Of course, we have said absolutely nothing about what $$ {\alpha}&fg=000000$$ and $$ {\beta}&fg=000000$$ actually are. We can see that $$ {\alpha}&fg=000000$$ is going to have three components, just like momentum has $$ {x,y,z}&fg=000000$$, and that $$ {\beta}&fg=000000$$ will have a single component. To satisfy the ``perfect square'' constraint, we can ``distill'' out three constraints.  
$$ \displaystyle \alpha\_i^2 = \beta^2 = 1, \qquad \alpha\_i\alpha\_j = - \alpha\_j \alpha\_i, i \neq j, \qquad \alpha\_i\beta = -\beta\alpha\_i \ \ \ \ \ (11)&fg=000000$$

Well, there is no way we are going to satisfy the constraints with $$ {\alpha}&fg=000000$$ and $$ {\beta}&fg=000000$$ as scalars! So let's look to rank-2 matrices, such as the Pauli matrices:  
$$ \displaystyle \sigma\_x = \begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix} \ \ \ \ \ (12)&fg=000000$$

$$ \displaystyle \sigma\_y = \begin{bmatrix} 0 & -i \\ i & 0 \end{bmatrix} \ \ \ \ \ (13)&fg=000000$$

$$ \displaystyle \sigma\_z = \begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix} \ \ \ \ \ (14)&fg=000000$$

and the identity  
$$ \displaystyle \mathbf{I}\_2 = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} \ \ \ \ \ (15)&fg=000000$$

Well, while it might seem like these would work, unfortunately, we have to include the identity. Because the identity commutes with all of the rank-2 matrices, we will never get the proper commutation relations to satisfy the constraints above. So we must look to a higher rank. It turns out that the lowest rank that satisfies the Dirac equation constraints is the set of rank-4 unitary matrices  
$$ \displaystyle \alpha\_k = \begin{bmatrix} \mathbf{0}\_2 & \sigma\_k \\ \sigma\_k & \mathbf{0}\_2 \end{bmatrix}, k = x,y,z \ \ \ \ \ (16)&fg=000000$$

and  
$$ \displaystyle \beta = \begin{bmatrix} \mathbf{I}\_2 & \mathbf{0}\_2 \\ \mathbf{0}\_2 & \mathbf{I}\_2 \end{bmatrix} \ \ \ \ \ (17)&fg=000000$$

A few notes before we wrap things up here. First, these matrices are by no means unique. This representation of the $$ {\alpha}&fg=000000$$ matrices is known as the standard representation. Any other representation is just a similarity transformation away! For example, another representation is known as the Weyl representation. We also got the matrices purely by mathematical means. The use of Pauli matrices surely hints at a connection to spin. In the words of Dirac (1928): ``The $$ {\alpha}&fg=000000$$'s are new dynamical variables which it is necessary to introduce in order to satisfy the conditions of the problem. They may be regarded as describing some internal motions of the electron, which for most purposes may be taken as the spin of the electron postulated in previous theories''. You'll also note that the $$ {\alpha}&fg=000000$$'s are connected to the momentum operator, which suggests a coupling between spin and momentum. As for the $$ {\beta}&fg=000000$$, it can be interpreted as the inverse of the Lorentz $$ {\gamma}&fg=000000$$ factor in special relativity. Finally, you will also see that the solutions to the equation (which we haven't solved yet) will be rank-4. The wave function will be rank-4 as well, leading to four-component methods. Single electron wave functions of this type are known as ``4-spinors''. (Spinor is the relativistic analog to orbital.)

Questions? Comments? Find any errors? Let me know!

