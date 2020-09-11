---
title: Random Python Recipes
author: Gregory Saxton
type: post
date: 2015-04-26T16:44:11+00:00
url: /random-python-recipes/
featured_image: /wp-content/uploads/2014/02/1159613_85120857.jpg
categories:
  - python
tags:
  - python

---
This page is mostly for me as a handy reference for all those Python commands I tend to forget. That said, if it proves helpful to any others, all the better!

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    Contents
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Lists"><span class="toc_number toc_depth_1">1</span> Lists</a>
    </li>
    <li>
      <a href="#Dictionaries"><span class="toc_number toc_depth_1">2</span> Dictionaries</a>
    </li>
    <li>
      <a href="#Regular_Expressions"><span class="toc_number toc_depth_1">3</span> Regular Expressions</a>
    </li>
    <li>
      <a href="#Miscellaneous"><span class="toc_number toc_depth_1">4</span> Miscellaneous</a>
    </li>
  </ul>
</div>

## <span id="Lists">Lists</span>

Create list by slicing items of another list:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">b = [x[:8] for x in cusips_compustat]</pre>

Combine two lists into a dictionary:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">dict(zip([1,2,3,4], [a,b,c,d]))</pre>

Get list of all files in a directory:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">filenames = next(os.walk(directory_name))[2]</pre>

Find items in one list that are not in another:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">a = [some list]
b = [another list]
c = []
for bx in b:
    if bx not in a:
        c.append(bx)
if c:
    print "these are the list elements of b not present in a:", c
else:
     print "no elements of list b are not in list a"</pre>

<div style="margin-bottom:5em;">
  <span style="display:none;">.</span>
</div>

## <span id="Dictionaries">Dictionaries</span>

Merge two dictionaries (same keys in both dictionaries):

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">d1 = nx.betweenness_centrality(G)
d2 = nx.degree_centrality(G)
finaldict = {key:(d1[key], d2[key]) for key in d1}</pre>

Same as above, but values as list instead of tuple:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">finaldict = {key:[d1[key], d2[key]] for key in d1}</pre>

For converting to a PANDAS dataframe, you would normally want something like this &#8212; create a dictionary of dictionaries and add keys:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">finaldict = {key:{'degree': d2[key], 'betweenness': d1[key]} for key in d2}</pre>

To convert the above dictionary to a dataframe:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">df = pd.DataFrame.from_dict(finaldict, orient='index')</pre>

And you would want this if you are building a dictionary with more than one month:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">finaldict = {key:{month:{'degree': D2[key], 'betweenness': d1[key]}} for key in d2}</pre>

To merge the above nested dictionary, you have to do something more complicated to convert to a DF:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">ticks = []
frames = []
for i, d in finaldict.iteritems():
     ticks.append(i)
     frames.append(pd.DataFrame.from_dict(d, orient='index'))
df = pd.concat(frames, keys=ticks)</pre>

Sort dictionary by keys:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">for key in sorted(mydict.iterkeys()):
    print "%s: %s" % (key, mydict[key])
</pre>

Sort dictionary by numerical values:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">for key, value in sorted(mydict.iteritems(), key=lambda (k,v): (v,k), reverse=True):
    print "%s: %s" % (key, value)
</pre>

<div style="margin-bottom:5em;">
  <span style="display:none;">.</span>
</div>

## <span id="Regular_Expressions">Regular Expressions</span>

Find all instances of text in string starting with &#8216;Item &#8216;:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">itemx = soup(text=re.compile('Item '))</pre>

Find all instances of text that start with &#8216;Item &#8216; plus any number(s) then &#8216;.&#8217; then any number(s):

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">match = re.search('Item (\d+).(\d+)', data)
#match = re.search('Item (\d+).(\d+)', data, re.IGNORECASE) #case-insensitive search
if match:
    item = match.group()
</pre>

<div style="margin-bottom:5em;">
  <span style="display:none;">.</span>
</div>

## <span id="Miscellaneous">Miscellaneous</span>

Loop over directory and find and open specific file:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">indir = '/Users/BobSmith/Documents/SEC filings'
for root, dirs, filenames in os.walk(indir):
    for f in filenames:
        if f == '8-K.htm':
            file = indir+'/'+f
            data = open(os.path.join(root, f), 'r').read()
</pre>

Rename a file:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">import os
os.rename(dir_name+old_filename, dir_name+new_filename)
</pre>

<div style="margin-bottom:5em;">
  <span style="display:none;">.</span>
</div>

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>