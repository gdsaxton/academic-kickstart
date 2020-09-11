---
title: Python PANDAS Code Bytes
author: Gregory Saxton
type: post
date: 2018-03-24T20:01:20+00:00
url: /python-data-analytics-code-bytes/
featured_image: /wp-content/uploads/2015/05/16042948632_433f02b708_o.jpg
categories:
  - Big Data
  - Data Analytics
  - jupyter_notebook
  - pandas
  - research
  - Twitter
tags:
  - Big Data
  - Data Analytics
  - PANDAS
  - python

---
This page contains brief (generally one-liner) blocks of code for working with Python and <a href="http://pandas.pydata.org/" target="_blank">PANDAS</a> for data analytics. I created it as a handy reference for PANDAS commands I tended to forget when I was learning. I hope it proves useful to you, too! I also have a page with longer <a href="http://social-metrics.org/python-data-analytics-tutorials/" rel="noopener" target="_blank">data analytics tutorials</a>. 

##### Table of Contents<div id="toc\_container" class="no\_bullets" padding-top:0px> 

<!--

<div class="border-box-transparent-bytes"> -->

  


<div class='content-column one_half'>
  <ul class="toc_list">
    <li>
      <a href="#Jupyter_Notebook_Settings"><span class="toc_number toc_depth_1"></span> Jupyter Notebook Settings</a>
    </li>
    <li>
      <a href="#Working_with_Python_Lists"><span class="toc_number toc_depth_1"></span> Working with Python Lists</a>
    </li>
    <li>
      <a href="#Working_with_Python_Dictionaries"><span class="toc_number toc_depth_1"></span> Working with Python Dictionaries</a>
    </li>
    <li>
      <a href="#Analysis"><span class="toc_number toc_depth_1"></span> Analysis</a>
    </li>
    <li>
      <a href="#Generating_New_Variables_Arrays_etc"><span class="toc_number toc_depth_1"></span> Generating New Variables, Arrays, etc.</a>
    </li>
    <li>
      <a href="#IO"><span class="toc_number toc_depth_1"></span> I/O</a>
    </li>
    <li>
      <a href="#Looping"><span class="toc_number toc_depth_1"></span> Looping</a>
    </li>
  </ul>
</div>

<div class='content-column one_half last_column'>
  <ul class="toc_list">
    <li>
      <a href="#Time_Series"><span class="toc_number toc_depth_1"></span> Time Series</a>
    </li>
    <li>
      <a href="#Indexing_and_Sorting"><span class="toc_number toc_depth_1"></span> Indexing and Sorting</a>
    </li>
    <li>
      <a href="#Missing_Data"><span class="toc_number toc_depth_1"></span> Missing Data</a>
    </li>
    <li>
      <a href="#Custom_Functions"><span class="toc_number toc_depth_1"></span> Custom Functions</a>
    </li>
    <li>
      <a href="#DataFrame_Manipulations"><span class="toc_number toc_depth_1"></span> DataFrame Manipulations</a>
    </li>
    <li>
      <a href="#Custom_Twitter_Variables"><span class="toc_number toc_depth_1"></span> Custom Twitter Variables</a>
    </li>
    <li>
      <a href="#Mongo_DB"><span class="toc_number toc_depth_1"></span> Working with MongoDB in Python</a>
    </li>
  </ul>
</div>

<div class='clear_column'>
</div></p></div> 



## <span id="Jupyter_Notebook_Settings">Jupyter Notebook Settings</span> {#Jupyter_Notebook_Settings}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Set width of columns for display:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">'display.max_columns'</span><span class="p">,</span> <span class="bp">None</span><span class="p">)</span>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Set cell width:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s1">'max_colwidth'</span><span class="p">,</span> <span class="bp">150</span><span class="p">)</span>
      </div>
    </div>
  </div>
</div>



