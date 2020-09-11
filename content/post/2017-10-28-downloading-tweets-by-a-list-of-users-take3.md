---
title: Downloading Tweets, Take III – MongoDB
author: Gregory Saxton
type: post
date: 2017-10-28T19:26:21+00:00
url: /downloading-tweets-by-a-list-of-users-take3/
featured_image: /wp-content/uploads/2015/05/16044856481_78fb44e40d_o.jpg
categories:
  - Big Data
  - Featured
  - python
  - Twitter
tags:
  - Big Data
  - Database
  - MongoDB
  - Programming
  - python
  - social media
  - socialmedia
  - tutorial
  - Twitter

---
In this tutorial I walk you through how to use Python and MongoDB to download tweets from a list of Twitter users.

This tutorial builds on several recents posts on how to use Python to download Twitter data. Specifically, in <a href="http://social-metrics.org/downloading-tweets-by-a-list-of-users-take2/" rel="noopener" target="_blank">a previous post</a> I showed you how to download tweets using Python and an SQLite database &#8212; a type of traditional _relational_ database. More and more people are interested in _noSQL_ databases such as MongoDB, so in <a href="http://social-metrics.org/sqlite-vs-mongodb/" rel="noopener" target="_blank">a follow-up post</a> I talked about the advantages and disadvantages of using SQLite vs MongoDB to download social media data for research purposes. Today I go into detail about how to actually use MongoDB to download your data and I point out the differences from the SQLite approach along the way. 

### Overview

This tutorial is directed at those who are new to Python, MongoDB, and/or downloading data from the Twitter API. We will be using Python to download the tweets and will be inserting the tweets into a MongoDB database. This code will allow you to download up to the latest 3,200 tweets sent by each Twitter user. I will not go over the script line-by-line but will instead attempt to provide you a &#8216;high-level&#8217; understanding of what we are doing &#8212; just enough so that you can run the script successfully yourself.

Before running this script, you will need to:

  * Have Anaconda Python 2.7 installed
  * Have your Twitter API details handy
  * Have MongoDB installed and running 
  * Have created a CSV file (e.g., in Excel) containing the Twitter handles you wish to download. Below is a sample you can download and use for this tutorial. Name it _accounts.csv_ and place it in the same directory as the Python script.



If you are completely new to Python and the Twitter API, you should first make your way through the following tutorials, which will help you get set up and working with Python:

  * <a href="http://social-metrics.org/python-where-to-start/" target="_blank">Which version of Python to download</a>
  * <a href="http://social-metrics.org/starting-on-python-1/" target="_blank">Running your first code</a>
  * <a href="http://social-metrics.org/starting-on-python-2/" target="_blank">Four ways to run your code</a>
  * <a href="http://social-metrics.org/api-keys/" target="_blank">Setting up access to the Twitter API</a>

Another detailed tutorial I have created, <a href="http://social-metrics.org/python-tutorial-1/" target="_blank">Python Code Tutorial</a>, is intended to serve as an introduction to how to access the Twitter API and then read the JSON data that is returned. It will be helpful for understanding what we&#8217;re doing in this script.

Also, if you are not sure you want to use MongoDB as your database, take a look at <a href="http://social-metrics.org/sqlite-vs-mongodb/" rel="noopener" target="_blank">this post</a>, which covers the advantages and disadvantages of using SQLite vs MongoDB to download social media data. As noted in that post, MongoDB has a more detailed installation process.

At the end of this post I&#8217;ll show the entire script. For now, I&#8217;ll go over it in sections. The code is divided into seven parts:

### Part I: Importing Necessary Python Packages

The first line in the code is the <a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank">shebang</a> &#8212; you&#8217;ll find this in all Python code.

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">#!/usr/bin/env python</pre>

&nbsp;

Lines 3 &#8211; 23 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank">docstring</a> &#8212; also a Python convention. This is a multi-line comment that describes the code. For single-line comments, use the _#_ symbol at the start of the line.

