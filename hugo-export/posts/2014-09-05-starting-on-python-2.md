---
title: 'Your First Steps with Python: Part II — Four Ways to Run your Code'
author: Gregory Saxton
type: post
date: 2014-09-05T07:13:20+00:00
url: /starting-on-python-2/
dsq_thread_id:
  - 6565774980
categories:
  - python
tags:
  - python
  - tutorial

---
This is the second in a series of posts to get you up and running on Python. In the <a href="http://social-metrics.org/starting-on-python-1/" title="Starting with Python" target="_blank">first post </a> I showed you which version of Python to install, how to check that the installation succeeded, and how to type in and run your first simple Python command. 

In this tutorial I will show you four different ways of writing and running your code. For simplicity&#8217;s sake, each of these four methods will run the same <a href="http://en.wikipedia.org/wiki/%22Hello,_world!%22_program" target="_blank">typical beginners&#8217; &#8220;Hello, world!&#8221; code</a>. For the purposes of the tutorial I am assuming you are using a Mac. Instructions will vary slightly for PC or Linux.

### Method One: Interactive Mode

The most basic way to run code is to enter and run lines of code in the Terminal. This was covered in <a href="http://social-metrics.org/starting-on-python-1/" title="Your First Steps with Python: Part I — Running your First Python Code" target="_blank">Part I</a> of the tutorial series. To recap, open _/Applications/Utilities/Terminal.app_, start Python by typing in `python` at the `$` command prompt, type in `print "Hello, world!"` and hit enter. The expected output, &#8220;Hello world&#8221;, is seen in the below screenshot.

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png" alt="Screen Shot 2014-09-03 at 4.55.22 PM" width="505" height="367" class="alignnone size-full wp-image-629" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM.png 505w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-03-at-4.55.22-PM-300x218.png 300w" sizes="(max-width: 505px) 100vw, 505px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div> This 

_interactive_ mode works, but is really only helpful for basic coding. Your code isn&#8217;t saved, so you&#8217;ll want want to take a different approach.</p> 

### Method 2: Running Python from a Code-Friendly Text Interpreter

Python code is written in plain text files, typically given a &#8220;.py&#8221; extension. Once a script (e.g., _twitter.py_) has been written, it can then be &#8220;run&#8221; by Python and perform whichever tasks are laid out in the script. So, you&#8217;ll need to find a good program for editing these text files. On my Mac I use <a href="http://www.barebones.com/products/textwrangler/features.html" target="_blank">TextWrangler</a>. <a href="http://www.vim.org/" target="_blank">Vim</a> is popular on other machines. Your choice here is not terribly important. These programs are all generally free and easy to install. One benefit you&#8217;ll get from these programs over say, the basic TextEdit app on the Mac is that they will highlight various elements of the Python code syntax, which helps in code formatting. Running the code is also easier through these specialized programs. Let&#8217;s say you download and install TextWrangler and enter your code. This is what is might look like. 

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-04-at-7.13.03-PM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-04-at-7.13.03-PM.png" alt="Screen Shot 2014-09-04 at 7.13.03 PM" width="1147" height="317" class="alignnone size-full wp-image-715" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-04-at-7.13.03-PM.png 1147w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-04-at-7.13.03-PM-300x82.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-04-at-7.13.03-PM-1024x283.png 1024w" sizes="(max-width: 1147px) 100vw, 1147px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div> The first line in the code is the 

<a href="http://en.wikipedia.org/wiki/Shebang_(Unix)" target="_blank">shebang</a> &#8212; you&#8217;ll find this in all your Python scripts.</p> 

Lines 3 &#8211; 8 contain the <a href="http://legacy.python.org/dev/peps/pep-0257/" target="_blank">docstring</a> &#8212; also a Python convention. This is a multi-line comment demarcated by the docstrings `"""` that describes the code. Write whatever is helpful to you as well as anyone who might use your script in the future. For single-line comments, use the _#_ symbol at the start of the line. 

Line 10 contains the python code

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">print "Hello, world!"
</pre>

OK, so you have written and saved your code in a file called `hello_world.py`. You can now run your code through TextWrangler and other text interpreters. Go to the `#!` menu and select &#8220;Run in Terminal&#8221; as in the following screenshot.

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.24.18-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.24.18-AM.png" alt="Screen Shot 2014-09-05 at 2.24.18 AM" width="1440" height="900" class="alignnone size-full wp-image-732" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.24.18-AM.png 1440w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.24.18-AM-300x187.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.24.18-AM-1024x640.png 1024w" sizes="(max-width: 1440px) 100vw, 1440px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div> What happens is that the Terminal will open another window and run your code. Below you&#8217;ll see the output on my MacBook Pro.</p> 

<div class="su-spacer" style="height:20px">
</div>

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.21.14-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.21.14-AM.png" alt="Screen Shot 2014-09-05 at 2.21.14 AM" width="814" height="357" class="alignnone size-full wp-image-730" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.21.14-AM.png 814w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.21.14-AM-300x131.png 300w" sizes="(max-width: 814px) 100vw, 814px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

### Method 3: Running a Python Script in the Terminal

