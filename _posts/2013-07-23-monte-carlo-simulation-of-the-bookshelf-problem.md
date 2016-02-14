---
layout: post 
title: Monte Carlo Simulation of the "Bookshelf" Problem 
---

I had a friend share with me this probability problem her professor had posed to the class --- and, yes, it was actually posed this colorfully:

"During a massive earthquake, all twelve of your books --- of which five are mathematical, four are literary, and three are reference --- are cast haphazardly across your living room. A fireman graciously put them back on the shelf while your wounds are being tended; however, he simply decides to randomly arrange them. What is the probability that the books are in natural sets; i.e., all mathematical books are adjacent, and all reference books are adjacent?"

Okay. Now, probability is one of those things I love doing, but am absolutely horrid at. I had no idea how to approach the problem, so I thought it would be a good candidate for a [Monte Carlo simulation](http://en.wikipedia.org/wiki/Monte_Carlo_method "Monte Carlo method") instead. The idea behind a Monte Carlo simulation comes from the frequentist school of probability. The idea is that the probability of an event happening is the relative frequency of that event happening in the limit of a large number of trials. For example, if we were to say that flipping a coin has a 50% probability of landing 'heads' and a 50% probability of landing 'tails', this would be equivalent to saying that if we were to flip a coin two million times, we'd expect it to land heads 1 million of those times. Now flipping a coin two million times (or more!) is tedious and terrible work for people, but computers excel at doing the same thing over and over again. So with a suitable [random number generator](http://en.wikipedia.org/wiki/Random_number_generation "Random number generation"), computers can accurately reproduce probabilities of events, especially if the exact probability is not as obvious as flipping a coin. Like arranging a bookshelf, say.

In the bookshelf problem, we can program our computer to take the 12 books, arrange them at random, and then count up the times it formed a 'natural set'. Simply divide the number of times the bookshelf was ordered by the number of times we arranged the bookshelf, and we get a probability for an ordered bookshelf! Here is an example of how I solved it in Python:

First, import the `random` and `itertools` modules, to help us generate random numbers and iterate among the lists. Then define two functions: one to check if two lists (or parts of lists) have all the same elements, and one to generate random numbers from 1 to 12 inclusive.

```python

#!/bin/python

from __future__ import division  
import random  
import itertools  
from time import time

# returns True if lists are the same, False if not  
def checkEqual(lst):  
    return lst[1:] == lst[:-1]

# Get random integer from [1,12]  
def rnum():  
    return random.randint(0,12)  

```

Then we build our bookshelf. You can see that --- pre-earthquake --- the books formed a so-called 'natural set'. We initialize the total number of times we arrange our shelf, as well as the number of ordered arrangements, to zero. We haven't done anything yet!

Then we begin the main loop. Each iteration of the loop does two big things: first, it randomly arranges the bookshelf, and two, it checks to see if it forms a natural set. The checking is where you see all the "if/elif/else" sections of code. Since there are only 6 ways we can form a natural set (3! ways to arrange 3 types of books), I just go ahead and check each case explicitly.

```python  

#!/bin/python

from __future__ import division
import random
import itertools
from time import time

# returns True if lists are the same, False if not
def checkEqual(lst):
  return lst[1:] == lst[:-1]

# Get random integer from [1,12]
def rnum():
  return random.randint(0,12)

# Build our bookshelf!
bookshelf = ['math','math','math','math','math','lit','lit','lit','lit','ref','ref','ref']
TOTAL = 0
ORDERED = 0
t0 = time()
for i in range(0,5000000):
  TOTAL += 1   # Count number of times we put the bookshelf back together
  pile = [] # Nothing in our pile yet!
  pile += bookshelf # Books falling off into our pile!
  new_shelf = [] #Now the shelf is empty!
  while len(pile) > 0:
    book = random.choice(pile) # Put the books on the shelf at random
    new_shelf.append(book)
    pile.remove(book) # remove book from pile once we put it on the shelf

  # At this point, we evaluate how the shelf is arranged. There are 3! ways
  # of arranging the shelf so that it it ordered, and we evaluate each one to see
  # if the new shelf fits the 'natural set' criteria.
  if checkEqual(new_shelf[:5]):
    if checkEqual(new_shelf[5:9]):
      if checkEqual(new_shelf[9:]):
        ORDERED +=1
    elif checkEqual(new_shelf[5:8]):
      if checkEqual(new_shelf[8:]):
        ORDERED +=1
  if checkEqual(new_shelf[:4]):
    if checkEqual(new_shelf[4:9]):
      if checkEqual(new_shelf[9:]):
        ORDERED +=1
    elif checkEqual(new_shelf[4:7]):
      if checkEqual(new_shelf[7:]):
        ORDERED +=1
  if checkEqual(new_shelf[:3]):
    if checkEqual(new_shelf[3:8]):
      if checkEqual(new_shelf[8:]):
        ORDERED +=1
    elif checkEqual(new_shelf[3:7]):
      if checkEqual(new_shelf[7:]):
        ORDERED +=1
t1 = time()
print 'ORDERED = ',ORDERED
print 'TOTAL = ',TOTAL
print 'PERCENT = ',(ORDERED/TOTAL)*100,'%'
print 'TIME = ',round(t1-t0,5),'seconds'

```

And we're done! Running the code for a suitable number of iterations gives the probability that the books are ordered. More simulations gives a more accurate answer. We'd get the perfect answer if we ran this for an infinite amount of times. Running it 1 million times gave me a probability of 0.0228%. Of course, since they were random trials, this number may change a bit, and if you run the code, you may get a different number --- though hopefully not too different!

So how does this compare? The exact answer is 0.02165%. We get this by treating the math books as one set, the literary books as one set, and the reference books as one set. For these sets, there are 3! ways to arrange them. Inside each set, there are 5! ways to arrange the math books, 4! ways to arrange the literary books, and 3! ways to arrange the reference books. Thus we have (3!5!4!3!) ways to arrange the books in a natural set. Ignoring order, since we have 12 books total, we have 12! ways to arrange the books in any order. This gives us our final probability of (3!5!4!3!)/(12!) or 0.02165%.

So our Monte Carlo simulation works, though it obviously does not get the exact answer. This is not surprising, considering we performed only 1 million trials --- which seems like a lot, but for a computer, it isn't. To really reproduce the data, we'd need the total number of trials to come close to the 12! we had in the exact denominator...about 479 million times. For many problems, a big challenge is determining how many trials you have to perform for confident results.

All said and done: don't bet on that dashing firefighter putting your books back in order :)

UPDATE: I was still curious about how the simulation would run if we approached the total number of ways to arrange the books --- that is, somewhere around 479 million trials. So I uploaded my program to our group's computing clusters, and parallelized the run over 5 processors, each running 100 million trials. The results? Out of 500 million trials, 108084 of them were ordered. This gives us a probability of 0.021617%, which is accurate to +/- 0.0001%! Not bad at all. In case you were curious, each 100 million trials took about 45 minutes. Glad I ran them on separate nodes --- otherwise I'd be waiting almost 4 hours! (Which admittedly is not very long in scientific computing...but considering the problem we are dealing with, even 45 minutes is excessive).

