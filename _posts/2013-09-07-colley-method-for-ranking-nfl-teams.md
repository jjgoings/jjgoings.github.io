--- 
layout: post 
title: Colley Method for Ranking NFL Teams 
---

The NFL season started this week, which means it is a perfect time to set up a program for ranking teams! My fiancee bought me a book last Christmas called [Who's #1](http://www.amazon.com/Whos-The-Science-Rating-Ranking/dp/0691154228), which is an awesome book on how ranking and rating methods work. Specifically the book is geared towards sports, but I was surprised to learn how many companies use ranking algorithms --- for example, Google and [Netflix](http://en.wikipedia.org/wiki/Netflix "Netflix"). I am --- by and large --- ignorant of most things sports related, but this past year I had lived with five other guys who love sports and who had invited me to join their [March Madness](http://en.wikipedia.org/wiki/NCAA_Men%27s_Division_I_Basketball_Championship "NCAA Men's Division I Basketball Championship") bracket group. Since I don't really follow college basketball, but I wanted a shot at winning our groups bracket challenge (there was a cash prize!), I used the methods in the book to rank college basketball teams and fill out the brackets algorithmically. I ended up taking the second place prize out of a group of nearly 25 brackets in our group, and in the top 5% nationally. I took first in my bracket group I did with the other graduate students...but I didn't put any money in that one! (Bummer...)

One of the first methods I learned is called the Colley Method, and you can read all about it [here](http://www.colleyrankings.com/matrate.pdf). You might recognize it as one of the key computer methods in college football's [Bowl Championship Series](http://en.wikipedia.org/wiki/Bowl_Championship_Series "Bowl Championship Series") (no comment on that). The method takes the win-loss record of each team, assigns them a numerical rating based on who they beat (or lost to), and ranks them according to that rating. The big idea is that if you beat a very good team, it should count more than if you beat a poor team, and if you lose to a very good team, you should not be 'penalized' as much as if you lose to a terrible team. In a sense, it works by interconnecting teams based on who they won and lost against --- kind of like a pseudo-social network. If you beat me, and I beat your friend, then we assume you would have beaten your friend, even if you never go to play them. Hopefully that makes sense!

Anyway, if you want to try it yourself, [here is a link to the code that ranks both the 2012 and 2013 NFL teams](https://github.com/jjgoings/nfl-colley-method). I included an option for preseason games, since there is (at the time of this writing) only one regular season game that has been played in the NFL. Note that you will need the `numpy` module for this to work.

To run it, type

~~~
python ranking.py -e -y 2013
~~~

This will call all the other `python` files to fetch the data from `http://www.masseyratings.com` and will then process it an implement the Colley method, giving you a `colley.txt` file containing the ratings of each team (sorted of course). The flag `-y` gives input for the year (2012 or 2013), and the `-e` flag, if present, includes [exhibition matches](http://en.wikipedia.org/wiki/Exhibition_game "Exhibition game") as well (e.g. preseason games).

Now for the guts of the code (for those who are interested).

First we need a way to get the data from masseyratings.com, and put the games into an array as well as get our teams. Because the games use an integer to represent the teams, I create a `python` dictionary to map the number to the team name. So `getdata.py` does precisely this:

~~~python  
def get_teams():  
     """ Get team data from masseyratings.com,  
       parse it into a dictionary with team number  
       as the key, team name as the value  
     """  
     f = urllib.urlopen("http://www.masseyratings.com/scores.php?s=199229&sub=199229&all=1&mode=3&exhib=on&format=2")  
     s = f.read().split()  
     my_teamnames = {}  
     for i in range(0,len(s)/2):  
         my_teamnames.update({i : s[i*2 + 1]})  
     return my_teamnames

def get_games(year,exhibition):  
    """ Get game data from masseyratings.com,  
      parse it into a numpy array.  
    """  
    if year == 2013:  
        if exhibition == True:  
            f = urllib.urlopen('http://www.masseyratings.com/scores.php?s=199229&sub=199229&all=1&mode=3&exhib=on&format=1')  
        elif exhibition == False:  
            f = urllib.urlopen('http://www.masseyratings.com/scores.php?s=199229&sub=199229&all=1&mode=3&format=1')  
        else:  
            sys.exit('"exhibition" must be "True" or "False"')  
    elif year == 2012:  
        if exhibition == True:  
            f = urllib.urlopen('http://www.masseyratings.com/scores.php?s=181613&sub=181613&all=1&mode=3&exhib=on&format=1')  
        elif exhibition == False:  
            f = urllib.urlopen('http://www.masseyratings.com/scores.php?s=181613&sub=181613&all=1&mode=3&format=1')  
        else:  
            sys.exit('"exhibition" must be "True" or "False"')  
    else:  
        sys.exit('Not a valid year')  
    s = f.read()  
    if exhibition == False:  
        file_name = str('games_'+str(year)+'.txt')  
    elif exhibition == True:  
        file_name = str('games_'+str(year)+'_exhib.txt')  
    k = open(file_name,'w')  
    k.write(s)  
    k.close()  
    f.close()

    my_games = genfromtxt(file_name, dtype = None, delimiter=',')

    return my_games  
~~~

Once we have our games and teams, we need to set up the Colley matrix ('A'), and solve it against Colley's 'b' vector. The `colley.py` takes care of this. We take data about the games, and set up a square matrix with the number of teams as the dimension. Where teams intersect contains data about how they fared against each other. The mathematical details can be found in the Who's #1 and in the link to the Colley Method I gave. The end result of this code is a rating vector (called `rating` here). Anyway, here is that code:

~~~python  
def colley(num_teams,num_games,my_teams,my_games):

    A = np.zeros((num_teams,num_teams))  
    wins = np.zeros(num_teams)  
    losses = np.zeros(num_teams)  
    total = np.zeros(num_teams)
    
    for game in range(0,num_games):  
        w = my_games[game,2] - 1.0  
        l = my_games[game,5] - 1.0
    
        A[w,w] = A[w,w] + 1.0  
        A[l,l] = A[l,l] + 1.0  
        A[l,w] = A[l,w] - 1.0  
        A[w,l] = A[w,l] - 1.0
    
    for i in range(0,num_teams):  
        total[i] = total[i] + wins[i] + losses[i]
    
    b = np.zeros(num_teams)  
    for i in range(0,num_teams):  
        A[i,i] = 2 + total[i] + A[i,i]  
        b[i] = 1 + (wins[i] - losses[i])/2
    
    rating = np.linalg.solve(A,b)  
    return rating  
~~~

Once we have these, we pair it up with our dictionary element containing the team names, and sort it. This is the `finalsort.py` code. I wrapped everything in the file `ranking.py` if you are checking this out in my repo. It takes care of making all the files play nicely together.

So now the big question is, how does it fare? Here is the list as of today (9/7/13):

~~~
    Seattle, 0.806187648116
    Detroit, 0.76229943304
    Washington, 0.734350377447
    Cleveland, 0.691797811483
    New_England, 0.666157176065
    New_Orleans, 0.657992419938
    NY_Jets, 0.652519130556
    San_Francisco, 0.648158042535
    Arizona, 0.647296343048
    Houston, 0.647271431013
    Denver, 0.614105025386
    Carolina, 0.600878984866
    Buffalo, 0.563322480133
    Cincinnati, 0.557969510878
    Philadelphia, 0.53328007273
    Indianapolis, 0.525416655862
    Chicago, 0.522801819437
    Kansas_City, 0.479567506516
    Dallas, 0.453378981006
    San_Diego, 0.437407308856
    Miami, 0.414388770684
    Oakland, 0.406726811416
    Green_Bay, 0.37888674304
    Tampa_Bay, 0.36195341794
    Minnesota, 0.357868414451
    Baltimore, 0.356824183447
    St_Louis, 0.340268960559
    NY_Giants, 0.339410132678
    Tennessee, 0.288458533025
    Jacksonville, 0.280125144891
    Pittsburgh, 0.192367833585
    Atlanta, 0.0805628953732
~~~

Not surprisingly, Seattle is at the top (Woot woot! Go Hawks!), having finished the preseason perfectly against tough teams. Atlanta is at the bottom, having lost every preseason game. Generally, the ratings stack up similar to how the teams did in the preseason.

Also not surprising? How poor of a representation I think it really is. Preseason games are the time where teams test out their second and third strings and avoid playing their top players. So I think, for example, Atlanta will fare a lot better than this preseason ranking suggests. While I like the Colley Method's simplicity, I think it performs poorly as a predictive algorithm. The Massey method, on the other hand, is much better at predicting future match-ups. This was my experience with it in March Madness anyway. Google it if you are curious. If you are serious about doing any sports ranking, I also want to suggest that you take a look at weighting methods...for example, games played later in the season 'count more'. I think that is a critical step to getting predictive algorithms. How to do that well, though, is more of an art :)

If you have any questions or comments, let me know!

