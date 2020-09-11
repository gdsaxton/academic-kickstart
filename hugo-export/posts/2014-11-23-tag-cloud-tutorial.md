---
title: Tag Cloud Tutorial
author: Gregory Saxton
type: post
date: 2014-11-23T19:28:34+00:00
url: /tag-cloud-tutorial/
categories:
  - python
  - Twitter
tags:
  - python
  - tutorial
  - Twitter

---
[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg" alt="1072645_98618032" width="2340" height="2100" class="alignnone size-full wp-image-49" srcset="http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg 2340w, http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032-300x269.jpg 300w, http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032-1024x918.jpg 1024w" sizes="(max-width: 2340px) 100vw, 2340px" />][1]

In this post I&#8217;ll provide a brief tutorial on how to create a tag cloud, as seen <a href="http://social-metrics.org/arnova14-tag-cloud/" target="_blank">here</a>.

First, this assumes you have downloaded a set of tweets into an SQLite database. If you are using a different database please modify accordingly. Also, to get to this stage, work through <a href="http://social-metrics.org/tutorial-list/" target="_blank">the first 8 tutorials listed here</a> (you can skip over the seventh tutorial on downloading tweets by a list of users). 

Here is the full code for processing the Twitter data you&#8217;ve downloaded so that you can generate a tag cloud:



Now I&#8217;ll try to walk you through the basic steps here. For those of you who are completely new to Python, you should work through <a href="http://social-metrics.org/tutorial-list/" target="_blank">some of my other tutorials</a>.

### Understanding the Code

The first line in the code above is the <a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank">shebang</a> &#8212; you&#8217;ll find this in all Python code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">#!/usr/bin/env python</pre>

&nbsp;

Lines 3 &#8211; 6 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank">docstring</a> &#8212; also a Python convention. This is a multi-line comment that describes the code. For single-line comments, use the _#_ symbol at the start of the line.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">"""

tags_from_tweets.py - Take hashtags from tweets in SQLite database. 
Output to text file.

"""
</pre>

&nbsp;

Next we&#8217;ll import several Python packages needed to run the code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">import sys
import re
import sqlite3

</pre>

&nbsp;

In lines 14-16 we create a connection with the SQLite database, make a query to select all of the tweets in the database, and assign the returned tweets to the variable _tweets_.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">database = "arnova14.sqlite"
    conn = sqlite3.connect(database)
    c = conn.cursor()
    c.execute('SELECT * FROM search_tweets')  
    tweets = c.fetchall() 
</pre>

&nbsp;

Line 21 creates an empty _dictionary_ in which we will place all of the hashtags from each tweet.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">all_text = []
</pre>

&nbsp;

In lines 23-36 we loop over each tweet. First we identify the two specific columns in the database we&#8217;re interested in (the tweet id and the hashtags column), then add the tags to the _all_text_ variable created earlier.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">for row in tweets:
        id = row[0]
        hashtags = row[31] #the tags   
        if hashtags:       
            tags = hashtags.lower() 
            print tags
        else:
            tags = ''
        tags = re.sub('\n', ' ', tags)
        
        # to remove 'u' before each tweet in the list --&gt; DOESN'T WORK WITH SQLITE INSERTION
        tags = tags.encode("utf-8")                  
            
        all_text.append(tags)     
</pre>

&nbsp;

Finally, in lines 43-46 we translate the _all_text_ variable from a dictionary to a string, then output it to a text file. 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">all_hashtags = ' '.join(all_text)
    out=file('all_text_HASHTAGS.txt','w')
    out.write(all_hashtags)    
</pre>

&nbsp;

Once you&#8217;ve got this text file, open it, copy all of the text, and use it to create your own word cloud on <a href="http://www.wordle.net/" target="_blank">Wordle</a>.

I hope this helps. If you need help with actually getting the tweets into your database, take a look at some of the <a href="http://social-metrics.org/tutorial-list/" target="_blank">other tutorials</a> I&#8217;ve posted. If you have any questions, let me know, and have fun with the data!

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg