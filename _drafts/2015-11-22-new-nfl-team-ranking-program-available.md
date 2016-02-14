---
layout: post 
title: New NFL team ranking program available 
---

I released some new code today that should allow you to easily rank NFL teams for any given season (back through 2009) using either the Colley or Massey methods. Both methods have several weighting schemes implemented, and with the Massey method you can additionally rank according to point differential or total yard differential.

You can check it out on my GitHub [here](https://github.com/jjgoings/nflranking).

I've become increasingly dissatisfied with my old [NFL Colley ranking system](https://github.com/jjgoings/nfl-colley-method) and its derivatives, mostly because (a) I didn't write it in an object-oriented style, and (b) it became very (VERY) hard to modify later on. The new structure, by encapsulating everything in a "Season" object should keep everything pretty self-contained.

For example, now  

```python
from season import Season

season = Season()  
season.year = 2014 # default season is 2015  
season.massey() # Massey ranking method, unweighted  
for team in season.rating:  
    print team  
```

Which gives the output

```bash
['NE', 11.407605241747872]  
['DEN', 9.6038904227178108]  
['SEA', 9.5169656599013628]  
['GB', 8.2526935620363258]  
...  
['OAK', -8.9899785292554917]  
['TB', -9.8107991356959232]  
['JAC', -10.427123019821691]  
['TEN', -11.805248019821692]
```

So obviously the NE Patriots were ranked #1 for the 2014 season with this method. You'll recall they ended up winning the Super Bowl that same season.

So anyway, I'm starting over and making use of some great NFL APIs that I have found elsewhere on GitHub. In particular, I am using [nflgame](https://github.com/BurntSushi/nflgame/tree/master/nflgame), which does a lot of the heavy lifting for me associated with scraping necessary data.

[Check it out](https://github.com/jjgoings/nflranking) if this sounds like it may be something you're interested in!