<pre class="brush: python; first-line: 3; light: false; title: ; toolbar: true; notranslate" title="">"""
Social_Metrics_Tutorial_Script_User_Timeline_All_Pages.py - DOWNLOADS ALL AVAILABLE RECENT
TWEETS FROM 5 MLB ACCOUNTS INTO MONGODB DATABASE

BEFORE RUNNING THIS SCRIPT, YOU WILL NEED TO:
  1. HAVE ANACONDA PYTHON 2.7 INSTALLED
  2. HAVE CREATED CSV FILE (E.G., IN EXCEL) CONTAINING TWITTER HANDLES YOU 
     WISH TO DOWNLOAD (SEE TUTORIAL FOR DETAILS)
  3. HAVE MONGODB INSTALLED AND RUNNING


THE CODE IS DIVIDED INTO SEVEN PARTS:
  1. Importing necessary Python packages 
  2. Importing Twython and Twitter app key and access token
       - YOU NEED TO MODIFY THIS SECTION IN ORDER TO GET SCRIPT TO WORK (LINES 39-41)
  3. Defining function for getting Twitter data
  4. Set up MongoDB database and collections (tables)
  5. Read in Twitter accounts (and add to MongoDB database if first run)
  6. Main loop over each of the Twitter handles in the accounts table of the database.  
  7. Print out number of tweets in database per account    
"""
</pre>

&nbsp;

In lines 26 &#8211; 31 we’ll import some Python packages needed to run the code. Twython can be installed by opening your Terminal and installing by entering `pip install Twython`. For more details on this process see <a href="http://social-metrics.org/python-code-prerequisites/" rel="noopener" target="_blank">this blog post</a>. 

<pre class="brush: python; first-line: 26; light: false; title: ; toolbar: true; notranslate" title="">###### PART I: IMPORT PYTHON PACKAGES (ALL BUT TWYTHON ARE INSTALLED W/ ANACONDA PYTHON ###### 
import sys
import time
import json
import pandas as pd
from twython import Twython #NEEDS TO BE INSTALLED SEPARATELY ONCE: pip install Twython
</pre>

### Part II: Import Twython and Twitter App Key and Access Token

Lines 37-42 is where you will enter your Twitter _App Key_ and _Access Token_ (lines 40-41). If you have yet to do this you can refer to the tutorial on <a href="http://social-metrics.org/api-keys/" target="_blank">Setting up access to the Twitter API</a>.

<pre class="brush: python; first-line: 37; light: false; title: ; toolbar: true; notranslate" title="">###### PART II: IMPORT TWYTHON, ADD TWITTER APP KEY & ACCESS TOKEN (TO ACCESS API) ###### 

#REPLACE 'APP_KEY' AND 'ACCESS_TOKEN' WITH YOUR APP KEY & ACCESS TOKEN IN THE NEXT 2 LINES
APP_KEY = ' '    
ACCESS_TOKEN = ' '
twitter = Twython(APP_KEY, access_token=ACCESS_TOKEN)
</pre>

### Part III: Define a Function for Getting Twitter Data

In this block of code we are creating a Python _function_. The function sets up which part of the Twitter API we wish to access (specifically, it is the <a href="https://dev.twitter.com/rest/reference/get/statuses/user_timeline" rel="noopener" target="_blank">get user timeline</a> API), the number of tweets we want to get per page (I have chosen the maximum of 200), and whether we want to include retweets. We will call this function later on in the code. 

<pre class="brush: python; first-line: 48; light: false; title: ; toolbar: true; notranslate" title="">###### PART III: DEFINE TWYTHON FUNCTION FOR GETTING ALL AVAILABLE TWEETS PER USER ###### 

def get_data_user_timeline_all_pages(kid, page):
    try:        
        '''
        'count' specifies the number of tweets to try and retrieve, up to a maximum of 200
        per distinct request. The value of count is best thought of as a limit to 
        the number of tweets to return because suspended or deleted content is removed 
        after the count has been applied. We include retweets in the count, even if 
        include_rts is not supplied. It is recommended you always send include_rts=1 when 
        using this API method.
        '''        
        d = twitter.get_user_timeline(screen_name=kid, count="200", page=page, include_entities="true", include_rts="1")          
    except Exception, e:
        print "Error reading id %s, exception: %s" % (kid, e)
        return None
    print len(d) #d[0]  #NUMBER OF ENTRIES RETURNED, FIRST ENTRY
    #print "d.keys(): ", d[0].keys()
    return d
</pre>

### Part IV: Set up MongoDB Database and Collections (Tables)

Lines 72-111 are where you set up your MongoDB database and &#8216;collections&#8217; (tables).

