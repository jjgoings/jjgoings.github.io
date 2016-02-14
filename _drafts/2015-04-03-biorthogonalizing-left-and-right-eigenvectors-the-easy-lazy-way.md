--- 
layout: post 
title: Biorthogonalizing left and right eigenvectors the easy (lazy?) way 
---

Lately I have been diagonalizing some nasty matrices.

Large. Non-Hermitian. Complex. Matrices. The only thing I _suppose_ I have going for me is that they are relatively sparse.

Usually I haven't have much of a problem getting eigenvalues. Eigenvalues are easy. Plug into ZGEEV, compute, move on.

The problem I ran into came when I wanted to use the eigenvectors. If you are used to using symmetric matrices all the time, you might not realize that non-Hermitian matrices have two sets of eigenvectors, left and right. In general, these eigenvectors of a non-Hermitian matrix are not orthonormal. But you can biorthogonalize them.

Why do you care if your eigenvectors are biorthogonalized?

Well, if your matrix corresponds to a Hamiltonian, and&nbsp;if you want to compute wave function properties, then you need a biorthonormal set of eigenvectors. This happens in linear response coupled cluster theory, for example. It is essential for a unique and physical description of molecular properties, e.g. transition dipole moments.

Now, with Hermitian&nbsp;matrices, your left and right eigenvectors are just conjugate transposes of each other, so it's super easy to orthogonalize a set of&nbsp;eigenvectors. You can compute the QR decomposition (_a la_ Gram-Schmidt) of your right eigenvectors&nbsp;$latex \mathbf{C}$ to get

$$\n \mathbf{C} = \mathbf{QR} $$

where $latex \mathbf{Q}$ is your set of orthogonalized eigenvectors. (Usually they are orthogonalized&nbsp;anyway during your eigenvalue decomposition.)

For non-Hermitian matrices, this situation is different. You have two eigenvalue equations you want to solve:

$latex \mathbf{HR} = \mathbf{RE}$, and, $latex \mathbf{LH} = \mathbf{LE}$

where $latex \mathbf{R}$ and $latex \mathbf{L}$ are your right and left eigenvectors, and $latex \mathbf{H}$ and $latex \mathbf{E}$ are your matrix and eigenvalues. The eigenvalues are the same regardless of which side you solve for.

To biorthonormalize $latex \mathbf{L}$ and $latex \mathbf{R}$, we want to enforce the constraint

$latex \mathbf{LR} = \mathbf{I}$

which says that the inner product of these two set of vectors is the identity. This is what biorthonormalization means.

Many times $latex \mathbf{LR} = \mathbf{D}$ where $latex \mathbf{D}$ is diagonal. This is easy. It's already orthogonal, so you can just scale by the norm.

If that isn't the case, how do you do it? One way would be to modify Gram-Schmidt. You could do that, but you won't find a LAPACK routine to do it for you (that I know of). So you'd have to write one yourself, and doing that well is time-consuming and may be buggy. Furthermore, I've found the modified Gram-Schmdt to run into to serious problems when you encounter&nbsp;degenerate eigenvalues. In that case, the eigenvectors for each degenerate eigenvalue aren't unique, even after constraining for biorthonormality, and so it's tough to enforce biorthonormality overall.

Here's a trick if you just want to get those dang eigenvectors biorthonormalized and be on your way. The trick lies in the LU decomposition.

Consider the following. Take the inner product of $latex \mathbf{L}$ and $latex \mathbf{R}$ to get the matrix $latex \mathbf{M}$.

$latex \mathbf{LR} = \mathbf{M}$

Now take the LU decomposition of $latex \mathbf{M}$

$latex \mathbf{M} = \mathbf{M}\_L \mathbf{M}\_U$

Where $latex \mathbf{M}\_L$ is lower triangular, and $latex \mathbf{M}\_U$ is upper triangular. So our equation now reads:

$latex \mathbf{LR} = \mathbf{M}\_L\mathbf{M}\_U$

Triangular matrices are&nbsp; **super** easy to invert, so invert the right hand side to get:

$latex \mathbf{M}\_L^{-1}\mathbf{LR}\mathbf{M}\_U^{-1} = \mathbf{I}$

Now, since we want left and right eigenvectors that are biorthonormal, we can replace the identity:

$latex \mathbf{M}\_L^{-1}\mathbf{LR}\mathbf{M}\_U^{-1} = \mathbf{L}'\mathbf{R}'$

where the prime indicates our new biorthonormal left and right eigenvectors.

This suggests our&nbsp;new biorthonormal left and right eigenvectors take the form:

$latex \mathbf{L}' = \mathbf{M}\_L^{-1}\mathbf{L}$

and

$latex \mathbf{R}' = \mathbf{R}\mathbf{M}\_U^{-1}$

And there you have it! An easy to implement method of biorthonormalizing your eigenvectors. All of the steps have a corresponding LAPACK routine. I've found it to be pretty robust. &nbsp;You can go a step further and prove that the new eigenvectors are still eigenvectors of the Hamiltonian. Just plug them in to the eigenvalue equation and you'll see.

While I think this doesn't scale any worse than your diagonalization in the first place, it&nbsp;is still&nbsp;a super useful trick. For example, it even works for set of eigenvectors that aren't full rank (e.g. rectangular). Because you do the LU on the inner product of the left and right eigenvectors, you'll get a much smaller square matrix the dimension of the number of eigenvectors you have.

Another use you might find with this is if the eigenvectors are nearly biorthonormal (which often happens when you have degenerate eigenvalues). You can do the same trick, but on the subspace of the eigenvectors corresponding to the degenerate eigenvalues. So if you have three degenerate eigenvalues, you can do an LU decomposition plus inversion on a 3x3 matrix.

