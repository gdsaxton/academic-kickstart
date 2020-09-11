---
title: Downloading Tweets – Take II
author: Gregory Saxton
type: post
date: 2017-09-25T18:36:13+00:00
url: /downloading-tweets-by-a-list-of-users-take2/
featured_image: /wp-content/uploads/2015/05/16140423092_0638bfe844_o.jpg
dsq_thread_id:
  - 6565774873
categories:
  - Big Data
  - python
  - Twitter
tags:
  - Big Data
  - Database
  - Programming
  - python
  - social media
  - socialmedia
  - tutorial
  - Twitter

---
The goal of this post is to walk you through a Python script designed to download tweets by a set of Twitter users and insert them into an SQLite database. 

In a <a href="http://social-metrics.org/downloading-tweets-by-a-list-of-users/" target="_blank">previous post</a> I supplied a brief, temporary attempt at providing an overview of how to download tweets sent by a list of Twitter users &#8212; but I ended the post by pointing pointing people to a good <a href="http://www.curiositybits.com/new-page-3/" target="_blank">tutorial written by my former PhD student and now co-author Wayne Xu</a>.

Now I am finally getting around to posting my own tutorial on how to download tweets sent by a list of different Twitter users. It is directed at those who are new to Python and/or downloading data from the Twitter API. We will be using Python to download the tweets and will be inserting the tweets into an SQLite database. This code will allow you to download up to the latest 3,200 tweets sent by each Twitter user. I will not go over the script line-by-line but will instead attempt to provide you a &#8216;high-level&#8217; understanding of what we are doing &#8212; just enough so that you can run the script successfully yourself.

Before running this script, you will need to:

  * Have Anaconda Python 2.7 installed
  * Have your Twitter API details handy
  * Have created a CSV file (e.g., in Excel) containing the Twitter handles you wish to download. Below is a sample you can download and use for this tutorial. Name it _accounts.csv_ and place it in the same directory as the Python script.

<div class="embedpress-wrapper ose-github ose-uid-02b2d1b70a78194561645865a5d6c0d0 responsive">
</div>

If you are completely new to Python and the Twitter API, you should first make your way through the following tutorials, which will help you get set up and working with Python:

  * <a href="http://social-metrics.org/python-where-to-start/" target="_blank">Which version of Python to download</a>
  * <a href="http://social-metrics.org/starting-on-python-1/" target="_blank">Running your first code</a>
  * <a href="http://social-metrics.org/starting-on-python-2/" target="_blank">Four ways to run your code</a>
  * <a href="http://social-metrics.org/api-keys/" target="_blank">Setting up access to the Twitter API</a>

Another detailed tutorial I have created, <a href="http://social-metrics.org/python-tutorial-1/" target="_blank">Python Code Tutorial</a>, is intended to serve as an introduction to how to access the Twitter API and then read the JSON data that is returned. It will be helpful for understanding what we&#8217;re doing in this script.

At the end of this post I&#8217;ll show the entire script. For now, I&#8217;ll go over it in sections. The code is divided into six parts:

### Part I: Overview and Importing Necessary Python Packages

The first line in the code is the <a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank">shebang</a> &#8212; you&#8217;ll find this in all Python code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">#!/usr/bin/env python</pre>

&nbsp;

Lines 4 &#8211; 24 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank">docstring</a> &#8212; also a Python convention. This is a multi-line comment that describes the code. For single-line comments, use the _#_ symbol at the start of the line.

<pre class="brush: python; first-line: 4; light: false; title: ; toolbar: true; notranslate" title="">"""
Social_Metrics_Tutorial_Script_User_Timeline_All_Pages.py - DOWNLOADS ALL AVAILABLE RECENT
TWEETS FROM 5 MLB ACCOUNTS INTO SQLITE DATABASE

BEFORE RUNNING THIS SCRIPT, YOU WILL NEED TO:
  1. HAVE ANACONDA PYTHON 2.7 INSTALLED
  2. HAVE CREATED CSV FILE (E.G., IN EXCEL) CONTAINING TWITTER HANDLES YOU 
     WISH TO DOWNLOAD (SEE TUTORIAL FOR DETAILS)


THE CODE IS DIVIDED INTO SIX PARTS:
  1. Importing necessary Python packages 
  2. Importing Twython and Twitter app key and access token
       - YOU NEED TO MODIFY THIS SECTION IN ORDER TO GET SCRIPT TO WORK (LINES 53-54)
  3. Defining function for getting Twitter data
  4. Set up columns for database to allow use of SQLAlchemy
  5. Writing function for parsing data returned by Twitter API/creating variables to store
  6. Main loop over each of the Twitter handles in the accounts table of the database.  
       - YOU CAN MODIFY DATABASE NAME HERE BY CHANGING 'test.sqlite' (LINE 564)
       - # OF PAGES OF TWEETS TO BE DOWNLOADED PER ACCOUNT CAN BE CHANGED (LINES 596, 615)         
"""
</pre>

&nbsp;

