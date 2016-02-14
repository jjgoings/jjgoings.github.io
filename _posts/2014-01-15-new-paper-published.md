--- 
layout: post 
title: New paper published! 
---

I have a new paper published in the latest issue of Advances in Quantum Chemistry, called " [Self-Consistent Field using Direct Inversion in Iterative Subspace Method and Quasi-Newton Vectors](http://www.sciencedirect.com/science/article/pii/B9780128005361000046)". Quite the mouthful, but hey, it *is* science. The idea behind the paper was to "steal" some ideas from geometry optimizations, and apply them to the problem of converging an SCF calculation (that is, a Hartree-Fock or DFT calculation). The general acceleration method for converging SCF type equations is to use an algorithm called DIIS (pronounced "dice"). Without going into the mathematics, DIIS is a way of improving your iterative guess at each step of the calculation. A really cool introduction can be found online at [Dr. David Sherrill's website](http://vergil.chemistry.gatech.edu/notes/diis/diis.html). Generally, it brings a modest speed-up to your calculation, and some form of DIIS is always used nowadays in electronic structure calculations. Our twist was to use a different type of vector (a quasi-Newton vector, which gets a lot of use in geometry optimizations) to help the DIIS acceleration. Practically, we found that using a QN-DIIS method got a Hartree-Fock calculation to converge faster by a few iterations. That's pretty cool!

You can read the paper [here](http://www.sciencedirect.com/science/article/pii/B9780128005361000046), but it's probably behind a paywall for most of you. If you are really interested (it won't hurt my feelings if you are not), feel free to email me and I'll send you a reprint.

