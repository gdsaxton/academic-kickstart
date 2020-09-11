---
title: APIs and Big Data
author: Gregory Saxton
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1408
categories:
  - Big Data
  - python
  - research
  - Twitter
tags:
  - academic research
  - Big Data
  - python
  - social media
  - Twitter

---
[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg" alt="Big Data" width="1024" height="500" class="alignnone size-full wp-image-1327" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg 1024w, http://social-metrics.org/wp-content/uploads/2015/05/Big-Data-300x146.jpg 300w" sizes="(max-width: 1024px) 100vw, 1024px" />][1]

So you want to download &#8220;Big Data.&#8221; You could be a social scientist wanting to take your first stab at downloading and analyzing 100 organizations&#8217; worth of tweets. Or a marketing or public relations practitioner interested in analyzing Facebook or Instagram or Pinterest YouTube activity by your competitors. Or a budding data scientist interested in getting your toes wet and doing your first Big Data download.

This post is the first in a series designed to help you understand at a conceptual level the main moving parts you&#8217;ll have to grasp in order to successfully get the data you need. This one deals with _levels of analysis_ in Big Data. It is critical to have a basic understanding of this concept if you are to understand how to correctly get the data you need.

So you want to download &#8220;Big Data.&#8221; You could be a social scientist wanting to take your first stab at downloading and analyzing 100 organizations&#8217; worth of tweets. Or a marketing or public relations practitioner interested in analyzing Facebook or Instagram or Pinterest activity by your competitors. Or a budding data scientist interested in getting your toes wet and doing your first Big Data download.

This post is here to help you understand at a conceptual level the main moving parts you&#8217;ll have to grasp in order to successfully get the data you need. There are five basic elements:

  1. <a href="http://social-metrics.org/levels-of-analysis-in-big-data/" title="Levels of Analysis in Big Data" target="_blank" rel="noopener noreferrer">Level of Analysis</a>
  2. API
  3. Data Format
  4. Programming Language
  5. Database

### Introduction: What is an API

In line with what I&#8217;ve noted earlier, you can access all of the above account-level data through a specific portion of the Twitter application programming interface (API). 

Think of Twitter (for instance) having a number of different datasets on each organization &#8212; one for user data, one for tweet data, and one for friend and follower data. In each dataset are a number of different variables. The API tells you how to access each dataset, and then what the variable names and descriptions are. 

### What is a Level of Analysis?

In the abstract, the term _level of analysis_ refers to the scale of your research project. More concretely, it refers to the level at which your analyses are conducted. For instance, a political scientist would generally conduct research at one of three levels of analysis: the individual, the state, or the system. A communication scholar, in turn, might study, among others, the individual, the message, or the conversation. And a finance scholar might study the trader, the firm, the transaction, the security, the stock exchange, or the country. 

&#8216;Big Data&#8217; can derive from many sources, but for the purposes of this post I&#8217;m assuming you&#8217;re interested in capturing some form of social media data &#8212; such as Tumblr, Twitter, Facebook, Pinterest, or Instagram. What is important to realize is that on all social media sites there are three fundamental levels of analysis &#8212; the _account_, the _message_, and the _connections_ &#8212; and that these correspond to the three basic building blocks of social media engagement. Importantly, the social media sites generally allow you (with limits) to access their data, and the data are organized according to the level of analysis.

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Screen-Shot-2015-05-25-at-8.39.11-PM.png" alt="Screen Shot 2015-05-25 at 8.39.11 PM" width="1426" height="934" class="alignnone size-full wp-image-1394" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Screen-Shot-2015-05-25-at-8.39.11-PM.png 1426w, http://social-metrics.org/wp-content/uploads/2015/05/Screen-Shot-2015-05-25-at-8.39.11-PM-300x196.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Screen-Shot-2015-05-25-at-8.39.11-PM-1024x670.png 1024w" sizes="(max-width: 1426px) 100vw, 1426px" />][2]

To demonstrate these ideas I will use the example of the Community Foundation for Greater Buffalo&#8217;s Twitter page.

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level.png" alt="Twitter - CFGB (account-level)" width="2850" height="1586" class="alignnone size-full wp-image-1349" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level.png 2850w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level-300x166.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level-1024x569.png 1024w" sizes="(max-width: 2850px) 100vw, 2850px" />][3]

### Level One: The Account Level