In lines 29 &#8211; 44 we’ll import some Python packages needed to run the code. Twython and simplejson can be installed by opening your Terminal and installing by entering `pip install simplejson` and then `pip install Twython`. For more details on this process see <a href="http://social-metrics.org/python-code-prerequisites/" rel="noopener" target="_blank">this blog post</a>. 

<pre class="brush: python; first-line: 29; light: false; title: ; toolbar: true; notranslate" title="">###### PART I: IMPORT PYTHON PACKAGES (ALL BUT SIMPLEJSON & TWYTHON COME W/ ANACONDA) ###### 
import sys
import string
import sqlite3
import time
import datetime
from pprint import pprint
import sqlalchemy
from sqlalchemy.orm import mapper, sessionmaker
from sqlalchemy import Column, Integer, String, ForeignKey, Text, DateTime, Unicode, Float 
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import exc
from types import *
from datetime import datetime, date, time
import simplejson           #NEEDS TO BE INSTALLED SEPARATELY ONCE: pip install simplejson
from twython import Twython #NEEDS TO BE INSTALLED SEPARATELY ONCE: pip install Twython
</pre>

### Part II: Import Twython and Twitter App Key and Access Token

Lines 50-55 is where you will enter your Twitter _App Key_ and _Access Token_ (lines 53-54). If you have yet to do this you can refer to the tutorial on <a href="http://social-metrics.org/api-keys/" target="_blank">Setting up access to the Twitter API</a>.

<pre class="brush: python; first-line: 50; light: false; title: ; toolbar: true; notranslate" title="">###### PART II: IMPORT TWYTHON, ADD TWITTER APP KEY & ACCESS TOKEN (TO ACCESS API) ###### 

#REPLACE 'APP_KEY' WITH YOUR APP KEY, ACCESS_TOKEN WITH YOUR ACCESS TOKEN, IN THE NEXT TWO LINES
APP_KEY = ' '    
ACCESS_TOKEN = ' '
twitter = Twython(APP_KEY, access_token=ACCESS_TOKEN)
</pre>

### Part III: Define a Function for Getting Twitter Data

In this block of code we are creating a Python _function_. The function sets up which part of the Twitter API we wish to access (specifically, it is the <a href="https://dev.twitter.com/rest/reference/get/statuses/user_timeline" rel="noopener" target="_blank">get user timeline</a> API), the number of tweets we want to get per page (I have chosen the maximum of 200), and whether we want to include retweets. We will call this function later on in the code. 

<pre class="brush: python; first-line: 59; light: false; title: ; toolbar: true; notranslate" title="">###### PART III: DEFINE TWYTHON FUNCTION FOR GETTING ALL AVAILABLE PAGES OF TWEETS PER USER ###### 

def get_data_user_timeline_all_pages(kid, page):
    try:        
        '''
        'count' specifies the number of tweets to try and retrieve, up to a maximum of 200 per distinct request. 
        The value of count is best thought of as a limit to the number of tweets to return because suspended or 
        deleted content is removed after the count has been applied. We include retweets in the count, 
        even if include_rts is not supplied. It is recommended you always send include_rts=1 when using this API method.
        
        THE SCRIPT IS CURRENT SET UP TO DOWNLOAD ALL AVAILABLE PAGES -- 16 PAGES OF 200 TWEETS = 3,200 TWEETS/ACCOUNT TOTAL
        
        '''  
        d = twitter.get_user_timeline(screen_name=kid, count="200", page=page, include_entities="true", include_rts="1")          
    except Exception, e:
        print "Error reading id %s, exception: %s" % (kid, e)
        return None
    #print len(d), #d[0]  #NUMBER OF ENTRIES RETURNED, FIRST ENTRY
    #print "d.keys(): ", d[0].keys()
    return d
</pre>

### Part IV: Set up SQLite Database Tables

Lines 85-255 are where you set up columns for the database to allow use of SQLite and SQLAlchemy. For the reasons why we&#8217;re using SQLite <a href="http://social-metrics.org/python-code-prerequisites/" rel="noopener" target="_blank">you can refer to this post</a>. 

This is a very long, mechanical block of code. We are defining two _tables_ for our SQLite database &#8212; one for the tweets and one for the Twitter account names we want to download. Within each table we are defining variable names and variable types. That is, we are naming every variable (column) we wish to create and saying whether it is a _string_ variable (i.e., text) or an _integer_ variable. 

Why do we need to do this? We don&#8217;t actually have to go into such detail, but doing this &#8216;set-up&#8217; work now will make managing and analyzing the data later easier. When I use SQLite I specifically like to use SQLAlchemy (we imported it earlier), which makes working with an SQLite database even easier. Though it is long, it is a standard piece of code that you can cut-and-paste into any tweet download script. I usually split this block of code into a separate file and then import it, but I&#8217;m including all code here in a single script to make it easier to understand all of the moving parts. 

<pre class="brush: python; first-line: 85; light: false; title: ; toolbar: true; notranslate" title="">###### PART IV: SET UP COLUMNS FOR TWEET AND ACCOUNT TABLES IN DATABASE ###### 
'''
THIS PART OF THE SCRIPT CAN BE SPLIT OFF TO A SEPARATE FILE -- WILL ALSO BE USED 
FOR OTHER SCRIPTS TO ANALYZE THE DATA AFTER DOWNLOADING THE TWEETS
'''

