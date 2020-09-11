---
title: Levels of Analysis in Big Data
author: Gregory Saxton
type: post
date: 2015-05-26T00:52:53+00:00
url: /levels-of-analysis-in-big-data/
featured_image: /wp-content/uploads/2015/05/Big-Data.jpg
categories:
  - Big Data
  - python
  - research
  - Twitter
tags:
  - Big Data
  - social media
  - Twitter

---
[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg" alt="Big Data" width="1024" height="500" class="alignnone size-full wp-image-1327" srcset="http://social-metrics.org/wp-content/uploads/2015/05/Big-Data.jpg 1024w, http://social-metrics.org/wp-content/uploads/2015/05/Big-Data-300x146.jpg 300w" sizes="(max-width: 1024px) 100vw, 1024px" />][1]

So you want to download &#8220;Big Data.&#8221; You could be a social scientist wanting to take your first stab at downloading and analyzing 100 organizations&#8217; worth of tweets. Or a marketing or public relations practitioner interested in analyzing Facebook or Instagram or Pinterest YouTube activity by your competitors. Or a budding data scientist interested in getting your toes wet and doing your first Big Data download.

This post is the first in a series designed to help you understand at a conceptual level the main moving parts you&#8217;ll have to grasp in order to successfully get the data you need. This one deals with _levels of analysis_ in Big Data. It is critical to have a basic understanding of this concept if you are to understand how to correctly get the data you need.

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

In line with what I&#8217;ve noted earlier, you can access all of the above account-level data through a specific portion of the Twitter application programming interface (API). Specifically, the _users/lookup_ part of the Twitter API allows for the bulk downloading of Twitter user information. You can see a <a href="https://dev.twitter.com/docs/api/1.1/get/users/lookup" target="_blank">description of this part of the API here</a>, along with definitions for the <a href="https://dev.twitter.com/docs/platform-objects/users" target="_blank">variables returned</a>. For an overview of how to gather such data, take a look at <a href="http://social-metrics.org/twitter-user-data/" target="_blank">this tutorial</a> I&#8217;ve written.

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