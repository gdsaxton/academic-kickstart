---
title: Analyzing Big Data with Python PANDAS
author: Gregory Saxton
type: post
date: 2015-10-23T23:59:33+00:00
url: /analyzing-big-data-with-python-pandas/
dsq_thread_id:
  - 6565774846
categories:
  - Big Data
  - ipython_notebook
  - notebooks
  - pandas
  - python
  - research
  - Twitter
tags:
  - academic research
  - Big Data
  - hashtags
  - iPython
  - PANDAS
  - Programming
  - python
  - research
  - social media
  - socialmedia
  - tutorial
  - Twitter

---
This is a series of iPython notebooks for analyzing Big Data &#8212; specifically Twitter data &#8212; using Python&#8217;s powerful <a href="http://pandas.pydata.org/" target=_blank>PANDAS</a> (Python Data Analysis) library. Through these tutorials I&#8217;ll walk you through how to analyze your raw social media data using a typical social science approach.

The target audience is those who are interested in covering key steps involved in taking a social media dataset and moving it through the stages needed to deliver a valuable research product. I&#8217;ll show you how to import your data, aggregate tweets by organization and by time, how to analyze hashtags, how to create new variables, how to produce a summary statistics table for publication, how to analyze audience reaction (e.g., # of retweets) and, finally, how to run a logistic regression to test your hypotheses. Collectively, these tutorials cover essential steps needed to move from the data collection to the research product stage. 

**Prerequisites**

I&#8217;ve put these tutorials in a GitHub repository called <a href="http://github.com/gdsaxton/PANDAS" target=_blank>PANDAS</a>. For these tutorials I am assuming you have already downloaded some data and are now ready to begin examining it. In the first notebook I will show you how to set up your ipython working environment and import the Twitter data we have downloaded. If you are new to Python, you may wish to go through a <a href="http://social-metrics.org/tutorial-list/" target=_blank>series of tutorials</a> I have created in order. 

If you want to skip the data download and just use the sample data, but don&#8217;t yet have Python set up on your computer, you may wish to go through the tutorial <a href="http://social-metrics.org/python-code-prerequisites/" target=_blank>&#8220;Setting up Your Computer to Use My Python Code&#8221;</a>.

Also note that we are using the <a href="http://ipython.org/notebook.html" target=_blank>iPython notebook interactive computing framework</a> for running the code in this tutorial. If you&#8217;re unfamiliar with this see this tutorial <a href="http://social-metrics.org/starting-on-python-2/" target=_blank>&#8220;Four Ways to Run your Code&#8221;</a>.

For a more general set of PANDAS notebook tutorials, I&#8217;d recommend <a href="http://jvns.ca/blog/2013/12/22/cooking-with-pandas/" target=_blank>this cookbook by Julia Evans</a>. I also have <a href="http://social-metrics.org/python-pandas-cookbook/" target=_blank>a growing list of &#8220;recipes&#8221;</a> that contains frequently used PANDAS commands.

As you may know from my other tutorials, I am a big fan of the free <a href="https://store.continuum.io/cshop/anaconda/" target=_blank>Anaconda version of Python 2.7</a>. It contains all of the prerequisites you need and will save you a lot of headaches getting your system set up. 

**Chapters:**

At the GitHub site you&#8217;ll find the following chapters in the tutorial set:

<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%201%20-%20Import%20Data%2C%20Select%20Cases%20and%20Variables%2C%20Save%20DataFrame.ipynb" target="_blank">Chapter 1 &#8211; Import Data, Select Cases and Variables, Save DataFrame.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%202%20-%20Aggregating%20and%20Analyzing%20Data%20by%20Twitter%20Account.ipynb" target="_blank">Chapter 2 &#8211; Aggregating and Analyzing Data by Twitter Account.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%203%20-%20Analyzing%20Twitter%20Data%20by%20Time%20Period.ipynb" target="_blank">Chapter 3 &#8211; Analyzing Twitter Data by Time Period.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%204%20-%20Analyzing%20Hashtags.ipynb" target="_blank">Chapter 4 &#8211; Analyzing Hashtags.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%205%20-%20Generating%20New%20Variables.ipynb" target="_blank">Chapter 5 &#8211; Generating New Variables.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%206%20-%20Producing%20a%20Summary%20Statistics%20Table%20for%20Publication.ipynb" target="_blank">Chapter 6 &#8211; Producing a Summary Statistics Table for Publication.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%207%20-%20Analyzing%20Audience%20Reaction%20on%20Twitter.ipynb" target="_blank">Chapter 7 &#8211; Analyzing Audience Reaction on Twitter.ipynb</a>  
<a href="http://nbviewer.ipython.org/github/gdsaxton/PANDAS/blob/master/Chapter%208%20-%20Running%2C%20Interpreting%2C%20and%20Outputting%20Logistic%20Regression.ipynb" target="_blank">Chapter 8 &#8211; Running, Interpreting, and Outputting Logistic Regression.ipynb</a>

I hope you find these tutorials helpful; please acknowledge the source in your own research papers if you&#8217;ve found them useful:

&nbsp; &nbsp; Saxton, Gregory D. (2015). _Analyzing Big Data with Python._ Buffalo, NY: http://social-metrics.org

Also, please share and spread the word to help build a vibrant community of PANDAS users. 

Happy coding!

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>