Base = declarative_base()

#TWEET TABLE - THIS TABLE WILL BE CREATED AND POPULATED BY THIS PYTHON SCRIPT
class TWEET(Base):
    __tablename__ = 'user_timeline'                 #NAME OF TABLE HERE
    rowid = Column(Integer, primary_key=True)  
    query = Column(String)
    tweet_id = Column(String) 
    tweet_id_str = Column(String, unique=True)		##### UNIQUE CONSTRAINT ##### 
    inserted_date = Column(DateTime)
    truncated = Column(String)
    language = Column(String)
    possibly_sensitive = Column(String)  ### NEW 
    coordinates = Column(String)					#Represents the geographic location of this Tweet as reported by the user or client application. The inner coordinates array is formatted as geoJSON (longitude first, then latitude). 
    retweeted_status = Column(String)
    withheld_in_countries = Column(String)
    withheld_scope = Column(String)
    created_at_text = Column(String)   				#UTC time when this Tweet was created. 
    created_at = Column(DateTime)
    month = Column(String)
    year = Column(String)
    content = Column(Text)
    from_user_screen_name = Column(String)			#The screen name, handle, or alias that this user identifies themselves with. screen_names are unique but subject to change. Use id_str as a user identifier whenever possible. 
    from_user_id = Column(String)   
    from_user_followers_count = Column(Integer)  	#The number of followers this account currently has. 
    from_user_friends_count = Column(Integer)  		#The number of users this account is following (AKA their "followings"). 
    from_user_listed_count = Column(Integer)  		#The number of public lists that this user is a member of.
    from_user_favourites_count = Column(Integer)	#The number of tweets this user has favorited in the account's lifetime. British spelling used in the field name for historical reasons. 
    from_user_statuses_count = Column(Integer)  	#The number of tweets (including retweets) issued by the user. 
    from_user_description = Column(String)  		#The user-defined UTF-8 string describing their account. 
    from_user_location = Column(String)  			#The user-defined location for this account's profile. 
    from_user_created_at = Column(String)  			#The UTC datetime that the user account was created on Twitter. 
    retweet_count = Column(Integer)
    favorite_count = Column(Integer)				#Indicates approximately how many times this Tweet has been "favorited" by Twitter users. 
    entities_urls = Column(Unicode(255))
    entities_urls_count = Column(Integer)        
    entities_hashtags = Column(Unicode(255))
    entities_hashtags_count = Column(Integer)    
    entities_mentions = Column(Unicode(255))    
    entities_mentions_count = Column(Integer)  
    in_reply_to_screen_name = Column(String)  
    in_reply_to_status_id = Column(String)  
    source = Column(String)
    entities_expanded_urls = Column(Text) 
    entities_media_count = Column(Integer)
    media_expanded_url = Column(Text) 
    media_url = Column(Text) 
    media_type = Column(Text) 
    video_link = Column(Integer)
    photo_link = Column(Integer)
    twitpic = Column(Integer)
    num_characters = Column(Integer)    				
    num_words = Column(Integer)        					
    retweeted_user = Column(Text) 
    retweeted_user_description = Column(Text) 
    retweeted_user_screen_name = Column(Text) 
    retweeted_user_followers_count = Column(Integer) 
    retweeted_user_listed_count = Column(Integer) 
    retweeted_user_statuses_count = Column(Integer) 
    retweeted_user_location = Column(Text) 
    retweeted_tweet_created_at = Column(DateTime)		
    Unique_ID = Column(Integer)							#SPECIFIC TO EACH ACCOUNT
    
    def __init__(self, query, tweet_id, tweet_id_str, inserted_date, truncated, language, possibly_sensitive, coordinates, 
    retweeted_status, withheld_in_countries, withheld_scope, created_at_text, created_at, month, year, content, 
    from_user_screen_name, from_user_id, from_user_followers_count, from_user_friends_count,   
    from_user_listed_count, from_user_favourites_count, from_user_statuses_count, from_user_description,   
    from_user_location, from_user_created_at, retweet_count, favorite_count, entities_urls, entities_urls_count,         
    entities_hashtags, entities_hashtags_count, entities_mentions, entities_mentions_count,   
    in_reply_to_screen_name, in_reply_to_status_id, source, entities_expanded_urls,
    entities_media_count, media_expanded_url, media_url, media_type, video_link, photo_link, twitpic, 
    num_characters, num_words,  
    retweeted_user, retweeted_user_description, retweeted_user_screen_name, retweeted_user_followers_count,
    retweeted_user_listed_count, retweeted_user_statuses_count, retweeted_user_location,
    retweeted_tweet_created_at, 
    Unique_ID, 
    ):
     
    
        self.query = query
        self.tweet_id = tweet_id
        self.tweet_id_str = tweet_id_str
        self.inserted_date = inserted_date
        self.truncated = truncated
        self.language = language
        self.possibly_sensitive = possibly_sensitive
        self.coordinates = coordinates
        self.retweeted_status = retweeted_status
        self.withheld_in_countries = withheld_in_countries
        self.withheld_scope = withheld_scope
        self.created_at_text = created_at_text
        self.created_at = created_at 
        self.month = month
        self.year = year
        self.content = content
        self.from_user_screen_name = from_user_screen_name
        self.from_user_id = from_user_id       
        self.from_user_followers_count = from_user_followers_count
        self.from_user_friends_count = from_user_friends_count
        self.from_user_listed_count = from_user_listed_count
        self.from_user_favourites_count = from_user_favourites_count
        self.from_user_statuses_count = from_user_statuses_count
        self.from_user_description = from_user_description
        self.from_user_location = from_user_location
        self.from_user_created_at = from_user_created_at
        self.retweet_count = retweet_count
        self.favorite_count = favorite_count
        self.entities_urls = entities_urls
        self.entities_urls_count = entities_urls_count        
        self.entities_hashtags = entities_hashtags
        self.entities_hashtags_count = entities_hashtags_count
        self.entities_mentions = entities_mentions
        self.entities_mentions_count = entities_mentions_count     
        self.in_reply_to_screen_name = in_reply_to_screen_name
        self.in_reply_to_status_id = in_reply_to_status_id
        self.source = source
        self.entities_expanded_urls = entities_expanded_urls
        self.entities_media_count = entities_media_count
        self.media_expanded_url = media_expanded_url
        self.media_url = media_url
        self.media_type = media_type
        self.video_link = video_link
        self.photo_link = photo_link
        self.twitpic = twitpic
        self.num_characters = num_characters
        self.num_words = num_words
        self.retweeted_user = retweeted_user
        self.retweeted_user_description = retweeted_user_description
        self.retweeted_user_screen_name = retweeted_user_screen_name
        self.retweeted_user_followers_count = retweeted_user_followers_count
        self.retweeted_user_listed_count = retweeted_user_listed_count
        self.retweeted_user_statuses_count = retweeted_user_statuses_count
        self.retweeted_user_location = retweeted_user_location
        self.retweeted_tweet_created_at = retweeted_tweet_created_at    
        self.Unique_ID = Unique_ID
        
    def __repr__(self):
       return "&lt;sender, created_at('%s', '%s')&gt;" % (self.from_user_screen_name,self.created_at)
        


