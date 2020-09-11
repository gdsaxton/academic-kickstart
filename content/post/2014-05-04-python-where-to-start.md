---
title: 'Python: Where to Start?'
author: Gregory Saxton
type: post
date: 2014-05-04T20:17:11+00:00
url: /python-where-to-start/
featured_image: /wp-content/uploads/2014/05/6300398185_3876a65dda_b.jpg
dsq_thread_id:
  - 2660619983
categories:
  - python
tags:
  - python
  - tutorial

---
For the complete beginner, getting up and running in a new programming language can be a daunting task. I&#8217;ll try to simplify it here by walking you through the key steps. 

### Choose a version of Python

There is more than one version of the Python language. Most people choose between version 2.7 and 3.3. Go for 2.7, because some of the utilities you&#8217;ll be using won&#8217;t be readily available in the newer 3.3. 

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/05/5528275910_52c9b1ffb41.jpg"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/05/5528275910_52c9b1ffb41.jpg" alt="" width="300" height="201" class="size-full wp-image-501" srcset="http://social-metrics.org/wp-content/uploads/2014/05/5528275910_52c9b1ffb41.jpg 500w, http://social-metrics.org/wp-content/uploads/2014/05/5528275910_52c9b1ffb41-300x201.jpg 300w" sizes="(max-width: 300px) 100vw, 300px" /></a></span></span> 

Now you have to choose where to get the software. There are lots of choices. If you own a Mac, it comes with Python pre-installed. Forget about that one. For Unix, Windows, and Mac users alike I&#8217;d recommend you install <a href="https://store.continuum.io/cshop/anaconda/" target="_blank" rel="noopener noreferrer">Anaconda Python 2.7</a>. This distribution of Python is free and easy to install. Moreover, it includes most of the add-on packages necessary for scientific computing, including Numpy, Pandas, iPython, Statsmodels, Sqlalchemy, and Matplotlib.

### Familiarize Yourself with the Basics

I recommend a two-pronged learning approach: 1) familiarizing yourself with the basics of the language and 2) playing around with other people&#8217;s &#8220;recipes.&#8221; For the former, I highly recommend doing some of the many excellent tutorials now available online for learning how to use and run Python. A great place to start is <a href="http://www.codecademy.com/catalog/language/python" target="_blank" rel="noopener noreferrer">Codeacademy</a>. It takes an estimated 13 hours to complete this self-paced, 12-part interactive tutorial. Do one each day and you&#8217;ll have a basic understanding in less than two weeks. 

### Play around with code &#8212; Step 1

Python code is written in plain text files, typically given a &#8220;.py&#8221; extension. Once a script (e.g., _twitter.py_) has been written, it can then be &#8220;run&#8221; by Python and perform whichever tasks are laid out in the script. So, you&#8217;ll need to find a good program for editing these text files. On my Mac I use <a href="http://www.barebones.com/products/textwrangler/features.html" target="_blank" rel="noopener noreferrer">TextWrangler</a>. <a href="http://www.vim.org/" target="_blank" rel="noopener noreferrer">Vim</a> is popular on other machines. Your choice here is not terribly important. These programs are all generally free and easy to install. The one benefit you&#8217;ll get from these programs over say, the basic TextEdit app on the Mac is that they will highlight various elements of the Python code syntax, as in the following example, which helps in code formatting:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">def add_edge(n1, n2, weight=None):
    if not G.has_edge(n1,n2):
        G.add_edge(n1,n2)
        G[n1][n2]['weight']=1		   
    else:
        G[n1][n2]['weight']+=1       
</pre>

I would also recommend that you familiarize yourself with the <a href="http://opentechschool.github.io/python-data-intro/core/notebook.html " target="_blank" rel="noopener noreferrer">iPython Notebook</a>, which comes included with Anaconda Python. The link provides an overview of the Notebook. Simply put, it has become a boon for _interactive_ code development, that is, for &#8220;playing around&#8221; with the code. I now use the iPython Notebook for developing all of my code. In the same window it allows you to write blocks of code, run them, check whether they worked as intended and, if not, modify them. Highly recommended for learning as it allows for quick error checking. 

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/02/code-on-the-wall.jpg"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/02/code-on-the-wall.jpg" alt="Code on the Wall" width="300" height="400" class="alignnone size-full wp-image-84" srcset="http://social-metrics.org/wp-content/uploads/2014/02/code-on-the-wall.jpg 300w, http://social-metrics.org/wp-content/uploads/2014/02/code-on-the-wall-225x300.jpg 225w" sizes="(max-width: 300px) 100vw, 300px" /></a></span></span> 

### Play around with code &#8212; Step 2

This brings us to the second part of your learning strategy: playing around with other people&#8217;s code. There are lots of places to find pre-existing code. Just Google it. Just start with something simple, copy it into the iPython Notebook or Textwrangler, etc., and run it. Modify. Play around with. Try to understand it. Annotate your code to help facilitate the learning process. 

If you&#8217;re interested in the same types of questions as I am you may find some of my code useful. A good place to start, once you&#8217;ve made it through some of the CodeAcademy tutorials, is my <a href="http://social-metrics.org/python-tutorial-1/" title="Python Code Tutorial: Part I" target="_blank" rel="noopener noreferrer">Python Code Tutorial: Part I</a>.

### Ask Questions

You will run into errors. You will run into problems. You will run into roadblocks. The Web will be your friend. If you&#8217;ve checked your code, Googled error messages, and can&#8217;t find an answer, <a href="http://stackoverflow.com/" target="_blank" rel="noopener noreferrer">StackOverflow</a> will be your friend. It is likely someone has already asked the same question there. If not, ask away and you will typically get an answer the same day. Just respect the community norms and you will find StackOverflow to be a tremendously helpful resource. 

### Contribute

Python and other open-source communities only thrive through the volunteer efforts of countless individuals across the globe. They will have contributed to your learning, so once you&#8217;ve developed sufficient knowledge give back. Answer others&#8217; questions on StackOverflow. Write a tutorial on your blog. Share your code on <a href="http://github.com/" target="_blank" rel="noopener noreferrer">Github</a>. 

### Step-by-Step Tutorial

I&#8217;ve also just begun a series of <a href="http://social-metrics.org/starting-on-python-1/" title="Your First Steps with Python: Part I — Running your First Python Code" target="_blank" rel="noopener noreferrer">step-by-step tutorials</a> to walk you through installing Python and running you first code. Take a look if you&#8217;re interested, and please share this on social media if you know others who may be interested. 

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>