---
title: 'Your First Steps with Python: Part I — Running your First Python Code'
author: Gregory Saxton
type: post
date: 2014-09-04T00:50:48+00:00
url: /starting-on-python-1/
dsq_thread_id:
  - 6565774975
categories:
  - python
tags:
  - python
  - tutorial

---
For the beginning coder, every step involved in getting up and running the programming language presents a new (and potentially frustrating) learning experience. In a <a href="http://social-metrics.org/python-where-to-start/" title="Python: Where to Start?" target="_blank">prior post</a> I gave an overview of my preferred Python distributions and my general thoughts on how to approach learning Python. In this and subsequent posts I will walk you through some of the concrete first steps involved in actually using Python. 

I am assuming you are using a Mac (slightly different instructions for PC or Linux) and that you are interested in developing code especially for processing social media data. Most of the steps are generalizable to other applications, but I&#8217;m tailoring the instructions to those who wish to run my code. 

### Step One: Download and Install Python

For Unix, Windows, and Mac users alike I recommend you install <a href="https://store.continuum.io/cshop/anaconda/" target="_blank">Anaconda Python 2.7</a>. This distribution of Python is free and easy to install. Moreover, it includes most of the add-on packages necessary for scientific computing, including Numpy, Pandas, iPython, Statsmodels, Sqlalchemy, and Matplotlib.

So, download the software. Double-click on it and run the software. Easy as that! 

### Step Two: Verify Anaconda is Now Default Version of Python

To use Python you will occasionally have to do something in the <a href="http://en.wikipedia.org/wiki/Terminal_(OS_X)" target="_blank">Terminal</a>. The Terminal provides a text-based interface to your computer&#8217;s operating system and is necessary for certain permissions changes, etc. If this is your first programming experience you may not even know it&#8217;s there. Now that you know, you may wish to you keep Terminal in the Dock to keep it handy. 

Open _/Applications/Utilities/Terminal.app_ and find out which version of Python is the default by typing in `which python` at the `$` command prompt. It should look like the screenshot you see below. What you should get back is some indication that Anaconda Python is the default Python installation on your computer, such as `//anaconda/bin/python`

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.46.46-PM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.46.46-PM.png" alt="Screen Shot 2014-09-03 at 4.46.46 PM" width="507" height="367"  class="alignnone size-full wp-image-621" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.46.46-PM.png 507w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.46.46-PM-300x217.png 300w" sizes="(max-width: 507px) 100vw, 507px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

### Step Three: Verify Python is working

Start Python by typing in `python` at the `$` command prompt. You should see some language letting you know which version of Python has started and then a `>>>` command prompt. This is the prompt for you to enter Python code. Below I&#8217;ve included a screenshot of what this looks like on my device.

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.51.12-PM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.51.12-PM.png" alt="Screen Shot 2014-09-03 at 4.51.12 PM" width="507" height="367" class="alignnone size-full wp-image-626" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.51.12-PM.png 507w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.51.12-PM-300x217.png 300w" sizes="(max-width: 507px) 100vw, 507px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

### Step Four: Type in Some Code

Let&#8217;s type in the typical first command of a programmer, `print "Hello, world!"` and hit enter. The expected output, &#8220;Hello world&#8221;, is seen in the following screenshot.

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png" alt="Screen Shot 2014-09-03 at 4.55.22 PM" width="505" height="367" class="alignnone size-full wp-image-629" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png 505w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM-300x218.png 300w" sizes="(max-width: 505px) 100vw, 505px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div> You&#8217;ve just executed your first Python command! </p> 

Note that this is just one way of running your code. Specifically, when you&#8217;re typing in commands in the Terminal you are working in the _interactive_ mode. Your code is not saved, and thus the interactive mode is used only for simple tests. In the next tutorial I will walk you through two more powerful ways of creating and running Python code.

If you have found this helpful please share it, and I always welcome feedback. 

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>