#ACCOUNTS TABLE -- THIS IS WHAT YOU IMPORTED INTO SQLITE EARLIER IN THE TUTORIAL
class ACCOUNT(Base):
    __tablename__ = 'accounts'
    Unique_ID = Column(Integer, primary_key=True)     
    org_name = Column(String)
    org_URL = Column(String)
    Twitter_URL = Column(String)  
    Twitter_handle = Column(String)  
    earliest_tweet_in_db = Column(String)
    number_of_tweets_in_db = Column(Integer)
    
    def __init__(self, org_name, org_URL, Twitter_URL, Twitter_handle,
        earliest_tweet_in_db, number_of_tweets_in_db, 
    ):       
    
        self.org_name = org_name
        self.org_URL = org_URL
        self.Twitter_URL = Twitter_URL       
        self.Twitter_handle = Twitter_handle
        self.earliest_tweet_in_db = earliest_tweet_in_db
        self.number_of_tweets_in_db = number_of_tweets_in_db
     
    def __repr__(self):
       return "&lt;Twitter handle, org_type('%s', '%s')&gt;" % (self.Twitter_handle,self.org_type)
</pre>

### Part V: Write function for parsing and storing data returned by Twitter API

In Lines 263-554 we are writing a long function to help _write_ the data to the SQLite database. At this point in the code we have still not downloaded any data. We are just setting up a function that we&#8217;ll call later. 

I won&#8217;t go into all of the details of what we&#8217;re doing here. The &#8216;big picture&#8217; is that with this function we are looping over all 200 tweets in each page. For each tweet, we are grabbing certain bits of information returned by the Twitter API and then assigning those bits of information to the database variables we set up earlier.

<pre class="brush: python; first-line: 263; light: false; title: ; toolbar: true; notranslate" title="">###### PART V: DEFINE FUNCTION FOR PARSING JSON-BASED TWEET DATA RETURNED BY TWITTER API -- CREATE VARIABLES TO BE STORED ###### 
        
