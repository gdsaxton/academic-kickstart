---
title: Producing a Summary Statistics Table in iPython
author: Gregory Saxton
type: post
date: 2015-05-29T03:22:49+00:00
draft: true
url: /?p=1414
categories:
  - notebooks
  - pandas
  - python
  - research
tags:
  - academic research
  - iPython
  - ipython_notebook
  - PANDAS
  - python
  - research
  - tutorial

---
Below is a converted version of an iPython notebook. To see it in its prettier, native, format or to download a copy of the code, visit <a href="http://nbviewer.ipython.org/gist/gdsaxton/b5fea065e6dd746050e7" target="_blank" rel="noopener noreferrer">http://nbviewer.ipython.org/gist/gdsaxton/b5fea065e6dd746050e7</a>

  
</p> 

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    In this notebook I will show you how to run and then save for output your descriptive statistics. The desired end product is the a CSV table of key summary statistics &#8212; count, mean, std. dev., min. and max &#8212; for the variables in your dataset.
  </p>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <h3 id="Import-packages">
    Import packages<a class="anchor-link" href="#Import-packages">&#182;</a>
  </h3>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[1]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">from</span> <span class="nn">pandas</span> <span class="kn">import</span> <span class="n">DataFrame</span>
<span class="kn">from</span> <span class="nn">pandas</span> <span class="kn">import</span> <span class="n">Series</span>
<span class="kn">import</span> <span class="nn">statsmodels</span> <span class="c">&nbsp;&nbsp; #FOR RUNNING REGRESSIONS (NEXT STEP)</span>
<span class="kn">import</span> <span class="nn">statsmodels.api</span> <span class="kn">as</span> <span class="nn">sm</span>
<span class="kn">import</span> <span class="nn">statsmodels.formula.api</span> <span class="kn">as</span> <span class="nn">smf</span>   <span class="c">#FOR &#39;R&#39;-STYLE REGRESSION FORMULAS</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    PANDAS allows you to set various options for, among other things, inspecting the data. I like to be able to see all of the columns. Therefore, I typically include this line at the top of all my notebooks.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[2]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="c">#Set PANDAS to show all columns in DataFrame</span>
<span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s">&#39;display.max_columns&#39;</span><span class="p">,</span> <span class="bp">None</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>



<div class="text_cell_render border-box-sizing rendered_html">
  <p>
    I like suppressing scientific notation in my numbers. So, if you&#8217;d rather see "0.48" than "4.800000e-01", then run the following line. Note that this does not change the actual values. For outputting to CSV we&#8217;ll have to run some additional code later on.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[3]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">pd</span><span class="o">.</span><span class="n">set_option</span><span class="p">(</span><span class="s">&#39;display.float_format&#39;</span><span class="p">,</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="s">&#39;</span><span class="si">%.2f</span><span class="s">&#39;</span> <span class="o">%</span> <span class="n">x</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    I&#8217;m running PANDAS 0.13 here.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[4]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="k">print</span> <span class="n">pd</span><span class="o">.</span><span class="n">__version__</span>
<span class="k">print</span> <span class="n">statsmodels</span><span class="o">.</span><span class="n">__version__</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt">
        </div>
        
        <div class="box-flex1 output_subarea output_stream output_stdout">
          <pre>
0.13.1
0.6.1