The first level is the _account_ level. Take a look at the screenshot below. As I&#8217;ve indicated on the image, there are a variety of account-level data &#8212; the images the organization has uploaded, its description, its location, its website address, and the date it joined Twitter. You can also see how many tweets it has sent to date (194), how many other Twitter users it follows (220), how many other users are following the organization (1,526), and how many tweets the organization has &#8216;favorited&#8217; or archived (93). All of these data are at the **_account_** level of analysis. They are, effectively, characteristics of the organization&#8217;s account at a snapshot in time. 

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_account-level.png" alt="Twitter_-_CFGB_-_account-level" width="2850" height="1586" class="alignnone size-full wp-image-1376" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_account-level.png 2850w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_account-level-300x166.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_account-level-1024x569.png 1024w" sizes="(max-width: 2850px) 100vw, 2850px" />][4]

If we are being strict with social scientific language, we would say that the account is the _unit of observation_ for our data here. But we can save the distinction between unit of observation and unit/level of analysis for a future post. For now, the key takeaway is to understand that these account-level data are at a higher level than the tweet, or friendship, or conversation level. They are characteristics of the organization &#8212; or more specifically, the organization&#8217;s Twitter account. 

In line with what I&#8217;ve noted earlier, you can access all of the above account-level data through a specific portion of the Twitter application programming interface (API). Specifically, the _users/lookup_ part of the Twitter API allows for the bulk downloading of Twitter user information. You can see a <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank" rel="noopener noreferrer">description of this part of the API here</a>, along with definitions for the <a href="https://dev.twitter.com/docs/platform-objects/users" target="_blank" rel="noopener noreferrer">variables returned</a>. For an overview of how to gather such data, take a look at <a href="http://social-metrics.org/twitter-user-data/" target="_blank" rel="noopener noreferrer">this tutorial</a> I&#8217;ve written.

There are good reasons why you would want to gather these data. For instance, you might want to track how many followers an organization has over time. In all of my studies using Twitter data I always start the data-gathering process by downloading these account-level data. But you should note that the account-level data are typically the least interesting. It is at this level that we see what I refer to as the static _architecture_ of an organization&#8217;s engagement efforts on social media (see the first figure in this post). Think of this as the venue in which customer or stakeholder engagement can take place. On Twitter, the ability to modify the architecture is limited: the organization can add pictures, write a compelling description, and include a link to other social media accounts, but it cannot change the nature of any interactions that take place &#8212; those are hard-coded into the Twitter platform. Other social media sites allow for more customizable architecture. For instance, Facebook allows page administrators to change options for fan commenting while allowing greater customizability in the static architecture via apps. 

### Level Two: The Messages

The second is the _message_ level. Here is where we really get to the heart of the social media data. No matter the social media platform, the heart of an organization&#8217;s engagement efforts occurs not through static architectural elements but through dynamic engagement efforts &#8212; through the day-to-day messages the organization sends and the daily connecting actions it takes. The _messages_ are the heart of any social media platform, though they go by different names according to the platform. On Twitter, they are tweets. On Facebook, it&#8217;s statuses. On YouTube, videos. On Pinterest, it&#8217;s pins. On Instagram, it&#8217;s photos. Despite the different names, the point is that at their core all social media platforms stress _dynamic communication_, as manifested in the discrete visual or textual messages an organization sends to its followers. 

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_message-level.png" alt="Twitter_-_CFGB_-_message-level" width="2850" height="1586" class="alignnone size-full wp-image-1370" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_message-level.png 2850w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_message-level-300x166.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_message-level-1024x569.png 1024w" sizes="(max-width: 2850px) 100vw, 2850px" />][5]

Take a look at the above screenshot. You&#8217;ll see I&#8217;ve indicated the _message-level data_. These are the tweets. Through accessing Twitter&#8217;s _user_timeline_ API, you can access all of the information seen in the screenshot &#8212; the full text of the tweet, whether it was a retweet, how many times the tweet has been retweeted and favorited, links to included photos, etc. In almost any Twitter study you will want to gather these data. And fortunately, you can generally acquire the last 3,200 tweets sent by a Twitter user. If you have 100 organizations in your sample, this means you could easily &#8212; in a single day &#8212; build a database with 320,000 tweets. 

### Level Three: The Connections

Finally, there is the _connections_ level. You can&#8217;t see these immediately on the Community Foundation&#8217;s Twitter page, but by clicking on &#8216;Following&#8217; or &#8216;Followers&#8217; you can get details on the other users the organization is following or followed by, respectively.

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections1.png" alt="Twitter - CFGB (connections1)" width="2850" height="1586" class="alignnone size-full wp-image-1371" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections1.png 2850w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections1-300x166.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections1-1024x569.png 1024w" sizes="(max-width: 2850px) 100vw, 2850px" />][6]

