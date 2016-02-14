--- 
layout: post 
title: Kinetic Balance
--- 

[PDF](http://joshuagoings.files.wordpress.com/2014/04/kinetic-balance.pdf)

Kinetic balance was discovered when early attempts at relativistic SCF calculations failed to converge to a bound state. Often, the energy was too low because of the negative energy continuum. The crux of the problem was that the four components of the spinor in relativistic methods were each allowed to vary independently. In other words, scientists treated each component with its own, independent basis without regard to how the components depended on each other. This problem was eventually solved by paying attention to the non-relativistic limit of the kinetic energy, and noting that the small and large components of the four-spinor are not independent. There is, in fact, a coupling that we refer to as ``kinetic balance''. I'll show you how it works.

First, as you may have guessed, we only need to consider the one-electron operator. This is the matrix form of the Dirac equation, and it contains (in addition to other terms) the contributions to the kinetic energy. Written as a pair of coupled equations, we have

$$ \displaystyle \begin{array}{c} \left[\mathbf{V}^{LL} - E \mathbf{S}^{LL} \right] \mathbf{c}^L + c \mathbf{\Pi}^{LS} \mathbf{c}^S = 0 \\ c \mathbf{\Pi}^{SL} \mathbf{c}^L + \left[\mathbf{V}^{SS} - (2mc^2 + E)\mathbf{S}^{SS}\right]\mathbf{c}^S = 0 \end{array} \ \ \ \ \ (1)&fg=000000$$

Where $$ {\mathbf{V}^{LL} = \langle \chi^{L} | V | \chi^{L} \rangle}&fg=000000$$, $$ {\mathbf{S}^{LL} = \langle \chi^{L} | \chi^{L} \rangle}&fg=000000$$, and $$ {\mathbf{\Pi}^{LS} = \langle \chi^{L} | -i\hbar \mathbf{\sigma} \cdot \mathbf{\nabla} | \chi^{S} \rangle}&fg=000000$$, and so on. These are the potential, overlap, and momentum terms of the Dirac equation in a basis $$ {| \chi \rangle}&fg=000000$$.

Now, if we look at the second of the two paired equations, we note that for potentials of chemical interest (e.g. molecular or atomic), $$ {\mathbf{V}^{SS}}&fg=000000$$ is negative definite. We also know that when we solve the equation, we are looking for and energy above the negative energy continuum, which is to say we want $$ {E \> -2mc^2}&fg=000000$$. Since the overlap is positive definite, putting all of these constraints together mean that we have a nonsingular matrix (and therefore invertible!) matrix in the second of our coupled equations. We can rewrite the second equation as

$$ \displaystyle \mathbf{c}^S = \left[(2mc^2 + E)\mathbf{S}^{SS} - \mathbf{V}^{SS} \right]^{-1}c\mathbf{\Pi}^{SL} \mathbf{c}^L \ \ \ \ \ (2)&fg=000000$$

Substituting this expression back into the first (top) equation yields

$$ \displaystyle \left[\mathbf{V}^{LL} - E \mathbf{S}^{LL} \right] \mathbf{c}^L + c \mathbf{\Pi}^{LS} \left[(2mc^2 + E)\mathbf{S}^{SS} - \mathbf{V}^{SS} \right]^{-1}c\mathbf{\Pi}^{SL} \mathbf{c}^L = 0 \ \ \ \ \ (3)&fg=000000$$

This form is very useful for analysis. Now, we are going to use the matrix relation

$$ \displaystyle (\mathbf{A} - \mathbf{B})^{-1} = \mathbf{A}^{-1} + \mathbf{A}^{-1}\mathbf{B}(\mathbf{A}-\mathbf{B})^{-1} \ \ \ \ \ (4)&fg=000000$$

with $$ {\mathbf{A} = 2mc^2\mathbf{S}^{SS}}&fg=000000$$ and $$ {\mathbf{B} = \mathbf{V}^{SS} - E\mathbf{S}^{SS}}&fg=000000$$. This leads to the rather long expression

$$ \displaystyle \begin{array}{c} \left[\mathbf{V}^{LL} - E\mathbf{S}^{LL} + \frac{1}{2m} \mathbf{\Pi}^{LS} \left[\mathbf{S}^{SS}\right]^{-1}\mathbf{\Pi}^{SL}\right] \mathbf{c}^{L} = \cdots \\ \cdots = \frac{1}{2m}\mathbf{\Pi}^{LS}\left[\mathbf{S}^{SS}\right]^{-1} \left[\mathbf{V}^{SS} - E\mathbf{S}^{SS}\right]\left[\mathbf{V}^{SS} - (2mc^2+E)\mathbf{S}^{SS}\right]^{-1} \mathbf{\Pi}^{SL}\mathbf{c}^{L} \end{array} \ \ \ \ \ (5)&fg=000000$$

Why this ridiculous form? Look closely at each side and their dependence on the speed of light, $$ {c}&fg=000000$$. The left hand side has the $$ {c^0}&fg=000000$$ terms, and the right hand side has the $$ {c^{-2}}&fg=000000$$ terms. Since the non relativistic limit is found when the speed of light is infinite ($$ {c \rightarrow \infty}&fg=000000$$), the whole right hand side goes to zero. This gives us

$$ \displaystyle \left[\mathbf{V}^{LL} - E\mathbf{S}^{LL} + \frac{1}{2m} \mathbf{\Pi}^{LS} \left[\mathbf{S}^{SS}\right]^{-1}\mathbf{\Pi}^{SL}\right] \mathbf{c}^{L} = 0 \ \ \ \ \ (6)&fg=000000$$

Now, if this is indeed the true non-relativistic limit, then we find that our kinetic energy term $$ {\mathbf{T}^{LL}}&fg=000000$$ is given by

$$ \displaystyle \mathbf{T}^{LL} = \frac{1}{2m} \mathbf{\Pi}^{LS} \left[\mathbf{S}^{SS}\right]^{-1}\mathbf{\Pi}^{SL} \ \ \ \ \ (7)&fg=000000$$

Or, more explicitly,

$$ \displaystyle T^{LL}\_{\mu \nu} = \frac{-\hbar^2}{2m} \sum\limits\_{\kappa \lambda} \langle \chi\_{\mu}^{L} | \mathbf{\sigma}\cdot\mathbf{\nabla}| \chi\_{\kappa}^{S} \langle \left[S^{SS}\right]\_{\kappa \lambda}^{-1} \langle \chi\_{\lambda}^{S} | \mathbf{\sigma} \cdot \mathbf{\nabla} | \chi\_{\nu}^{L} \rangle \ \ \ \ \ (8)&fg=000000$$

Where that inner part, $$ {| \chi\_{\kappa}^{S} \langle \left[S^{SS}\right]\_{\kappa \lambda}^{-1} \langle \chi\_{\lambda}^{S} |}&fg=000000$$, is an inner projection onto the small component basis space. Less formally, the small component is the ``mathematical glue'' that connects the two momentum operators. If the small component spans the same space as the momentum operators in the large component space, $$ {\{\sigma\cdot\nabla\chi\_{\mu}^{L}\}}&fg=000000$$, then that inner projection just becomes the identity. This means that the expression becomes

$$ \displaystyle T\_{\mu \nu} = \frac{-\hbar^2}{2m}\langle \chi\_{\mu}^{L} | (\mathbf{\sigma}\cdot\mathbf{\nabla})(\mathbf{\sigma} \cdot \mathbf{\nabla}) | \chi\_{\nu}^{L} \rangle = \frac{-\hbar^2}{2m} \langle \chi\_{\mu}^{L} | \mathbf{\nabla}^2 | \chi\_{\nu}^{L} \rangle \ \ \ \ \ (9)&fg=000000$$

Which is the kinetic energy term in the non-relativistic formulation! (N.B. We used the relation $$ {(\mathbf{\sigma}\cdot\mathbf{\nabla})(\mathbf{\sigma}\cdot\mathbf{\nabla}) = \mathbf{\nabla}^2}&fg=000000$$).

So, when we set up our relativistic calculations, as long as we have the constraint that

$$ \displaystyle \chi\_{\mu}^{S} = (\mathbf{\sigma}\cdot\mathbf{p})\chi\_{\mu}^{L} \ \ \ \ \ (10)&fg=000000$$

Then we will find that we recover the correct non-relativistic limit of our equations. The basis is called ``kinetically balanced'', and we won't collapse to energies lower than $$ {-2mc^2}&fg=000000$$.

A few stray observations before we finish. First, if we enforce the relation between small and large component basis functions, then we find that $$ {\mathbf{\Pi}^{SL} = \mathbf{S}^{SS}}&fg=000000$$ and $$ {\mathbf{\Pi}^{LS} = 2m\mathbf{T}^{LL} = 2m\mathbf{T}}&fg=000000$$. Second, this constraint actually maximizes kinetic energy, and any approximation that does not satisfy the kinetic balance condition will lower the energy. This was weird to me coming from the non relativistic Hartree-Fock background, where variationally, if you remove basis functions you raise the energy. The thing is that when doing relativistic calculations, you aren't bounded from below like their non-relativistic counterparts. While you can get variational stability, you are actually doing an ``excited state'' calculation (I am using the term ``excited state'' very loosely). Kind of odd, but the negative energy continuum does exist, and was a big factor in the predicting the existence of antimatter.

Finally, modern methods of relativistic electronic structure theory make use of the kinetic balance between large and small component basis functions to eliminate the small component completely. These are called ``Dirac-exact'' methods. One such example is NESC, or Normalized Elimination of the Small Component. In addition to reproducing the Dirac equation exactly, they have numerous computational benefits, as well as easily allowing for most (if not all) non-relativistic correlated methods to be applied directly. Thus after doing an NESC calculation, you get relativistic ``orbitals'' which can immediately be used in, say, a coupled cluster calculation with no computational modification.

Comments, questions, or corrections? Let me know!

