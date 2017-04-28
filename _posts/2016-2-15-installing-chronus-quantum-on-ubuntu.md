---
layout: post
title: Installing Chronus Quantum on Ubuntu 15.10 
---

[`Chronus Quantum`](http://www.chronusquantum.org/) is a free, open-source software package to perform ab-initio computational chemistry calculations. It is primarily developed by [Xiaosong Li and his research group](https://depts.washington.edu/ligroup/) at the University of Washington. 

In particular, it was designed to excel with explicitly time-dependent calculations, as well as otherwise unconventional electronic structure methods.

In other words, `Chronus Quantum` is a free software package that solves the underlying quantum mechanics that determines how molecules react and behave.

Just like physics engines in video games make your gameplay more realistic and lifelike, here `Chronus Quantum` is an engine to give a realistic simulation of molecules on computers. 

These types of calculations reveal just what electrons are doing in molecules, helping researchers design better drugs, better solar panels, and better computer chips, among many others.

<p align="center">
  <img src="/assets/cq_logo.png" height="250"/>
</p>


`Chronus Quantum` is free and open-source, meaning anyone can download it, try it, and even contribute to it. 

The latest public release is hosted on GitHub (just like this website), and you can browse and download the entire source code [here](https://github.com/liresearchgroup/chronusq_public).

I want to walk you through the steps I took to get `Chronus Quantum` working on my fresh install of Ubuntu 15.10. The steps should work for the past few releases of Ubuntu Linux, so if you are on 14.10 or something like that you needn't worry.

I'll assume that you are comfortable working on the command line, and have root/sudo privileges, but other than that no particular expertise is necessary!

Obtaining `Chronus Quantum`
-------

For starters, open up your terminal. Move to a directory where you want to install (home directory is probably fine, it's where I installed my copy).

Since the source is hosted on GitHub, we will use `git` to obtain our copy of the code. Type

{% highlight text %}
$ git clone https://github.com/liresearchgroup/chronusq_public.git
{% endhighlight %} 

If you don't have `git`, you can install it by typing

{% highlight text %}
$ sudo apt-get update && sudo apt-get install git-all
{% endhighlight %}

In fact, if Ubuntu ever complains about not having some package, 95% of the time you can just

{% highlight text %}
$ sudo apt-get install <whatever-package-ubuntu-is-whining-about>
{% endhighlight %}

Okay, you should now have `chronusq_public` in your directory. `cd` into it.

{% highlight text %}
$ cd chronusq_public
{% endhighlight %}

Take care of a few dependencies...
-------

At this point in time, `chronus` won't handle all the dependencies on its own, so we have to help it with a few things before we compile.

You may have some of these installed already, but I'm working with a fresh install. `apt-get` will let you know if you already have a certain package.

Let's take care of `python` first, following the `apt-get` commands we've seen before.

**Python**

Although `chronus` is mostly C++, the high level execution is handled by a `python` script. So let's get that set up. Type

{% highlight text %}
$ sudo apt-get install python-dev libxml2-dev libxstl1-dev python-pip
{% endhighlight %}

Followed by 

{% highlight text %}
$ sudo pip install configparser
{% endhighlight %}

This takes care of the `python` dependencies.

**Math libraries**

Same idea as above, but for the required linear algebra libraries.

Let's knock it out in one shot. Type

{% highlight text %}
$ sudo apt-get install libeigen3-dev libblas-dev liblapacke-dev libhdf5-dev
{% endhighlight %}

Okay, we are done here.

Configure
-------

Now, you should still be in the top of the `chronusq_public` directory. If not, 

{% highlight text %}
$ cd /path/to/chronusq_public
{% endhighlight %}

From this directory, make a `build` directory and `cd` into it.

{% highlight text %}
$ mkdir build && cd build
{% endhighlight %}

Now, inside the `build/` directory, type

{% highlight text %}
$ cmake -DCMAKE_CXX_FLAGS='-w -O2 -std=c++11' -DBUILD_LIBINT=ON ..
{% endhighlight %}

This will configure your compilation. 

There are more options you can pass to `cmake`, and you can find them in the `Chronus Quantum` [documentation](https://github.com/liresearchgroup/chronusq_public/blob/master/doc/ChronusQUserManual.pdf) (in the folder `chronusq_public/doc/`). 

Most of the defaults should work for us. I wanted to pass the optimizer flag to `cmake` as well (`-O2`). 

We also want `chronus` to deal with compiling the external integral package, [`LibInt`](https://github.com/evaleev/libint), so we tell it to do so explicitly with `-DBUILD_LIBINT=ON`.

Don't forget the `..` at the end!

Compile
-------

Perfect. Now just type

{% highlight text %}
$ make -j <nproc>
{% endhighlight %}

where `<nproc>` is the number of processors. I recommend you use all CPUs available. You can check via

{% highlight text %}
$ nproc --all
{% endhighlight %}

I had four, so 

{% highlight text %}
$ make -j 4
{% endhighlight %}

Now `chronus` will take care of the rest! It will clean up several more dependencies, so a lot more junk will dump to your terminal, but that's expected. You can pretty much ignore the `boost` "warnings" it dumps out.

Heads up: this will probably take a while. It took me around 2 hours to compile. Granted, we are making `chronus` deal with `LibInt` which accounts for at least half of that compile time, but now would be a good time to take a long lunch or go outside. 

Test it out!
-------

In your `build` directory, there should now be a `chronus` python script, called `chronusq.py`. 

You can run it on a test file like so

{% highlight text %}
$ python chronusq.py <input-file>
{% endhighlight %}

Here's a test case from the documentation, which will do a Hartree-Fock SCF calculation on a water molecule:

{% highlight text %}
#
# Molecule Specification
#

[Molecule]
charge = 0
mult = 1
geom:
  O 0  0.000000000 -0.0757918436 0.0
  H 0  0.866811829  0.6014357793 0.0
  H 0 -0.866811829  0.6014357793 0.0

#
# Job Specification
#

[QM]
reference = HF
job = SCF
basis = sto3g.gbs

#
# Misc Settings
#

[Misc]
nsmp = 1 
{% endhighlight %}

Save this file to a file named `water.inp`. Then you can run `chronus` by

{% highlight text %}
$ python chronusq.py water.inp
{% endhighlight %}

The output will be named `water.out`.

Open this file up, and scroll down until you see 

{% highlight text %}
...

------------------------------------------------------------------
SCF Iteration   Energy (Eh)       ΔE (Eh)          |ΔP(α)|
-------------   -----------       -------           -------
  SCFIt: 1      -74.8749392555    -3.9671535e-01   2.0386303e+00
  SCFIt: 2      -74.9381834290    -6.3244173e-02   6.8448936e-01
  SCFIt: 3      -74.9414265478    -3.2431189e-03   1.2919179e-01
  SCFIt: 4      -74.9419370087    -5.1046089e-04   5.7926335e-02
  SCFIt: 5      -74.9420469702    -1.0996144e-04   2.4808865e-02
  SCFIt: 6      -74.9420722506    -2.5280437e-05   1.2054431e-02
  SCFIt: 7      -74.9420798968    -7.6462320e-06   1.1052335e-02
  SCFIt: 8      -74.9420798968    -4.3200998e-12   5.9411624e-06
  SCFIt: 9      -74.9420798968    -3.2684966e-13   1.0888457e-06
  SCFIt: 10     -74.9420798968     4.2632564e-14   4.5029536e-07
  SCFIt: 11     -74.9420798968    -4.2632564e-14   1.7644888e-07
  SCFIt: 12     -74.9420798968    -2.8421709e-14   8.5174409e-08
  SCFIt: 13     -74.9420798968    -2.8421709e-14   7.7070096e-08
  SCFIt: 14     -74.9420798968     8.5265128e-14   2.2941389e-14

SCF Completed: E(ℝ-RHF) = -74.9420798968  Eh after  14  SCF Iterations

...
{% endhighlight %}

And there you have it! The results of the Hartree-Fock SCF iteration. 

The total energy of the water molecule is there at the bottom: `E(ℝ-RHF) = -74.9420798968` in units of Hartrees.

There is plenty more you can do with `chronus`, and I've only scratched the very surface. You can check out the docs for more information about setting up real-time calculations and more.

If this project sounds interesting to you, and you want to contribute, feel free to [fork](https://github.com/liresearchgroup/chronusq_public) it!








