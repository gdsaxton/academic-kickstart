---
title: Setting up Your Computer to Use My Python Code for Downloading Twitter Data
author: Gregory Saxton
type: post
date: 2014-11-24T02:51:00+00:00
url: /python-code-prerequisites/
dsq_thread_id:
  - 6565774913
categories:
  - academia
  - python
  - research
  - Twitter
tags:
  - academic research
  - python
  - tutorial
  - Twitter

---
I frequently get requests for how to download social media data in general, as well as for help on how to run code I have written to download and analyze the data I analyzed for a particular piece of research. Often, these requests are from people who are excited about doing social media research but have yet to gain much experience in using computer programming. For this reason, I have created a <a href="http://social-metrics.org/tutorial-list" target="_blank">set of tutorials</a> designed precisely for such users. 

I am always happy to share the code I&#8217;ve used in my research. That said, there are barriers to actually using someone else&#8217;s code. One of the key barriers is getting your own computer &#8220;set up&#8221; to actually run the code. The aim of this post is to walk you through the steps needed to run and modify the code I&#8217;ve written to download and analyze social media data. 

### Step One: Download and Install Python

As I write about <a href="http://social-metrics.org/python-where-to-start/" target="_blank">here</a>, for Unix, Windows, and Mac users alike I&#8217;d recommend you install <a href="https://store.continuum.io/cshop/anaconda/" target="_blank">Anaconda Python 2.7</a>. This distribution of Python is free and easy to install. Moreover, it includes most of the add-on packages necessary for scientific computing, including Numpy, Pandas, iPython, Statsmodels, Sqlalchemy, and Matplotlib.

Go to <a href="http://social-metrics.org/starting-on-python-1/" target="_blank">this tutorial</a> for instructions on how to install and run Anaconda Python.

### Step Two: Install Python Add-On Packages

Anaconda Python comes pre-installed with _almost_ everything you need. There are a couple of modules you will have to install manually: 

_Twython_ &#8212; for accessing the Twitter data

and 

_simplejson_ &#8212; for parsing the <a href="http://en.wikipedia.org/wiki/JSON" target="_blank">JSON</a> data that is returned by the Twitter <a href="http://en.wikipedia.org/wiki/Application_programming_interface" target="_blank">API</a> (Application Programming Interface).

Assuming you are on a Mac and using Anaconda Python, the simplest way is to use <a href="http://www.pip-installer.org/en/latest/" target="_blank">pip</a>. On a Mac or Linux machine, you would simply open the Terminal and type _pip install Twython_ and _pip install simplejson._ If you&#8217;re on a PC, please take a look at <a href="http://curiositybits.com/python-for-mining-the-social-web/python-tutorial-mining-twitter-user-profile/" target="_blank">Wayne Xu&#8217;s tutorial</a> (see Slide #8).

### Step Three: The Database

I generally download my Twitter data into an SQLite database. SQLite is a common relational database. It is lightweight and easy to use, and comes preinstalled in Anaconda Python. 

You may already know other ways of downloading social media data, such as NodeXL in Excel for Windows. Why then would you want to using SQLite? There are two reasons. First, SQLite is better plugged into the Python architecture, which will come in handy when you are ready to actually manipulate and analyze the data. Second, if you are downloading tweets more than once, a database is the much better solution for a simple reason: it allows you to write a check for duplicates in the database and stop them from being inserted. This is an almost essential feature that you cannot easily implement outside of a database. 

Also know that once you have downloaded the data into an SQLite database, you can view and edit the data in the same manner as an Excel file, and even export the data into CSV format for viewing in Excel. To do this, simply download and install <a href="http://sqlitebrowser.org/" target="_blank">Database Browser for SQLite</a>. If you use Firefox, you can alternatively use a plug-in called <a href="https://addons.mozilla.org/en-us/firefox/addon/sqlite-manager/" target="_blank">SQLite Manager</a>. 

### Step Four: Accessing the Twitter API

Almost all of my Twitter code grabs data from the Twitter API, which sets up procedures for reliably accessing the Twitter data. Beginning in 2013 Twitter made it more difficult to access its APIs. Now <a href="https://dev.twitter.com/docs/auth/oauth/faq" target="_blank">OAuth authentication</a> is needed for almost everything. This means you need to go on Twitter and create an &#8216;app.&#8217; You won&#8217;t actually use the app for anything &#8212; you just need the password and authentication code. You can <a href="https://dev.twitter.com/apps" target="_blank">create your app here</a>. For more detailed instructions on creating the app take a look at slides 4 through 6 of Wayne Xu&#8217;s (my excellent former PhD student) tutorial <a href="http://www.slideshare.net/cosmopolitanvan/curiosity-bits-tutorial-mining-twitter-user-profile-v2" target="_blank">tutorial</a>.

### Step Five: Start Using the Code

Once you&#8217;ve completed the above four steps you will have all the necessary building blocks for successfully running <a href="http://social-metrics.org/tutorial-list" target="_blank">my Python scripts</a> for downloading and parsing Twitter data. Happy coding! 

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>