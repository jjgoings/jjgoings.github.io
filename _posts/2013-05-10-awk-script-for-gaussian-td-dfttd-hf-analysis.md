--- 
layout: post 
title: Awk Script for Gaussian TD-DFT/TD-HF Analysis 
---

When I am generating [UV-Vis](http://en.wikipedia.org/wiki/Ultraviolet%E2%80%93visible_spectroscopy "Ultraviolet–visible spectroscopy") spectra (in some cases near-IR spectra) for some system, I am often dealing with hundreds of individual electronic transitions. And most of the time, these transitions don't even matter (e.g. their [oscillator strength](http://en.wikipedia.org/wiki/Oscillator_strength "Oscillator strength") is ~ 0). This happens a ton when I am generating spectra for semiconductor quantum dots. TD analysis shows tons of 'transitions' but they exist in the band gap, and I'd rather filter them out. See, for example, below:

[![qd33spectra]({{ site.baseurl }}/assets/qd33spectra.jpg?w=300)](http://joshuagoings.files.wordpress.com/2013/05/qd33spectra.jpg)

[TD-DFT](http://en.wikipedia.org/wiki/Time-dependent_density_functional_theory "Time-dependent density functional theory") actually shows tons of transitions from ~2 to 4.5 [eV](http://en.wikipedia.org/wiki/Electronvolt "Electronvolt")...they just don't matter! So for my own sanity in pouring through the data, I wrote this [Awk](http://cm.bell-labs.com/cm/cs/awkbook "AWK") script (well, Awk in a Bash script) to pull out the transitions I want, based on oscillator strength (intensity). If you don't know Awk, you really should. It has nasty syntax (like [Perl](http://www.perl.org "Perl")...), but once you get used to it, it makes text editing and parsing SO SO EASY. I love it. I use Awk all the time for my work. Take a look, and feel free to grab a copy for yourself. To run the script, just type (minus the quotes, and assuming you saved it as 'tdanalysis'): 

```
./tdanalysis [FILE] [minimum oscillator strength]
```

Enjoy!

```bash

#!/bin/bash

if ["$#" == "0"]; then  
 printf "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\nTD_ANALYSIS\nPrints TDDFT Excitations above a given oscillator strength.\nUSE: td_analysis [LOG FILE] [MINIMUM OSCILLATOR STRENGTH]\n\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n"  
 exit 1  
fi

# Grab file (Gaussian .log file) and desired minimum oscillator strength

# The MULT variable is used to give you

# % contributions based on whether the system is open or closed shell.

FILE=$1  
OSCIL=$2  
MULT=`gawk '/Charge/ && /Multiplicity/ {print $6%2+1}' $1`  
gawk -v mult=$MULT 'BEGIN {format = "%-6s %-10s %10s %10s %6s\n"  
 print "TD Analysis of",ARGV[1]}  
 /f=([0-9])/ { printf format, "\nEnergy [eV]:",$5, " ","Oscillator Strength:", substr($9,3,6)"\n ----------------------------------------------------------------"};  
 /->/ {printf format, "", $1$2$3,$4," ","("mult*100*($4)^2"%)"}  
 END { print "\nEnd of Analysis\n\n"}' $FILE | gawk -v oscil=$OSCIL 'RS="\n\n" {if($6 > oscil) {print $0"\n"}}'

```

You may need to change `gawk` to `awk`, depending on your system. I've never had problems with `gawk` though.

