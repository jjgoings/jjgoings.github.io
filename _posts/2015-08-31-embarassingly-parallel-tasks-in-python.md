--- 
layout: post 
title: Embarassingly parallel tasks in Python
--- 

Recently, I found myself executing the same commands (or some variation thereof) at the command line.

Over and over and over and over.

Sometimes I just write a do loop (`bash`) or for loop (`python`). But the command I was executing was taking almost a minute to finish. Not terrible if you are doing this once, but several hundred (thousand?) times more and I get antsy.

If you are curious, I was generating `.cube` files for a large quantum dot, of which I needed the molecular orbital density data to analyze. There was no way I was waiting half a day for these files to generate.

So instead, I decided to parallelize the for loop that was executing my commands. It was easier than I thought, so I am writing it here not only so I don't forget how, but also because I'm sure there are others out there like me who (a) aren't experts at writing parallel code, and (b) are lazy.

Most of the following came from following along [here](https://pythonhosted.org/joblib/parallel.html).

First, the package I used was the [joblib](https://pythonhosted.org/joblib/index.html) package in `python`. I'll assume you have it installed, if not, you can use [pip](https://packaging.python.org/en/latest/installing.html#use-pip-for-installing) or something like that to get it on your system. You want to import `Parallel` and `delayed`.

So start off your code with  

{% highlight python %}  
from joblib import Parallel, delayed  
{% endhighlight %}

If you want to execute a system command, you'll also need the `call` function from the subprocess package. So you have  

{% highlight python %}  
from joblib import Parallel, delayed  
from subprocess import call  
{% endhighlight %}

Once you have these imported, you have to structure your code (according to the `joblib` people) like so:

{% highlight python %}  
import ....

def function1(...):  
 ...

def function2(...):  
 ...

...  
if __name__ == '__main__':  
 # do stuff with imports and functions defined about  
 ...  
{% endhighlight %}

So do you imports first (duh), then define the functions you want to do (in my case, execute a command on the command line), and then finally call that function in the main block.

I learn by example, so I'll show you how I pieced the rest of it together.

Now, the command I was executing was the Gaussian " [cubegen](http://www.gaussian.com/g_tech/g_ur/u_cubegen.htm)" utility. So an example command looks like  

{% highlight bash %}
cubegen 0 MO=50 qd.fchk 50.cube 120 h  
{% endhighlight %}

Which makes a `.cube` file (`50.cube`) containing the volumetric data of molecular orbital 50 (MO=50) from the formatted checkpoint file (`qd.fchk`). I wanted 120 points per side, and I wanted headers printed (`120 h`).

Honestly, the command doesn't matter. If you want to parallelize  

{% highlight bash %}
ls -lh  
{% endhighlight %}  
over a for loop, you certainly could. That's not my business. 

What _does_ matter is that we can execute these commands from a python script using the `call` function that we imported from the `subroutine` package.

So we replace our functions with the system calls

{% highlight python %}  
from joblib import Parallel, delayed  
from subprocess import call

def makeCube(cube,npts):  
    call(["cubegen","1","MO="+str(cube),"qd.fchk",str(cube)+".cube",  
    str(npts),"h"])

def listDirectory(i): #kidding, sorta.  
    call(["ls", "-lh"])

if __name__ == '__main__':  
 # do stuff with imports and functions defined about  
 ...  
{% endhighlight %}

Now that we have the command(s) defined, we need to piece it together in the main block.

In the case of the `makeCube` function, I want to feed it a list of molecular orbital (MO) numbers and let that define my for loop. So let's start at MO #1 and go to, say, MO #500. This will define our inputs. I also want the cube resolution (`npts`) as a variable (well, parameter really).

I'll also use 8 processors, so I'll define a variable `num_cores` and set it to 8. Your mileage may vary. `Parallel()` is smart enough to handle fairly dumb inputs.

(Also, if you do decide to use `cubegen`, like I did, please make sure you have enough space on disk.)

Putting this in, our code looks like  

{% highlight python %}  
from joblib import Parallel, delayed  
from subprocess import call

def makeCube(cube,npts):  
    call(["cubegen","1","MO="+str(cube),"qd.fchk",str(cube)+".cube",  
    str(npts),"h"])

def listDirectory(i): #kidding, sorta  
    call(["ls", "-lh"])

if __name__ == '__main__':  
    start = 1  
    end = 501 # python's range ends at N-1  
    inputs = range(start,end)  
    npts = 120  
    num_cores = 8

{% endhighlight %}

Great. Almost done.

Now we need to call this function from within `Parallel()` from `joblib`.

{% highlight python %}  
results = Parallel(n_jobs=num_cores)(delayed(makeCube)(i,npts)  
    for i in inputs)  
{% endhighlight %}

The `Parallel` function (object?) first takes the number of cores as an input. You could easily hard code this if you want, or let Python's `multiprocessing` package determine the number of CPUs available to you. Next we call the function using the `delayed()` function. This is "a trick to create a tuple (function, args, kwargs) with a function-call syntax".

It's on the developer's web page. I can't make this stuff up.

Then we feed it the list defined by our start and end values.

If you wanted to list the contents of your directory 500 times and over 8 cores, it would look like (assuming you defined the function and inputs above)

{% highlight python %}  
results = Parallel(n_jobs=8)(delayed(listDirectory)(i)  
     for i in inputs)  
{% endhighlight %}

Essentially we are making the equivalence that

{% highlight python %}  
delayed(listDirectory)(i) for i in inputs
{% endhighlight %}

is the same as

{% highlight python %}  
for i in inputs:
    listDirectory(i)
{% endhighlight %}  

Does that make sense? It's just

{% highlight python %}  
delayed(function)(arguments)
{% endhighlight %}  

instead of

{% highlight python %}
function(arguments)
{% endhighlight %}

Okay. Enough already. Putting it all together we have:  

{% highlight python %}  
from joblib import Parallel, delayed  
from subprocess import call

def makeCube(cube,npts):  
    call(["cubegen","1","MO="+str(cube),"qd.fchk",str(cube)+".cube",  
    str(npts),"h"])

def listDirectory(i): #kidding, sorta  
    call(["ls", "-lh"])

if __name__ == '__main__':  
    start = 1  
    end = 501 # python's range ends at N-1  
    inputs = range(start,end)  
    npts = 120  
    num_cores = 8  
    results = Parallel(n_jobs=num_cores)(delayed(makeCube)(i,npts)  
        for i in inputs)  
{% endhighlight %}

There you have it!