For instance, clicking on &#8216;Following&#8217; you will get what is shown in the screenshot below. Here you&#8217;ll see the first six Twitter users that the Community Foundation for Greater Buffalo follows. After the messages (tweets), this is the second most-important set of data &#8212; once again, here we can see the results of the organization&#8217;s dynamic engagement efforts &#8212; the formal social network connections it is making with other Twitter users. 

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections.png" alt="Twitter - CFGB (connections)" width="2842" height="1616" class="alignnone size-full wp-image-1348" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections.png 2842w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-300x170.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-1024x582.png 1024w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-332x190.png 332w" sizes="(max-width: 2842px) 100vw, 2842px" />][7]

As with the account-level and message-level data, these data are also available for download. To get a list of users the organization follows, access Twitter&#8217;s _GET friends/ids_ API, while to get a list of users that follow the organization, access the _GET followers/ids_ API. This is where you would go to get the data for a social network analysis of a sample of organizations&#8217; friend and follower networks. Future tutorials will cover how to do this. 

### Summary

Here are the two key takeaways. One, I hope you now understand that all social media sites have three fundamental elements that individuals or organizations can employ to engage with their audience: 1) static architecture, 2) discrete messages, and 3) discrete connecting actions. The first is interesting and necessary but not terribly important for most research projects. The latter two reflect an organization&#8217;s attempts at _dynamic_ engagement with its audience. These two levels are also the building blocks for aggregating to higher levels of analysis &#8212; notably, using tweet-level data to conduct _conversation-level_ analyses or using connection-level data to conduct _network-level_ analyses. I&#8217;ll cover those in future posts.

Two, Twitter &#8212; as with other social media sites &#8212; organizes and grants access to its data through series of APIs that roughly conform to the levels of analysis covered above. What I hope to have conveyed here is that to get the data you need, you first have to understand this essential differentiation of the data. Understanding the different levels of analysis is the first step to understanding the nature of social media data. 

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg" alt="Big Data" width="1024" height="500" class="alignnone size-full wp-image-1327" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg 1024w, http://social-metrics.org/wp-content/uploads/2015/05/Big-Data-300x146.jpg 300w" sizes="(max-width: 1024px) 100vw, 1024px" />][1]

So you want to download &#8220;Big Data.&#8221; You could be a social scientist wanting to take your first stab at downloading and analyzing 100 organizations&#8217; worth of tweets. Or a marketing or public relations practitioner interested in analyzing Facebook or Instagram or Pinterest activity by your competitors. Or a budding data scientist interested in getting your toes wet and doing your first Big Data download.

This post is here to help you understand at a conceptual level the main moving parts you&#8217;ll have to grasp in order to successfully get the data you need. There are five basic elements:

  1. Level of Analysis
  2. API
  3. Data Format
  4. Programming Language
  5. Database

### Level of Analysis

The first level is the _account_ level. The second is the _message_ level.

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level.png" alt="Twitter - CFGB (account-level)" width="2850" height="1586" class="alignnone size-full wp-image-1349" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level.png 2850w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level-300x166.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level-1024x569.png 1024w" sizes="(max-width: 2850px) 100vw, 2850px" />][3]

Finally, there is the _connections_ level.

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections.png" alt="Twitter - CFGB (connections)" width="2842" height="1616" class="alignnone size-full wp-image-1348" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections.png 2842w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-300x170.png 300w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-1024x582.png 1024w, http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections-332x190.png 332w" sizes="(max-width: 2842px) 100vw, 2842px" />][7]

### Overview &#8212; Miscellaneous 

To start, Python is a great tool for grabbing data from the Web. Generally speaking, you&#8217;ll get your data by either accessing an API (Application Programming Interface) or by &#8216;scraping&#8217; the data off a webpage. The easiest scenario is when a site makes available an API. Twitter is such a site. Accordingly, as an introductory example I&#8217;ll walk you through the basic steps of using Python to access the Twitter API, read and manipulate the data returned, and save the output.

