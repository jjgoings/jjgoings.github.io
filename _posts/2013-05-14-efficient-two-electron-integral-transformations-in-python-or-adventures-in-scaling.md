--- 
layout: post 
title: Efficient Two-Electron Integral Transformations in Python, or, Adventures in Scaling 
---

Low-scaling algorithms are important in any computational development, and this is never more true than in quantum chemistry. A golden example is in the integral transformation routines in electronic structure packages. Without a smarter algorithm, the transformations scale as $$ O(N^8)$$ (yikes!!), making computations on large systems nearly impossible. But with a little thought, we can reign in that transformation to a (not _nearly_ as bad) $$ N^5$$ method.

If you have performed a [Hartree-Fock](http://en.wikipedia.org/wiki/Hartree%E2%80%93Fock_method "Hartree–Fock method") (HF) calculation, you are left with a matrix of coefficients. Mathematically, these coefficients are the _eigenvectors_ that correspond to your HF Hamiltonian (Fock matrix). The eigenvalues are your orbital energies. So far so good. The real accurate (and interesting) work in electronic structure theory comes afterward, where we either refine the energies we have obtained or calculate molecular properties like UV-Vis spectra and so on. Most of these methods -- actually, _all_ these methods -- require transforming your two electron integrals from an atomic orbital basis (your standard run-of-the-mill [basis functions](http://en.wikipedia.org/wiki/Basis_function "Basis function") are your AO basis) into a molecular orbital basis. Put another way, now that you have solved the wavefunction of the Hartree-Fock system, you need to project your two electron integrals onto that wavefunction. The way you do this looks like so:

$$ (pq\vert rs)=\sum_\mu\sum_\nu\sum_\lambda\sum_\sigma C^{p}_\mu C^{q}_\nu C^{r}_\lambda C^{s}_\sigma(\mu\nu\vert \lambda\sigma)$$

In code, that looks something like:

{% highlight python %}

for p in range(0,dim):  
    for q in range(0,dim):  
        for r in range(0,dim):  
            for s in range(0,dim):  
                for mu in range(0,dim):  
                    for nu in range(0,dim):  
                        for lam in range(0,dim):  
                            for sig in range(0,dim):  
                                TxInt[p,q,r,s] += C[p,mu]*C[q,nu]*C[r,lam]*C[s,sig]*UnTxInt[mu,nu,lam,sig]

{% endhighlight %}

Holy cow. EIGHT loops of dimension number of basis functions. That should scale on the order of $$ N^8$$. Few methods in electronic structure theory scale worse than that (though they do exist...here's lookin' at you [Full CI](http://en.wikipedia.org/wiki/Full_configuration_interaction "Full configuration interaction")). This means that for most calculations, if you use this method of integral transformation, this transformation will be your most expensive step. Thankfully, we can come up with a smarter way to do the above transformation. Because the coefficients are independent (i.e $$ C^{p}_\mu$$ is independent of $$ C^{q}_\nu$$), we can rewrite our first equation as

$$ (pq\vert rs)=\sum_\mu C^{p}_\mu [\sum_\nu C^{q}_\nu [\sum_\lambda C^{r}_\lambda [\sum_\sigma C^{s}_\sigma(\mu\nu\vert \lambda\sigma)]]]$$

Or, like this, which is a lot clearer to me:

$$ (\mu\nu\vert \lambda s)=\sum_\sigma C^{s}_\sigma(\mu\nu\vert \lambda\sigma)$$

$$ (\mu\nu\vert rs)=\sum_\lambda C^{r}_\lambda(\mu\nu\vert \lambda s)$$

$$ (\mu q\vert rs)=\sum_\nu C^{q}_\nu(\mu\nu\vert rs)$$

$$ (pq\vert rs)=\sum_\mu C^{p}_\mu(\mu q\vert rs)$$

Where we perform four "quarter-transformations", save each transformation, and use in the next transformation. Doing it this way gives us four steps of 5-dimension loops, so it should scale on the order of $$ N^5$$. In code, that looks like:

{% highlight python %}

for p in range(0,dim):  
    for mu in range(0,dim):  
        temp[p,:,:,:] += C[p,mu]*UnTXInt[mu,:,:,:]  
    for q in range(0,dim):  
        for nu in range(0,dim):  
            temp2[p,q,:,:] += C[q,nu]*temp[p,nu,:,:]  
        for r in range(0,dim):  
            for lam in range(0,dim):  
                temp3[p,q,r,:] += C[r,lam]*temp2[p,q,lam,:]  
            for s in range(0,dim):  
                for sig in range(0,dim):  
                    TxInt[p,q,r,s] += C[s,sig]*temp3[p,q,r,sig]
{% endhighlight %}

Much nicer. You'll notice that we had to pre-allocate the 'temp' matrices, to store the results between quarter transformations. The transformation also makes use of the 'slice' notation in Python/ [NumPy](http://www.numpy.org/ "NumPy"). Using this, we perform a transformation over a whole dimension, instead of one index at a time. It's a little weird to be working with full dimensions, instead of just indices, but it works well. Here is the full code, with random integer arrays built in to act as our toy four-dimensional integrals. The toy matrix of coefficients, is, like all matrices, 2D. I built in a check, so you can compare the two methods. It spits out two transformed integrals with randomly chosen indices -- if/when you run it, you should make sure that the values match. If they don't, something is wrong!

{% highlight python %} 
#!/usr/bin/python

####################################  
#  
# SAMPLE INTEGRAL TRANSFORMATION CODE  
#  
####################################

from __future__ import division  
import sys  
import math  
import numpy as np  
import time

#####################################

# Initialize Arrays  
dim = 2 # dimension of arrays ... e.g number of basis functions  
MO1 = np.zeros((dim,dim,dim,dim)) # For our first dumb O[N^8] method  
MO2 = np.zeros((dim,dim,dim,dim)) # For our smarter O[N^5] method

INT = np.random.randint(9,size=(dim,dim,dim,dim)) # Our toy "two electron integrals"  
C = np.random.randint(9,size=(dim,dim)) # Toy "wavefunction coefficients"

# Begin first method. It scales as N^8, as you could  
# have guessed with there being 8 loops over dimension 'dim' (N)

t0 = time.time()  
for i in range(0,dim):  
    for j in range(0,dim):  
        for k in range(0,dim):  
            for l in range(0,dim):  
                for m in range(0,dim):  
                    for n in range(0,dim):  
                        for o in range(0,dim):  
                            for p in range(0,dim):  
                                MO1[i,j,k,l] += C[i,m]*C[j,n]*C[k,o]*C[l,p]*INT[m,n,o,p]  
t1 = time.time()

# Begin second method, scaling as N^5. We end up having four 5-loops, each  
# over dimension 'dim' (N).

t2 = time.time()  
temp = np.zeros((dim,dim,dim,dim))  
temp2 = np.zeros((dim,dim,dim,dim))  
temp3= np.zeros((dim,dim,dim,dim))  
for i in range(0,dim):  
    for m in range(0,dim):  
        temp[i,:,:,:] += C[i,m]*INT[m,:,:,:]  
    for j in range(0,dim):  
        for n in range(0,dim):  
            temp2[i,j,:,:] += C[j,n]*temp[i,n,:,:]  
        for k in range(0,dim):  
            for o in range(0,dim):  
                temp3[i,j,k,:] += C[k,o]*temp2[i,j,o,:]  
            for l in range(0,dim):  
                for p in range(0,dim):  
                    MO2[i,j,k,l] += C[l,p]*temp3[i,j,k,p]  
t3 = time.time()

# Set up random index to check correctness.  
i = np.random.randint(dim)  
j = np.random.randint(dim)  
k = np.random.randint(dim)  
l = np.random.randint(dim)

print MO1[i,j,k,l]  
print MO2[i,j,k,l]  
print "TIME1: ", t1-t0  
print "TIME2: ", t3-t2  
{% endhighlight %}

When I ran the code, moving from a dimension of 4 to a dimension of 8 (e.g I doubled the basis functions), the first method went from 0.29 seconds to 71.5 seconds, a jump of 246 times longer, versus the second method, which went from 0.01 seconds to 0.29 seconds, a jump of only 29 times. This is almost exactly as predicted. Doubling the basis for an $$ N^8$$ method gives $$ 2^8 = 256$$ times longer, and doubling the basis for an $$ N^5$$ algorithm gives $$ 2^5 = 32$$ times longer.

The new method is also very amenable to parallelization. Most electronic structure computations need to be parallelized, as model systems get larger and larger. Note that the $$ N^5$$ method is performed in four independent steps. Because of this independence, we can make our code run in parallel, and perform the quarter transformations on separate processors.

A great example why choosing your algorithm matters in quantum chemistry!

