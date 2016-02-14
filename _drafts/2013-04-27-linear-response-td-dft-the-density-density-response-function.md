--- 
layout: post 
title: 'Linear Response TD-DFT: The density-density response function' 
---

Linear response time-dependent density function theory (LR-TDDFT) is kind of a mouthful to say, but is a really simple idea in practice. In computational chemistry, many ideas are quite simple, but they are so laden with jargon it just scares other people away! LR-TDDFT is one way of determining single excitation energies of a molecule from first principles. It is a way of describing how matter interacts with light (or any electromagnetic field). An everyday example is color: sunlight is absorbed by some material, which excites an electron. When this electron finally relaxes, it emits light of a certain energy -- that light is the color you see!

To derive the LR-TDDFT working equations (e.g. the equations you can implement on a computer), we start by deriving a density-density response function. This function describes the response of electron density (the 'density' of 'density functional theory') to an external field: light of some kind, or a magnetic field, or whatever. The potential and the electronic density 'couple' in some way.

We describe this interacting system with a partitioned Hamiltonian:

$$ H = H\_0 + V\_{ext} $$

Where $$ H\_0$$ is time-independent unperturbed system, and $$ V\_{ext}$$ is the time-_dependent_ Hamiltonian describing the field potential. Investigating the potential a little more closely, we find that the potential is:

$$ V\_{ext} = \int \rho(\textbf{r})V\_{ext}(\textbf{r},t)\mathrm{d}\textbf{r}$$

Where the density operator $$ p(\textbf{r})$$ is defined as:

