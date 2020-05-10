---
layout: page
title: Projects 
---

Here are a couple of side projects I've been working on for fun.

### [Natural language processing (NLP) of Trump's COVID-19 briefings](https://github.com/jjgoings/trump-covid-briefings)

<p align="center">
<img alt="" src="{{ site.baseurl }}/assets/NMF-topics.jpeg" height="300" border="1"/>
</p>

Like many people, I have been following the news closely during the coronavirus pandemic. I got interested in [how Trump was talking about the coronavirus](https://github.com/jjgoings/trump-covid-briefings) and thought it would be fun to use natural language processing (NLP) techniques to identify what topics Trump talks about and how his sentiment is connected to world events. 

---

### [Interactive New Haven crime map](https://github.com/jjgoings/new-haven-major-crimes) 

<p align="center">
<a href="https://new-haven-crime-data.herokuapp.com/"><img alt="New Haven Crime" src="{{ site.baseurl }}/assets/crime_map_demo.gif" height="300" border="1"/></a>
</p>

New Haven isn't exactly [known for being the safest city](https://www.cbsnews.com/pictures/americas-10-most-dangerous-cities/7/) in America, and I wanted to learn more. But the data didn't exist in a nice form. So I made an interactive map of recent crime that I scraped from the [New Haven Police Department](https://www.newhavenct.gov/gov/depts/nhpd/compstat_reports.htm). It was fun to learn how to scrape data from PDFs, clean it with OpenRefine, geo-tag the results, and deploy as an interactive webapp.

---

### [McMurchie-Davidson](https://github.com/jjgoings/McMurchie-Davidson) 

<p align="center">
<img alt="" src="{{ site.baseurl }}/assets/nonlinear.jpeg" height="300" border="1"/>
</p>

It was a dream in graduate school to build a quantum chemistry program from scratch. [This was the result](https://github.com/jjgoings/McMurchie-Davidson), using the McMurchie-Davidson algorithm to compute the (very expensive) electronic integrals. With no experimental input, it allows you to solve for the wave function of any molecule. Among other things, you can use it to simulate how molecules respond to light in real-time. I also dabbled in learning Cython to optimize the algorithm in performance-critical routines, without sacrificing code readability.

---