In any given project I will run a number of different scripts to grab all of the relevant data. We&#8217;ll start with a simple example. This script is designed to grab the  information on a set of Twitter users. First, as stated above, what we&#8217;re doing to get the data is tapping into the <a href="https://dev.twitter.com/start" target="_blank" rel="noopener noreferrer">Twitter API</a>. For our purposes, think of the Twitter API as a set of routines Twitter has set up for allowing us to access specific chunks of data. I use Python for this, given its <a title="Why I Use Python for Academic Research" href="/python-for-academic-research/" target="_blank" rel="noopener noreferrer">many benefits</a>, though any programming language will work. If you are really uninterested in programming and have more limited data needs, you can use <a href="http://social-dynamics.org/twitter-network-data/" target="_blank" rel="noopener noreferrer">NodeXL </a> (if you&#8217;re on a Windows machine) or other services for gathering the data. If you do go the Python route, I highly recommend you install <a href="https://store.continuum.io/cshop/anaconda/" target="_blank" rel="noopener noreferrer">Anaconda Python 2.7</a> &#8212; it&#8217;s free, it works on Mac and PC, and includes most of the add-on packages necessary for scientific computing. In short, you pick a programming language and learn some of it and then develop code that will extract and process the data for you. Even though you can start with my code as a base, it is still useful to understand the basics, so I highly recommend doing some of the many excellent tutorials now available online for learning how to use and run Python. A great place to start is <a href="http://www.codecademy.com/tracks/python" target="_blank" rel="noopener noreferrer">Codeacademy</a>.

### ADDED IN &#8212; ACCESSING TWITTER API

Almost all of my Twitter code grabs data from the Twitter API, which sets up procedures for reliably accessing the Twitter data. Beginning in 2013 Twitter made it more difficult to access its APIs. Now <a href="https://dev.twitter.com/docs/auth/oauth/faq" target="_blank" rel="noopener noreferrer">OAuth authentication</a> is needed for almost everything. This means you need to go on Twitter and create an &#8216;app.&#8217; You won&#8217;t actually use the app for anything &#8212; you just need the password and authentication code. You can <a href="https://dev.twitter.com/apps" target="_blank" rel="noopener noreferrer">create your app here</a>. For more detailed instructions on creating the app take a look at slides 4 through 6 of Wayne Xu&#8217;s (my excellent PhD student) tutorial <a href="http://curiositybits.com/python-for-mining-the-social-web/python-tutorial-mining-twitter-user-profile/" target="_blank" rel="noopener noreferrer">tutorial</a>.

### Accessing the Twitter API

Almost all of my Twitter code grabs data from the Twitter API. The first step is to determine which part of the Twitter API you&#8217;ll need to access to get the type of data you want &#8212; there are different API methods for accessing information on tweets, retweets, users, following relationships, etc. The code we&#8217;re using here plugs into the users/lookup part of the Twitter API, which allows for the bulk downloading of Twitter user information. You can see a <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank" rel="noopener noreferrer">description of this part of the API here</a>, along with definitions for the <a href="https://dev.twitter.com/docs/platform-objects/users" target="_blank" rel="noopener noreferrer">variables returned</a>. Here is a list of the most useful of the variables returned by the API for each user (modified descriptions taken from the Twitter website): [table id=1 /] &nbsp;</p> 

Second, beginning in 2013 Twitter made it more difficult to access the API. Now <a href="https://dev.twitter.com/docs/auth/oauth/faq" target="_blank" rel="noopener noreferrer">OAuth authentication</a> is needed for almost everything. This means you need to go on Twitter and create an &#8216;app.&#8217; You won&#8217;t actually use the app for anything &#8212; you just need the password and authentication code. You can <a href="https://dev.twitter.com/apps" target="_blank" rel="noopener noreferrer">create your app here</a>. For more detailed instructions on creating the app take a look at this <a href="slideshare-tutorial/" target="_blank" rel="noopener noreferrer">presentation</a>.

Third, as a Python &#8216;wrapper&#8217; around the Twitter API I use <a href="http://twython.readthedocs.org/en/latest/" target="_blank" rel="noopener noreferrer">Twython</a>. This is a package that is an add-on to Python. You will need to install this as well as simplejson (for parsing the JSON data that is returned by the API). Assuming you installed Anaconda Python, the simplest way is to use <a href="http://www.pip-installer.org/en/latest/" target="_blank" rel="noopener noreferrer">pip</a>. On a Mac or Linux machine, you would simply open the Terminal and type _pip install Twython_ and _pip install simplejson. _