$$ \rho(\textbf{r}) = \sum\limits\_{i=1}^N \delta(\textbf{r - r}')$$

Now, we will consider the time-dependent [Schrodinger equation](http://en.wikipedia.org/wiki/Schr%C3%B6dinger_equation "Schrödinger equation"), but we will use the interaction picture, which describes the interacting system's time dependence as:

$$ i \frac{d}{dt} |\Psi(t)\_{I} \rangle = V\_I |\Psi(t)\_I\rangle$$

With $$ |\Psi(t)\_I \rangle = e^{iH\_0t}|\Psi(t)\_I\rangle$$ and $$ V\_I = e^{iH\_0t}V\_{ext}e^{-iH\_0t} $$.

Now, we can solve this interaction picture as a [Dyson series](http://en.wikipedia.org/wiki/Dyson_series "Dyson series"), which we truncate after the first-order term (this is where we get _linear_ response theory). In principle, we could keep going to get quadratic terms and so on, but the equations get much more complicated. And so:

$$ |\Psi(t)\_I \rangle \approx |\Psi(0) \rangle - i \int\limits\_{-\infty}^t dt'V\_I(t') |\Psi(0)\rangle$$

A few notes about this expression are in order. The first term is simply the system at time zero. This is our first approximation. The second term introduces the perturbation of the potential, acting on the unperturbed wavefunction. The lower limit of infinity means that we "turn on" the perturbation infinitely long ago: this is an _adiabatic_ approximation. In other words, we turn on the perturbation slowly enough that the ground state wavefunction can track with the disturbance. If we turn on the perturbation too sharply, the response won't be smooth, and will display complicated ringing behavior (which we don't care about anyway). This equation is also only valid for small perturbations -- an approximation that holds true in most situations!

Now, we don't care too much about the time evolution of the wavefunction _per se_. What we really care about is the response of some observable $$ O$$ (energy, whatever). In general, we can write this response as:

$$ \delta\langle O \rangle = \langle\Psi(t)|O|\Psi(t)\rangle - \langle\Psi(0)|O|\Psi(0)\rangle$$

$$ \delta\langle O \rangle = \langle\Psi(t)\_I|O\_I|\Psi(t)\_I\rangle - \langle\Psi(0)|O|\Psi(0)\rangle$$

$$ \delta\langle O \rangle = \lim\_{\\\eta \to 0} -i\int\limits\_{-\infty}^tdt'e^{\eta t'}\langle\Psi(0)|[O\_I(\textbf{r},t),V\_I(t')]|\Psi(0)\rangle$$

$$ \delta\langle O \rangle = \lim\_{\eta \to 0} -ie^{\eta t}\int\limits\_{-\infty}^tdt'e^{\eta (t-t')}\langle\Psi(0)|[O\_I(\textbf{r},t),V\_I(t')]|\Psi(0)\rangle$$

Note that the term $$ [O\_I,V\_I]$$ is just the commutator expression. The $$ e^{\eta t'}$$ ensures adiabatic switching on, and $$ \eta$$ is an infinitesimal real number. Eventually we will send $$ \eta$$ to zero, but for now we need it for $$ t \to 0$$ compared with $$ -\infty$$. If you still don't buy that explanation, consider what the function does at $$ t = 0$$ and $$ t = -\infty$$: at time $$ t = 0$$ the exponential is one, at time $$ t = -\infty$$, the exponential is zero.

With that said, we need to derive an expression for $$ V\_I$$. Since $$ V\_{ext}$$ commutes with $$ H\_0$$, we have:

$$ V\_I = e^{iH\_0t}V\_{ext}e^{-iH\_0t} = e^{iH\_0t} \int d\mathbf{r}\rho(\mathbf{r})V\_{ext}(\mathbf{r},t)e^{-iH\_0t} = \int d\mathbf{r}\rho\_I(\mathbf{r})V\_{ext}(\mathbf{r},t)$$

Where $$ \rho\_I(\mathbf{r}) = e^{iH\_0t}\rho(\mathbf{r})e^{-iH\_0t}$$. If we substitute this expression into our expression for $$ \delta\langle O\rangle$$, and perform the integration from $$ t' = -\infty$$ to $$ t' = t$$, we get (after a little math):

$$ \delta\langle O\rangle = \int\limits\_{-\infty}^{\infty} dt' \int d\mathbf{r}' \chi(\mathbf{r},t;\mathbf{r}',t')V\_{ext}(\mathbf{r}',t')$$

Where $$ \chi(\mathbf{r},t;\mathbf{r}',t')$$ is our response function, defined as:

$$ \chi (\mathbf{r},t;\mathbf{r}',t') = \lim\_{\eta \to 0} -i\theta(t-t')\langle\Psi(0)|[O\_I(\textbf{r},t),V\_I(t')]|\Psi(0)\rangle e^{\eta(t'-t)}$$

The term $$ \theta(t - t')$$ is the [Heaviside function](http://en.wikipedia.org/wiki/Heaviside_step_function "Heaviside step function"). This is a step function which is zero for $$ t - t' \< 0$$ and 1 for $$ t - t' \> 0$$. In other words, there is no response before we turn on the perturbation, and a full response once we do. We keep this to preserve causality of the response (no sense responding before there is something to respond to!)

Quick recap of what we have done so far. At this point we have a function for the response of _any_ observable to some external potential (a laser, a magnet, whatever). In the case of LR- [TD-DFT](http://en.wikipedia.org/wiki/Time-dependent_density_functional_theory "Time-dependent density functional theory"), we are concerned with the _density_ response to an external potential. And what do you know? Density is an observable! In fact, we gave the operator earlier in our derivation. So the next step is to plug in the density operator for $$ \langle O\rangle$$ and carry the results through. Plugging in we have:

$$ \delta\langle \rho(\textbf{r},t)\rangle = \delta\langle \rho(\mathbf{r}) \rangle = \int\limits\_{-\infty}^{\infty} dt' \int d\mathbf{r}' \chi(\mathbf{r},t;\mathbf{r}',t')V\_{ext}(\mathbf{r}',t')$$

with

$$ \chi (\mathbf{r},t;\mathbf{r}',t') = \lim\_{\eta \to 0} -i\theta(t-t')\langle\Psi(0)|[\rho\_I(\textbf{r},t),\rho\_I(\textbf{r}',t')]|\Psi(0)\rangle e^{\eta(t'-t)}$$.

Nothing too fancy here, just a bit of math. If we use our definition of $$ \rho\_I(\textbf{r},t) = e^{iH\_0t}\rho(\textbf{r})e^{-iH\_0t}$$, the response function can be written as:

$$ \chi (\mathbf{r},\mathbf{r}',t-t') = \lim\_{\eta \to 0} -i\theta(t-t')\langle\Psi(0)|[\rho\_I(\textbf{r},0),\rho\_I(\textbf{r}',t'-t)]|\Psi(0)\rangle e^{\eta(t'-t)}$$

Here is where it gets interesting. Up until now, our response function has been in the time domain. If we introduce a [Fourier transform](http://en.wikipedia.org/wiki/Fourier_transform "Fourier transform"), and make use of the convolution theorem, we can transform the time-dependent equations to the equivalent frequency-dependent equations. This allows us to determine responses to _individual frequencies of light_. This is perfect, because it allows for us to later determine specific energies (i.e frequencies) of light that give distinct electronic excitations. Performing the aforementioned Fourier transform and convoluting, we get:

$$ \delta\langle \rho(\textbf{r},\omega)\rangle = \int d\mathbf{r}' \chi(\mathbf{r},\mathbf{r}',\omega)V\_{ext}(\mathbf{r}',\omega)$$

with

$$ \chi (\mathbf{r},\mathbf{r}',\omega) = \lim\_{\eta \to 0} -i\int\limits\_{-\infty}^{0} d\tau \langle\Psi(0)|[\rho\_I(\textbf{r},0),\rho\_I(\textbf{r}',\tau)]|\Psi(0)\rangle e^{-(i\omega - \eta)\tau}$$

$$ V\_{ext}(\textbf{r}',\omega) = \int\limits\_{-\infty}^{\infty} V\_{ext}(\textbf{r}',t')e^{i\omega t'}dt'$$

Alright, let's wrap this up and get the spectral representation of the density response function. If the system is initially in the ground state, e.g. ( $$ |\Psi(0)\rangle = |\Psi\_0\rangle$$ with lowest eigenvalue $$ E\_0$$ ), and $$ H\_0|\Psi\_n\rangle = E\_n|\Psi\_n\rangle$$, we can insert the complete set of unperturbed states ( $$ \sum\limits\_n |\Psi\_n\rangle\langle\Psi\_n|$$ = 1 ) into the response function to get:

$$ \chi(\textbf{r},\textbf{r}',\omega) = \lim\_{\eta \to 0} \sum\limits\_n [\frac{\langle\Psi\_0|\rho(\textbf{r})|\Psi\_n\rangle\langle\Psi\_n|\rho(\textbf{r}'|\Psi\_0\rangle}{\omega - (E\_n - E\_0) + i\eta} - \frac{\langle\Psi\_0|\rho(\textbf{r}')|\Psi\_n\rangle\langle\Psi\_n|\rho(\textbf{r}|\Psi\_0\rangle}{\omega + (E\_n - E\_0) + i\eta}]$$

And there you have it! The spectral representation of the response function. The function has poles when $$ \omega \to (E\_n - E\_0)$$, which are the excitation energies. Thus we have a way to determine the excitation energies of the system! Later, I will show how we can use this result in the Kohn-Sham scheme to get excitation energies from the density functional theory framework.