def write_data(self, d, Twitter_handle,  Unique_ID):        

    Unique_ID = Unique_ID
    query = Twitter_handle  #d['search_metadata']['query']  #THIS IS DIFFERENT FROM MENTIONS AND DMS FILES
    
    #for sender in d['results']:
    for entry in d: 			#d['statuses']:	#THIS IS DIFFERENT FROM MENTIONS AND DMS FILES
        #json_output = str(entry)
        #print json_output
        #json_output = unicode.join(u'\n',map(unicode,json_output_string))
        
        #ids.append(sender['id'])
        #print sender.keys()       
        
        tweet_id = entry['id']
        tweet_id_str = entry['id_str']        
        inserted_date = datetime.now()   #CURRENT DATE AND TIME
    
       
        ##### NEW VARIABLES -- UNTESTED #####
        truncated = entry['truncated']
        language = entry['lang']
        

        #WE NEED THE 'IF' CONDITION CHECK HERE BECAUSE THERE IS NOT A VALUE FOR ALL TWEETS, UNLIKE, 
        #SAY, WITH THE 'TEXT' VARIABLE
        if 'possibly_sensitive' in entry:
            possibly_sensitive= entry['possibly_sensitive']
        else:
            possibly_sensitive = ''
        
        coordinates = []
        if 'coordinates' in entry and entry['coordinates'] != None:
            #print entry['coordinates']['coordinates']
            #[-98.0738001, 27.75346355]
            #-98.0738001 &lt;type 'float'&gt;
            #27.75346355 &lt;type 'float'&gt;
            for coordinate in entry['coordinates']['coordinates']:
                #print coordinate, type(coordinate)
                #coordinates.append(str(coordinate))
                coordinates.append(coordinate)
            #print "HERE ARE THE COORDINATES----------------------&gt;", "".join(format(x, "10.8f") for x in coordinates)
            coordinates = ', '.join(map(str, coordinates))							#WILL NOT WORK
            #coordinates = entry['coordinates']['coordinates']
            #coordinates = ",".join("'{0}'".format(n) for n in coordinates)  #THIS IS A LIST OF INTEGERS
            #print type(coordinates), len(coordinates), coordinates
            #print type(coordinates), coordinates
        else:
            coordinates = ''
            
        if 'retweeted_status' in entry:
            retweeted_status = 'THIS IS A RETWEET'

            retweeted_user = entry['retweeted_status']['user']['id_str']  ###I SHOULD USE ALL STR OR NOT
            retweeted_user_description = entry['retweeted_status']['user']['description'] 
            retweeted_user_screen_name = entry['retweeted_status']['user']['screen_name'] 
            retweeted_user_followers_count = entry['retweeted_status']['user']['followers_count']
            retweeted_user_listed_count = entry['retweeted_status']['user']['listed_count']
            retweeted_user_statuses_count = entry['retweeted_status']['user']['statuses_count'] 
            retweeted_user_location = entry['retweeted_status']['user']['location'] 
            retweeted_tweet_created_at_text = entry['retweeted_status']['created_at']
            retweeted_tweet_created_at = datetime.strptime(retweeted_tweet_created_at_text, '%a %b %d %H:%M:%S +0000 %Y')   #&lt;type 'datetime.datetime'&gt;
        
        else:
            retweeted_status = ''  
            retweeted_user = ''
            retweeted_user_description = ''
            retweeted_user_screen_name = ''
            retweeted_user_followers_count = ''
            retweeted_user_listed_count = ''
            retweeted_user_statuses_count = ''
            retweeted_user_location = ''
            retweeted_tweet_created_at = None
            
        if 'withheld_in_countries' in entry:
            withheld_in_countries = 'WITHHELD --&gt; CHECK JSON'
        else:
            withheld_in_countries = ''
     
        if 'withheld_scope' in entry:
            withheld_scope = entry['withheld_scope']
        else:
            withheld_scope = ''
       

        #print sender['text']

        # init field values
        content = entry['text']
        content = content.replace('\n','')      
        
        print '\n', content.encode('utf-8') 
        
        num_characters = len(content) #NUMBER OF CHARACTERS (SPACES INCLUDED)
        words = content.split()
        num_words = len(words)
        
        created_at_text = entry['created_at']     ##### Fri Jun 24 18:14:34 +0000 2011 --&gt; &lt;type 'str'&gt;

        ##### EXAMPLE OF HOW TO CONVERT STRING TO DATETIME FORMAT AND THEN MODIFY
        #t = datetime.strptime("20091229050936", "%Y%m%d%H%M%S")
        #print t.strftime('%H:%M %d %B %Y (UTC)')
        #fred = t.strftime('%H:%M %d %B %Y (UTC)')  ## 05:09 29 December 2009 (UTC) --&gt; &lt;type 'str'&gt;    

        #date_test = datetime.strptime('Fri Jun 24 18:14:34 +0000 2011', '%a %b %d %H:%M:%S +0000 %Y')   #&lt;type 'datetime.datetime'&gt;
        
        created_at = datetime.strptime(created_at_text, '%a %b %d %H:%M:%S +0000 %Y')   #&lt;type 'datetime.datetime'&gt;
        #date = twitter_date.strftime('%Y-%B-%d %H:%M')     ### BETTER OPTION BELOW (HAS MONTH, DAY AS NUMBERS)
        created_at2 = created_at.strftime('%Y-%m-%d %H:%M:%S')   ### THIS WORKS WELL, BUT IS SAME AS twitter_date ABOVE
        
        #month = datetime.strptime(created_at_text, '%b') 
        #year = datetime.strptime(created_at_text, '%Y')   #ValueError: time data 'Thu Oct 17 17:47:34 +0000 2013' does not match format '%Y'

        month = created_at.strftime('%m')
        year = created_at.strftime('%Y')
        #print 'month', month, 'year', year
        
        
        #print created_at, created_at2
        
        #from_user = sender['from_user']            ##### THIS NEEDS TO BE UPDATED --&gt; 7/11/13 IT'S UNDER user, WHICH HAS SUB-KEYS
        from_user_screen_name = entry['user']['screen_name']
        #from_user_id = sender['from_user_id']      ##### THIS NEEDS TO BE UPDATED  --&gt; 7/11/13 IT'S UNDER user, WHICH HAS SUB-KEYS
        from_user_id = entry['user']['id'] 
        from_user_followers_count = entry['user']['followers_count']
        from_user_friends_count = entry['user']['friends_count']   
        from_user_listed_count = entry['user']['listed_count']
        from_user_favourites_count = entry['user']['favourites_count']
        print '\n', 'from_user_favourites_count--------------&gt;', from_user_favourites_count
        from_user_statuses_count = entry['user']['statuses_count'] 
        from_user_description = entry['user']['description'] 
        from_user_location = entry['user']['location'] 
        from_user_created_at = entry['user']['created_at']
        
        retweet_count = entry['retweet_count'] 
        favorite_count = entry['favorite_count']
        
        in_reply_to_screen_name = entry['in_reply_to_screen_name']
        in_reply_to_status_id = entry['in_reply_to_status_id']



        #GENERATES VARIABLES FOR #URLS, HASHTAGS, AND MENTIONS
        entities_urls_count = len(entry['entities']['urls'])    
        entities_hashtags_count = len(entry['entities']['hashtags'])   
        entities_mentions_count = len(entry['entities']['user_mentions']) 
    
        source = entry['source']
        

        #NOW WE ARE GOING TO CREATE VARIABLES FOR URLS, TAGS, AND MENTIONS --&gt; THE DIFFICULTY HERE
        #IS THAT THERE IS NO UNIFORM NUMBER OF, SAY, TAGS IN EACH TWEET, SO WE CANNOT CREATE 
        #A FIXED NUMBER OF COLUMNS/VARIABLES BEFOREHAND. INSTEAD, WE'LL CREATE A STRING FOR EACH 
        #VARIABLE --&gt; CAN BE PARSED OUT OR LOOPED OVER LATER AS NEEDED.

        entities_urls, entities_expanded_urls, entities_hashtags, entities_mentions = [], [], [], []
        
        #print type(entry['entities']['urls'])     ##### IT'S A LIST
        #urls = entry['entities']['urls']               
        for link in entry['entities']['urls']:
            if 'url' in link:
                url = link['url']
                expanded_url = link['expanded_url']
                #print link['url'], link['expanded_url']
                entities_urls.append(url)
                entities_expanded_urls.append(expanded_url)
            else:
                print "No urls in entry"

        for hashtag in entry['entities']['hashtags']:
            if 'text' in hashtag:
                tag = hashtag['text']
                #print hashtag['text']
                entities_hashtags.append(tag)
            else:
                print "No hashtags in entry"

        for at in entry['entities']['user_mentions']:
            if 'screen_name' in at:
                mention = at['screen_name']
                #print at['screen_name']
                entities_mentions.append(mention)
            else:
                print "No mentions in entry"
                
        entities_mentions = string.join(entities_mentions, u", ")
        entities_hashtags = string.join(entities_hashtags, u", ")
        entities_urls = string.join(entities_urls, u", ")
        entities_expanded_urls = string.join(entities_expanded_urls, u", ")    
        
        video_link = 0
        if 'vimeo' in entities_expanded_urls or 'youtube' in entities_expanded_urls or 'youtu' in entities_expanded_urls or 'vine' in entities_expanded_urls:
            video_link = 1					#All of these videos show up in 'View Media' in tweets
            #print "FOUND A VIDEO!!!"
        else:
            video_link = 0
            
        #if photo_text.find('twitpic'): # or photo_text.find('instagram') or photo_text.find('instagr'):
        #if 'twitpic' in photo_text:
        if 'twitpic' in entities_expanded_urls:
            twitpic = 1						#twitpic images show up in 'View Media' in tweets
            #print "FOUND A TWITPIC LINK!"
        else:
            twitpic = 0
        if 'twitpic' in entities_expanded_urls or 'instagram' in entities_expanded_urls or 'instagr' in entities_expanded_urls:
            photo_link = 1					#instagram images DO NOT show up in 'View Media' in tweets
            #print "FOUND A TWITPIC OR INSTAGRAM LINK!!!"
        else:
            photo_link = 0

        
        #CONVERT TO UNICODE FOR INSERTION INTO SQLITE DB        
        entities_urls = unicode(entities_urls)
        entities_expanded_urls = unicode(entities_expanded_urls)
        entities_hashtags = unicode(entities_hashtags)
        entities_mentions = unicode(entities_mentions)
        
        #print "urls...?....", entities_urls 
        #print "user_mentions...?....", entities_mentions
        #print "hashtags...?....", entities_hashtags


        #if 'symbols' in entry['entities']:
		#    print "HERE ARE THE SYMBOLS.......", entry['entities']['symbols']
        #else:
		#    print "THERE AIN'T NO entry['entities']['symbols']"
		
        if 'media' in entry['entities']:
			#print "HERE ARE THE MEDIA.......", entry['entities']['media']
			entities_media_count = len(entry['entities']['media'])   
			#'expanded_url' #The fully resolved media URL [FULL TWEET PLUS PICTURE] --&gt; e.g., http://twitter.com/StJude/status/347801636351135744/photo/1
			#'display_url' # 	Not a URL but a string to display instead of the media URL --&gt; e.g., pic.twitter.com/hO4BjuqrnE
			#'media_url_https'  #The SSL URL of the media file --&gt; e.g., https://pbs.twimg.com/media/BNOjvtuCUAA4S66.jpg
			#'type' # 	only photo for now --&gt; e.g., photo
			#'media_url'  # The URL of the media file --&gt; e.g., http://pbs.twimg.com/media/BNOjvtuCUAA4S66.jpg          
        else:
            entities_media_count = ''
					
					
			#for a in entry['entities']['media']:
			#print a['expanded_url'], a['media_url']  #, a['media_type'] 
			#bob = entry['entities']['media'][0]
			#print bob
			#print bob['expanded_url']
        

        if 'media' in entry['entities']:
            if 'expanded_url' in entry['entities']['media'][0]:
		        media_expanded_url = entry['entities']['media'][0]['expanded_url']
            else:
                #print "THERE AIN'T NO expanded_url in entry['entities']['media']"
                media_expanded_url = ''
					    
            if 'media_url' in entry['entities']['media'][0]:
		        media_url = entry['entities']['media'][0]['media_url']
            else:
		        #print "THERE AIN'T NO media_url in entry['entities']['media']"
		        media_url = ''
					    
            if 'type' in entry['entities']['media'][0]:
		        media_type = entry['entities']['media'][0]['type']
            else:
		        #print "THERE AIN'T NO type in entry['entities']['media']"
		        media_type = ''
        else:
		    media_type = ''
		    media_url = ''
		    media_expanded_url = ''
      
        upd = TWEET(query, tweet_id, tweet_id_str, inserted_date, truncated, language, possibly_sensitive, 
                coordinates, retweeted_status, withheld_in_countries, withheld_scope, created_at_text, 
                created_at, month, year, content, from_user_screen_name, from_user_id, from_user_followers_count, 
                from_user_friends_count, from_user_listed_count, from_user_favourites_count, from_user_statuses_count, from_user_description,   
                from_user_location, from_user_created_at, retweet_count, favorite_count, entities_urls, entities_urls_count,         
                entities_hashtags, entities_hashtags_count, entities_mentions, entities_mentions_count,   
                in_reply_to_screen_name, in_reply_to_status_id, source, entities_expanded_urls, #json_output, 
                entities_media_count, media_expanded_url, media_url, media_type, video_link, photo_link, twitpic, 
                num_characters, num_words,
                retweeted_user, retweeted_user_description, retweeted_user_screen_name, retweeted_user_followers_count,
                retweeted_user_listed_count, retweeted_user_statuses_count, retweeted_user_location,
                retweeted_tweet_created_at, 
                Unique_ID,
                )
                
        self.session.add(upd)
        try:
            self.session.commit()
        except exc.SQLAlchemyError:
            self.session.rollback()
            print "     NOT INSERTING --&gt; IT'S A DUPLICATE"
