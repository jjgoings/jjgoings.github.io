--- 
layout: post 
title: Data Munging with Pandas 
---

I'm almost embarassed I haven't heard of pandas until now. [pandas](http://pandas.pydata.org/) is a suite of python tools for data munging, and works more or less like a really fast Excel spreadsheet. I find it a pain to get data in a form I can use, and usually my first instinct is to just hack together something workable and then leave it. But that is sloppy in practice, and not very satisfying. So I'll redo some parts of my [last post](http://joshuagoings.wordpress.com/2013/09/07/colley-method-for-ranking-nfl-teams/) on rating teams, so you can see it in action.

So before when I wanted to get a list of NFL teams for my ranking programs, I did something like this:

```python  
def get\_teams():  
 """ Get team data from masseyratings.com,  
 parse it into a dictionary with team number  
 as the key, team name as the value  
 """  
 f = urllib.urlopen("http://www.masseyratings.com/scores.php?s=199229&sub=199229&all=1&mode=3&exhib=on&format=2")  
 s = f.read().split()  
 my\_teamnames = {}  
 for i in range(0,len(s)/2):  
 my\_teamnames.update({i : s[i\*2 + 1]})  
 return my\_teamnames  
```

Not really intuitive what I did there, mostly a lot of hacking to get the list of teams in a usable fashion for the rest of the program. It returns a python dictionary, and it looks like this:

    {0: 'Arizona',
     1: 'Atlanta',
     2: 'Baltimore',
     ...
     29: 'Tampa_Bay',
     30: 'Tennessee',
     31: 'Washington'}

Let's do it a better way.  
Here is how we do it with pandas (imported as 'pd'):

```python  
def get\_teams():  
 team\_data = urllib2.urlopen('http://www.masseyratings.com/scores.php?s=199229&sub=199229&all=1&mode=3&format=2')  
 teams = pd.read\_csv(team\_data, header=None)  
 teams.columns = ['Team\_ID', 'Team\_name']  
 return teams  
```

A mere four lines of code, each with a distinct (and clear) purpose! First line, open the webpage containing data. Second line, read in the data to a pandas 'DataFrame' object (think a spreadsheet). Third, name the columns, and finally return the object, which looks like so:

    Team_ID Team_name
    0 1 Arizona
    1 2 Atlanta
    2 3 Baltimore
    ... ... ...
    29 30 Tampa_Bay
    30 31 Tennessee
    31 32 Washington

The first column is the index, which starts at zero in a pythonic manner. The second column is team ID, which is what the data itself uses. So don't get confused by those numbers. Having a DataFrame object allows us to easily index the columns and rows. It also easily allows us to add columns to it. So say we get a rating vector, and want to pair it up with our team names. Before I did it like so:

```python  
def write\_sorted(teams,rating):  
 combine = np.vstack((rating,teams))  
 sort\_combine = np.array(sorted(combine.T,key=tuple,reverse=True))  
 f = open(str(filename)+'.txt','w')  
 for i in range(0,len(teams)):  
 f.write(str(team\_name[int(sort\_combine[i,1])])+', '+str(sort\_combine[i,0])+'\n')  
 f.close()  
```

Again, kind of a hack to stack the lists (via 'vstack'), then sort them by rating, which involves transposing the array, using tuple keys...and if you've never done this before you have to look up all the options. And then you have to write to file in such a way as to link up team names with the ID in the vector...it's messy and I don't like it. So let's try it with pandas. You saw the team object before, right? Now we do:

```python  
def write\_sorted(teams,rating,filename):  
 teams['rating'] = rating  
 teams = teams.sort(columns='rating',ascending=False)  
 teams.to\_csv(filename)  
```

Done. (Of course we can add different formatting options, too). Add a column titled 'rating' to our teams object, sort by the column 'rating', in descending order, then write to file. SO EASY. And here we have it:

    Team_ID,Team_name,rating
    13, Houston,0.7603317475519333
    19, New_England,0.7582151079219482
    16, Kansas_City,0.7420115719733623
    ...
    15, Jacksonville,0.30074546774453426
    18, Minnesota,0.2838074821824212
    25, Pittsburgh,0.24660385713879754
    32, Washington,0.20859838193293445

It's just so simple, and I'm really glad that I found this module for my python programs!

And as a bonus for reading this far, here is a picture of a laughing panda.

[![Oh internet, you so FUNNY]({{ site.baseurl }}/assets/laughing_panda.jpg?w=300)](http://joshuagoings.files.wordpress.com/2013/09/laughing_panda.jpg)