You don&#8217;t want to do it this way. If you want to run your scripts, use Method 2 instead. But I&#8217;ll show you quickly just so you know it&#8217;s possible. Open up a Terminal window. Let&#8217;s say you saved your script with the name `hello_world.py` in your `Documents` folder. Navigate to the Documents folder by typing in `cd Documents` and hit enter. Then to run your code type in `python hello_world.py` and hit enter. Your code will run and you&#8217;ll see the output as shown below. 

<span class="su-frame su-frame-align-left su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.47.46-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.47.46-AM.png" alt="Screen Shot 2014-09-05 at 2.47.46 AM" width="507" height="144" class="alignnone size-full wp-image-739" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.47.46-AM.png 507w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.47.46-AM-300x85.png 300w" sizes="(max-width: 507px) 100vw, 507px" /></a><br /> </span></span> 

<div class="su-spacer" style="height:20px">
</div>

### Method 4: iPython Notebook

This is the preferred way for running your code. I recommend that you familiarize yourself with the <a href="http://opentechschool.github.io/python-data-intro/core/notebook.html " target="_blank">iPython Notebook</a>, which comes included with Anaconda Python. The link provides an overview of the Notebook. Simply put, it has become a boon for _interactive_ code development, that is, for &#8220;playing around&#8221; with the code. I now use the iPython Notebook for developing all of my code. In the same window it allows you to write blocks of code, run them, check whether they worked as intended and, if not, modify them. Highly recommended for learning as it allows for quick error checking. Annotation of your code is also facilitated.

Here is what you&#8217;ll do. Open up the Terminal and type in `ipython notebook`. 

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.57.31-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.57.31-AM.png" alt="Screen Shot 2014-09-05 at 2.57.31 AM" width="753" height="305" class="alignnone size-full wp-image-746" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.57.31-AM.png 753w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.57.31-AM-300x121.png 300w" sizes="(max-width: 753px) 100vw, 753px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

You&#8217;ll see some lines of script running in your Terminal window indicating that the Notebook app is running. Wait a few seconds, and a browser window will open. This is your iPython Notebook interface. It will show all available _notebooks_, which are just fancy Python scripts you&#8217;ve developed in iPython. An example is below.

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.00-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.00-AM.png" alt="Screen Shot 2014-09-05 at 2.51.00 AM" width="1434" height="422" class="alignnone size-full wp-image-741" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.00-AM.png 1434w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.00-AM-300x88.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.00-AM-1024x301.png 1024w" sizes="(max-width: 1434px) 100vw, 1434px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

Hit _New Notebook_ and another browser window will open. This is where you will type in your `print "Hello, world!"` code in the first cell, as shown below. 

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.33-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.33-AM.png" alt="Screen Shot 2014-09-05 at 2.51.33 AM" width="1435" height="295" class="alignnone size-full wp-image-742" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.33-AM.png 1435w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.33-AM-300x61.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.33-AM-1024x210.png 1024w" sizes="(max-width: 1435px) 100vw, 1435px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div> In iPython you can run each block of code, or cell, individually. Put your cursor anywhere in the first cell and hit 

`Shift enter`. You code will run. See below.</p> <span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.44-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.44-AM.png" alt="Screen Shot 2014-09-05 at 2.51.44 AM" width="1431" height="320" class="alignnone size-full wp-image-743" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.44-AM.png 1431w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.44-AM-300x67.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-2.51.44-AM-1024x228.png 1024w" sizes="(max-width: 1431px) 100vw, 1431px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

One final step remains. You&#8217;ll want to rename and save your new notebook for future use. Click on &#8216;Untitled0&#8217; and a dialogue box will open like you see below. 

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.18-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.18-AM.png" alt="Screen Shot 2014-09-05 at 3.06.18 AM" width="1433" height="440" class="alignnone size-full wp-image-750" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.18-AM.png 1433w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.18-AM-300x92.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.18-AM-1024x314.png 1024w" sizes="(max-width: 1433px) 100vw, 1433px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

Type in `hello_world` and hit OK and you&#8217;ll see that the code has been saved.

<span class="su-frame su-frame-align-right su-frame-style-default"><span class="su-frame-inner"><a href="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.34-AM.png"><img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.34-AM.png" alt="Screen Shot 2014-09-05 at 3.06.34 AM" width="1430" height="321" class="alignnone size-full wp-image-751" srcset="http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.34-AM.png 1430w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.34-AM-300x67.png 300w, http://social-metrics.org/wp-content/uploads/2014/09/Screen-Shot-2014-09-05-at-3.06.34-AM-1024x229.png 1024w" sizes="(max-width: 1430px) 100vw, 1430px" /></a></span></span> 

<div class="su-spacer" style="height:20px">
</div>

Et voila! You now know 4 different ways of running Python code. In general, you won&#8217;t want to do methods 1 (interactive mode in the Terminal) or 3 (run scripts through Terminal). You may wish to use Method 2 from time to time by typing up entire scripts in TextWrangler, but that&#8217;s a topic for another day. Until you learn a bit more, concentrate on the last method and do your coding in the iPython Notebook. 

Happy coding! 

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>