</pre>

Now, a key step to this is understanding the data that are returned by the API. As is increasingly common with Web data, this API call returns data in JSON format. Behind the scenes, Python has grabbed a JSON file, which will have data on 200 tweets (one page of tweets). Each tweet is an object in the JSON file, and we are looping over each object. If you&#8217;re interested in more details, the code we’re using here plugs into the <a href="https://dev.twitter.com/rest/reference/get/statuses/user_timeline" rel="noopener" target="_blank">user_timeline</a> part of the Twitter API; follow the link for a description of what the API does. You can also go <a href="https://dev.twitter.com/overview/api/tweets" rel="noopener" target="_blank">here</a> to see a list of the definitions for the variables returned by the API. To understand how this relates to JSON, you can take a look at <a href="http://social-metrics.org/twitter-user-data/" rel="noopener" target="_blank">my earlier post on downloading Twitter user data</a>.

I&#8217;ll give you two examples here: In line 279 we are taking the data included in the object&#8217;s [&#8216;id&#8217;] variable and assigning that to a variable called _tweet_id_. In line 358 we are creating a variable called _num_characters_ whose value is the number of characters in the tweet. We are doing this for every variable we have set up in Part IV earlier. 

After we&#8217;ve created these variables, we now need to write them to our database. In lines 534-547 we tell our SQLite database that we want to update our TWEET database and which variables to include. You&#8217;ll see these are the same variable names we used in Part IV. Line 549 contains the command to add the tweet data to our database. 

