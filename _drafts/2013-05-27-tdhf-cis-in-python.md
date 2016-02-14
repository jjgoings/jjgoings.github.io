---
layout: post 
title: TDHF + CIS in Python 
---

So you completed a [Hartree-Fock procedure](http://joshuagoings.wordpress.com/2013/04/24/hartree-fock-self-consistent-field-procedure/ "Hartree-Fock Self Consistent Field Procedure"), and you even [transformed your two electron integrals](http://joshuagoings.wordpress.com/2013/05/14/efficient-two-electron-integral-transformations-in-python-or-adventures-in-scaling/ "Efficient Two-Electron Integral Transformations in Python, or, Adventures in Scaling"). Now what can you do? We can use those results, specifically the orbital energies (eigenvalues of the Fock matrix) and the transformed two-electron integrals (using the eigenvalues of the Fock matrix), to calculate some simple response properties, such as excitation energies! A derivation of the working equations for time-dependent Hartree Fock (TDHF)  can be found [here](http://joshuagoings.wordpress.com/2013/05/03/derivation-of-time-dependent-hartree-fock-tdhf-equations/ "Derivation of Time Dependent Hartree-Fock (TDHF) Equations"). Configuration Interaction Singles (CIS), is a subset of the TDHF equations. If you haven't performed the previous calculations, I'll include my initial eigenvalues and transformed two electron integrals at the end. The values are for  [HeH+](http://en.wikipedia.org/wiki/Helium_hydride_ion "Helium hydride ion") at a bond length of 0.9295 Angstrom with an  [STO-3G](http://en.wikipedia.org/wiki/STO-nG_basis_sets "STO-nG basis sets") basis set. We create and solve:

$$ \displaystyle \begin{bmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{-B} & \mathbf{-A} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} = \omega \begin{bmatrix} \mathbf{1} & \mathbf{0} \\ \mathbf{0} & \mathbf{1} \\ \end{bmatrix} \begin{bmatrix} \mathbf{X} \\ \mathbf{Y} \\ \end{bmatrix} $$

With the elements of $$ {\mathbf{A}}$$ and $$ {\mathbf{B}}$$ as

$$ \displaystyle A\_{ia,jb} = \delta\_{ij}\delta\_{ab}(\epsilon\_a - \epsilon\_i) + \langle aj||ib \rangle $$

and

$$ \displaystyle B\_{ia,jb} = \langle ab || ij \rangle $$

Now, when we transformed our two electron integrals from atomic orbital (AO) basis to molecular orbital (MO) basis, we made the implicit assumption that we were working under a closed-shell approximation. Electrons have spin, and we assumed we had an even number of electrons so that all their spins paired and integrated out. If you've taken any general chemistry, you know that we fill each orbital with two electrons: one spin up, and one spin down. (Electrons are fermions, which means two electrons of opposite spin can occupy the same spatial location. Their opposite, bosons, are a little weirder, which is why we can get [Bose-Einstein condensates](http://en.wikipedia.org/wiki/Bose%E2%80%93Einstein_condensate "Bose–Einstein condensate") --- think a lot of particles occupying the same place in space). Anyway, we make the assumption that opposite spin electrons can share the same spatial orbital, which is reasonable for most calculations, but not strictly true -- after all, the definition of an orbital is a  **one** electron wavefunction. Moving along now...

We need to explicitly account for the spin of the electrons, which means we need to satisfy this transformation:

$$ \langle pq|rs\rangle = (pr|qs)\int d\omega\_1 d\omega\_2 \sigma\_p(\omega\_1) \sigma\_q(\omega\_2) \sigma\_r(\omega\_1) \sigma\_s(\omega\_2) $$

Where $$ \omega$$ is the spin of the electron, with coordinates 1 and 2. Note that $$ (pq|rs) \neq \langle pq | rs\rangle $$, this is because we will be moving from _chemists'_ notation to _physicists'_ notation, which dominates the literature. Since the CIS and TDHF equations need only double bar integrals, e.g.

$$ \langle pq||rs \rangle =\langle pq|rs \rangle - \langle ps|qr \rangle $$

We can also account for that in our transformation. In Python this gives:

~~~python  
# Create spin-adapted two electron integral  
# in double-bar format in a 4D array 'ints'  
# teimo(i,j,k,l) grabs MO basis (pq|rs) value  
# Note index change from starting at '1' to '0'  
ints=np.zeros((dim\*2,dim\*2,dim\*2,dim\*2))  
for p in range(1,dim\*2+1):  
 for q in range(1,dim\*2+1):  
 for r in range(1,dim\*2+1):  
 for s in range(1,dim\*2+1):  
 value1 = teimo((p+1)//2,(r+1)//2,(q+1)//2,(s+1)//2) \* (p%2 == r%2) \* (q%2 == s%2)  
 value2 = teimo((p+1)//2,(s+1)//2,(q+1)//2,(r+1)//2) \* (p%2 == s%2) \* (q%2 == r%2)  
 ints[p-1,q-1,r-1,s-1] = value1 - value2

~~~

Now, because Python begins its indexing at '0', and I began my indexing at '1', I had to make the index change at the end. From now on, the indexing starts at '0', so that $$ (11|11) = (00|00)$$ and so on. Now that we have our integrals, we can also spin adapt our orbital energies. This basically maps spatial orbital energy 1 (which contains two electrons) to spin orbital 1 and 2: odd numbers are spin up, even numbers are spin down. If the spatial orbitals are found in an array 'E', now moved to an array of double the dimension 'fs':

~~~python  
# Spin basis fock matrix eigenvalues  
fs = np.zeros((dim\*2))  
for i in range(0,dim\*2):  
 fs[i] = E[i//2]  
fs = np.diag(fs)  
~~~

Simple enough.

Putting it altogether then (I hard coded the initial values for self-containment):

~~~python  
#!/usr/bin/python

####################################  
#  
# CI Singles (CIS) and  
#  
# Time-Dependent Hartree Fock (TDHF)  
#  
####################################

from \_\_future\_\_ import division  
import math  
import numpy as np

####################################  
#  
# FUNCTIONS  
#  
####################################

# Return compound index given four indices  
def eint(a,b,c,d):  
 if a \> b: ab = a\*(a+1)/2 + b  
 else: ab = b\*(b+1)/2 + a  
 if c \> d: cd = c\*(c+1)/2 + d  
 else: cd = d\*(d+1)/2 + c  
 if ab \> cd: abcd = ab\*(ab+1)/2 + cd  
 else: abcd = cd\*(cd+1)/2 + ab  
 return abcd

# Return Value of spatial MO two electron integral  
# Example: (12|34) = tei(1,2,3,4)  
def teimo(a,b,c,d):  
 return ttmo.get(eint(a,b,c,d),0.0e0)

####################################  
#  
# INITIALIZE ORBITAL ENERGIES  
# AND TRANSFORMED TWO ELECTRON  
# INTEGRALS  
#  
####################################

Nelec = 2 # we have 2 electrons in HeH+  
dim = 2 # we have two spatial basis functions in STO-3G  
# Spatial orbital eigenvalues  
E = [-1.52378656, -0.26763148]  
# Two electron integrals, in a python dictionary  
# Using compound indices, see definition of eint()  
# and teimo() above.  
ttmo = {5.0: 0.94542695583037617, 12.0: 0.17535895381500544, 14.0: 0.12682234020148653, 17.0: 0.59855327701641903, 19.0: -0.056821143621433257, 20.0: 0.74715464784363106}

####################################################  
#  
# CONVERT SPATIAL TO SPIN ORBITAL MO  
#  
####################################################

# This makes the spin basis double bar integral (physicists' notation)

ints=np.zeros((dim\*2,dim\*2,dim\*2,dim\*2))  
for p in range(1,dim\*2+1):  
 for q in range(1,dim\*2+1):  
 for r in range(1,dim\*2+1):  
 for s in range(1,dim\*2+1):  
 value1 = teimo((p+1)//2,(r+1)//2,(q+1)//2,(s+1)//2) \* (p%2 == r%2) \* (q%2 == s%2)  
 value2 = teimo((p+1)//2,(s+1)//2,(q+1)//2,(r+1)//2) \* (p%2 == s%2) \* (q%2 == r%2)  
 ints[p-1,q-1,r-1,s-1] = value1 - value2

#####################################################  
#  
# Spin basis fock matrix eigenvalues  
#  
#####################################################

fs = np.zeros((dim\*2))  
for i in range(0,dim\*2):  
 fs[i] = E[i//2]  
fs = np.diag(fs)

######################################################  
#  
# CIS and TDHF CALCULATION  
#  
######################################################

A = np.zeros((2\*dim,2\*dim))  
B = np.zeros((2\*dim,2\*dim))  
I = -1  
for i in range(0,Nelec):  
 for a in range(Nelec,dim\*2):  
 I = I + 1  
 J = -1  
 for j in range(0,Nelec):  
 for b in range(Nelec,dim\*2):  
 J = J+1  
 A[I,J] = (fs[a,a] - fs[i,i]) \* ( i == j ) \* (a == b) + ints[a,j,i,b]  
 B[I,J] = ints[a,b,i,j]

# Solve CIS matrix equation  
ECIS,CCIS = np.linalg.eig(A)  
print 'E(CIS) = ', np.amax(ECIS)  
# Solve TDHF matrix equation  
M = np.bmat([[A,B],[-B,-A]])  
ETD,CTD = np.linalg.eig(M)  
print 'E(TDHF) = ', abs(np.amax(ETD))  
~~~

Running the code we find our first excitation energy at the CIS level is E(CIS) = 0.911, and our first excitation at the TDHF level is E(TDHF) = 0.902, (all in Hartrees) in agreement with the literature values in the paper [here](http://link.aip.org/link/doi/10.1063/1.3020336 "Modeling the doubly excited state with time-dependent Hartree–Fock and density functional theories"). A couple of notes about the method. First, the TDHF method can be seen as an extension of the CIS approach. The $$ A$$ matrix in the TDHF working equations is just the CIS matrix. This also means that the TDHF matrix is _twice_ the dimension of the CIS matrix ( **four** times as large), which can get very costly. With a little bit of (linear) algebra, we can get the TDHF equations in the form:

$$ ({\mathbf A} + {\mathbf B}) ({\mathbf A} - {\mathbf B})({\mathbf X} - {\mathbf Y}) = \omega^2 ({\mathbf X} - {\mathbf Y})$$

Which is the same dimension as the CIS matrix. This is why you rarely see CIS in practice: for the same cost, you can get a TDHF calculation, which is more accurate because it includes the block off-diagonal elements. I also want to mention that TDDFT takes almost exactly the same form. The only difference is that the replace the two electron integrals with the exchange elements in DFT, and the HF orbital energies are the Kohn-Sham(KS) orbital eigenvalues. Because DFT generally handles correlation better, most single excitations are modeled using TDDFT. Finally, we _did_ solve for all the excitation energies in the minimal basis...but in general we don't need them all, and it is way to costly to do so. In this case, we can use iterative solvers --- like the Davidson iteration --- to pick off just the lowest few eigenvalues. Gaussian09, by default, solves for just the lowest three eigenvalues unless you ask for more.

For your reference, the transformed two electron integrals (pq|rs) are given below, first four columns are index of p,q,r,s, and the last column is the value:

[code language="text"]  
1 1 1 1 0.94542695583  
1 1 1 2 0.175358953815  
1 1 2 1 0.175358953815  
1 1 2 2 0.598553277016  
1 2 1 1 0.175358953815  
1 2 1 2 0.126822340201  
1 2 2 1 0.126822340201  
1 2 2 2 -0.0568211436214  
2 1 1 1 0.175358953815  
2 1 1 2 0.126822340201  
2 1 2 1 0.126822340201  
2 1 2 2 -0.0568211436214  
2 2 1 1 0.598553277016  
2 2 1 2 -0.0568211436214  
2 2 2 1 -0.0568211436214  
2 2 2 2 0.747154647844

~~~

 

**Addendum: Getting transition dipole moment**

Let's say you have your z-component dipole moment integrals (in the molecular orbital basis) collected into a matrix $$ Z\_{pq} = \langle p |\overrightarrow{z} | q \rangle$$.

You can compute the z-component of the transition dipole moment from your transition density, which is either the appropriate eigenvector for a given excitation $$ X\_{ia}$$ (CIS) or $$ X\_{ia}$$ and $$ Y\_{ai}$$ (TDHF). If the dipole integral matrix is $$ N \times N$$, you'll want to reshape your $$ X\_{ia}$$ and $$ Y\_{ai}$$ to be $$ N \times N$$ as well, instead of $$ OV \times 1$$. This gives you a $$ N \times N$$ transition density matrix of

$$ \mathbf{D} = \displaystyle \begin{bmatrix} \mathbf{0} & \mathbf{X} \\ \mathbf{Y} & \mathbf{0} \\ \end{bmatrix}$$

The expectation value of the z-component of this transition dipole moment is then the trace of the density dotted into the z-component dipole integrals, e.g.

$$ \langle z \rangle = Tr(\mathbf{D}\mathbf{Z})$$

Then do the same for $$ \langle x \rangle$$ and $$ \langle y \rangle$$ and sum each component for the total transition dipole.

You'll also need to repeat the process for each transition you are interested in.

Note that most dipole moment integrals are computed in the atomic orbital basis, so don't forget to transform your transition density to the AO basis (or dipole integrals to MO--it doesn't matter which way, expectation values are independent of basis--the key is that both matrices are in the same basis).