The above steps can be a bit of a pain depending on your familiarity with UNIX, but you&#8217;ll only have to do them once. It may take you a while. But once they&#8217;re all set up you won&#8217;t need to do it again.

### Understanding the Code

At the end of this post I&#8217;ll show the entire script. For now, I&#8217;ll go over it in sections. The first line in the code is the <a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank" rel="noopener noreferrer">shebang</a> &#8212; you&#8217;ll find this in all Python code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">#!/usr/bin/env python</pre>

&nbsp;

Lines 3 &#8211; 10 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank" rel="noopener noreferrer">docstring</a> &#8212; also a Python convention. This is a multi-line comment that describes the code. For single-line comments, use the _#_ symbol at the start of the line.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">&quot;&quot;&quot;

Use Twitter API to grab user information from list of organizations;
export text file

Uses Twython module to access Twitter API

&quot;&quot;&quot;
</pre>

&nbsp;

Next we&#8217;ll import several Python packages needed to run the code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">import sys
import string
import simplejson
from twython import Twython
</pre>

&nbsp;

In lines 18-22 we will create day, month, and year variables to be used for naming the output file.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">import datetime
now = datetime.datetime.now()
day=int(now.day)
month=int(now.month)
year=int(now.year)
</pre>

&nbsp;

### Modify the Code

There are two areas you&#8217;ll need to modify. First, you&#8217;ll need to add your OAuth tokens to lines 26-30. 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">t = Twython(app_key='APP_KEY', #REPLACE 'APP_KEY' WITH YOUR APP KEY, ETC., IN THE NEXT 4 LINES
    app_secret='APP_SECRET',
    oauth_token='OAUTH_TOKEN',
    oauth_token_secret='OAUTH_TOKEN_SECRET')
</pre>

&nbsp;

Second, you&#8217;ll need to modify lines 32-35 with the ids from your set of Twitter users. If you don&#8217;t have user\_ids for these, you can use screen\_names and change line 39 to &#8216;screen_name = ids&#8217;

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">ids = &quot;4816,9715012,13023422, 13393052,  14226882,  14235041, 14292458, 14335586, 14730894,
    15029174, 15474846, 15634728, 15689319, 15782399, 15946841, 16116519, 16148677, 16223542,
    16315120, 16566133, 16686673, 16801671, 41900627, 42645839, 42731742, 44157002, 44988185,
    48073289, 48827616, 49702654, 50310311, 50361094,&quot;
</pre>

&nbsp;

Line 39 is where we actually access the API and grab the data. If you&#8217;ve read over the <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank" rel="noopener noreferrer">description of users/lookup API</a>, you know that this method allows you to grab user information on up to 100 Twitter IDs with each API call. 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">users = t.lookup_user(user_id = ids)</pre>

&nbsp;

### Understanding JSON

Now, a key step to this is understanding the data that are returned by the API. As is increasingly common with Web data, this API call returns data in <a href="http://www.json.org/" target="_blank" rel="noopener noreferrer">JSON format</a>. Behind the scenes, Python has grabbed this JSON file, which has data on the 32 Twitter users listed above in the variable _ids_. Each user is an _object_ in the JSON file; objects are delimited by left and right curly braces, as shown here for one of the 32 users:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">{
  'id': 171314974,
  'id_str': '171314974',
  'name': 'Global Partnership ',
  'screen_name': 'GPforEducation',
  'location': 'Washington, DC',
  'url': 'http://www.globalpartnership.org',
  'description': 'We work with partners in nearly 60 low-income countries to ensure all children go to school and receive a quality education.',
  'protected': false,
  'followers_count': 23712,
  'friends_count': 335,
  'listed_count': 391,
  'created_at': 'Tue Jul 27 02:17:01 +0000 2010',
  'favourites_count': 231,
  'utc_offset': -18000,
  'time_zone': 'Eastern Time (US &amp; Canada)',
  'geo_enabled': true,
  'verified': true,
  'statuses_count': 4394,
  'lang': 'en',
  'contributors_enabled': false,
  'is_translator': false,
  'profile_background_color': '127CB8',
  'profile_background_image_url': 'http://a0.twimg.com/profile_background_images/753645368/74e12a386aed1524700a3b1f08c16707.jpeg',
  'profile_background_image_url_https': 'https://si0.twimg.com/profile_background_images/753645368/74e12a386aed1524700a3b1f08c16707.jpeg',
  'profile_background_tile': false,
  'profile_image_url': 'http://pbs.twimg.com/profile_images/2479080709/g9iii4vpz2ra71c0efuo_normal.jpeg',
  'profile_image_url_https': 'https://pbs.twimg.com/profile_images/2479080709/g9iii4vpz2ra71c0efuo_normal.jpeg',
  'profile_banner_url': 'https://pbs.twimg.com/profile_banners/171314974/1379613316',
  'profile_link_color': '000000',
  'profile_sidebar_border_color': 'FFFFFF',
  'profile_sidebar_fill_color': 'FFFFFF',
  'profile_text_color': '4A494A',
  'profile_use_background_image': true,
  'default_profile': false,
  'default_profile_image': false,
  'following': null,
  'follow_request_sent': null,
  'notifications': null
},
</pre>

