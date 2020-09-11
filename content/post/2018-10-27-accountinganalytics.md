---
title: What is Accounting Analytics?
author: Gregory Saxton
type: post
date: 2018-10-27T18:10:28+00:00
url: /accountinganalytics/
featured_image: /wp-content/uploads/2018/10/venn.png
dsq_thread_id:
  - 7000385066
categories:
  - Accounting Analytics
  - Big Data
  - Data Analytics
  - jupyter_notebook
  - notebooks
  - pandas
  - python
tags:
  - AccountingAnalytics
  - Big Data
  - Data Analytics
  - MongoDB
  - nonprofits
  - python
  - research

---

One of the buzz-words in business schools is _data analytics_ or, in an accounting school, _accounting analytics_. But what exactly is &#8216;accounting analytics&#8217;? How is it different from existing tools and disciplines such as &#8216;statistics&#8217;, &#8216;computer science&#8217;, &#8216;machine learning, &#8216;Big Data&#8217;, or &#8216;managerial accounting&#8217;? In this post I will disentangle this emerging field. This is a first crack at this issue &#8212; I will continue to edit as the field (and my understanding of it) develops.

# Accounting Analytics Defined

Accounting analytics, in a nutshell, is the examination of _Big Data_ using _data science_ or _data analytics_ tools to help answer accounting-related questions. Let&#8217;s break that down further.

# The Emergence of _Big Data_