</pre>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <h3 id="Read-in-dataframe">
    Read in dataframe<a class="anchor-link" href="#Read-in-dataframe">&#182;</a>
  </h3>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
    I&#8217;m using data on a sample of 1,500 Facebook statuses of a sample of US-based health organizations
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[81]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_excel</span><span class="p">(</span><span class="s">&#39;fb.xls&#39;</span><span class="p">,</span> <span class="s">&#39;Sheet1&#39;</span><span class="p">,</span> <span class="n">header</span><span class="o">=</span><span class="mi"></span><span class="p">)</span>
<span class="k">print</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt">
        </div>
        
        <div class="box-flex1 output_subarea output_stream output_stdout">
          <pre>
1500

</pre>
        </div>
      </div>
      
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[81]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    No.
                  </th>
                  
                  <th>
                    id
                  </th>
                  
                  <th>
                    feed_id
                  </th>
                  
                  <th>
                    org_name
                  </th>
                  
                  <th>
                    FB_org_id
                  </th>
                  
                  <th>
                    location
                  </th>
                  
                  <th>
                    link
                  </th>
                  
                  <th>
                    message_id
                  </th>
                  
                  <th>
                    org_id
                  </th>
                  
                  <th>
                    status_id
                  </th>
                  
                  <th>
                    status_link
                  </th>
                  
                  <th>
                    content
                  </th>
                  
                  <th>
                    published_date
                  </th>
                  
                  <th>
                    date_inserted
                  </th>
                  
                  <th>
                    last_comment
                  </th>
                  
                  <th>
                    type
                  </th>
                  
                  <th>
                    status_type
                  </th>
                  
                  <th>
                    video_source
                  </th>
                  
                  <th>
                    picture_link
                  </th>
                  
                  <th>
                    link_name
                  </th>
                  
                  <th>
                    link_caption
                  </th>
                  
                  <th>
                    link_description
                  </th>
                  
                  <th>
                    num_mentions
                  </th>
                  
                  <th>
                    mentions
                  </th>
                  
                  <th>
                    num_likes
                  </th>
                  
                  <th>
                    like_count
                  </th>
                  
                  <th>
                    comment_count
                  </th>
                  
                  <th>
                    share_count
                  </th>
                  
                  <th>
                    hashtag_count
                  </th>
                  
                  <th>
                    hashtags
                  </th>
                  
                  <th>
                    mentions_count
                  </th>
                  
                  <th>
                    actions
                  </th>
                  
                  <th>
                    application
                  </th>
                  
                  <th>
                    properties
                  </th>
                  
                  <th>
                    message_output
                  </th>
                  
                  <th>
                    time_since_post_days
                  </th>
                  
                  <th>
                    like_count_7days
                  </th>
                  
                  <th>
                    comment_count_7days
                  </th>
                  
                  <th>
                    share_count_7days
                  </th>
                  
                  <th>
                    time_since_post_14days
                  </th>
                  
                  <th>
                    like_count_14days
                  </th>
                  
                  <th>
                    comment_count_14days
                  </th>
                  
                  <th>
                    share_count_14days
                  </th>
                  
                  <th>
                    feed_organization
                  </th>
                  
                  <th>
                    images
                  </th>
                  
                  <th>
                    urls_count
                  </th>
                  
                  <th>
                    urls_count_true
                  </th>
                  
                  <th>
                    mentions_scrape
                  </th>
                  
                  <th>
                    source
                  </th>
                  
                  <th>
                    mission/non-mission
                  </th>
                  
                  <th>
                    mission_focus
                  </th>
                  
                  <th>
                    I-C-A
                  </th>
                  
                  <th>
                    subcode
                  </th>
                  
                  <th>
                    source_External
                  </th>
                  
                  <th>
                    source_Internal
                  </th>
                  
                  <th>
                    mission_N
                  </th>
                  
                  <th>
                    mission_Y
                  </th>
                  
                  <th>
                    mission_focus_Building capacity
                  </th>
                  
                  <th>
                    mission_focus_Patient advocacy
                  </th>
                  
                  <th>
                    mission_focus_Prevention
                  </th>
                  
                  <th>
                    ICA_A
                  </th>
                  
                  <th>
                    ICA_C
                  </th>
                  
                  <th>
                    ICA_I
                  </th>
                  
                  <th>
                    ICA_subcode_AIDS-related day
                  </th>
                  
                  <th>
                    ICA_subcode_Awareness
                  </th>
                  
                  <th>
                    ICA_subcode_Complementary support
                  </th>
                  
                  <th>
                    ICA_subcode_Cover/profile photo
                  </th>
                  
                  <th>
                    ICA_subcode_Dialogue
                  </th>
                  
                  <th>
                    ICA_subcode_Donation
                  </th>
                  
                  <th>
                    ICA_subcode_Event info
                  </th>
                  
                  <th>
                    ICA_subcode_Event promotion
                  </th>
                  
                  <th>
                    ICA_subcode_Event update
                  </th>
                  
                  <th>
                    ICA_subcode_Get tested
                  </th>
                  
                  <th>
                    ICA_subcode_HIV/AIDS info/news
                  </th>
                  
                  <th>
                    ICA_subcode_Idea promotion
                  </th>
                  
                  <th>
                    ICA_subcode_LGBT/Transgender information
                  </th>
                  
                  <th>
                    ICA_subcode_Lobbying
                  </th>
                  
                  <th>
                    ICA_subcode_Media action
                  </th>
                  
                  <th>
                    ICA_subcode_Medication
                  </th>
                  
                  <th>
                    ICA_subcode_National holiday/Holiday
                  </th>
                  
                  <th>
                    ICA_subcode_Organizational news/announcement
                  </th>
                  
                  <th>
                    ICA_subcode_Other
                  </th>
                  
                  <th>
                    ICA_subcode_Patient stories
                  </th>
                  
                  <th>
                    ICA_subcode_Recognition
                  </th>
                  
                  <th>
                    ICA_subcode_Research/survey
                  </th>
                  
                  <th>
                    ICA_subcode_Viewing action
                  </th>
                  
                  <th>
                    ICA_subcode_Volunteer
                  </th>
                  
                  <th>
                    type_event
                  </th>
                  
                  <th>
                    type_link
                  </th>
                  
                  <th>
                    type_music
                  </th>
                  
                  <th>
                    type_photo
                  </th>
                  
                  <th>
                    type_status
                  </th>
                  
                  <th>
                    type_video
                  </th>
                  
                  <th>
                    status_type_added_photos
                  </th>
                  
                  <th>
                    status_type_added_video
                  </th>
                  
                  <th>
                    status_type_created_event
                  </th>
                  
                  <th>
                    status_type_created_note
                  </th>
                  
                  <th>
                    status_type_mobile_status_update
                  </th>
                  
                  <th>
                    status_type_published_story
                  </th>
                  
                  <th>
                    status_type_shared_story
                  </th>
                  
                  <th>
                    video_dummy
                  </th>
                  
                  <th>
                    picture_dummy
                  </th>
                  
                  <th>
                    Org_ID
                  </th>
                  
                  <th>
                    Org_Name
                  </th>
                  
                  <th>
                    Total_Revenue
                  </th>
                  
                  <th>
                    Assets
                  </th>
                  
                  <th>
                    followers_count
                  </th>
                  
                  <th>
                    talking_about_count
                  </th>
                  
                  <th>
                    were_here_count
                  </th>
                  
                  <th>
                    Log_of_Assets
                  </th>
                  
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <th>
                    Log_of_Followers
                  </th>
                  
                  <th>
                    likes_binary
                  </th>
                  
                  <th>
                    comment_binary
                  </th>
                  
                  <th>
                    share_binary
                  </th>
                </tr>
                
                <tr>
                  <th>
                  </th>
                  
                  <td>
                    1118
                  </td>
                  
                  <td>
                    74
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    AIDS Healthcare Foundation
                  </td>
                  
                  <td>
                    34661411150
                  </td>
                  
                  <td>
                    {&#8216;location&#8217;: {&#8216;city&#8217;: &#8216;Los Angeles&#8217;, &#8216;zip&#8217;: &#8216;9&#8230;
                  </td>
                  
                  <td>
                    https://www.facebook.com/AIDShealth/photos/a.1&#8230;
                  </td>
                  
                  <td>
                    34661411150_10152940344646151
                  </td>
                  
                  <td>
                    34661411150
                  </td>
                  
                  <td>
                    10152940344646100
                  </td>
                  
                  <td>
                    https://www.facebook.com/34661411150/posts/101&#8230;
                  </td>
                  
                  <td>
                    &#8216;TIS THE SEASON: We know you&#8217;ve heard us say, &#8230;
                  </td>
                  
                  <td>
                    2014-12-18T05:19:30+0000
                  </td>
                  
                  <td>
                    2015-03-09 00:00:39
                  </td>
                  
                  <td>
                    2014-12-20T13:33:45+0000
                  </td>
                  
                  <td>
                    photo
                  </td>
                  
                  <td>
                    added_photos
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    https://scontent.xx.fbcdn.net/hphotos-xpf1/v/t&#8230;
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    Art Hearts Fashion
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    UseACondom
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    [{&#8216;link&#8217;: &#8216;https://www.facebook.com/3466141115&#8230;
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    {&#8216;picture&#8217;: &#8216;https://scontent.xx.fbcdn.net/hph&#8230;
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    81.00
                  </td>
                  
                  <td>
                    101
                  </td>
                  
                  <td>
                    3
                  </td>
                  
                  <td>
                    6
                  </td>
                  
                  <td>
                    AIDS HEALTHCARE FOUNDATION
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    Internal
                  </td>
                  
                  <td>
                    Y
                  </td>
                  
                  <td>
                    Building capacity
                  </td>
                  
                  <td>
                    A
                  </td>
                  
                  <td>
                    Event promotion
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    AIDS HEALTHCARE FOUNDATION
                  </td>
                  
                  <td>
                    209986539
                  </td>
                  
                  <td>
                    227735541
                  </td>
                  
                  <td>
                    721419
                  </td>
                  
                  <td>
                    896
                  </td>
                  
                  <td>
                    3891
                  </td>
                  
                  <td>
                    19.24
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    13.49
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                </tr>
                
                <tr>
                  <th>
                    1
                  </th>
                  
                  <td>
                    1262
                  </td>
                  
                  <td>
                    79
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    AIDS Healthcare Foundation
                  </td>
                  
                  <td>
                    34661411150
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    http://www.frontiersmedia.com/frontiers-blog/2&#8230;
                  </td>
                  
                  <td>
                    34661411150_10152926215086151
                  </td>
                  
                  <td>
                    34661411150
                  </td>
                  
                  <td>
                    10152926215086100
                  </td>
                  
                  <td>
                    https://www.facebook.com/34661411150/posts/101&#8230;
                  </td>
                  
                  <td>
                    AHF mourns the tragic loss of our friend and c&#8230;
                  </td>
                  
                  <td>
                    2014-12-11T18:02:10+0000
                  </td>
                  
                  <td>
                    2015-03-09 00:00:40
                  </td>
                  
                  <td>
                    2014-12-14T16:41:29+0000
                  </td>
                  
                  <td>
                    link
                  </td>
                  
                  <td>
                    shared_story
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    https://fbexternal-a.akamaihd.net/safe_image.p&#8230;
                  </td>
                  
                  <td>
                    Dana Millerâ€”Producer, AIDS Advocate, Frontie&#8230;
                  </td>
                  
                  <td>
                    frontiersmedia.com
                  </td>
                  
                  <td>
                    â€œDana was legendary in gay Los Angeles and H&#8230;
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    DanaMiller
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    [{&#8216;link&#8217;: &#8216;https://www.facebook.com/3466141115&#8230;
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    NaN
                  </td>
                  
                  <td>
                    {&#8216;picture&#8217;: &#8216;https://fbexternal-a.akamaihd.net&#8230;
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    88.00
                  </td>
                  
                  <td>
                    78
                  </td>
                  
                  <td>
                    9
                  </td>
                  
                  <td>
                    4
                  </td>
                  
                  <td>
                    AIDS HEALTHCARE FOUNDATION
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    nan
                  </td>
                  
                  <td>
                    External
                  </td>
                  
                  <td>
                    Y
                  </td>
                  
                  <td>
                    Building capacity
                  </td>
                  
                  <td>
                    C
                  </td>
                  
                  <td>
                    Recognition
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    AIDS HEALTHCARE FOUNDATION
                  </td>
                  
                  <td>
                    209986539
                  </td>
                  
                  <td>
                    227735541
                  </td>
                  
                  <td>
                    721419
                  </td>
                  
                  <td>
                    896
                  </td>
                  
                  <td>
                    3891
                  </td>
                  
                  <td>
                    19.24
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    13.49
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    1
                  </td>
                </tr>
              </table>
              
              <p>
                2 rows × 115 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    List all the columns in the DataFrame
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[82]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span><span class="o">.</span><span class="n">columns</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[82]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <pre>
Index([u';No.';, u';id';, u';feed_id';, u';org_name';, u';FB_org_id';, u';location';, u';link';, u';message_id';, u';org_id';, u';status_id';, u';status_link';, u';content';, u';published_date';, u';date_inserted';, u';last_comment';, u';type';, u';status_type';, u';video_source';, u';picture_link';, u';link_name';, u';link_caption';, u';link_description';, u';num_mentions';, u';mentions';, u';num_likes';, u';like_count';, u';comment_count';, u';share_count';, u';hashtag_count';, u';hashtags';, u';mentions_count';, u';actions';, u';application';, u';properties';, u';message_output';, u';time_since_post_days';, u';like_count_7days';, u';comment_count_7days';, u';share_count_7days';, u';time_since_post_14days';, u';like_count_14days';, u';comment_count_14days';, u';share_count_14days';, u';feed_organization';, u';images';, u';urls_count';, u';urls_count_true';, u';mentions_scrape';, u';source';, u';mission/non-mission';, u';mission_focus';, u';I-C-A';, u';subcode';, u';source_External';, u';source_Internal';, u';mission_N';, u';mission_Y';, u';mission_focus_Building capacity';, u';mission_focus_Patient advocacy';, u';mission_focus_Prevention';, u';ICA_A';, u';ICA_C';, u';ICA_I';, u';ICA_subcode_AIDS-related day';, u';ICA_subcode_Awareness';, u';ICA_subcode_Complementary support';, u';ICA_subcode_Cover/profile photo';, u';ICA_subcode_Dialogue';, u';ICA_subcode_Donation';, u';ICA_subcode_Event info';, u';ICA_subcode_Event promotion';, u';ICA_subcode_Event update';, u';ICA_subcode_Get tested';, u';ICA_subcode_HIV/AIDS info/news';, u';ICA_subcode_Idea promotion';, u';ICA_subcode_LGBT/Transgender information';, u';ICA_subcode_Lobbying';, u';ICA_subcode_Media action';, u';ICA_subcode_Medication';, u';ICA_subcode_National holiday/Holiday';, u';ICA_subcode_Organizational news/announcement';, u';ICA_subcode_Other';, u';ICA_subcode_Patient stories';, u';ICA_subcode_Recognition';, u';ICA_subcode_Research/survey';, u';ICA_subcode_Viewing action';, u';ICA_subcode_Volunteer';, u';type_event';, u';type_link';, u';type_music';, u';type_photo';, u';type_status';, u';type_video';, u';status_type_added_photos';, u';status_type_added_video';, u';status_type_created_event';, u';status_type_created_note';, u';status_type_mobile_status_update';, u';status_type_published_story';, u';status_type_shared_story';, ...], dtype=';object';)
</pre>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <h3 id="Create-Sub-Set-of-DataFrame-with-only-Desired-Variables">
    Create Sub-Set of DataFrame with only Desired Variables<a class="anchor-link" href="#Create-Sub-Set-of-DataFrame-with-only-Desired-Variables">&#182;</a>
  </h3>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
    You might not want to include all of your variables in the summary statistics table. When you&#8217;re dealing with a dataset with a lot of columns, I find the easiest way is to output the column names to a list, copy and paste the output into a text editor, do a replace all command to delete the all the u&#8217;s before each column name, and then paste back into iPython and create your desired sub-set.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[56]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="o">.</span><span class="n">tolist</span><span class="p">()</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[56]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <pre>
[u';No.';,
 u';id';,
 u';feed_id';,
 u';org_name';,
 u';FB_org_id';,
 u';location';,
 u';link';,
 u';message_id';,
 u';org_id';,
 u';status_id';,
 u';status_link';,
 u';content';,
 u';published_date';,
 u';date_inserted';,
 u';last_comment';,
 u';type';,
 u';status_type';,
 u';video_source';,
 u';picture_link';,
 u';link_name';,
 u';link_caption';,
 u';link_description';,
 u';num_mentions';,
 u';mentions';,
 u';num_likes';,
 u';like_count';,
 u';comment_count';,
 u';share_count';,
 u';hashtag_count';,
 u';hashtags';,
 u';mentions_count';,
 u';actions';,
 u';application';,
 u';properties';,
 u';message_output';,
 u';time_since_post_days';,
 u';like_count_7days';,
 u';comment_count_7days';,
 u';share_count_7days';,
 u';time_since_post_14days';,
 u';like_count_14days';,
 u';comment_count_14days';,
 u';share_count_14days';,
 u';feed_organization';,
 u';images';,
 u';urls_count';,
 u';urls_count_true';,
 u';mentions_scrape';,
 u';source';,
 u';mission/non-mission';,
 u';mission_focus';,
 u';I-C-A';,
 u';subcode';,
 u';source_External';,
 u';source_Internal';,
 u';mission_N';,
 u';mission_Y';,
 u';mission_focus_Building capacity';,
 u';mission_focus_Patient advocacy';,
 u';mission_focus_Prevention';,
 u';ICA_A';,
 u';ICA_C';,
 u';ICA_I';,
 u';ICA_subcode_AIDS-related day';,
 u';ICA_subcode_Awareness';,
 u';ICA_subcode_Complementary support';,
 u';ICA_subcode_Cover/profile photo';,
 u';ICA_subcode_Dialogue';,
 u';ICA_subcode_Donation';,
 u';ICA_subcode_Event info';,
 u';ICA_subcode_Event promotion';,
 u';ICA_subcode_Event update';,
 u';ICA_subcode_Get tested';,
 u';ICA_subcode_HIV/AIDS info/news';,
 u';ICA_subcode_Idea promotion';,
 u';ICA_subcode_LGBT/Transgender information';,
 u';ICA_subcode_Lobbying';,
 u';ICA_subcode_Media action';,
 u';ICA_subcode_Medication';,
 u';ICA_subcode_National holiday/Holiday';,
 u';ICA_subcode_Organizational news/announcement';,
 u';ICA_subcode_Other';,
 u';ICA_subcode_Patient stories';,
 u';ICA_subcode_Recognition';,
 u';ICA_subcode_Research/survey';,
 u';ICA_subcode_Viewing action';,
 u';ICA_subcode_Volunteer';,
 u';type_event';,
 u';type_link';,
 u';type_music';,
 u';type_photo';,
 u';type_status';,
 u';type_video';,
 u';status_type_added_photos';,
 u';status_type_added_video';,
 u';status_type_created_event';,
 u';status_type_created_note';,
 u';status_type_mobile_status_update';,
 u';status_type_published_story';,
 u';status_type_shared_story';,
 u';video_dummy';,
 u';picture_dummy';,
 u';Org_ID';,
 u';Org_Name';,
 u';Total_Revenue';,
 u';Assets';,
 u';followers_count';,
 u';talking_about_count';,
 u';were_here_count';,
 u';Log_of_Assets';,
 u';Log_of_Total_Revenue';,
 u';Log_of_Followers';,
 u';likes_binary';,
 u';comment_binary';,
 u';share_binary';]
</pre>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    I&#8217;ve copy and pasted the above output into TextWrangler, omitted all the &#8216;u&#8217;s, and selected the columns I want. I will now limit the dataframe to just those columns I want.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[84]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span> <span class="o">=</span> <span class="n">df</span><span class="p">[[</span><span class="s">&#39;hashtag_count&#39;</span><span class="p">,</span> <span class="s">&#39;like_count_14days&#39;</span><span class="p">,</span> <span class="s">&#39;comment_count_14days&#39;</span><span class="p">,</span> <span class="s">&#39;share_count_14days&#39;</span><span class="p">,</span>
 <span class="s">&#39;source&#39;</span><span class="p">,</span> <span class="s">&#39;source_External&#39;</span><span class="p">,</span> <span class="s">&#39;video_dummy&#39;</span><span class="p">,</span> <span class="s">&#39;picture_dummy&#39;</span><span class="p">,</span>
 <span class="s">&#39;Total_Revenue&#39;</span><span class="p">,</span> <span class="s">&#39;Log_of_Total_Revenue&#39;</span><span class="p">,</span> <span class="s">&#39;followers_count&#39;</span><span class="p">,</span>  <span class="s">&#39;Log_of_Followers&#39;</span><span class="p">]]</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    As you can see, you now have a dataframe with only 12 columns (variables)
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[85]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="k">print</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="p">)</span> 
<span class="k">print</span> <span class="nb">len</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">columns</span><span class="p">)</span>
<span class="n">df</span><span class="o">.</span><span class="n">head</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt">
        </div>
        
        <div class="box-flex1 output_subarea output_stream output_stdout">
          <pre>
1500
12

</pre>
        </div>
      </div>
      
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[85]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    hashtag_count
                  </th>
                  
                  <th>
                    like_count_14days
                  </th>
                  
                  <th>
                    comment_count_14days
                  </th>
                  
                  <th>
                    share_count_14days
                  </th>
                  
                  <th>
                    source
                  </th>
                  
                  <th>
                    source_External
                  </th>
                  
                  <th>
                    video_dummy
                  </th>
                  
                  <th>
                    picture_dummy
                  </th>
                  
                  <th>
                    Total_Revenue
                  </th>
                  
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <th>
                    followers_count
                  </th>
                  
                  <th>
                    Log_of_Followers
                  </th>
                </tr>
                
                <tr>
                  <th>
                  </th>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    101
                  </td>
                  
                  <td>
                    3
                  </td>
                  
                  <td>
                    6
                  </td>
                  
                  <td>
                    Internal
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    209986539
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    721419
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
                
                <tr>
                  <th>
                    1
                  </th>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    78
                  </td>
                  
                  <td>
                    9
                  </td>
                  
                  <td>
                    4
                  </td>
                  
                  <td>
                    External
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                  </td>
                  
                  <td>
                    1
                  </td>
                  
                  <td>
                    209986539
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    721419
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                2 rows × 12 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <h3 id="Generate-Summary-Statistics">
    Generate Summary Statistics<a class="anchor-link" href="#Generate-Summary-Statistics">&#182;</a>
  </h3>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
    This is the basic way to produce summary statistics for all variables in your dataframe
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[86]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[86]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    hashtag_count
                  </th>
                  
                  <th>
                    like_count_14days
                  </th>
                  
                  <th>
                    comment_count_14days
                  </th>
                  
                  <th>
                    share_count_14days
                  </th>
                  
                  <th>
                    source_External
                  </th>
                  
                  <th>
                    video_dummy
                  </th>
                  
                  <th>
                    picture_dummy
                  </th>
                  
                  <th>
                    Total_Revenue
                  </th>
                  
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <th>
                    followers_count
                  </th>
                  
                  <th>
                    Log_of_Followers
                  </th>
                </tr>
                
                <tr>
                  <th>
                    count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    mean
                  </th>
                  
                  <td>
                    0.48
                  </td>
                  
                  <td>
                    30.59
                  </td>
                  
                  <td>
                    0.59
                  </td>
                  
                  <td>
                    3.11
                  </td>
                  
                  <td>
                    0.42
                  </td>
                  
                  <td>
                    0.03
                  </td>
                  
                  <td>
                    0.88
                  </td>
                  
                  <td>
                    11486117.19
                  </td>
                  
                  <td>
                    15.36
                  </td>
                  
                  <td>
                    20150.46
                  </td>
                  
                  <td>
                    7.79
                  </td>
                </tr>
                
                <tr>
                  <th>
                    std
                  </th>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    355.34
                  </td>
                  
                  <td>
                    2.62
                  </td>
                  
                  <td>
                    14.95
                  </td>
                  
                  <td>
                    0.49
                  </td>
                  
                  <td>
                    0.18
                  </td>
                  
                  <td>
                    0.33
                  </td>
                  
                  <td>
                    31061197.86
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    107022.51
                  </td>
                  
                  <td>
                    1.34
                  </td>
                </tr>
                
                <tr>
                  <th>
                    min
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1015497.00
                  </td>
                  
                  <td>
                    13.83
                  </td>
                  
                  <td>
                    45.00
                  </td>
                  
                  <td>
                    3.81
                  </td>
                </tr>
                
                <tr>
                  <th>
                    25%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    2.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1954081.00
                  </td>
                  
                  <td>
                    14.49
                  </td>
                  
                  <td>
                    1089.50
                  </td>
                  
                  <td>
                    6.99
                  </td>
                </tr>
                
                <tr>
                  <th>
                    50%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    5.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    4179577.00
                  </td>
                  
                  <td>
                    15.25
                  </td>
                  
                  <td>
                    2134.00
                  </td>
                  
                  <td>
                    7.67
                  </td>
                </tr>
                
                <tr>
                  <th>
                    75%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    12.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    10633968.00
                  </td>
                  
                  <td>
                    16.18
                  </td>
                  
                  <td>
                    3481.00
                  </td>
                  
                  <td>
                    8.16
                  </td>
                </tr>
                
                <tr>
                  <th>
                    max
                  </th>
                  
                  <td>
                    10.00
                  </td>
                  
                  <td>
                    11004.00
                  </td>
                  
                  <td>
                    59.00
                  </td>
                  
                  <td>
                    219.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    209986539.00
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    721419.00
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                8 rows × 11 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    If you&#8217;d like to see the help for the describe function
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">DataFrame</span><span class="o">.</span><span class="n">describe</span><span class="err">?</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    Use the <i>dir</i> function to get an alphabetical listing of valid names (attributes) in an object.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[93]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="nb">dir</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">())</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    CHANGE TO TWO DECIMALS (n.b. &#8211; This step is not necessary if you have run the display.float_format command earlier)
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[88]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[88]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    hashtag_count
                  </th>
                  
                  <th>
                    like_count_14days
                  </th>
                  
                  <th>
                    comment_count_14days
                  </th>
                  
                  <th>
                    share_count_14days
                  </th>
                  
                  <th>
                    source_External
                  </th>
                  
                  <th>
                    video_dummy
                  </th>
                  
                  <th>
                    picture_dummy
                  </th>
                  
                  <th>
                    Total_Revenue
                  </th>
                  
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <th>
                    followers_count
                  </th>
                  
                  <th>
                    Log_of_Followers
                  </th>
                </tr>
                
                <tr>
                  <th>
                    count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    1500.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    mean
                  </th>
                  
                  <td>
                    0.48
                  </td>
                  
                  <td>
                    30.59
                  </td>
                  
                  <td>
                    0.59
                  </td>
                  
                  <td>
                    3.11
                  </td>
                  
                  <td>
                    0.42
                  </td>
                  
                  <td>
                    0.03
                  </td>
                  
                  <td>
                    0.88
                  </td>
                  
                  <td>
                    11486117.19
                  </td>
                  
                  <td>
                    15.36
                  </td>
                  
                  <td>
                    20150.46
                  </td>
                  
                  <td>
                    7.79
                  </td>
                </tr>
                
                <tr>
                  <th>
                    std
                  </th>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    355.34
                  </td>
                  
                  <td>
                    2.62
                  </td>
                  
                  <td>
                    14.95
                  </td>
                  
                  <td>
                    0.49
                  </td>
                  
                  <td>
                    0.18
                  </td>
                  
                  <td>
                    0.33
                  </td>
                  
                  <td>
                    31061197.86
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    107022.51
                  </td>
                  
                  <td>
                    1.34
                  </td>
                </tr>
                
                <tr>
                  <th>
                    min
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1015497.00
                  </td>
                  
                  <td>
                    13.83
                  </td>
                  
                  <td>
                    45.00
                  </td>
                  
                  <td>
                    3.81
                  </td>
                </tr>
                
                <tr>
                  <th>
                    25%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    2.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1954081.00
                  </td>
                  
                  <td>
                    14.49
                  </td>
                  
                  <td>
                    1089.50
                  </td>
                  
                  <td>
                    6.99
                  </td>
                </tr>
                
                <tr>
                  <th>
                    50%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    5.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    4179577.00
                  </td>
                  
                  <td>
                    15.25
                  </td>
                  
                  <td>
                    2134.00
                  </td>
                  
                  <td>
                    7.67
                  </td>
                </tr>
                
                <tr>
                  <th>
                    75%
                  </th>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    12.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    10633968.00
                  </td>
                  
                  <td>
                    16.18
                  </td>
                  
                  <td>
                    3481.00
                  </td>
                  
                  <td>
                    8.16
                  </td>
                </tr>
                
                <tr>
                  <th>
                    max
                  </th>
                  
                  <td>
                    10.00
                  </td>
                  
                  <td>
                    11004.00
                  </td>
                  
                  <td>
                    59.00
                  </td>
                  
                  <td>
                    219.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    209986539.00
                  </td>
                  
                  <td>
                    19.16
                  </td>
                  
                  <td>
                    721419.00
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                8 rows × 11 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    NOW LET&#8217;S TRANSPOSE THE OUTPUT &#8212; necessary for a more typical social scientific presentation of the data
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[89]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">T</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[89]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    count
                  </th>
                  
                  <th>
                    mean
                  </th>
                  
                  <th>
                    std
                  </th>
                  
                  <th>
                    min
                  </th>
                  
                  <th>
                    25%
                  </th>
                  
                  <th>
                    50%
                  </th>
                  
                  <th>
                    75%
                  </th>
                  
                  <th>
                    max
                  </th>
                </tr>
                
                <tr>
                  <th>
                    hashtag_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.48
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    10.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    like_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    30.59
                  </td>
                  
                  <td>
                    355.34
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    2.00
                  </td>
                  
                  <td>
                    5.00
                  </td>
                  
                  <td>
                    12.00
                  </td>
                  
                  <td>
                    11004.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    comment_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.59
                  </td>
                  
                  <td>
                    2.62
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    59.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    share_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    3.11
                  </td>
                  
                  <td>
                    14.95
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    219.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    source_External
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.42
                  </td>
                  
                  <td>
                    0.49
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    video_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.03
                  </td>
                  
                  <td>
                    0.18
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    picture_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.88
                  </td>
                  
                  <td>
                    0.33
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    11486117.19
                  </td>
                  
                  <td>
                    31061197.86
                  </td>
                  
                  <td>
                    1015497.00
                  </td>
                  
                  <td>
                    1954081.00
                  </td>
                  
                  <td>
                    4179577.00
                  </td>
                  
                  <td>
                    10633968.00
                  </td>
                  
                  <td>
                    209986539.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    15.36
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    13.83
                  </td>
                  
                  <td>
                    14.49
                  </td>
                  
                  <td>
                    15.25
                  </td>
                  
                  <td>
                    16.18
                  </td>
                  
                  <td>
                    19.16
                  </td>
                </tr>
                
                <tr>
                  <th>
                    followers_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    20150.46
                  </td>
                  
                  <td>
                    107022.51
                  </td>
                  
                  <td>
                    45.00
                  </td>
                  
                  <td>
                    1089.50
                  </td>
                  
                  <td>
                    2134.00
                  </td>
                  
                  <td>
                    3481.00
                  </td>
                  
                  <td>
                    721419.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Followers
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    7.79
                  </td>
                  
                  <td>
                    1.34
                  </td>
                  
                  <td>
                    3.81
                  </td>
                  
                  <td>
                    6.99
                  </td>
                  
                  <td>
                    7.67
                  </td>
                  
                  <td>
                    8.16
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                11 rows × 8 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    We won&#8217;t typically want the percentile columns in a social scientific publication. In version 0.16 of PANDAS, you can use &#8216;percentiles=None&#8217; with the describe command to omit the percentiles. In PANDAS 0.13 we can instead select only those columns we want, then output to CSV
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[90]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">T</span><span class="p">[[</span><span class="s">&#39;count&#39;</span><span class="p">,</span><span class="s">&#39;mean&#39;</span><span class="p">,</span> <span class="s">&#39;std&#39;</span><span class="p">,</span> <span class="s">&#39;min&#39;</span><span class="p">,</span> <span class="s">&#39;max&#39;</span><span class="p">]]</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[90]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    count
                  </th>
                  
                  <th>
                    mean
                  </th>
                  
                  <th>
                    std
                  </th>
                  
                  <th>
                    min
                  </th>
                  
                  <th>
                    max
                  </th>
                </tr>
                
                <tr>
                  <th>
                    hashtag_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.48
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    10.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    like_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    30.59
                  </td>
                  
                  <td>
                    355.34
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    11004.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    comment_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.59
                  </td>
                  
                  <td>
                    2.62
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    59.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    share_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    3.11
                  </td>
                  
                  <td>
                    14.95
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    219.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    source_External
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.42
                  </td>
                  
                  <td>
                    0.49
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    video_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.03
                  </td>
                  
                  <td>
                    0.18
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    picture_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.88
                  </td>
                  
                  <td>
                    0.33
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    11486117.19
                  </td>
                  
                  <td>
                    31061197.86
                  </td>
                  
                  <td>
                    1015497.00
                  </td>
                  
                  <td>
                    209986539.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    15.36
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    13.83
                  </td>
                  
                  <td>
                    19.16
                  </td>
                </tr>
                
                <tr>
                  <th>
                    followers_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    20150.46
                  </td>
                  
                  <td>
                    107022.51
                  </td>
                  
                  <td>
                    45.00
                  </td>
                  
                  <td>
                    721419.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Followers
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    7.79
                  </td>
                  
                  <td>
                    1.34
                  </td>
                  
                  <td>
                    3.81
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                11 rows × 5 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[92]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="c">#ALTERNATIVE WAY OF WRITING</span>
<span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">transpose</span><span class="p">()</span>
</pre>
      </div>
    </div>
  </div>
  
  <div class="vbox output_wrapper">
    <div class="output vbox">
      <div class="hbox output_area">
        <div class="prompt output_prompt">
          Out[92]:
        </div>
        
        <div class="box-flex1 output_subarea output_pyout">
          <div class="output_html rendered_html">
            <div style="max-height:1000px;max-width:1500px;overflow:auto;">
              <table border="1" class="dataframe">
                <tr style="text-align: right;">
                  <th>
                  </th>
                  
                  <th>
                    count
                  </th>
                  
                  <th>
                    mean
                  </th>
                  
                  <th>
                    std
                  </th>
                  
                  <th>
                    min
                  </th>
                  
                  <th>
                    25%
                  </th>
                  
                  <th>
                    50%
                  </th>
                  
                  <th>
                    75%
                  </th>
                  
                  <th>
                    max
                  </th>
                </tr>
                
                <tr>
                  <th>
                    hashtag_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.48
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    10.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    like_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    30.59
                  </td>
                  
                  <td>
                    355.34
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    2.00
                  </td>
                  
                  <td>
                    5.00
                  </td>
                  
                  <td>
                    12.00
                  </td>
                  
                  <td>
                    11004.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    comment_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.59
                  </td>
                  
                  <td>
                    2.62
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    59.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    share_count_14days
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    3.11
                  </td>
                  
                  <td>
                    14.95
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    219.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    source_External
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.42
                  </td>
                  
                  <td>
                    0.49
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    video_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.03
                  </td>
                  
                  <td>
                    0.18
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    picture_dummy
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    0.88
                  </td>
                  
                  <td>
                    0.33
                  </td>
                  
                  <td>
                    0.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                  
                  <td>
                    1.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    11486117.19
                  </td>
                  
                  <td>
                    31061197.86
                  </td>
                  
                  <td>
                    1015497.00
                  </td>
                  
                  <td>
                    1954081.00
                  </td>
                  
                  <td>
                    4179577.00
                  </td>
                  
                  <td>
                    10633968.00
                  </td>
                  
                  <td>
                    209986539.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Total_Revenue
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    15.36
                  </td>
                  
                  <td>
                    1.12
                  </td>
                  
                  <td>
                    13.83
                  </td>
                  
                  <td>
                    14.49
                  </td>
                  
                  <td>
                    15.25
                  </td>
                  
                  <td>
                    16.18
                  </td>
                  
                  <td>
                    19.16
                  </td>
                </tr>
                
                <tr>
                  <th>
                    followers_count
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    20150.46
                  </td>
                  
                  <td>
                    107022.51
                  </td>
                  
                  <td>
                    45.00
                  </td>
                  
                  <td>
                    1089.50
                  </td>
                  
                  <td>
                    2134.00
                  </td>
                  
                  <td>
                    3481.00
                  </td>
                  
                  <td>
                    721419.00
                  </td>
                </tr>
                
                <tr>
                  <th>
                    Log_of_Followers
                  </th>
                  
                  <td>
                    1500.00
                  </td>
                  
                  <td>
                    7.79
                  </td>
                  
                  <td>
                    1.34
                  </td>
                  
                  <td>
                    3.81
                  </td>
                  
                  <td>
                    6.99
                  </td>
                  
                  <td>
                    7.67
                  </td>
                  
                  <td>
                    8.16
                  </td>
                  
                  <td>
                    13.49
                  </td>
                </tr>
              </table>
              
              <p>
                11 rows × 8 columns
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <h3 id="Save-the-Output-of-the-Table-as-a-CSV-File">
    Save the Output of the Table as a CSV File<a class="anchor-link" href="#Save-the-Output-of-the-Table-as-a-CSV-File">&#182;</a>
  </h3>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
    We can use the above commands and output to CSV
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[41]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="c">#WITH FOUR DECIMAL PLACES (DEFAULT)</span>
<span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span><span class="o">.</span><span class="n">transpose</span><span class="p">()</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s">&#39;summary stats.csv&#39;</span><span class="p">,</span> <span class="n">sep</span><span class="o">=</span><span class="s">&#39;,&#39;</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    For a typical social scientific publication, we would not need the percentile columns. In version 0.16 of PANDAS, you can use &#8216;percentiles=None&#8217; with the describe command to omit the percentiles. In PANDAS 0.13 we can instead select only those columns we want, then output to CSV
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[42]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">()</span><span class="o">.</span><span class="n">transpose</span><span class="p">()[[</span><span class="s">&#39;count&#39;</span><span class="p">,</span><span class="s">&#39;mean&#39;</span><span class="p">,</span> <span class="s">&#39;std&#39;</span><span class="p">,</span> <span class="s">&#39;min&#39;</span><span class="p">,</span> <span class="s">&#39;max&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s">&#39;summary stats.csv&#39;</span><span class="p">,</span> <span class="n">sep</span><span class="o">=</span><span class="s">&#39;,&#39;</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    The problem with the above output is that more than 2 decimal places are showing. If you want only two, then run the following version.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[43]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="c">#WITH TWO DECIMAL PLACES</span>
<span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">T</span><span class="p">[[</span><span class="s">&#39;count&#39;</span><span class="p">,</span><span class="s">&#39;mean&#39;</span><span class="p">,</span> <span class="s">&#39;std&#39;</span><span class="p">,</span> <span class="s">&#39;min&#39;</span><span class="p">,</span> <span class="s">&#39;max&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s">&#39;summary stats.csv&#39;</span><span class="p">,</span> <span class="n">sep</span><span class="o">=</span><span class="s">&#39;,&#39;</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>

<div class="text_cell_render border-box-sizing rendered_html">
  <p>
  </p>
  
  <p>
    Now you have a CSV file containing the columns you&#8217;ll need for a typical Summary Statistics or Descriptive Statistics table for a submission to a social science journal. You likely won&#8217;t want all of the columns in the final table, so I would probably open up the CSV file in Excel, delete unwanted variables, then copy and paste into Word. At that point you just need some formatting for aesthetics. If you do want to select which specific variables to include, you can specify the columns like this.
  </p>
</div>

<div class="cell border-box-sizing code_cell vbox">
  <div class="input hbox">
    <div class="prompt input_prompt">
      In&nbsp;[55]:
    </div>
    
    <div class="input_area box-flex1">
      <div class="highlight">
        <pre><span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s">&#39;hashtag_count&#39;</span><span class="p">,</span><span class="s">&#39;like_count_14days&#39;</span><span class="p">]</span>
<span class="n">np</span><span class="o">.</span><span class="n">round</span><span class="p">(</span><span class="n">df</span><span class="p">[</span><span class="n">cols</span><span class="p">]</span><span class="o">.</span><span class="n">describe</span><span class="p">(),</span> <span class="mi">2</span><span class="p">)</span><span class="o">.</span><span class="n">T</span><span class="p">[[</span><span class="s">&#39;count&#39;</span><span class="p">,</span><span class="s">&#39;mean&#39;</span><span class="p">,</span> <span class="s">&#39;std&#39;</span><span class="p">,</span> <span class="s">&#39;min&#39;</span><span class="p">,</span> <span class="s">&#39;max&#39;</span><span class="p">]]</span><span class="o">.</span><span class="n">to_csv</span><span class="p">(</span><span class="s">&#39;summary stats (partial).csv&#39;</span><span class="p">,</span> <span class="n">sep</span><span class="o">=</span><span class="s">&#39;,&#39;</span><span class="p">)</span>
</pre>
      </div>
    </div>
  </div>
</div>

</body>  
</html>

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>