This is where you&#8217;ll see the first major differences from an SQLite implementation of this code. First, unlike SQLite, you will need to make sure MongoDB is _running_ by typing `mongod` or `sudo mongod` in the terminal. So, that&#8217;s one extra step you have to take with MongoDB. If you&#8217;re running the code on a machine that is running 24/7 that is no issue; if not you&#8217;ll just have to remember.

There is a big benefit to MongoDB here, however. Unlike with the SQLite implementation, there is no need to pre-define every column in our database tables. As you can see in <a href="http://social-metrics.org/downloading-tweets-by-a-list-of-users-take2/" rel="noopener" target="_blank">the SQLite version</a>, we devoted 170 lines of code to defining and naming database columns.

Below, in contrast, we are simply making a connection to MongoDB, creating our database, then our database tables, then indexes on those tables. Note that, if this is the first time you&#8217;re running this code, the database and tables and indexes will be _created_; if not, the code will simply access the database and tables. Note also that MongoDB refers to database tables as &#8216;collections&#8217; and refers to columns or variables as &#8216;fields.&#8217; 

One thing that is similar to the SQLite version is that we are setting indexes on our database tables. This means that no two tweets with the same index value &#8212; the tweet&#8217;s ID string (_id_str_) &#8212; can be inserted into our database. This is to avoid duplicate entries. 

One last point: we are setting up two tables, one for the tweets and one to hold the Twitter account names for which we wish to download tweets.

<pre class="brush: python; first-line: 72; light: false; title: ; toolbar: true; notranslate" title="">###### PART IV: SET UP MONGODB DATABASE AND ACCOUNTS AND TWEETS TABLES ###### 

#MAKE CONNECTION TO MONGODB
import pymongo
from pymongo import MongoClient
client = MongoClient()


# DEFINE YOUR MONGODB DATABASE
db = client['MLB']

# CREATE ACCOUNTS COLLECTION (TABLE) IN YOUR DATABASE FOR TWITTER ACCOUNT-LEVEL DETAILS
accounts = db['accounts']

# CREATE AN INDEX ON THE COLLECTION TO AVOID INSERTION OF DUPLICATES
db.accounts.create_index([('Twitter_handle', pymongo.ASCENDING)], unique=True)

# SHOW INDEX ON ACCOUNTS TABLE
#list(db.accounts.index_information())

#SHOW NUMBER OF ACCOUNTS IN TABLE
#accounts.count()

# DEFINE COLLECTION (TABLE) WHERE YOU'LL INSERT THE TWEETS
tweets = db['tweets']

# CREATE UNIQUE INDEX FOR TABLE (TO AVOID DUPLICATES)
db.tweets.create_index([('id_str', pymongo.ASCENDING)], unique=True)

#SHOW INDEX ON TWEETS COLLECTION
#list(db.tweets.index_information())

#SHOW NUMBER OF TWEETS IN TABLE
#tweets.count()

#TO SEE LIST OF CURRENT MONGODB DATABASES
#client.database_names()

#TO SEE LIST OF COLLECTIONS IN THE *MLB* DATABASE
#db.collection_names()
</pre>

### Part V: Read in Twitter Accounts (and add to MongoDB database if first run)

In Lines 117-139 we are creating a Python _list_ of Twitter handles for which we want to download tweets. The first part of the code (lines 119-130) is to check if this is the first time you&#8217;re running the code. If so, it will read the Twitter handle data from your local CSV file and insert it into the _accounts_ table in your MongoDB database. In all subsequent runs of the code the script will skip over this block and go directly to line 137 &#8212; that creates a list called _twitter_accounts_ that we&#8217;ll loop over in Part VI of the code.

<pre class="brush: python; first-line: 117; light: false; title: ; toolbar: true; notranslate" title="">###### PART V: READ IN TWITTER ACCOUNTS (AND ADD TO MONGODB IF FIRST RUN)

# IF ACCOUNTS COLLECTION IS EMPTY READ IN CSV FILE AND ADD TO MONGODB
if accounts.count() &lt; 1:
    df = pd.read_csv('accounts.csv')
    records = json.loads(df.T.to_json()).values()
    print "No account data in MongoDB, attempting to insert", len(records), "records"
    try:
        accounts.insert_many(records)
    except pymongo.errors.BulkWriteError, e:
        print e, '\n'
        #pass  
else:
    print "There are already", accounts.count(), "records in the *accounts* table"


#LIST ROWS IN ACCOUNTS COLLECTION
#list(accounts.find())[:1]