&nbsp;

JSON output can get messy, so it&#8217;s useful to bookmark a <a href="http://jsonviewer.stack.hu/" target="_blank" rel="noopener noreferrer">JSON viewer</a> for formatting JSON output. What you&#8217;re seeing above is 38 different variables returned by the API &#8212; one for each row &#8212; and arranged in _key: value_ (or _variable: value_) pairs. For instance, the value for the _screen_name_ variable for this user is _GPforEducation_. Now, we do not always want to use all of these variables, so what we&#8217;ll do is pick and label those that are most useful for us. 

So, we first initialize the output file, putting in the day/month/year in the file name, which is useful if you&#8217;re regularly downloading this user information:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">outfn = 'twitter_user_data_%i.%i.%i.txt' % (now.month, now.day, now.year)
</pre>

&nbsp;

We then create a variable with the names for the variables (columns) we&#8217;d like to include in our output file, open the output file, and write the header row:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">fields = 'id screen_name name created_at url followers_count friends_count statuses_count 
    favourites_count listed_count contributors_enabled description protected location lang expanded_url'.split()

outfp = open(outfn, 'w')
outfp.write(string.join(fields, 't') + 'n')  # header
</pre>

&nbsp;

Recall that in line 39 we grabbed the user information on the 32 users and assigned these data to the variable _users_. The final block of code in lines 55-90 loops over each of these IDs (each one a different object in the JSON file), creates the relevant variables, and writes a new row of output. Here&#8217;s the first few rows: 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">for entry in users:
    #CREATE EMPTY DICTIONARY
    r = {}
    for f in fields:
        r[f] = ''
    #ASSIGN VALUE OF 'ID' FIELD IN JSON TO 'ID' FIELD IN OUR DICTIONARY
    r['id'] = entry['id']
    #SAME WITH 'SCREEN_NAME' HERE, AND FOR REST OF THE VARIABLES
    r['screen_name'] = entry['screen_name']
</pre>

&nbsp;

If you compare this code to the raw JSON output shown earlier, what we&#8217;re doing here is creating an empty Python <a href="http://www.tutorialspoint.com/python/python_dictionary.htm" target="_blank" rel="noopener noreferrer">dictionary</a>, which we&#8217;ll call &#8216;r&#8217;, to hold our data for each user, creating variables called _id_ and _screen_name_, and assigning the values held in the _entry[&#8216;id&#8217;]_ and _entry[&#8216;screen_name&#8217;]_ elements of the JSON output to those two respective variables. This is all placed inside a Python <a href="http://www.tutorialspoint.com/python/python_for_loop.htm" target="_blank" rel="noopener noreferrer">for loop</a> &#8212; we could have called &#8216;entry&#8217; anything so long as we&#8217;re consistent.

Now let&#8217;s put the whole thing together. To recap, what this entire script does is to loop over each of the Twitter accounts in the _ids_ variable &#8212; and for each one it will grab its profile information and add that to a row of the output file (a text file that can be imported into Excel, etc.). The filename given to the output file varies according to the date. Now you can download this script, modify the lines noted above, and be on your way to downloading your own Twitter data!

<div class="embedpress-wrapper ose-githubgist ose-uid-d5c39cb4261bdc2e48645ced3c068d0b responsive">
</div>

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg
 [2]: http://social-metrics.org/wp-content/uploads/2015/05/Screen-Shot-2015-05-25-at-8.39.11-PM.png
 [3]: http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-account-level.png
 [4]: http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_account-level.png
 [5]: http://social-metrics.org/wp-content/uploads/2015/05/Twitter_-_CFGB_-_message-level.png
 [6]: http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections1.png
 [7]: http://social-metrics.org/wp-content/uploads/2015/05/Twitter-CFGB-connections.png