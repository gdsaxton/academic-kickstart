---
title: Using Python to Grab Twitter User Data
author: Gregory Saxton
type: post
date: 2014-04-21T04:20:31+00:00
url: /twitter-user-data/
featured_image: /wp-content/uploads/2014/02/1072645_98618032.jpg
dsq_thread_id:
  - 2638871694
tmac_last_id:
  - 435844462871597056
categories:
  - python
  - Twitter
tags:
  - python
  - Twitter

---
[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg" alt="1072645_98618032" width="2340" height="2100" class="alignnone size-full wp-image-49" srcset="http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg 2340w, http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032-300x269.jpg 300w, http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032-1024x918.jpg 1024w" sizes="(max-width: 2340px) 100vw, 2340px" />][1]

I often get requests to explain how I obtained the data I used in a particular piece of academic research. I am always happy to share my code along with my data (and frankly, I think academics who are unwilling to share should be forced to take remedial Kindergarten). The problem is, many of those who would like to use the code don&#8217;t know where to start. There are too many new steps involved for the process to be accessible. So, I&#8217;ll try to walk you through the basic steps here through periodic tutorials. 

To start, Python is a great tool for grabbing data from the Web. Generally speaking, you&#8217;ll get your data by either accessing an API (Application Programming Interface) or by &#8216;scraping&#8217; the data off a webpage. The easiest scenario is when a site makes available an API. Twitter is such a site. Accordingly, as an introductory example I&#8217;ll walk you through the basic steps of using Python to access the Twitter API, read and manipulate the data returned, and save the output.

In any given project I will run a number of different scripts to grab all of the relevant data. We&#8217;ll start with a simple example. This script is designed to grab the  information on a set of Twitter users. First, as stated above, what we&#8217;re doing to get the data is tapping into the <a href="https://dev.twitter.com/start" target="_blank">Twitter API</a>. For our purposes, think of the Twitter API as a set of routines Twitter has set up for allowing us to access specific chunks of data. I use Python for this, given its <a title="Why I Use Python for Academic Research" href="/python-for-academic-research/" target="_blank">many benefits</a>, though any programming language will work. If you are really uninterested in programming and have more limited data needs, you can use <a href="http://social-dynamics.org/twitter-network-data/" target="_blank">NodeXL </a> (if you&#8217;re on a Windows machine) or other services for gathering the data. If you do go the Python route, I highly recommend you install <a href="https://store.continuum.io/cshop/anaconda/" target="_blank">Anaconda Python 2.7</a> &#8212; it&#8217;s free, it works on Mac and PC, and includes most of the add-on packages necessary for scientific computing. In short, you pick a programming language and learn some of it and then develop code that will extract and process the data for you. Even though you can start with my code as a base, it is still useful to understand the basics, so I highly recommend doing some of the many excellent tutorials now available online for learning how to use and run Python. A great place to start is <a href="http://www.codecademy.com/catalog/language/python" target="_blank">Codeacademy</a>.

### Accessing the Twitter API

Almost all of my Twitter code grabs data from the Twitter API. The first step is to determine which part of the Twitter API you&#8217;ll need to access to get the type of data you want &#8212; there are different API methods for accessing information on tweets, retweets, users, following relationships, etc. The code we&#8217;re using here plugs into the users/lookup part of the Twitter API, which allows for the bulk downloading of Twitter user information. You can see a <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank">description of this part of the API here</a>, along with definitions for the <a href="https://dev.twitter.com/docs/platform-objects/users" target="_blank">variables returned</a>. Here is a list of the most useful of the variables returned by the API for each user (modified descriptions taken from the Twitter website): [table id=1 /] &nbsp;</p> 

Second, beginning in 2013 Twitter made it more difficult to access the API. Now <a href="https://dev.twitter.com/docs/auth/oauth/faq" target="_blank">OAuth authentication</a> is needed for almost everything. This means you need to go on Twitter and create an &#8216;app.&#8217; You won&#8217;t actually use the app for anything &#8212; you just need the password and authentication code. You can <a href="https://dev.twitter.com/apps" target="_blank">create your app here</a>. For more detailed instructions on creating the app take a look at this <a href="slideshare-tutorial/" target="_blank">presentation</a>.

Third, as a Python &#8216;wrapper&#8217; around the Twitter API I use <a href="http://twython.readthedocs.org/en/latest/" target="_blank">Twython</a>. This is a package that is an add-on to Python. You will need to install this as well as simplejson (for parsing the JSON data that is returned by the API). Assuming you installed Anaconda Python, the simplest way is to use <a href="http://www.pip-installer.org/en/latest/" target="_blank">pip</a>. On a Mac or Linux machine, you would simply open the Terminal and type _pip install Twython_ and _pip install simplejson. _

The above steps can be a bit of a pain depending on your familiarity with UNIX, but you&#8217;ll only have to do them once. It may take you a while. But once they&#8217;re all set up you won&#8217;t need to do it again.

### Understanding the Code

At the end of this post I&#8217;ll show the entire script. For now, I&#8217;ll go over it in sections. The first line in the code is the <a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank">shebang</a> &#8212; you&#8217;ll find this in all Python code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">#!/usr/bin/env python</pre>

&nbsp;

Lines 3 &#8211; 10 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank">docstring</a> &#8212; also a Python convention. This is a multi-line comment that describes the code. For single-line comments, use the _#_ symbol at the start of the line.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">"""

Use Twitter API to grab user information from list of organizations;
export text file

Uses Twython module to access Twitter API

"""
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

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">ids = "4816,9715012,13023422, 13393052,  14226882,  14235041, 14292458, 14335586, 14730894,\
    15029174, 15474846, 15634728, 15689319, 15782399, 15946841, 16116519, 16148677, 16223542,\
    16315120, 16566133, 16686673, 16801671, 41900627, 42645839, 42731742, 44157002, 44988185,\
    48073289, 48827616, 49702654, 50310311, 50361094,"
</pre>

&nbsp;

Line 39 is where we actually access the API and grab the data. If you&#8217;ve read over the <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank">description of users/lookup API</a>, you know that this method allows you to grab user information on up to 100 Twitter IDs with each API call. 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">users = t.lookup_user(user_id = ids)</pre>

&nbsp;

### Understanding JSON

Now, a key step to this is understanding the data that are returned by the API. As is increasingly common with Web data, this API call returns data in <a href="http://www.json.org/" target="_blank">JSON format</a>. Behind the scenes, Python has grabbed this JSON file, which has data on the 32 Twitter users listed above in the variable _ids_. Each user is an _object_ in the JSON file; objects are delimited by left and right curly braces, as shown here for one of the 32 users:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">{
  "id": 171314974,
  "id_str": "171314974",
  "name": "Global Partnership ",
  "screen_name": "GPforEducation",
  "location": "Washington, DC",
  "url": "http://www.globalpartnership.org",
  "description": "We work with partners in nearly 60 low-income countries to ensure all children go to school and receive a quality education.",
  "protected": false,
  "followers_count": 23712,
  "friends_count": 335,
  "listed_count": 391,
  "created_at": "Tue Jul 27 02:17:01 +0000 2010",
  "favourites_count": 231,
  "utc_offset": -18000,
  "time_zone": "Eastern Time (US & Canada)",
  "geo_enabled": true,
  "verified": true,
  "statuses_count": 4394,
  "lang": "en",
  "contributors_enabled": false,
  "is_translator": false,
  "profile_background_color": "127CB8",
  "profile_background_image_url": "http://a0.twimg.com/profile_background_images/753645368/74e12a386aed1524700a3b1f08c16707.jpeg",
  "profile_background_image_url_https": "https://si0.twimg.com/profile_background_images/753645368/74e12a386aed1524700a3b1f08c16707.jpeg",
  "profile_background_tile": false,
  "profile_image_url": "http://pbs.twimg.com/profile_images/2479080709/g9iii4vpz2ra71c0efuo_normal.jpeg",
  "profile_image_url_https": "https://pbs.twimg.com/profile_images/2479080709/g9iii4vpz2ra71c0efuo_normal.jpeg",
  "profile_banner_url": "https://pbs.twimg.com/profile_banners/171314974/1379613316",
  "profile_link_color": "000000",
  "profile_sidebar_border_color": "FFFFFF",
  "profile_sidebar_fill_color": "FFFFFF",
  "profile_text_color": "4A494A",
  "profile_use_background_image": true,
  "default_profile": false,
  "default_profile_image": false,
  "following": null,
  "follow_request_sent": null,
  "notifications": null
},
</pre>

&nbsp;

JSON output can get messy, so it&#8217;s useful to bookmark a <a href="http://jsonviewer.stack.hu/" target="_blank">JSON viewer</a> for formatting JSON output. What you&#8217;re seeing above is 38 different variables returned by the API &#8212; one for each row &#8212; and arranged in _key: value_ (or _variable: value_) pairs. For instance, the value for the _screen_name_ variable for this user is _GPforEducation_. Now, we do not always want to use all of these variables, so what we&#8217;ll do is pick and label those that are most useful for us. 

So, we first initialize the output file, putting in the day/month/year in the file name, which is useful if you&#8217;re regularly downloading this user information:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">outfn = "twitter_user_data_%i.%i.%i.txt" % (now.month, now.day, now.year)
</pre>

&nbsp;

We then create a variable with the names for the variables (columns) we&#8217;d like to include in our output file, open the output file, and write the header row:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">fields = "id screen_name name created_at url followers_count friends_count statuses_count \
    favourites_count listed_count \
    contributors_enabled description protected location lang expanded_url".split()

outfp = open(outfn, "w")
#outfp.write(string.join(fields, "\t") + "\n")  # header
outfp.write("\t".join(fields) + "\n")  # header
</pre>

&nbsp;

Recall that in line 39 we grabbed the user information on the 32 users and assigned these data to the variable _users_. The final block of code in lines 55-90 loops over each of these IDs (each one a different object in the JSON file), creates the relevant variables, and writes a new row of output. Here&#8217;s the first few rows: 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">for entry in users:
    #CREATE EMPTY DICTIONARY
    r = {}
    for f in fields:
        r[f] = ""
    #ASSIGN VALUE OF 'ID' FIELD IN JSON TO 'ID' FIELD IN OUR DICTIONARY
    r['id'] = entry['id']
    #SAME WITH 'SCREEN_NAME' HERE, AND FOR REST OF THE VARIABLES
    r['screen_name'] = entry['screen_name']
</pre>

&nbsp;

If you compare this code to the raw JSON output shown earlier, what we&#8217;re doing here is creating an empty Python <a href="http://www.tutorialspoint.com/python/python_dictionary.htm" target="_blank">dictionary</a>, which we&#8217;ll call &#8216;r&#8217;, to hold our data for each user, creating variables called _id_ and _screen_name_, and assigning the values held in the _entry[&#8216;id&#8217;]_ and _entry[&#8216;screen_name&#8217;]_ elements of the JSON output to those two respective variables. This is all placed inside a Python <a href="http://www.tutorialspoint.com/python/python_for_loop.htm" target="_blank">for loop</a> &#8212; we could have called &#8216;entry&#8217; anything so long as we&#8217;re consistent.

Now let&#8217;s put the whole thing together. To recap, what this entire script does is to loop over each of the Twitter accounts in the _ids_ variable &#8212; and for each one it will grab its profile information and add that to a row of the output file (a text file that can be imported into Excel, etc.). The filename given to the output file varies according to the date. Now you can download this script, modify the lines noted above, and be on your way to downloading your own Twitter data!



<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/wp-content/uploads/2014/02/1072645_98618032.jpg