The first piece of the puzzle is \`Big Data.&#8217; Big Data is different from previous forms of data in terms of _volume_, _variety_, and _velocity_: There is a lot more of it, it comes in a variety of structures and formats, and it is updated and produced quickly. Any of the following might be considered sources of Big Data for an accounting analytics project:

  * social media data
  * web search data
  * journal entries
  * transactional data (e.g., customer transactions)
  * call centre transcripts
  * store videos, web cams, etc.
  * online customer reviews
  * XBRL
  * proprietary databases
  * websites
  * IoT devices
  * image repositories
  * sensor data
  * public data (crime, health, education, etc.)
  * media/journalism
  * weather forecasts
  * company emails
  * company disclosures

There are lots of good articles and blog posts out there on this point. The key to recognize is that Big Data goes beyond just social media data. 

# The Emergence of _Data Science_

The second piece of the puzzle is \`Data Science.&#8217; Data scientists examine Big Data using a combination of programming skills, statistical skills, and domain knowledge to answer relevant organizational or societal questions.

<img src="http://social-metrics.org/wp-content/uploads/2018/10/venn.png" />

Data science has emerged in the past decade with the emergence of Big Data and the concurrent development of readily accessible sophisticated computing tools. At its core, data science is a field, or perhaps an approach, that lies at the intersection of three things: 1) computer programming, or &#8216;hacking&#8217;, skills; 2) mathematical and (especially) statistical skills; and 3) domain expertise. 

![This is an image](/wp-content/uploads/2018/10/venn.png)



Programming skills are needed to help access and download Big Data, to \`wrangle&#8217; the data into a usable state, and to write programs that can run sophisticated machine learning and related algorithms. Statistical skills are needed to ensure the appropriate research design methodologies are followed and statistical techniques applied; without this, your projects findings will not have validity. Finally, domain expertise is needed in order to identify questions that are worth answering. In accounting analytics, domain expertise is knowledge about the business and industry along with understanding of the accounting information system. 

### Data Analytics vs. Data Science

There does not appear to be a consensus on the distinction between &#8216;data science&#8217; and &#8216;data analytics.&#8217; You can refer to a number of articles and blog posts that attempt to describe the difference. For example, some think of data analytics as a narrower sub-field of data science. To my mind, however, the two terms are more or less synonymous. Accordingly, accounting analytics can be thought of as the use of data science/data analytics techniques to answer accounting-related questions. 

### Generic Data Analytics Tools

A well-rounded data scientist needs to have a broad ranges of tools and techniques in her toolkit. We might think of these as encompassing four stages of the process: 1) data gathering, 2) data wrangling, 3) data management, and 4) data analysis. 

##### Data Gathering

Hacking skills are indispensable for accessing and downloading certain types of Big Data &#8212; particularly social media data. Here the data scientist will need to become familiar with application programming interfaces (APIs). I have written a <a href="http://social-metrics.org/api-keys/" rel="noopener" target="_blank">blog post</a> on how to set up access to the Twitter API, and there are lots of other resources out there. 

##### Data Wrangling

Data wrangling or &#8216;data munging&#8217; is a critical data analytics skill. Once you have the data you then need to get it into a usable format. This might involve generating &#8216;pivot tables&#8217; in Excel or PANDAS or R, or aggregating a time-series dataset to the daily or weekly or monthly level, or generating a series of new variables (aka &#8216;feature engineering&#8217;). And it might involve all of these things. Big Data are often _unstructured_ data, meaning they are lacking pre-defined fields (aka &#8216;columns&#8217; or &#8216;variables&#8217;) and linkages across databases. I don&#8217;t want to devote too much time to this issue as you&#8217;ll find plenty of resources online. The key takeaway is that data wrangling is something any social scientist or other type of researcher is familiar with &#8212; with Big Data there are just additional challenges in terms of scope and nature of the issues you&#8217;ll be dealing with. 

##### Data Management

Data scientists should have familiarity with database management. There are lots of options out there, ranging from traditional relational databases such as SQL to &#8216;noSQL&#8217; databases such as MongoDB. In my own research I have recently leaned toward the MongoDB approach, but the data scientist may not have a choice. For this reason a solid understanding of both major approaches is helpful. 

##### Data Analysis

Once you have the data in usable format and you&#8217;ve found a question worth answering, you then need to _analyze_ the data. There is a huge range of techniques for analyzing the data. In my training as a social scientist and then accounting scholar, I was trained to think of two broad sets of techniques &#8212; _descriptive statistics_ and _inferential statistics_. Examples of the former are the mean, mode, median, and standard deviation, and are used to describe the data that you&#8217;re working with. To help deliver answers to a given research question, we then turn to a wide range of more advanced statistical techniques, including ordinary least squares (OLS) regression, logistic regression, negative binomial regression, etc.

Data scientists avail themselves of all these techniques in addition to a much broader range of tools. This is due in part to the rapidly developing field of computer science as well as the different types of questions data scientists are asking (it is a long story, but the crux of the argument is &#8216;prediction vs. explanation&#8217;). 

Here the data scientist will be familiar with all of the &#8216;buzzwords&#8217; &#8212; artificial intelligence, deep learning, machine learning, text mining, sentiment analysis, clustering, and more. Again, I don&#8217;t want to reinvent the wheel, so any number of articles out there can explain these tools and how they are applied in data analytics.

# Accounting Analytics

OK, by this point I hope you have a better sense of what &#8216;data science&#8217; is. What you may not see is how this is practically applied in the field of _accounting analytics_. Here I have a somewhat different take than other articles and blog posts I&#8217;ve read. Most of them seem to categorize data analytics and/or accounting analytics questions into a &#8216;descriptive&#8217; (what is happening) vs. &#8216;retrospective&#8217; (backward-looking) vs. &#8216;prospective&#8217; (what will happen) framework. While accounting analytics is certainly used for description, retrospection, and prediction, I prefer to approach this field differently. Namely, I focus on two main research questions: 1) measurement and 2) finding relationships.

### Measuring Accounting Concepts

A first set of accounting analytics questions are designed to help _measure_ an accounting-related concept. Accounting is inherently a &#8216;measurement discipline&#8217;, but accounting information systems are not equipped to deliver insights into all variables of interest. Here&#8217;s a concrete example. Let&#8217;s take an intangible asset such as a company&#8217;s _brand community_. The company has built this intangible asset itself so it is off the books &#8212; it will not be seen on the balance sheet and thus will not automatically be measured. 

As shown in the figure below, it is critical that the accounting analytics practitioner first recognize that the notion of &#8216;brand community&#8217; exists at the conceptual level &#8212; we have no solid concrete measure of it. Instead, we need to examine a range of different indicators that, collectively, can help us _measure_ this concept. The figure below shows four variables, or indicators, that could be examined to help infer the strength of the company&#8217;s brand community. 

[<img loading="lazy" src="http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible.png" alt="" width="2742" height="1628" class="alignnone size-full wp-image-2457" srcset="http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible.png 2742w, http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible-300x178.png 300w, http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible-768x456.png 768w, http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible-1024x608.png 1024w" sizes="(max-width: 2742px) 100vw, 2742px" />][2]

![This is an image](/wp-content/uploads/2018/10/measurement-of-intangible.png)

None of these indicators in isolation would suffice. It is only by &#8216;triangulating&#8217; our findings that we are able to make any valid inferences. And it is only by employing data analytic techniques that we are able to gather and wrangle these data.

Most accounting students are not trained in separating the conceptual from the measurement level, yet it is a critical piece of the puzzle. It is one of the core competencies of the data scientist&#8217;s training in statistics and methods.

### Finding Relationships

The second type of accounting analytics question addressed is the _search for relationships_ between one variable and another. For example, the accounting analytics practitioner might be interested in what behaviors predict fraud. This is the search for the relationship between some set of &#8216;X&#8217; behaviors and a &#8216;Y&#8217; outcome variable (fraud). This is an &#8216;accounting&#8217; analytics question because of the accounting-related variable fraud. 

Similarly, the analytics practitioner might wish to segment job applicants into &#8216;good&#8217; and &#8216;bad&#8217; applicants. The analytical tool might involve a _clustering_ algorithm, and as in the above example, &#8216;under the hood&#8217; the analyst is using a variety of variables help separate promising from less promising applicants. In other words, the exercise involves finding patterns built concerning the relationship between a bunch of &#8220;X&#8217;s&#8221; and an outcome variable &#8220;Y&#8221; (job applicant quality).


<img src="/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13.png" />


I&#8217;ll give one last example here. The figure below shows an accounting-related variable _sales_. Sales data would already be gathered in the accounting information system. Here is where many accountants would stop. Accounting analytics, however, brings something new to the table. Namely, accounting analytics is not only interested in measuring sales but in relating sales to other variables. In other words, the accounting analytics practitioner is keenly interested in seeing what other variables can _predict_ the increase (or decline) in sales. This is the search for relationships. Where data science enters the picture is in two ways. One, inferring relationships is inherently a statistical or methodological pursuit, and training in statistics is not typically a forte of the accountant. Two, the data employed is often _non-financial_ in nature. Big Data is commonly used and thus data science tools are a necessity. 

<img loading="lazy" src="/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13.png" alt="" width="2232" height="1400" class="alignnone size-full wp-image-2463" srcset="http://social-metrics.org/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13.png 2232w, http://social-metrics.org/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13-300x188.png 300w, http://social-metrics.org/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13-768x482.png 768w, http://social-metrics.org/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13-1024x642.png 1024w" sizes="(max-width: 2232px) 100vw, 2232px" />


![This is an image](/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13.png)

As shown in the figure, the accounting analytics team is interested in predicting future sales for the company. To help answer this question, the team gathers an array of financial data (not shown) as well as non-financial data, including the strength of the online brand community, the number of five-star Amazon reviews, an assessment of the company&#8217;s CSR and sustainability initiatives, weather patterns, and customer complaints. Once these data are gathered and wrangled, operational measures are developed and then statistical analyses are applied. Based on these analyses the team will have answers to what the strongest predictors of sales performance are. 

These are just a few examples. There is a huge range of questions that could be answered using accounting analytics. The key is these questions involve at least one &#8216;accounting&#8217; variable and rely on Big Data and data analytics tools. 

# What The Typical Accountant Needs to Know

The great majority of accountants (and accounting students) are not going to become data scientists. What all practitioners should learn is _data literacy_. They need to know understand what types of questions can be asked (measurement and finding relationships), what types of information are available (Big Data), and what types of analyses can be run. In short, the typical accountant does not need to know how to _do_ data science but does need to understand what data science is. They should, in Cornelissen&#8217;s (2018) words, &#8220;speak the language of data.&#8221; Being &#8216;data literate&#8217; will help you and your team make better requests of the data scientists. As seen in the Henke et al. (2018) article linked below, a recent buzzword points to a new career path for those who are literate in data analytics &#8212; the &#8216;analytics translator.&#8217; 

# Further Reading

This is intended to be a relatively brief overview of the rapidly emerging field of accounting analytics. I hope this article has provided a useful overview. 

Accounting academics and practitioners are rapidly building knowledge of this emerging field. In an update I will add some key academic articles for further reading. For now, I refer you to four brief _Harvard Business Review_ articles. 

  * Andrew McAfee and Erik Brynjolfsson. <a href="https://hbr.org/2012/10/big-data-the-management-revolution" rel="noopener" target="_blank">Big Data: The Management Revolution</a>, _Harvard Business Review_, October 2012. 
  * Hugo Bowne-Anderson. <a href="https://hbr.org/2018/08/what-data-scientists-really-do-according-to-35-data-scientists " rel="noopener" target="_blank">What Data Scientists Really Do, According to 35 Data Scientists.</a>, _Harvard Business Review_, August 15, 2018.
  * Jonathan Cornelissen. <a href="https://hbr.org/2018/07/the-democratization-of-data-science" rel="noopener" target="_blank">The Democratization of Data Science.</a>, _Harvard Business Review_, July 27, 2018.
  * Nicolaus Henke, Jordan Levine, and Paul McInerney. <a href="https://hbr.org/2018/02/you-dont-have-to-be-a-data-scientist-to-fill-this-must-have-analytics-role?autocomplete=true" rel="noopener" target="_blank">You Don’t Have to Be a Data Scientist to Fill This Must-Have Analytics Role.</a>, _Harvard Business Review_, February 5, 2018. (Also available <a href="https://www.mckinsey.com/business-functions/mckinsey-analytics/our-insights/analytics-translator" rel="noopener" target="_blank">here</a>)

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>

 [1]: http://social-metrics.org/wp-content/uploads/2018/10/venn.png
 [2]: http://social-metrics.org/wp-content/uploads/2018/10/measurement-of-intangible.png
 [3]: http://social-metrics.org/wp-content/uploads/2018/10/Screenshot-2018-10-27-13.20.13.png