--- 
layout: post 
title: Research code dump! 
---

[![compy]({{ site.baseurl }}/assets/compy.jpg?w=300)](http://joshuagoings.files.wordpress.com/2013/12/compy.jpg)  
I've finally gotten around to cleaning up my home-brewed research code (at least a little bit), and I've hosted it [here](https://github.com/jjgoings/pyqchem) on my GitHub. I'm calling the project `pyqchem`, and it contains Hartree Fock, MP2, coupled cluster and a smattering of excited state methods. I'd love it if you check it out!

You'll notice that I still don't have a way of reading in molecular geometry and basis set, and so I am still reliant on parsing G09 outputfor the atomic orbital integrals. Oh well, it's a future project :) I'd also love to learn how to make it object oriented, as well as optimize the lower level routines in `C/C++`. It is so far far from optimized right now it is ridiculous. I think my EOM-CCSD code scales as N^8 instead of N^6, just because I haven't factored the equations right. But it works, and it has helped me learn so much about electronic structure methods. If you get the chance to look at it, I would love input for the future. I'm still developing as a programmer and I could use all the help I can get!

I hosted a lot of premade molecules (and their AO integrals), so all you have to do is execute `pyqchem.py` followed by the folder of interest.

For example:  

{% highlight text %}
 >>$ python pyqchem.py h2_3-21G 
{% endhighlight %}

Would execute the `pyqchem.py` script on the folder `h2_3-21G`, which contains all the precomputed atomic-orbital basis integrals. The type of calculation is changed by editing the `pyqchem.py` script itself. Say I wanted to perform an MP2 calculation on H2 in a 3-21G basis. I open `pyqchem.py`, and edit at the top:

{% highlight python %}  

""" Edit below to perform the calculation desired  
"""

do_DIIS = True         # DIIS acceleration (just keep on)  
do_ao2mo = True        # Set to true so we use our optimized (MO) orbitals from SCF  
do_mp2 = True          # Set to True so we do an MP2  
do_cistdhf = False     # Set to False so we don't do a CIS/TDHF  
do_ccsd = False        # Set to False so we don't do CCSD  
do_eomccsd = False     # Set to False so we don't do EOM-CCSD  
do_eommbpt2 = False    # Set to False so we don't do EOM-MBPT2  
do_eommbptp2 = False   # Set to False so we don't do EOM-MBPT(2)  
do_eommbptd = False    # Set to False so we don't do EOM-MBPT(D)  
printops = True        # True prints more stuff  
convergence = 1.0e-8   # Our iterative convergence criteria

{% endhighlight %}  

Then run:  

{% highlight text %}
 >>$ python pyqchem.py h2_3-21G  
{% endhighlight %}

And you'll see the pretty output dump to your terminal :)

That's all there is to it! Enjoy!

