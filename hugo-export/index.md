---
title: 'Python Data Analytics Code Bytes: PANDAS, Machine Learning, Big Data'
author: Gregory Saxton
type: page
date: -001-11-30T00:00:00+00:00
draft: true

---
  
  
</script>

More and more of my research involves some degree of &#8216;Big Data&#8217; &#8212; typically datasets with a million or so tweets. Getting these data prepped for analysis can involve massive amounts of data manipulation &#8212; anything from aggregating data to the daily or organizational level, to merging in additional variables, to generating data required for social network analysis. For all such steps I now almost exclusively use Python&#8217;s <a href="http://pandas.pydata.org/" target="_blank">PANDAS</a> library (&#8216;Python Data Analysis Library&#8217;). In conjunction with the <a href="http://ipython.org/notebook.html" target="_blank">iPython Notebook</a> interactive computing framework and <a href="https://networkx.github.io/" target="_blank">NetworkX</a>, you will have a powerful set of analysis tools at your disposal.

<div class="border-box-sizing">
  pd.crosstab(df[&#8216;8-K filing_info&#8217;], df[&#8216;8-K Item&#8217;])
</div>

Given that I am now doing almost all of my dataset manipulation &#8212; and much of the analysis &#8212; in <a href="http://pandas.pydata.org/" target="_blank">PANDAS</a>, and how new I am to the framework, I created this page mostly as a handy reference for all those PANDAS commands I tend to forget or find particularly useful. But if it proves helpful to any others, great!

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    WHAT
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#iPython_Notebook_Settings"><span class="toc_number toc_depth_1">1</span> iPython Notebook Settings</a>
    </li>
    <li>
      <a href="#Analysis"><span class="toc_number toc_depth_1">2</span> Analysis</a>
    </li>
    <li>
      <a href="#Generating_New_Variables_Arrays_etc"><span class="toc_number toc_depth_1">3</span> Generating New Variables, Arrays, etc.</a>
    </li>
    <li>
      <a href="#IO"><span class="toc_number toc_depth_1">4</span> I/O</a>
    </li>
    <li>
      <a href="#Looping"><span class="toc_number toc_depth_1">5</span> Looping</a>
    </li>
    <li>
      <a href="#Time_Series"><span class="toc_number toc_depth_1">6</span> Time Series</a>
    </li>
    <li>
      <a href="#Indexing_and_Sorting"><span class="toc_number toc_depth_1">7</span> Indexing and Sorting</a>
    </li>
    <li>
      <a href="#Missing_Data"><span class="toc_number toc_depth_1">8</span> Missing Data</a>
    </li>
    <li>
      <a href="#Custom_Functions"><span class="toc_number toc_depth_1">9</span> Custom Functions</a>
    </li>
    <li>
      <a href="#DataFrame_Manipulations"><span class="toc_number toc_depth_1">10</span> DataFrame Manipulations</a>
    </li>
    <li>
      <a href="#Custom_Twitter_Variables"><span class="toc_number toc_depth_1">11</span> Custom Twitter Variables</a>
    </li>
  </ul>
</div>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Find duplicates in list
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
  </div>
</div>

<div class='gist2' data-gist-id="90b4d2434ec3e7de1fa30f7c47770295">
</div>

<code data-gist-id="90b4d2434ec3e7de1fa30f7c47770295" data-gist-hide-line-numbers="true" 
  data-gist-hide-footer="true" data-gist-line="2"></code>

<div data-gist-id="90b4d2434ec3e7de1fa30f7c47770295" data-gist-hide-line-numbers="true" 
  data-gist-hide-footer="true" data-gist-line="2">
</div> [gist2 id=&#8221;90b4d2434ec3e7de1fa30f7c47770295&#8243; lines=&#8221;1&#8243;] 

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">&lt;gist data-gist-id="90b4d2434ec3e7de1fa30f7c47770295"&gt;</pre>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Create list from dataframe column:
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    <gist2 data-gist-id="90b4d2434ec3e7de1fa30f7c47770295"></gist>
  </div>
</div>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Create list from dataframe column:
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    <class='gist2' data-gist-id="90b4d2434ec3e7de1fa30f7c47770295"></class>
  </div>
</div>



## <span id="iPython_Notebook_Settings">iPython Notebook Settings</span>

Set width of columns for display:

<div class="highlight2">
  pd.set_option(&#8216;display.max_colwidth&#8217;, 200)
</div>

Set cell width:

<div class="highlight2">
  pd.set_option(&#8216;max_colwidth&#8217;,200)
</div>

## <span id="Analysis">Analysis</span>

Cross-tab (can be saved as dataframe):

<div class="highlight2">
  pd.crosstab(df[&#8216;8-K filing_info&#8217;], df[&#8216;8-K Item&#8217;])
</div>



## <span id="Generating_New_Variables_Arrays_etc">Generating New Variables, Arrays, etc.</span>

<a href="http://cubecolour.co.uk/wp" class="popup" data-width="300" data-height="300" data-scrollbars="1" alt="popup">Create list from dataframe column:</a>&#8216;</p> 

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Create list from dataframe column:
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    <div class="highlight2">
      screen_names = ticker_master[&#8216;screen_name&#8217;].tolist()
    </div>
  </div>
</div>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Create list from dataframe column:
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    https://gist.github.com/gdsaxton/b5fea065e6dd746050e7
  </div>
</div>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Create list from dataframe column:
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
  </div>
</div>

<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>Find duplicates in list
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
  </div>
</div>

Create list from dataframe column:  


<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>show code
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    screen_names = ticker_master[&#8216;screen_name&#8217;].tolist()
  </div>
</div>

Create list from dataframe column:  


<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>show code
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    <div class="highlight2">
      screen_names = ticker_master[&#8216;screen_name&#8217;].tolist()
    </div>
  </div>
</div>

Create list from dataframe column:  


<div class="su-spoiler su-spoiler-style-default su-spoiler-icon-plus su-spoiler-closed" data-scroll-offset="0">
  <div class="su-spoiler-title" tabindex="0" role="button">
    <span class="su-spoiler-icon"></span>show code
  </div>
  
  <div class="su-spoiler-content su-u-clearfix su-u-trim">
    <pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">screen_names = ticker_master['screen_name'].tolist()</pre>
  </div>
</div>

Create list from dataframe column:

<pre class="brush: python; light: false; title: ; toolbar: true; notranslate" title="">&lt;div class="highlight2"&gt;screen_names = ticker_master['screen_name'].tolist()</pre>

Create list from dataframe column:

<div class="highlight2">
  screen_names = ticker_master[&#8216;screen_name&#8217;].tolist()
</div>

Create list of unique column values in DF:

<div class="highlight2">
  tickers_in_df = pd.unique(df.ticker.ravel()).tolist()
</div>

Convert string variable to float:

<div class="highlight2">
  df[&#8216;count_V2&#8217;] = df[&#8216;count&#8217;].convert_objects(convert_numeric=True)
</div>

Convert float column to int (only works if there are no missing values):

<div class="highlight2">
  df_2014[&#8216;rt_count&#8217;] = df_2014[&#8216;rt_count&#8217;].astype(int)
</div>

Convert column to string:

<div class="highlight2">
  df.index = df.index.astype(str)
</div>

Create new variable as a slice of an existing one:

<div class="highlight2">
  df[&#8216;cusip8&#8217;] = df[&#8216;cusip&#8217;].apply(lambda x: x[:8])
</div>

Replace a word _within_ a column with another word:

<div class="highlight2">
  df[&#8216;8-K&#8217;] = df[&#8216;8-K&#8217;].str.replace(&#8216;Item&#8217;, &#8216;Section&#8217;)
</div>

Fill in missing values for one column with zero:

<div class="highlight2">
  df_2014[&#8216;rt_count&#8217;] = df_2014[&#8216;rt_count&#8217;].fillna(0)
</div>

Get new list of unique items in a list:

<div class="highlight2">
  screen_names_unique = list(set(screen_names))
</div>

Create dummy variable based on whether another column contains specific text (values will be &#8216;True&#8217; and &#8216;False&#8217;):

<div class="highlight2">
  df[&#8216;retweeted_status_dummy&#8217;] = df[&#8216;retweeted_status&#8217;].str.contains(&#8216;THIS&#8217;, na=False)
</div>

Then convert to float (will convert &#8216;True&#8217; and &#8216;False&#8217; categories of above variable into &#8216;1&#8217; and &#8216;0&#8217;, respectively):

<div class="highlight2">
  df[&#8216;retweeted_status_dummy&#8217;] = df[&#8216;retweeted_status_dummy&#8217;].astype(float)
</div>

Replace values (here, replace &#8216;None&#8217; with &#8216;0&#8217;):

<div class="highlight2">
  df[&#8216;reply_message&#8217;] = df[&#8216;in_reply_to_screen_name&#8217;].replace([None], [&#8216;0&#8217;])
</div>

Replace values (here, replace np.nan values with &#8216;0&#8217;):

<div class="highlight2">
  df.ix[df.Number_of_retweets.isnull(), &#8216;Number_of_retweets&#8217;] = 0
</div>

Switch values of &#8216;0&#8217; and &#8216;1&#8217;:

<div class="highlight2">
  df[&#8216;reply_message&#8217;] = df[&#8216;reply_message&#8217;].replace([1], [99]).replace([0],[1]).replace([99],[0])
</div>

Create binary variable from count variable (if old var=0, assign value of 0; otherwise 1):

<div class="highlight2">
  df[&#8216;urls&#8217;] = np.where(df[&#8216;entities_urls_count&#8217;]==0, 0, 1)
</div>

Change each unicode element in a list to string:

<div class="highlight2">
  tickers_in_df = [x.encode(&#8216;UTF8&#8217;) for x in tickers_in_df]
</div>

Change column values to upper case:

<div class="highlight2">
  df[&#8216;Name&#8217;] = df[&#8216;Name&#8217;].apply(lambda x: x.upper())
</div>

Change column values to upper case:

<div class="highlight2">
  sec[&#8216;8-K Item&#8217;] = sec[&#8216;8-K Item&#8217;].str.upper()
</div>

Find number of unique values:

<div class="highlight2">
  len(pd.unique(compustat_2013.cusip.ravel()))
</div>

Add leading zeros to string variable (as many as needed to reach 10 characters):

<div class="highlight2">
  df[&#8216;cik_x&#8217;] = df[&#8216;cik_x&#8217;].apply(lambda x: x.zfill(10))
</div>

Convert column to string and add leading zeros:

<div class="highlight2">
  df[&#8216;CIK_10&#8217;] = df[&#8216;CIK&#8217;].astype(str).apply(lambda x: x.zfill(10))
</div>

Get a list of values from a DF column:

<div class="highlight2">
  values_list = df[&#8216;8-K&#8217;].value_counts().keys().tolist()
</div>

Find number of cases with fewer than the mean value:

<div class="highlight2">
  sum(df[&#8216;followers_count&#8217;] < df['followers_count'].mean())
</div>



## <span id="IO">I/O</span>

Read in a pickled dataframe:

<div class="highlight2">
  ticker_master = pd.read_pickle(&#8216;valid_tickers_317.pkl&#8217;)
</div>

Read in JSON file:

<div class="highlight2">
  f = open(&#8216;valid_tickers_list_317.json&#8217;, &#8216;r&#8217;)<br /> valid_tickers = simplejson.load(f)
</div>

Read in JSON file &#8212; method 2:

<div class="highlight2">
  with open(&#8216;my_list.json&#8217;, &#8216;r&#8217;) as fp:<br /> &nbsp; &nbsp; my_list = json.load(fp)
</div>

Save a list as JSON file:

<div class="highlight2">
  f = open(&#8216;all_valid_screen_names.json&#8217;, &#8216;w&#8217;)<br /> simplejson.dump(valid_twitter_accounts, f)<br /> f.close()
</div>

Save a list as JSON file &#8212; method 2:  
import json

<div class="highlight2">
  with open(&#8216;my_list.json&#8217;, &#8216;w&#8217;) as fp:<br /> &nbsp; &nbsp; json.dump(my_list, fp)
</div>

Read in Excel file:

<div class="highlight2">
  twitter_accounts = pd.read_excel(&#8216;Twitter Account-level Database &#8212; non-excluded tickers and accounts only.xlsx&#8217;, &#8216;accounts&#8217;, header=0)
</div>

Write Excel file:

<div class="highlight2">
  df.to_excel(&#8216;df.xls&#8217;, sheet_name=&#8217;Sheet1&#8242;)
</div>



## <span id="Looping">Looping</span>

Looping over rows (note how to select a slice of rows):

<div class="highlight2">
  for index, row in df[:10].iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; print index, row[&#8216;content&#8217;]
</div>

Loop over rows and update existing variable:

<div class="highlight2">
  for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; df[&#8216;count&#8217;] = count
</div>

Loop over rows and create new variable, method 1:

<div class="highlight2">
  for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; #df.ix[df.index==index, &#8216;count&#8217;] = count #LONGER VERSION<br /> &nbsp; &nbsp; &nbsp; &nbsp; df.ix[index, &#8216;count&#8217;] = count #SHORTER VERSION
</div>

Loop over rows and create new variable, method 2:

<div class="highlight2">
  for index, row in df.iterrows():<br /> &nbsp; &nbsp; &nbsp; &nbsp; df.loc[index,&#8217;count&#8217;] = count
</div>



## <span id="Time_Series">Time Series</span>

Weekdays:<div class 

<div class="highlight2">
  weekdays_only = by_day2[by_day2[&#8216;weekday&#8217;] < 5 ]
</div>

<div class="highlight2">
  weekday_count = df.groupby(ts.index.weekday).apply(f)<br /> by_day3[&#8216;weekday&#8217;] = by_day[&#8216;date&#8217;].apply(lambda x: x.weekday())
</div>

Add missing days (with zeros) for every day in a dataframe:

<div class="highlight2">
  df_filled = df.unstack().fillna(0).stack()
</div>

Change specific columns&#8217; values to missing based on value in another column:

<div class="highlight2">
  df_filled.loc[df_filled[&#8216;Number of Firm Tweets&#8217;] == 0, [&#8216;Number of Firm Followers (start)&#8217;, &#8216;Number of Lists for Firm (start)&#8217;]] = np.nan
</div>

Set column to datetime:

<div class="highlight2">
  df[&#8216;created_at&#8217;] = pd.to_datetime(df[&#8216;created_at&#8217;])
</div>

Convert datetime column to date:

<div class="highlight2">
  df[&#8216;date&#8217;] = [t.date() for t in df[&#8216;datetime&#8217;]]
</div>

Generate lagged variable with multi-index DF:

<div class="highlight2">
  df[&#8216;Mentions [t-1]&#8217;] = df[&#8216;Mentions&#8217;].unstack().shift(1).stack()
</div>

Generate variable aggregated over 3-day window lagged one day:

<div class="highlight2">
  df[&#8216;Mentions [sum of t-1:t-3]&#8217;] = pd.rolling_sum(df[&#8216;Mentions&#8217;].unstack().shift(), window=3).stack()
</div>

Select date range for DF:

<div class="highlight2">
  df_2014 = df[&#8216;2014-1-1&#8242;:&#8217;2014-12-31&#8217;]
</div>



## <span id="Indexing_and_Sorting">Indexing and Sorting</span>

Set the index:

<div class="highlight2">
  df = df.set_index([&#8216;created_at&#8217;])
</div>

Reset Index:

<div class="highlight2">
  df.reset_index(inplace=True)
</div>

Set Multi-Index:

<div class="highlight2">
  df = df.set_index([&#8216;ticker&#8217;, &#8216;day&#8217;])
</div>

Sort dataframe:

<div class="highlight2">
  df.sort([&#8216;ticker&#8217;, &#8216;day&#8217;], inplace=True)
</div>

Name Existing Multi-index columns:

<div class="highlight2">
  df.index.names = [&#8216;day&#8217;, &#8216;ticker&#8217;]
</div>

With multi-index df &#8212; get unique items per index level:

<div class="highlight2">
  len(firm_day_counts_firm_tweets.index.levels[0])<br /> len(firm_day_counts_firm_tweets.index.levels[1])
</div>

Swap levels on multi-index dataframe:

<div class="highlight2">
  df_swapped = df.swaplevel(&#8216;ticker&#8217;, &#8216;day&#8217;)
</div>

Get minimum date in DF:

<div class="highlight2">
  df.index.min()
</div>

Complex conditional row selection during loop:

<div class="highlight2">
  if (row[&#8216;Form Type&#8217;] == &#8216;8-K&#8217;) and (row[&#8216;8-K Item&#8217;]==&#8221;) and (row[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;) or (row[&#8216;8-K Item&#8217;]==&#8217;Item that&#8217;) or (row[&#8216;8-K Item&#8217;]==&#8217;Item fo&#8217;):
</div>

## <span id="Missing_Data">Missing Data</span>

Interpolation with backfill and forward fill [n.b. &#8211; does not respect multi-index] 

<div class="highlight2">
  df[&#8216;F_x)&#8217;]=df[&#8216;F&#8217;].interpolate(method=&#8217;linear&#8217;).bfill().ffill()
</div>

Find rows with empty column:

<div class="highlight2">
  missing = df[df[&#8216;ticker&#8217;].isnull()]
</div>

Fill missing values in one column with values from another column:

<div class="highlight2">
  sec.loc[sec[&#8216;8-K Item_v2&#8242;].isnull(),&#8217;8-K Item_v2&#8217;] = sec[&#8216;8-K Item&#8217;]
</div>

## <span id="Custom_Functions">Custom Functions</span>

Function for generating a series of new one-day lag variables in a dataframe:

<div class="highlight2">
  def lag_one_day(df):<br /> &nbsp; &nbsp; #df_cols = df.columns<br /> &nbsp; &nbsp; df_cols = [u&#8217;Number of Firm Mentions&#8217;, u&#8217;Number of Firm Tweets&#8217;] &nbsp; &nbsp; for i in df_cols:<br /> &nbsp; &nbsp; &nbsp; &nbsp; col = str(i)+str(&#8216;[t-1]&#8217;)<br /> &nbsp; &nbsp; &nbsp; &nbsp; if &#8216;[t-1]&#8217; not in str(i):<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; df[col] = df[i].unstack().shift(1).stack()
</div>

Function for generating a series of new dataframe variables that aggregate over a multi-day period:

<div class="highlight2">
  def lag_one_day(df):<br /> &nbsp; &nbsp; #df_cols = df.columns<br /> &nbsp; &nbsp; df_cols = [u&#8217;Number of Firm Mentions&#8217;, u&#8217;Number of Firm Tweets&#8217;] &nbsp; &nbsp; for i in df_cols:<br /> &nbsp; &nbsp; &nbsp; &nbsp; col = str(i)+str(&#8216;[sum t-1:t-3]&#8217;)<br /> &nbsp; &nbsp; &nbsp; &nbsp; if &#8216;[t-1]&#8217; not in str(i):<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; df[col] = pd.rolling_sum(df[i].unstack().shift(),<br /> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; window=3).stack()
</div>

## <span id="DataFrame_Manipulations">DataFrame Manipulations</span>

Subset of DF &#8212; based on a condition in a column:

<div class="highlight2">
  df[df[&#8216;reply_message&#8217;] == 1]
</div>

Subset of DF &#8212; specific columns

<div class="highlight2">
  df[[&#8216;in_reply_to_screen_name&#8217;, &#8216;in_reply_to_status_id&#8217;, &#8216;reply_message&#8217;]].head()
</div>

Drop a column:

<div class="highlight2">
  df = df.drop(&#8216;entities_urls&#8217;,1)
</div>

Intersection of two lists:

<div class="highlight2">
  pd.Series(np.intersect1d(pd.Series(tickers_in_df), pd.Series(valid_tickers)))
</div>

Difference between two lists (all different elements from either list):

<div class="highlight2">
  set(tickers_in_df).symmetric_difference(valid_tickers_with_twitter)
</div>

Difference between two lists (elements from list1 missing from list2):

<div class="highlight2">
  set(list1) &#8211; set(list2)
</div>

Create DF based on whether column value is in a list:

<div class="highlight2">
  df = df[df.ticker.isin(mylist)]
</div>

Creat an empty dataframe:

<div class="highlight2">
  columns = [&#8216;ticker&#8217;, &#8216;month&#8217;, &#8216;degree&#8217;] 
  
  <p>
    df = pd.DataFrame(columns=columns)
  </p>
</div>

Add row (row 0) to empty dataframe:

<div class="highlight2">
  df.loc[0] = pd.Series({&#8216;ticker&#8217;:&#8217;Z&#8217;, &#8216;month&#8217;:&#8217;12&#8217;, &#8216;degree&#8217;: &#8221;})
</div>

Change cell column values for a specific row (index=16458): 

<div class="highlight2">
  sec.ix[16458, &#8220;8-K Item &#8212; V2&#8221;] = &#8216;Item 2.01&#8217;
</div>

Create dataframe from list/dictionary:

<div class="highlight2">
  months = [&#8216;2014-1&#8217;, &#8216;2014-2&#8217;, &#8216;2104-3&#8217;] 
  
  <p>
    data = {&#8216;month&#8217;: months}<br /> df = pd.DataFrame(data, columns=[&#8216;month&#8217;, &#8216;degree&#8217;])
  </p>
</div>

Add rows to a dataframe:

<div class="highlight2">
  df = df.append(df_month)
</div>

Create dataframe from list of column names:

<div class="highlight2">
  d = {&#8216;Variable Name&#8217;: list(df.columns.values)}<br /> variables = DataFrame(d)
</div>

Create dataframe by deleting all rows with null values in one column:

<div class="highlight2">
  df2 = df[df[&#8216;keep&#8217;].notnull()]
</div>

Rename a single column:

<div class="highlight2">
  df.rename(columns={&#8216;cusip&#8217;:&#8217;cusip_COMPUSTAT&#8217;}, inplace=True)
</div>

Create dataframe based on column value appearing in a list:

<div class="highlight2">
  missing = df[df[&#8216;cusip&#8217;].isin(mylist)]
</div>

Look for duplicates in a dataframe:

<div class="highlight2">
  counts = merged.groupby(&#8216;cusip&#8217;).size()<br /> df2 = pd.DataFrame(counts, columns = [&#8216;size&#8217;])<br /> <span>df2 = df2[df2.size>1]</span><br /> df2
</div>

Create version of dataframe with conditions on two variables (for removing a duplicate firm):

<div class="highlight2">
  merged = merged[~((merged[&#8216;fyear&#8217;]==2012) & (merged[&#8216;gvkey&#8217;]==&#8217;176103&#8242;))]
</div>

Select partial dataframe &#8212; complex conditions:

<div class="highlight2">
  sec[(sec[&#8216;Form Type&#8217;] == &#8216;8-K&#8217;) & (sec[&#8216;8-K Item&#8217;]==&#8221;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;) | (sec[&#8216;8-K Item&#8217;]==&#8217;Item fo&#8217;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;)| (sec[&#8216;8-K Item&#8217;]==&#8217;Item that&#8217;) & (sec[&#8216;8-K Item &#8212; V2&#8217;]==&#8221;)]
</div>

Merge two dataframes:

<div class="highlight2">
  merged = pd.merge(fb, org_data, left_on=&#8217;feed_id&#8217;, right_on=&#8217;Org_ID&#8217;)
</div>

Deep copy of DF:

<div class="highlight2">
  df2 = df.copy(deep=True)
</div>

Get a slice of dataframe (here, the two rows with the given indexes):

<div class="highlight2">
  df.loc[11516:11517]
</div>



## <span id="Custom_Twitter_Variables">Custom Twitter Variables</span>

Time on Twitter:

<div class="highlight2">
  import datetime
</div>

<div class="highlight2">
  df[&#8216;start&#8217;]=np.datetime64(&#8216;2016-04-01&#8217;)
</div>

<div class="highlight2">
  df[&#8216;created_at&#8217;] = pd.to_datetime(df[&#8216;created_at&#8217;])
</div>

<div class="highlight2">
  df[&#8216;time_on_twitter&#8217;] = df[&#8216;start&#8217;] &#8211; df[&#8216;created_at&#8217;]
</div>

<div class="highlight2">
  df[&#8216;time_on_twitter_days&#8217;] = df[&#8216;time_on_twitter&#8217;].astype(&#8216;timedelta64[D]&#8217;)
</div>

<div class="highlight2">
  df[&#8216;time_on_twitter_days&#8217;] = df.time_on_twitter_days.astype(&#8216;int&#8217;)
</div>

<div class="highlight2">
</div>

<div class="highlight2">
</div>

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>