Here comes a key part: lines 550-554 contain a _try&#8230;except_ loop designed to catch duplicate tweets. Simply put, if the tweet already exists in the database it will skip over it. This is really important and one of the best reasons to use a database for downloading tweets. If you wanted, you could simply download your tweets to an Excel spreadsheet. However, each time you ran the script you would likely be downloading a truckload of duplicates. You don&#8217;t want that. 

The key to this lies in how we set up our TWEET database earlier; specifically, line 99 contains a _unique_ constraint. 

<pre class="brush: python; first-line: 99; light: false; title: ; toolbar: true; notranslate" title="">tweet_id_str = Column(String, unique=True)
</pre>

There can only be one entry with a given tweet\_id\_str value. Given that every tweet has a unique tweet ID, this is the best variable on which to make a unique constraint.

### Part VI: Main Loop: Loop over each of the Twitter handles in the _Accounts_ table and Download Tweets.

In lines 560-627 we are at the last step. In this block the first important thing we do is name our SQLite database on line 579.

Then in line 571 we query the _ACCOUNT_ table in our database and assign that to a variable _all_ids_. This will work for the second time we run the script and all subsequent times.

The first time we run the script, though, our _ACCOUNT_ table will be empty. Lines 576-583 check whether it is empty and, if so, will grab the details from our _accounts.csv_ file and insert it into our database. 

