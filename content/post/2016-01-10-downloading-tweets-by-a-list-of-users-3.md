---
title: Downloading Tweets by a List of Users (copy)
author: Gregory Saxton
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1497
categories:
  - python
  - Twitter

---
This post is a brief, temporary attempt at pointing people in the right direction for a common task: downloading tweets sent by a number of different Twitter users. It is directed at those who are new to Python and/or downloading data from the Twitter API. 

OK, so I am assuming you have made it through (or intend to) the following tutorials, which should help you get set up and working with Python:

  * <a href="http://social-metrics.org/python-where-to-start/" target="_blank">Which version of Python to download</a>
  * <a href="http://social-metrics.org/starting-on-python-1/" target="_blank">Running your first code</a>
  * <a href="http://social-metrics.org/starting-on-python-2/" target="_blank">Four ways to run your code</a>

Another detailed tutorial I have created, <a href="http://social-metrics.org/python-tutorial-1/" target="_blank">Python Code Tutorial</a>, is intended to serve as an introduction to how to access the Twitter API and then read the JSON data that is returned. This gets you the account-level data for a Twitter user (such as when the account was created), but not the actual tweets. That is a more difficult process, but not a huge leap once you&#8217;ve made it through all of the above steps. 

I have yet to upload a tutorial showing how to use my code to download tweets by a list of Twitter users, but fortunately my PhD student Wayne Xu has. <a href="http://curiositybits.com/python-for-mining-the-social-web/python-tutorial-five-steps-to-collect-tweets-sent-by-a-list-of-users/" target="_blank">This tutorial</a> helps fill in the blanks. It will help walk you through the steps of getting a Twitter developer account (so you can access the API), of which database to use (SQLite), and then how to access and store data from the Twitter user_timeline API, which allows you to download up to the last 3,200 tweets sent by each Twitter user. 

I hope this helps. Happy coding!

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>