# CREATE LIST OF TWITTER HANDLES FOR DOWNLOADING TWEETS
twitter_accounts = accounts.distinct('Twitter_handle')
#print len(twitter_accounts)
#twitter_accounts[:5]
</pre>

### Part VI: Main Loop: Loop Over Each of the Twitter Handles in the _Accounts_ Table and Download Tweets

In lines 144-244 we are at the last important step. 

This code is much shorter here as well compared to the SQLite version. As noted in <a href="http://social-metrics.org/sqlite-vs-mongodb/" rel="noopener" target="_blank">my previous post comparing SQLite to MongoDB</a>, in MongoDB we do not need to define all of the columns we wish to insert into our database. MongoDB will just take whatever columns you throw at it and insert. In the SQLite version, in contrast, we had to devote 290 lines of code just specifying what specific parts of the Twitter data we are grabbing and how they relate to our pre-defined variable names.

After stripping out all of those details, the core of this code is the same as in the SQLite version. At line 151 we begin a _for loop_ where we are looping over each Twitter ID (as indicated by the _Twitter_handle_ variable in our _accounts_ database). 

Note that within this _for loop_ we have a _while loop_ (lines 166-238). What we are doing here is, for each Twitter ID, we are grabbing up to 16 pages&#8217; worth of tweets; this is the maximum allowed for by the Twitter API. It is in this loop (line 170) that we call our _get\_data\_user\_timeline\_all_pages_ function, which on the first loop will grab page 1 for the Twitter ID, then page 2, then page 3, &#8230;. up to page 16 so long as there are data to return. 

Lines 186-205 contains code for writing the data into our MongoDB database table. We have defined our variable _d_ to contain the result of calling our _get\_data\_user\_timeline\_all_pages_ function &#8212; this means that, if successful, _d_ will contain 200 tweets&#8217; worth of data. The _for loop_ starting on line 187 will loop over each tweet, add three variables to each tweet &#8212; _date_inserted_, _time\_date\_inserted_, and _screen_name_ &#8212; and then insert the tweet into our _tweets_ collection.

One last thing I&#8217;d like to point out here is the API limit checks I&#8217;ve written in lines 221-238. What this code is doing is checking how many remaining API calls you have. If it is too low, the code will pause for 5 minutes. 

<pre class="brush: python; first-line: 144; light: false; title: ; toolbar: true; notranslate" title="">###### PART VI: LOOP OVER TWITTER HANDLES & DOWNLOAD TWEETS INTO MONGODB COLLECTION ######  

import timeit
start_time = timeit.default_timer()

starting_count = tweets.count()