At line 586 we then begin a _for loop_ &#8212; we will be looping over each Twitter ID (as indicated by the _Twitter_handle_ variable in our _ACCOUNT_ database). 

Note that within this _for loop_ we have a _while loop_ (lines 596-618). What we are doing here is, for each Twitter ID, we are grabbing up to 16 pages&#8217; worth of tweets; this is the maximum allowed for by the Twitter API. It is in this loop that we actually call our functions. On line 598 we invoke our _get\_data\_user\_timeline\_all_pages_ function, which on the first loop will grab page 1 for the Twitter ID, then page 2, then page 3, &#8230;. up to page 16 so long as there are data to return. Line 606 invokes the _write_data_ function for each page.

<pre class="brush: python; first-line: 560; light: false; title: ; toolbar: true; notranslate" title="">###### PART VI: MAIN LOOP OVER EACH ID STORED IN 'ACCOUNT' TABLE OF DATABASE - 16 PAGES OF 200 TWEETS PER ID ###### 

class Scrape:
    def __init__(self):    
        engine = sqlalchemy.create_engine("sqlite:///test.sqlite", echo=False)  # YOUR DATABASE NAME HERE
        Session = sessionmaker(bind=engine)
        self.session = Session()  
        Base.metadata.create_all(engine)
    
    def main(self):
    
        all_ids = self.session.query(ACCOUNT).all()
        
        print 'len(all_ids)', len(all_ids)
        
        
        #CHECK IF THE 'ACCOUNTS' TABLE HAS BEEN POPULATED; IF NOT, ADD DATA FROM 
        #CSV FILE TO THE TABLE
        if len(all_ids) &lt; 1:
            conn = sqlite3.connect('test.sqlite')
            import pandas as pd
            df = pd.read_csv('accounts.csv')
            df.to_sql('accounts', conn, if_exists='append', index=False)
            all_ids = self.session.query(ACCOUNT).all()
            
        keys = []
        for i in all_ids: 
            Unique_ID = i.Unique_ID
            Twitter_handle = i.Twitter_handle
            kid = Twitter_handle    			
            rowid = i.Unique_ID
            print '\n', "\rprocessing id %s/%s  --  %s" % (rowid, len(all_ids), Twitter_handle),
            sys.stdout.flush()
                
            
            page = 1
            while page &lt; 17: #TO DOWNLOAD FEWER PAGES OF TWEETS, MODIFY THIS PLUS LINE 621
                print "------XXXXXX------ STARTING PAGE", page
                d = get_data_user_timeline_all_pages(kid, page)         
                if not d:
                    print "THERE WERE NO STATUSES RETURNED........MOVING TO NEXT ID"
                    break	        
                if len(d)==0:
                    print "THERE WERE NO STATUSES RETURNED........MOVING TO NEXT ID"
                    break
        
                write_data(self, d, Twitter_handle, Unique_ID)


                #self.session.commit()
        
                #print 'pausing for 1 second'
                #time.sleep(1) #PAUSE FOR 1 SECOND
                    
                page += 1
                if page &gt; 16:
                    print "WE'RE AT THE END OF PAGE 16!!!!!"
                    break
            self.session.commit()
                    
        print  '\n', '\n', '\n', "FINISHED WITH ALL IDS"
        self.session.close()



if __name__ == "__main__":
    s = Scrape()
    s.main()
</pre>

Now let&#8217;s put the whole thing together. To recap, what this entire script does is to loop over each of the Twitter accounts in the _Accounts_ table of our database &#8212; and for each one it will grab up to 3,200 tweets and insert the tweets into an SQLite database. 

Below is the entire script &#8212; download it and save it as _tweets.py_ (or something similar) in the same directory as your _accounts.csv_ file. Add in your Twitter API account details and you&#8217;ll be good to go! For a refresher on the different ways you can run the script see [this earlier post][1]. 

If you&#8217;ve found this post helpful please share on your favorite social media site. 

You&#8217;re on your way to downloading your own Twitter data! Happy coding!

https://gist.github.com/gdsaxton/b0d36c10bbdb80e26b692a1d1a3e11de

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/starting-on-python-2/