## <span id="Working_with_Python_Lists">Working with Python Lists</span> {#Working_with_Python_Lists}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Break list into chunks of 4 (needed for some APIs, for example)
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="n">mylist_chunked</span> <span class="o">=</span> <span class="p">[</span><span class="n">mylist</span><span class="p">[</span><span class="n">i</span><span class="p">:</span><span class="n">i</span><span class="o">+</span><span class="mi">4</span><span class="p">]</span> <span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">xrange</span><span class="p">(</span><span class="mi"></span><span class="p">,</span> <span class="nb">len</span><span class="p">(</span><span class="n">mylist</span><span class="p">),</span> <span class="mi">4</span><span class="p">)]</span>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Finding duplicates in a list:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="kn">import</span> <span class="nn">collections</span><br /> <span class="n">mylist = [</span><span class="s1">'twitter', 'facebook','instagram', 'twitter'</span><span class="n">]</span><br /> <span class="n">[item</span> <span class="kn">for</span> <span class="n">item, count</span> <span class="kn">in</span> <span class="n">collections.Counter(mylist).items()</span> <span class="kn">if</span> <span class="n">count</span><span class="o"> > </span><span class="mi">1</span><span class="n">]</span>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Remove list element:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="n">mylist</span><span class="o">.</span><span class="n">remove</span><span class="p">(</span><span class="s1">'revenue'</span><span class="p">)</span>
      </div>
    </div>
  </div>
</div>



## <span id="Working_with_Python_Dictionaries">Working with Python Dictionaries</span> {#Working_with_Python_Dictionaries}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Delete a key from a dictionary:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span class="k">del</span> <span class="nb">dict</span><span class="p">[</span><span class="n">key</span><span class="p">][</span><span class="s1">'key_to_delete'</span><span class="p">]</span>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create sub-dictionary (from sub-set of keys):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span></span><span class="n">subdict</span> <span class="o">=</span> <span class="p">{</span><span class="n">k</span><span class="p">:</span> <span class="nb">dict</span><span class="p">[</span><span class="n">k</span><span class="p">]</span> <span class="k">for</span> <span class="n">k</span> <span class="ow">in</span> <span class="p">(</span><span class="s1">'key1'</span><span class="p">,</span> <span class="s1">'key2'</span><span class="p">)}</span>
      </div>
    </div>
  </div>
</div>

## <span id="Analysis">Analysis</span> {#Analysis}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Cross-tabulation:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class=" highlight2">
        <span></span><span class="n">pd</span><span class="o">.</span><span class="n">crosstab</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="s1">'var1'</span><span class="p">],</span> <span class="n">df</span><span class="p">[</span><span class="s1">'var2'</span><span class="p">])</span>
      </div>
    </div>
  </div>
</div>



