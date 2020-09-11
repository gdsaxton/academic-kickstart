---
title: Why I Use Python for Academic Research
author: Gregory Saxton
type: post
date: 2014-04-24T11:24:04+00:00
url: /python-for-academic-research/
featured_image: /wp-content/uploads/2014/02/1206711_41147487.jpg
dsq_thread_id:
  - 2638869953
categories:
  - Featured
  - python
  - research
tags:
  - academic research
  - python

---
[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/02/1206711_41147487.jpg" alt="1206711_41147487" width="3877" height="2728" class="alignnone size-full wp-image-50" srcset="http://social-metrics.org/wp-content/uploads/2014/02/1206711_41147487.jpg 3877w, http://social-metrics.org/wp-content/uploads/2014/02/1206711_41147487-300x211.jpg 300w, http://social-metrics.org/wp-content/uploads/2014/02/1206711_41147487-1024x720.jpg 1024w" sizes="(max-width: 3877px) 100vw, 3877px" />][1]

Academics and other researchers have to choose from a variety of research skills. Most social scientists do not add computer programming into their skill set. As a strong proponent of the value of learning a programming language, I will lay out how this has proven to be useful for me. A budding programmer could choose from a number of good options &#8212; including perl, C++, Java, PHP, or others &#8212; but Python has a reputation as being one of the most accessible and intuitive. I obviously like it.

No matter your choice of language, there are variety of ways learning programming will be useful for social scientists and other data scientists. The most important areas are _data gathering, data manipulation,_ and _data visualization_ _and analysis__._

**Data Gathering**

<span style="line-height: 1.5em;">When I started learning Python four years ago, I kept a catalogue of the various scripts I wrote. Going over these scripts, I have personally written Python code to gather the following data:</span>

  * Download lender and borrower information for thousands of donation transactions on _kiva.org._
  * Download tweets from a list of 100 large nonprofit organizations.
  * Download Twitter profile information from a 150 advocacy nonprofits.
  * Scrape the &#8216;Walls&#8217; from 65 organizations&#8217; Facebook accounts.
  * Download @messages sent to 38 community foundations.
  * Traverse and download html files for thousands of webpages on large accounting firms&#8217; websites.
  * Scrape data from 1,000s of organizational profiles on a charity rating site.
  * <span style="line-height: 1.5em;">Scrape data from several thousand organizations raising money on the crowdfunding site </span><em style="line-height: 1.5em;">Indiegogo.</em>
  * __Download hundreds of _YouTube _videos used in _Indiegogo_ fundraising campaigns.
  * Gather data available through the _InfoChimps _API.
  * Scrape pinning and re-pinning data from health care organizations&#8217; _Pinterest_ accounts.
  * Tap into the Facebook Graph API to download status updates and number of likes, comments and shares for 100 charities.

This is just a sample. The point is that you can use a programming language like Python to get just about any data from the Web. When the website or social media platform makes available an API (application programming interface), accessing the data is easy. Twitter is fantastic for this very reason. In other cases &#8212; including most websites &#8212; you will have to _scrape_ the data through creative use of programming. Either way, you can gain access to valuable data.

There&#8217;s no need to be an expert to obtain real-world benefits from programming. I started learning Python four years ago (I now consider myself an intermediate-level programmer) and gained substantive benefits right from the start.

**Data **Manipulation****

Budding researchers often seem to under-estimate how much time they will be spending on manipulating, reshaping, and processing their data. Python excels at data munging. I have recently used Python code to

  * Loop over hundreds of thousands of tweets and modify characters, convert date formats, etc.
  * Identify and delete duplicate entries in an SQL database.
  * Loop over 74 nonprofit organizations&#8217; Twitter friend-follower lists to create a 74 x 74 friendship network.
  * Read in and write text and CSV data.
  * Countless grouping, merging, and aggregation functions.
  * <span style="line-height: 1.5em;">Automatically count the number of &#8220;negative&#8221; words in thousands of online donation appeals.</span>
  * Loop over hundreds of thousands of tweets to create an _edge list_ for a retweet network.
  * Compute word counts for a word-document matrix from thousands of crowdfunding appeals.
  * <span style="line-height: 1.5em;">Create text files combining all of an organizations&#8217; tweets for use in creating word clouds.</span>
  * Download images included in a set of tweets.
  * <span style="line-height: 1.5em;">Merging text files.</span>
  * Count number of Facebook statuses per organization.
  * Loop over hundreds of thousands of rows of tweets in an _SQLite _database and create additional variables for future analysis.
  * Dealing with missing data.
  * Creating dummy variables.
  * Find the oldest entry for each organization in a Twitter database.
  * Use _p__andas_ (Python Data Analysis Library) to aggregate Twitter data to the daily, weekly, and monthly level.
  * Create a text file of all hashtags in a Twitter database.

<strong style="line-height: 1.5em;">Data Visualization and <strong>Analysis</strong></strong>

With the proliferation of scientific computing modules such as _p__andas_ and _statsmodels _and _scikit-learn,_ Python&#8217;s data analysis capabilities have gotten much more powerful over the past few years. With such tools Python can now compete in many areas with devoted statistical programs such as _R _or _Stata,_ which I have traditionally used for most of my data analysis and visualization. Lately I&#8217;m doing more and more of this work directly in Python. Here are some of the analyses I have run recently using Python:

  * Implement a <span style="line-height: 1.5em;">naive Bayesian classifier to classify the sentiment in hundreds of thousands of tweets.</span>
  * Linguistic analysis of donation appeals and tweets using Python&#8217;s _Natural Language Tool Kit._
  * Create plots of number of tweets, retweets, and public reply messages per day, week, and month.
  * Run descriptive statistics and multiple regressions.

<pre><strong style="line-height: 1.5em;"><strong></strong></strong></pre>

<span style="line-height: 1.5em;"><b>Summary</b></span>

<span style="line-height: 1.5em;">Learning a programming language is a challenge. Of that there is little doubt. Yet the payoff in improved productivity alone can be substantial. Add to that the powerful analytical and data visualization capabilities that open up to the researcher who is skilled in a programming language. Lastly, leaving aside the buzzword &#8220;Big Data,&#8221; programming opens up a world of new data found on websites, social media platforms, and online data repositories. I would thus go so far as to say that any researcher interested in social media is doing themselves a great disservice by not learning some programming. For this very reason, one of my goals on this site is to provide guidance to those who are interested in getting up and running on Python for conducting academic and social media research.</span>

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/wp-content/uploads/2014/02/1206711_41147487.jpg