for s in twitter_accounts[:1]:
    
    #SET THE DUPLICATES COUNTER FOR THIS TWITTER ACCOUNT TO ZERO
    duplicates = 0
    
    #CHECK FOR TWITTER API RATE LIMIT (450 CALLS/15-MINUTE WINDOW)
    rate_limit = twitter.get_application_rate_limit_status()['resources']['statuses']['/statuses/user_timeline']['remaining']
    print '\n\n', '# of remaining API calls: ', rate_limit

    #tweet_id = str(mentions.find_one( { "query_screen_name": s}, sort=[("id_str", 1)])["id_str"])
    print 'Grabbing tweets sent by: ', s, '-- index number: ', twitter_accounts.index(s)
    
    page = 1
    
    #WE CAN GET 200 TWEETS PER CALL AND UP TO 3,200 TWEETS TOTAL, MEANING 16 PAGES' PER ACCOUNT 
    while page &lt; 17:
        print "------XXXXXX------ STARTING PAGE", page, '...estimated remaining API calls:', rate_limit

        d = get_data_user_timeline_all_pages(s, page)          
        if not d:
            print "THERE WERE NO STATUSES RETURNED........MOVING TO NEXT ID"
            break      
        if len(d)==0:    #THIS ROW IS DIFFERENT FROM THE MENTIONS AND DMS FILES
            print "THERE WERE NO STATUSES RETURNED........MOVING TO NEXT ID"
            break
        #if not d['statuses']:
        #    break
        
                
        #DECREASE rate_limit TRACKER VARIABLE BY 1
        rate_limit -= 1
        print '.......estimated remaining API rate_limit: ', rate_limit    
    

        ##### WRITE THE DATA INTO MONGODB -- LOOP OVER EACH TWEET
        for entry in d:
            #ADD THE FOLLOWING THREE VARIABLES TO THOSE RETURNED BY TWITTER API
            entry['date_inserted'] = time.strftime("%d/%m/%Y")
            entry['time_date_inserted'] = time.strftime("%H:%M:%S_%d/%m/%Y")
            entry['screen_name'] = entry['user']['screen_name']
        
            #CONVERT TWITTER DATA TO PREP FOR INSERTION INTO MONGO DB
            t = json.dumps(entry)
            #print 'type(t)', type(t)                   #&lt;type 'str'&gt;
            loaded_entry = json.loads(t)
            #print type(loaded_entry) , loaded_entry    #&lt;type 'dict'&gt;
        
            #INSERT THE TWEET INTO THE DATABASE -- UNLESS IT IS ALREADY IN THE DB
            try:
                 tweets.insert_one(loaded_entry)
            except pymongo.errors.DuplicateKeyError, e:
                #print e, '\n'
                duplicates += 1
                pass     
        
        
        print '------XXXXXX------ FINISHED PAGE', page, 'FOR ORGANIZATION', s, "--", len(d), "TWEETS"
    
        #IF THERE ARE TOO MANY DUPLICATES THEN SKIP TO NEXT ACCOUNT 
        if duplicates &gt; 20:
            print '\n********************There are %s' % duplicates, 'duplicates....moving to next ID********************\n'
            #continue        
            break
                    
        page += 1
        if page &gt; 16:
            print "WE'RE AT THE END OF PAGE 16"
            break    
                
        #THIS IS A SOMEWHAT CRUDE METHOD OF PUTTING IN AN API RATE LIMIT CHECK
        #THE RATE LIMIT FOR CHECKING HOW MANY API CALLS REMAIN IS 180, WHICH MEANS WE CANNOT
        if rate_limit &lt; 5:
            print 'Estimated fewer than 5 API calls remaining...check then pause 5 minutes if necessary'
            rate_limit_check = twitter.get_application_rate_limit_status()['resources']['statuses']['/statuses/user_timeline']['remaining']
            print '.......and here is our ACTUAL remaining API rate_limit: ', rate_limit_check
            if rate_limit_check&lt;5:
                print 'Fewer than 5 API calls remaining...pausing for 5 minutes'
                time.sleep(300) #PAUSE FOR 300 SECONDS
                rate_limit = twitter.get_application_rate_limit_status()['resources']['statuses']['/statuses/user_timeline']['remaining']
                print '.......here is our remaining API rate_limit after pausing for 5 minutes: ', rate_limit
                #if rate_limit_check == 450:
                #    rate_limit = 450

    #if twitter.get_application_rate_limit_status()['resources']['search']['/search/tweets']['remaining']&lt;5:
    if rate_limit &lt; 5:
        print 'Fewer than 5 estimated API calls remaining...pausing for 5 minutes'
        time.sleep(300) #PAUSE FOR 900 SECONDS
      
        
elapsed = timeit.default_timer() - start_time
print '# of minutes: ', elapsed/60
print "Number of new tweets added this run: ", tweets.count() - starting_count
print "Number of tweets now in DB: ", tweets.count(), '\n', '\n'   
</pre>

### Part VII: Print out Number of Tweets in Database per Account 

This final block of code will print out a summary of how many tweets there are per account in your _tweets_ database.

<pre class="brush: python; first-line: 250; light: false; title: ; toolbar: true; notranslate" title="">###### PART VII: PRINT OUT NUMBER OF TWEETS IN DATABASE FOR EACH ACCOUNT ######  

for org in db.tweets.aggregate([
    {"$group":{"_id":"$screen_name", "sum":{"$sum":1}}} 
    ]):
    print org['_id'], org['sum']
</pre>

Now let&#8217;s put the whole thing together. To recap, what this entire script does is to loop over each of the Twitter accounts in the _accounts_ table of your MongoDB database &#8212; and for each one it will grab up to 3,200 tweets and insert the tweets into the _tweets_ table of your database. 

Below is the entire script &#8212; download it and save it as _tweets.py_ (or something similar) in the same directory as your _accounts.csv_ file. Add in your Twitter API account details and you&#8217;ll be good to go! For a refresher on the different ways you can run the script see <a href="http://social-metrics.org/starting-on-python-2/" rel="noopener" target="_blank">this earlier post</a>. 

If you&#8217;ve found this post helpful please share on your favorite social media site. 

You&#8217;re on your way to downloading your own Twitter data! Happy coding!



<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>