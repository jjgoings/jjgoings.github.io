---                                                                             
layout: post
title: Easy transparent SSH tunnels 
---

Most of my development work is done on remote computing clusters, which are usually firewalled. 

This means I can't log in directly when I work from home. I have to log into a network machine, and then log in to my development machine from there.

It gets kind of tedious to keep doing something along the lines of 

~~~
home:>$ ssh network-host
network-host:>$ ssh development-machine
development-machine:>$
~~~
It also makes it a pain to copy files from home to the remote machine (and vice versa!).

However, you can easily set up a transparent tunnel through your network-host that lets you (effectively) log on to your development machine as if it weren't even firewalled.

Just open up (or create) `~/.ssh/config`:

Add the following lines (replacing `network-host` and `development-machine` with the names of your computers). You can name them whatever you want. Here I named each machine `network` and `devel`.


~~~bash
# Non-firewalled computer
Host network 
HostName network-machine

# Firewalled computer
Host devel
HostName development-machine 
ProxyCommand ssh -o 'ForwardAgent yes' network 'ssh-add && nc %h %p'

~~~

What this does is log you into the non-firewalled network-host, then establish a connection to the firewalled computer through `netcat` (`nc` in this case). You never actually see the network host, it acts on your behalf, invisibly in the background.

So, from your home computer, you can login directly to the development machine:

~~~
home:>$ ssh devel 
development-machine:>$
~~~

You can also `scp` directly from your development machine now, too.

~~~
home:>$ scp devel:~/path/to/files
files                           100% 4084     4.0KB/s   00:00 
home:>$
~~~