## <span id="Generating_New_Variables_Arrays_etc">Generating New Variables, Arrays, etc.</span> {#Generating_New_Variables_Arrays_etc}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create list from dataframe column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        screen_names = df[<span class="s1">&#8216;screen_name&#8217;</span>].tolist()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create list of unique column values in DF:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        tickers_in_df = pd.unique(df.ticker.ravel()).tolist()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Convert string variable to float:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;count_V2&#8217;] = df[&#8216;count&#8217;].convert_objects(convert_numeric=True)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Convert float column to int (only works if there are no missing values):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_2014[<span class="s1">&#8216;rt_count&#8217;</span>] = df_2014[<span class="s1">&#8216;rt_count&#8217;</span>].astype(int)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Convert column to string:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.index = df.index.astype(str)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create new variable as a slice of an existing one:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;cusip8&#8217;] = df[&#8216;cusip&#8217;].apply(lambda x: x[:8])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Replace a word <i>within</i> a column with another word:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;8-K&#8217;] = df[&#8216;8-K&#8217;].str.replace(&#8216;Item&#8217;, &#8216;Section&#8217;)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Fill in missing values for one column with zero:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_2014[<span class="s1">&#8216;rt_count&#8217;</span>] = df_2014[<span class="s1">&#8216;rt_count&#8217;</span>].fillna(<span class="m1"></span>)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Get new list of unique items in a list:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        screen_names_unique = list(set(screen_names))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create dummy variable based on whether another column contains specific text (values will be 'True' and 'False'):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;retweeted_status_dummy&#8217;] = df[&#8216;retweeted_status&#8217;].str.contains(&#8216;THIS&#8217;, na=False)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Then convert to float (will convert 'True' and 'False' categories of above variable into '1' and '0', respectively):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;retweeted_status_dummy&#8217;] = df[&#8216;retweeted_status_dummy&#8217;].astype(float)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Replace values (here, replace 'None' with '0'):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;reply_message&#8217;] = df[&#8216;in_reply_to_screen_name&#8217;].replace([None], [&#8216;0&#8217;])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Replace values (here, replace np.nan values with '0'):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.ix[df.Number_of_retweets.isnull(), &#8216;Number_of_retweets&#8217;] = 0
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Switch values of '0' and '1':
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;reply_message&#8217;] = df[&#8216;reply_message&#8217;].replace([1], [99]).replace([0],[1]).replace([99],[0])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create binary variable from count variable (if old var=0, assign value of 0; otherwise 1):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;urls&#8217;] = np.where(df[&#8216;entities_urls_count&#8217;]==0, 0, 1)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Change each unicode element in a list to string:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        tickers_in_df = [x.encode(&#8216;UTF8&#8217;) for x in tickers_in_df]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Change column values to upper case:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;Name&#8217;] = df[&#8216;Name&#8217;].apply(lambda x: x.upper())
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Change column values to upper case:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        sec[&#8216;8-K Item&#8217;] = sec[&#8216;8-K Item&#8217;].str.upper()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Find number of unique values:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        len(pd.unique(compustat_2013.cusip.ravel()))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Add leading zeros to string variable (as many as needed to reach 10 characters):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;cik_x&#8217;] = df[&#8216;cik_x&#8217;].apply(lambda x: x.zfill(10))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Convert column to string and add leading zeros:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;CIK_10&#8217;] = df[&#8216;CIK&#8217;].astype(str).apply(lambda x: x.zfill(10))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Get a list of values from a DF column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        values_list = df[&#8216;8-K&#8217;].value_counts().keys().tolist()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Find number of cases with fewer than the mean value:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        sum(df[&#8216;followers_count&#8217;] < df['followers_count'].mean())
      </div>
    </div>
  </div>
</div>



## <span id="IO">I/O</span> {#IO}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Read in a pickled dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        ticker_master = pd.read_pickle(&#8216;valid_tickers_317.pkl&#8217;)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Read in JSON file:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        f = open(&#8216;valid_tickers_list_317.json&#8217;, &#8216;r&#8217;)<br /> valid_tickers = simplejson.load(f)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Read in JSON file -- method 2:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        with open(&#8216;my_list.json&#8217;, &#8216;r&#8217;) as fp:<br /> &nbsp; &nbsp; my_list = json.load(fp)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Save a list as JSON file:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        f = open(&#8216;all_valid_screen_names.json&#8217;, &#8216;w&#8217;)<br /> simplejson.dump(valid_twitter_accounts, f)<br /> f.close()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Save a list as JSON file -- method 2:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      import json</p> 
      
      <div class="highlight2">
        with open(&#8216;my_list.json&#8217;, &#8216;w&#8217;) as fp:<br /> &nbsp; &nbsp; json.dump(my_list, fp)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Read in Excel file:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        twitter_accounts = pd.read_excel(&#8216;Twitter Account-level Database &#8212; non-excluded tickers and accounts only.xlsx&#8217;, &#8216;accounts&#8217;, header=0)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Write Excel file:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.to_excel(&#8216;df.xls&#8217;, sheet_name=&#8217;Sheet1&#8242;)
      </div>
    </div>
  </div>
</div>



## <span id="Looping">Looping</span> {#Looping}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Looping over rows (note how to select a slice of rows):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for index, row in df[:10].iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; print index, row[&#8216;content&#8217;]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Loop over rows and update existing variable:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; df[&#8216;count&#8217;] = count
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Loop over rows and create new variable, method 1:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; #df.ix[df.index==index, &#8216;count&#8217;] = count #LONGER VERSION<br /> &nbsp; &nbsp; &nbsp; &nbsp; df.ix[index, &#8216;count&#8217;] = count #SHORTER VERSION
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Loop over rows and create new variable, method 2:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; df.loc[index,&#8217;count&#8217;] = count
      </div>
    </div>
  </div>
</div>



## <span id="Time_Series">Time Series</span> {#Time_Series}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Weekdays:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        weekdays_only = by_day2[by_day2[&#8216;weekday&#8217;] < 5 ] weekday_count = df.groupby(ts.index.weekday).apply(f) by_day3['weekday'] = by_day['date'].apply(lambda x: x.weekday())
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Add missing days (with zeros) for every day in a dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_filled = df.unstack().fillna(0).stack()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Change specific columns
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_filled.loc[df_filled[&#8216;Number of Firm Tweets&#8217;] == 0, [&#8216;Number of Firm Followers (start)&#8217;, &#8216;Number of Lists for Firm (start)&#8217;]] = np.nan
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Set column to datetime:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;created_at&#8217;] = pd.to_datetime(df[&#8216;created_at&#8217;])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Convert datetime column to date:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;date&#8217;] = [t.date() for t in df[&#8216;datetime&#8217;]]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Generate lagged variable with multi-index DF:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;Mentions [t-1]&#8217;] = df[&#8216;Mentions&#8217;].unstack().shift(1).stack()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Generate variable aggregated over 3-day window lagged one day:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;Mentions [sum of t-1:t-3]&#8217;] = pd.rolling_sum(df[&#8216;Mentions&#8217;].unstack().shift(), window=3).stack()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Select date range for DF:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_2014 = df[&#8216;2014-1-1&#8242;:&#8217;2014-12-31&#8217;]
      </div>
    </div>
  </div>
</div>



## <span id="Indexing_and_Sorting">Indexing and Sorting</span> {#Indexing_and_Sorting}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Set the index:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df = df.set_index([&#8216;created_at&#8217;])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Reset Index:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.reset_index(inplace=True)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Set Multi-Index:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df = df.set_index([&#8216;ticker&#8217;, &#8216;day&#8217;])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Sort dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.sort([&#8216;ticker&#8217;, &#8216;day&#8217;], inplace=True)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Name Existing Multi-index columns:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.index.names = [&#8216;day&#8217;, &#8216;ticker&#8217;]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>With multi-index df -- get unique items per index level:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        len(firm_day_counts_firm_tweets.index.levels[0])<br /> len(firm_day_counts_firm_tweets.index.levels[1])
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Swap levels on multi-index dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df_swapped = df.swaplevel(&#8216;ticker&#8217;, &#8216;day&#8217;)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Get minimum date in DF:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.index.min()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Complex conditional row selection during loop:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        if (row[&#8216;Form Type&#8217;] == &#8216;8-K&#8217;) and (row[&#8216;8-K Item&#8217;]==&#8221;) and (row[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;) or (row[&#8216;8-K Item&#8217;]==&#8217;Item that&#8217;) or (row[&#8216;8-K Item&#8217;]==&#8217;Item fo&#8217;):
      </div>
    </div>
  </div>
</div>

## <span id="Missing_Data">Missing Data</span> {#Missing_Data}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Interpolation with backfill and forward fill (n.b. - does not respect multi-index):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[&#8216;F_x)&#8217;]=df[&#8216;F&#8217;].interpolate(method=&#8217;linear&#8217;).bfill().ffill()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Find rows with empty column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        missing = df[df[&#8216;ticker&#8217;].isnull()]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Fill missing values in one column with values from another column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        sec.loc[sec[&#8216;8-K Item_v2&#8242;].isnull(),&#8217;8-K Item_v2&#8217;] = sec[&#8216;8-K Item&#8217;]
      </div>
    </div>
  </div>
</div>

## <span id="Custom_Functions">Custom Functions</span> {#Custom_Functions}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Function for generating a series of new one-day lag variables in a dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        def lag_one_day(df):<br /> &nbsp; &nbsp; #df_cols = df.columns<br /> &nbsp; &nbsp; df_cols = [u&#8217;Number of Firm Mentions&#8217;, u&#8217;Number of Firm Tweets&#8217;] &nbsp; &nbsp; for i in df_cols:<br /> &nbsp; &nbsp; &nbsp; &nbsp; col = str(i)+str(&#8216;[t-1]&#8217;)<br /> &nbsp; &nbsp; &nbsp; &nbsp; if &#8216;[t-1]&#8217; not in str(i):<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; df[col] = df[i].unstack().shift(1).stack()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Function for generating a series of new dataframe variables that aggregate over a multi-day period:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        def lag_one_day(df):<br /> &nbsp; &nbsp; #df_cols = df.columns<br /> &nbsp; &nbsp; df_cols = [u&#8217;Number of Firm Mentions&#8217;, u&#8217;Number of Firm Tweets&#8217;] &nbsp; &nbsp; for i in df_cols:<br /> &nbsp; &nbsp; &nbsp; &nbsp; col = str(i)+str(&#8216;[sum t-1:t-3]&#8217;)<br /> &nbsp; &nbsp; &nbsp; &nbsp; if &#8216;[t-1]&#8217; not in str(i):<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; df[col] = pd.rolling_sum(df[i].unstack().shift(),<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; window=3).stack()
      </div>
    </div>
  </div>
</div>

## <span id="DataFrame_Manipulations">DataFrame Manipulations</span> {#DataFrame_Manipulations}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Subset of DF -- based on a condition in a column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[df[&#8216;reply_message&#8217;] == 1]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Subset of DF -- specific columns:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df[[&#8216;in_reply_to_screen_name&#8217;, &#8216;in_reply_to_status_id&#8217;, &#8216;reply_message&#8217;]].head()
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Drop a column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df = df.drop(&#8216;entities_urls&#8217;,1)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Intersection of two lists:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        pd.Series(np.intersect1d(pd.Series(tickers_in_df), pd.Series(valid_tickers)))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Difference between two lists (all different elements from either list):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        set(tickers_in_df).symmetric_difference(valid_tickers_with_twitter)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Difference between two lists (elements from list1 missing from list2):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        set(list1) &#8211; set(list2)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create DF based on whether column value is in a list:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df = df[df.ticker.isin(mylist)]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Creat an empty dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        columns = [&#8216;ticker&#8217;, &#8216;month&#8217;, &#8216;degree&#8217;] 
        
        <p>
          df = pd.DataFrame(columns=columns)
        </p>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Add row (row 0) to empty dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.loc[0] = pd.Series({&#8216;ticker&#8217;:&#8217;Z&#8217;, &#8216;month&#8217;:&#8217;12&#8217;, &#8216;degree&#8217;: &#8221;})
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Change cell column values for a specific row (index=16458):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        sec.ix[16458, &#8220;8-K Item &#8212; V2&#8221;] = &#8216;Item 2.01&#8217;
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create dataframe from list/dictionary:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        months = [&#8216;2014-1&#8217;, &#8216;2014-2&#8217;, &#8216;2104-3&#8217;] 
        
        <p>
          data = {&#8216;month&#8217;: months}<br /> df = pd.DataFrame(data, columns=[&#8216;month&#8217;, &#8216;degree&#8217;])
        </p>
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Add rows to a dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df = df.append(df_month)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create dataframe from list of column names:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        d = {&#8216;Variable Name&#8217;: list(df.columns.values)}<br /> variables = DataFrame(d)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create dataframe by deleting all rows with null values in one column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df2 = df[df[&#8216;keep&#8217;].notnull()]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Rename a single column:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.rename(columns={&#8216;cusip&#8217;:&#8217;cusip_COMPUSTAT&#8217;}, inplace=True)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create dataframe based on column value appearing in a list:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        missing = df[df[&#8216;cusip&#8217;].isin(mylist)]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Look for duplicates in a dataframe:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        counts = merged.groupby(&#8216;cusip&#8217;).size()<br /> df2 = pd.DataFrame(counts, columns = [&#8216;size&#8217;])<br /> <span>df2 = df2[df2.size>1]</span><br /> df2
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Create version of dataframe with conditions on two variables (for removing a duplicate firm):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        merged = merged[~((merged[&#8216;fyear&#8217;]==2012) & (merged[&#8216;gvkey&#8217;]==&#8217;176103&#8242;))]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Select partial dataframe -- complex conditions:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        sec[(sec[&#8216;Form Type&#8217;] == &#8216;8-K&#8217;) & (sec[&#8216;8-K Item&#8217;]==&#8221;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;) | (sec[&#8216;8-K Item&#8217;]==&#8217;Item fo&#8217;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;)| (sec[&#8216;8-K Item&#8217;]==&#8217;Item that&#8217;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;)]
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Merge two dataframes:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        merged = pd.merge(fb, org_data, left_on=&#8217;feed_id&#8217;, right_on=&#8217;Org_ID&#8217;)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Deep copy of DF:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df2 = df.copy(deep=True)
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Get a slice of dataframe (here, the two rows with the given indexes):
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        df.loc[11516:11517]
      </div>
    </div>
  </div>
</div>



## <span id="Custom_Twitter_Variables">Custom Twitter Variables</span> {#Custom_Twitter_Variables}

<div class="border-box-transparent-bytes">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Time on Twitter:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        import datetime<br /> df[&#8216;start&#8217;]=np.datetime64(&#8216;2016-04-01&#8217;)<br /> df[&#8216;created_at&#8217;] = pd.to_datetime(df[&#8216;created_at&#8217;])<br /> df[&#8216;time_on_twitter&#8217;] = df[&#8216;start&#8217;] &#8211; df[&#8216;created_at&#8217;] df[&#8216;time_on_twitter_days&#8217;] = df[&#8216;time_on_twitter&#8217;].astype(&#8216;timedelta64[D]&#8217;)<br /> df[&#8216;time_on_twitter_days&#8217;] = df.time_on_twitter_days.astype(&#8216;int&#8217;)
      </div>
    </div>
  </div></p>
</div>



## <span id="Working_with_MongoDB_in_PANDAS">Working with MongoDB in PANDAS</span> {#Mongo_DB}

<div class="border-box-transparent-bytes-ending">
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Show first 2 documents:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for user in users.find()[:2]:<br /> &nbsp; &nbsp; print user, &#8216;\n&#8217;
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Get frequency counts:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        from bson.son import SON<br /> pipeline = [ {&#8220;$group&#8221;: {&#8220;_id&#8221;: &#8220;$FormType&#8221;, &#8220;count&#8221;: {&#8220;$sum&#8221;: 1}}} ] list(file_list.aggregate(pipeline))
      </div>
    </div>
  </div>
  
  <div class="su-spoiler su-spoiler-style-default su-spoiler-icon-caret su-spoiler-closed" data-scroll-offset="0">
    <div class="su-spoiler-title" tabindex="0" role="button">
      <span class="su-spoiler-icon"></span>Loop over random sample of 100 with filtering:
    </div>
    
    <div class="su-spoiler-content su-u-clearfix su-u-trim">
      <div class="highlight2">
        for file in file_list.aggregate([<br /> &nbsp; &nbsp; { &#8216;$match&#8217;: {&#8216;FormType&#8217;: { &#8216;$in&#8217;: [&#8216;990PF&#8217;]}} },<br /> &nbsp; &nbsp; { &#8216;$sample&#8217;: {&#8216;size&#8217;: 100} }<br /> &nbsp; &nbsp; ]):<br /> &nbsp; &nbsp; print file
      </div>
    </div>
  </div>
</div>

I hope you have found this helpful. If so, please spread the word, and happy coding!

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>