---
layout: post 
title: Gaussian Matrix Parser 
---

I share a lot of code here on my blog, and for most of the quantum chemistry programs to work, I need some inputs, such as one and two electron integrals, overlap matrices, and the like. To be honest, aside from working through the Szabo and Ostlund integral evaluation code, I have no idea how to compute these quantities in practice. I know there are plenty of good algorithms out there (PRISM comes to mind), but I've never taken the time to work them out for myself (future project maybe?). Instead, I parse the codes directly from Gaussian09 output files. It's a little time consuming, to do that for each molecule, so I wanted to share my code with you.

Here is a link to the GitHub hosting [gauss\_parse](https://github.com/jjgoings/gaussian_matrix_parser).

The program, Gaussian Matrix Parser (gauss\_parse), is a command line routine to extract integrals from Gaussian output files and write them to text files as a 2D array. gauss\_parse takes the .log file as an argument, and then creates a directory with (named after the logfile), and fills it with the matrices you want, e.g:

    python gauss_parse.py my_molecule.log

This program assumes you have included the extra print options for matrices, e.g for minimal basis water, our `h2o.com` would look like:  
[code]  
#P rhf/STO-3G scf(conventional) Iop(3/33=6) Extralinks=L316 Noraff Symm=Noint Iop(3/33=1) pop(full)

Minimal basis H2O

0 1  
H  
O 1 r1  
H 2 r1 1 a1

r1 1.1  
a1 104.0  
[/code]  
Which has a suitable route section to print overlap, kinetic energy, two-electron repulsion, and potential energy integrals (and more)!

Say you have installed to a folder called `gauss_parse`. From the terminal, `cd` to that directory, and list the contents:

    $ cd gauss_parse
        $ ls
          LICENSE.txt README gauss_parse.py h2o.log
        $ python gauss_parse.py h2o.log
        $ ls
          LICENSE.txt README gauss_parse.py h2o.log h2o
        $

Note how `h2o` has been added to the directory. `cd` into that directory, and you should see:

    $ cd h2o
        $ ls
          kinetic_energy.dat number_basis_functions.dat
          overlap.dat two_electron_ints.dat
          nuclear_repulsion.dat number_electrons.dat
          potential_energy.dat
        $

Each `.dat` file contains the information extracted from the Gaussian `.log` file, which you can use for whatever you like! For example, say we want to see the overlap matrix for our H<sub>2</sub>O molecule:

    $ cd h2o
        $ vi overlap.dat

And we see in `vim`:  
[code]  
1.0000e+00 3.8405e-02 3.8613e-01 0.0000e+00 2.6843e-01 -2.0972e-01 1.8176e-01  
3.8405e-02 1.0000e+00 2.3670e-01 0.0000e+00 0.0000e+00 0.0000e+00 3.8405e-02  
3.8613e-01 2.3670e-01 1.0000e+00 0.0000e+00 0.0000e+00 0.0000e+00 3.8613e-01  
0.0000e+00 0.0000e+00 0.0000e+00 1.0000e+00 0.0000e+00 0.0000e+00 0.0000e+00  
2.6843e-01 0.0000e+00 0.0000e+00 0.0000e+00 1.0000e+00 0.0000e+00 -2.6843e-01  
-2.0972e-01 0.0000e+00 0.0000e+00 0.0000e+00 0.0000e+00 1.0000e+00 -2.0972e-01  
1.8176e-01 3.8405e-02 3.8613e-01 0.0000e+00 -2.6843e-01 -2.0972e-01 1.0000e+00  
[/code]  
With the ones along the diagonal --- just as expected! (Actual precision in `gauss_parse` is much higher).

