--- 
layout: post 
title: Several New Papers now Online 
---

The end of the year is rapidly approaching, and I'd like to draw your attention to three papers of mine that have been recently published online.

**[Theoretical Characterization of Conduction-Band Electrons in Photodoped and Aluminum-Doped Zinc Oxide (AZO) Quantum Dots](http://pubs.acs.org/doi/abs/10.1021/jp5090229)**

This first paper was a fun collaboration between our theoretical work in the Li group and the experimental work done by Dan Gamelin at the UW. The paper looks at calculated UV-Vis spectra of photodoped and Aluminum-doped ZnO quantum dots. Both types of doping added "extra" electrons to the conduction band, and this resulted in some interesting properties that you can see in both theory and experiment.

What I was most surprised to see was that the "extra" electron simply acted like an electron moving in a spherical potential, just like a hydrogen atom! On the left we have the HOMO, which looks like an s-orbital. Then the two on the right are different LUMOs, one that looks like a p-orbital and another that looks like a d-orbital. We called the "super-orbitals", since they look like atomic orbitals but exist in these tiny crystal structures. I think these are the first images of DFT-computed "superorbitals" ever published, though the "artificial atom" paradigm has been around for some time. It's interesting to see complicated systems behaving like the simple quantum mechanical models we study when we first learn quantum mechanics!

[![qds]({{ site.baseurl }}/assets/qds.jpeg?w=300)](https://joshuagoings.files.wordpress.com/2014/12/qds.jpeg)

J. J. Goings, A. Schimpf, J. W. May, R. Johns. D. R. Gamelin, X. Li, “ [Theoretical Characterization of Conduction-Band Electrons in Photodoped and Aluminum-Doped Zinc Oxide (AZO) Quantum Dots](http://pubs.acs.org/doi/abs/10.1021/jp5090229),” _J. Phys. Chem. C_, **2014** , _118_, 26584.

**[Assessment of Low-scaling Approximations to the Equation of Motion Coupled-Cluster Singles and Doubles Equations](http://scitation.aip.org/content/aip/journal/jcp/141/16/10.1063/1.4898709)**

This second paper details the implementation of several low-scaling methods for computing excited states (e.g. computing UV/Vis absorption). The idea was to take the highly accurate EOM-CCSD equations and simplify them using perturbation theory. That way, we could keep most of the accuracy of the method, while still having fast enough equations that large molecules could be studied. The resulting equations are closely related to other methods like CC2, CIS(D), and ADC(2), and I showed how they all relate to each other. We compared the performance to EOM-CCSD as well as experimental values. The results were promising, and the perturbative equations performed particularly well for Rydberg states. CC2, on the other hand, performs great for valence excitations.

J. J. Goings, M. Caricato, M. Frisch, X. Li, “ [Assessment of Low-scaling Approximations to the Equation of Motion Coupled-Cluster Singles and Doubles Equations](http://scitation.aip.org/content/aip/journal/jcp/141/16/10.1063/1.4898709),” _J. Chem. Phys._, **2014** , _141_, 164116.

**[_Ab Initio_ Non-Relativistic Spin Dynamics](http://scitation.aip.org/content/aip/journal/jcp/141/21/10.1063/1.4902884)**

Finally, in this paper, we extended the [generalized Hartree-Fock](http://joshuagoings.wordpress.com/2014/10/14/broken-symmetries-in-hartree-fock/ "Broken Symmetries in Hartree-Fock") method to the time domain. In this proof-of-concept paper, we showed how a magnetic field can guide the spin dynamics of simple spin-frustrated systems. The key is reformulating the real-time time-dependent Hartree-Fock equations in the complex spinor basis. This allows the spin magnetizations on each atom to vary as a response to, say, an externally applied magnetic field. Here's an example with a lithium trimer. Initially (left picture), all the spin magnetizations (that is, the spatial average of spin magnetic moment) point away from each other. Then, applying a static magnetic field (right picture) into the plane of the molecule causes each magnetization to precess at the Larmor frequency. The precession is shown in picoseconds by the colorization.

![image of FIG. 3.]({{ site.baseurl }}/assets/1.4902884.figures.online.f3.gif "image of FIG. 3.")

It's really a beautiful idea in my opinion, and there is so much more to be done with it. For example, in our simple ab initio model, the spins only "talk" through Pauli repulsion, so they behave more or less independently. What would happen if we include spin-orbit coupling and other perturbations? That remains to be seen.

F. Ding, J. J. Goings, M. Frisch, X. Li, “ [_Ab Initio_ Non-Relativistic Spin Dynamics](http://scitation.aip.org/content/aip/journal/jcp/141/21/10.1063/1.4902884),” _J. Chem. Phys._, **2014** , _141_, 214111.

