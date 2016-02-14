--- 
layout: post 
title: Fragment generator for polypeptide mass-spectroscopy 
---

[![Cobalt(II) Interface with ETR Important Residues]({{ site.baseurl }}/assets/cobaltii-interface-with-etr-important-residues.png?w=300)](http://joshuagoings.files.wordpress.com/2013/10/cobaltii-interface-with-etr-important-residues.png)

I have a friend here at the UW that is using mass spectroscopy to identify proteins. Proteins, also called polypeptides, are made up of building blocks called amino acids/peptides. Because polypeptides fragment differently, they can use the fragmentation patterns to determine what an unknown protein is. Kind of a cool idea, I think. The hope is to be able to use it for blood work analysis in medical settings, though I am sure there are plenty of other applications. In fact, C&EN just ran an article this past week on how mass spec was really getting used in biology. You can read it [here](http://cen.acs.org/articles/91/i42/Mass-Specs-Century-Change.html) (sorry, it's behind a paywall...).

Anyway, he was trying to fit patterns of polypeptides together to fit the different peaks he found. Like if he found a peak at 500.38 M/Z, he would assume he had a GLN-TRP-TRP residue, which has a mass of 500.38 (or some combination thereof). The problem, then, is determining what different combinations of amino acids could fit the peaks! Now, there are really only 20 amino acids he could be looking at, so this turns out to be an interesting combinatorics problem: **how many different ways can we combine amino acids residues to fit a given mass (or mass range?)**

I realized it wouldn't be too bad to write a program, and so I am sharing the script with you!

So for this problem, we need to have a set of amino acids, and their masses. So I just looked up the information and hard-coded it into the program. This is the set we will be drawing our combinations from, and it looks like this:

```python

# Build list of amino acids  
amino_acids = ['ALA','ARG','ASP','ASN','CYS','GLU','GLN','GLY','HIS','ILE', \  
    'LEU','LYS','MET','PHE','PRO','SER','THR','TRP','TYR','VAL']  
amino_acid_MW = [71.09,156.19,114.11,115.09,103.15,129.12,128.14,57.05,137.14,113.16, \  
    113.16,128.17,131.19,147.18,97.12,87.08,101.11,186.12,163.18,99.14]  
# Combine them into one list, AA  
AA = zip(amino_acids,amino_acid_MW)

```

We zip them together to pair up the name of the residue (or amino acid) and its mass.

Once we have this, we will start building our combinations. First we take all combinations of 1 amino acid, then 2 amino acids, then 3 and so on. We don't need to explicitly make and check each combination if we know will be below the mass specified, or if the chain will always be too high for our desired target mass. For example, say we want all combinations of residues that have a mass between 500.3 and 500.5. In this case, no chain of 2 amino acids alone can reach this, because the largest residue we are working with has a mass of 186.12! Similarly, if the lightest chain possible is too big (e.g. a chain of glycines), we better stop right there because there is no way we will find any more combinations of residues. So we have a check for if the mass is too small (increment chain length by one and continue) or if the mass is too big (break and exit). These bounds keep our computation relatively sane! Here it is in action:

```python

for count in range(1,max_chain_length+1):  
    if count*57.05 > upper_bound_mass:  
        break  
    elif count*186.12 < lower_bound_mass:  
        continue  
```

Finally we need to generate our combinations. So inside the loop, we use `itertools` to generate all the unique combinations of length N from our set of amino acids. `itertools` has two tools to perform this: `combinations` and `combinations_with_replacements`. `combinations` won't allow a residue to be used more than once, so we choose to use `combinations_with_replacements`. This allows for combinations such as a polyalanine chain, but it also allows for many more combinations. So it can get pretty slow! If we have a length 10 chain, we get 10! combinations with combinations, but 10^10 combinations with `combinations_with_replacements`. Once we have our unique combinations, we sum the mass of each one, see if it matches the criteria, and if it does, we add it to a list that stores all the polypeptides we want. Here it is:

```python  
tot_combinations = itertools.combinations_with_replacement(AA,count)  
for combination in tot_combinations:  
    MWs = [x[1] for x in combination]  
    if sum(MWs) >= lower_bound_mass:  
        if sum(MWs) <= upper_bound_mass:  
            possible.append(combination) 
```

This function will then return a list of all the polypeptide chains that fit our mass criteria. All we have to do is print/write to file and go! This script gets pretty slow quite quickly, as we saw from the scaling criteria. We scale as N^N, where N is the length of our chain. I'm sure there is even more going on behind the scenes in the itertools module, but simply treating the creation of one unique combination as an "operation", we have an incredibly slow scaling method. Do you know a better way to do this? Let me know! I'd love to hear how to make this more efficient, and I am certain that some computer scientist somewhere has explored this question before... Here is the whole script:

```python  
import random
import itertools
import csv
import time


# this is a function that returns a list of the possible combinations of amino acids that have a mass (in daltons) 
# greater than a lower bound, and lower than an upper bound, along with a maximum polypeptide chain length
def polypeptide_chain(max_chain_length,lower_bound_mass,upper_bound_mass):
    # Build list of amino acids
    amino_acids = ['ALA','ARG','ASP','ASN','CYS','GLU','GLN','GLY','HIS','ILE', \
                   'LEU','LYS','MET','PHE','PRO','SER','THR','TRP','TYR','VAL']
    amino_acid_MW = [71.09,156.19,114.11,115.09,103.15,129.12,128.14,57.05,137.14,113.16, \
                     113.16,128.17,131.19,147.18,97.12,87.08,101.11,186.12,163.18,99.14]
    # Combine them into one list, AA
    AA = zip(amino_acids,amino_acid_MW)
    possible = []
    for count in range(1,max_chain_length+1):
        if count*57.05 > upper_bound_mass:
            break
        elif count*186.12 < lower_bound_mass:
            continue
        else:
            tot_combinations = itertools.combinations_with_replacement(AA,count)
            for combination in tot_combinations:
                MWs = [x[1] for x in combination]
                if sum(MWs) >= lower_bound_mass:
                    if sum(MWs) <= upper_bound_mass:
                        possible.append(combination)
    return possible               

# here is an example of it in use: it looks for polypeptide chains no longer than 20 amino acids, with a combined mass between 949.9 Da and 950.1 Da

### ---  make your changes here in the arguments of the function
t0 = time.time()
poss = polypeptide_chain(20,500.3,500.5)   
t1 = time.time()
### --- end changes
# we write it to file, naming the file 'polypeptides.csv'
with open('polypeptides.csv','wb') as my_file:
    file_writer = csv.writer(my_file,delimiter=' ')
    for i in poss:
        aa,mass = zip(*i)        
        my_file.write(str(sum(mass))+'\t')
        file_writer.writerow(aa)

print "Time: ", t1-t0, " seconds"
```

Enjoy!  

