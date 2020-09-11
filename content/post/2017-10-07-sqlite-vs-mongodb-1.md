---
title: SQLite vs. MongoDB for Downloading Twitter Data (copy)
author: Gregory Saxton
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=1738
categories:
  - Big Data
  - python
  - Twitter
tags:
  - Big Data
  - Database
  - Programming
  - python
  - social media
  - socialmedia
  - tutorial
  - Twitter

---
In <a href="http://social-metrics.org/downloading-tweets-by-a-list-of-users-take2/" rel="noopener" target="_blank">my latest tutorial</a> I walked readers through a Python script designed to download tweets by a set of Twitter users and insert them into an SQLite database. In this post I will provide my own thoughts on the pros and cons of using a relational database such as SQLite vs. a &#8220;<a href="https://en.wikipedia.org/wiki/NoSQL" target="_blank">noSQL</a>&#8221; database such as MongoDB. These are my two go-to databases for downloading and managing Big Data and there are definite advantages and disadvantages to each.

The caveat is that this discussion is for researchers. Businesses will almost definitely not want to use SQLite for anything but simple applications. 

### The Pros and Cons of SQLite

SQLite has a lot going for it. I _much_ prefer SQLite over, say, SQL.

### The Pros and Cons of MongoDB

The Twitter API returns a JSON object for each tweet. In <a href="http://social-metrics.org/twitter-user-data/" rel="noopener" target="_blank">a prior tutorial</a> I provide an overview of this. For instance, a tweet object looks like this:

<pre class="brush: plain; light: false; title: ; toolbar: true; notranslate" title="">{
    &quot;_id&quot; : ObjectId(&quot;595a71173ffc5a01d8f27de7&quot;),
    &quot;contributors&quot; : null,
    &quot;quoted_status_id&quot; : NumberLong(880805966375202816),
    &quot;text&quot; : &quot;RT @FL_Bar_Found: Thank you for your support, Stephanie! https://t.co/2vxXe3VnTU&quot;,
    &quot;time_date_inserted&quot; : &quot;12:30:15_03/07/2017&quot;,
    &quot;query_screen_name&quot; : &quot;@FL_Bar_Found&quot;,
    &quot;is_quote_status&quot; : true,
    &quot;in_reply_to_status_id&quot; : null,
    &quot;id&quot; : NumberLong(881145993059864580),
    &quot;favorite_count&quot; : 0,
    &quot;source&quot; : &quot;&lt;a href=&quot;http://twitter.com/download/iphone&quot; rel=&quot;nofollow&quot;&gt;Twitter for iPhone&lt;/a&gt;&quot;,
    &quot;truncated&quot; : false,
    &quot;retweeted&quot; : false,
    &quot;coordinates&quot; : null,
    &quot;entities&quot; : {
        &quot;symbols&quot; : [],
        &quot;user_mentions&quot; : [ 
            {
                &quot;indices&quot; : [ 
                    3, 
                    16
                ],
                &quot;screen_name&quot; : &quot;FL_Bar_Found&quot;,
                &quot;id&quot; : NumberLong(2680494548),
                &quot;name&quot; : &quot;FloridaBarFoundation&quot;,
                &quot;id_str&quot; : &quot;2680494548&quot;
            }
        ],
        &quot;hashtags&quot; : [],
        &quot;urls&quot; : [ 
            {
                &quot;url&quot; : &quot;https://t.co/2vxXe3VnTU&quot;,
                &quot;indices&quot; : [ 
                    57, 
                    80
                ],
                &quot;expanded_url&quot; : &quot;https://twitter.com/theflabar/status/880805966375202816&quot;,
                &quot;display_url&quot; : &quot;twitter.com/theflabar/stat…&quot;
            }
        ]
    },
    &quot;date_inserted&quot; : &quot;03/07/2017&quot;,
    &quot;in_reply_to_screen_name&quot; : null,
    &quot;in_reply_to_user_id&quot; : null,
    &quot;retweet_count&quot; : 2,
    &quot;id_str&quot; : &quot;881145993059864580&quot;,
    &quot;favorited&quot; : false,
    &quot;retweeted_status&quot; : {
        &quot;contributors&quot; : null,
        &quot;truncated&quot; : false,
        &quot;text&quot; : &quot;Thank you for your support, Stephanie! https://t.co/2vxXe3VnTU&quot;,
        &quot;is_quote_status&quot; : true,
        &quot;in_reply_to_status_id&quot; : null,
        &quot;id&quot; : NumberLong(880957463801057281),
        &quot;favorite_count&quot; : 5,
        &quot;source&quot; : &quot;&lt;a href=&quot;http://twitter.com/download/iphone&quot; rel=&quot;nofollow&quot;&gt;Twitter for iPhone&lt;/a&gt;&quot;,
        &quot;quoted_status_id&quot; : NumberLong(880805966375202816),
        &quot;retweeted&quot; : false,
        &quot;coordinates&quot; : null,
        &quot;quoted_status&quot; : {
            &quot;contributors&quot; : null,
            &quot;truncated&quot; : true,
            &quot;text&quot; : &quot;New @FlaBarYLD #ProBono Chair Stephanie Cagnet Myron @CagnetMyronLaw has only been at work 1 week - but she's busy!… https://t.co/nASTbHyuzW&quot;,
            &quot;is_quote_status&quot; : false,
            &quot;in_reply_to_status_id&quot; : null,
            &quot;id&quot; : NumberLong(880805966375202816),
            &quot;favorite_count&quot; : 12,
            &quot;source&quot; : &quot;&lt;a href=&quot;http://twitter.com&quot; rel=&quot;nofollow&quot;&gt;Twitter Web Client&lt;/a&gt;&quot;,
            &quot;retweeted&quot; : false,
            &quot;coordinates&quot; : null,
            &quot;entities&quot; : {
                &quot;symbols&quot; : [],
                &quot;user_mentions&quot; : [ 
                    {
                        &quot;indices&quot; : [ 
                            4, 
                            14
                        ],
                        &quot;screen_name&quot; : &quot;FlaBarYLD&quot;,
                        &quot;id&quot; : 460499634,
                        &quot;name&quot; : &quot;Florida Bar YLD&quot;,
                        &quot;id_str&quot; : &quot;460499634&quot;
                    }, 
                    {
                        &quot;indices&quot; : [ 
                            53, 
                            68
                        ],
                        &quot;screen_name&quot; : &quot;CagnetMyronLaw&quot;,
                        &quot;id&quot; : NumberLong(4850153337),
                        &quot;name&quot; : &quot;Cagnet Myron Law, PA&quot;,
                        &quot;id_str&quot; : &quot;4850153337&quot;
                    }
                ],
                &quot;hashtags&quot; : [ 
                    {
                        &quot;indices&quot; : [ 
                            15, 
                            23
                        ],
                        &quot;text&quot; : &quot;ProBono&quot;
                    }
                ],
                &quot;urls&quot; : [ 
                    {
                        &quot;url&quot; : &quot;https://t.co/nASTbHyuzW&quot;,
                        &quot;indices&quot; : [ 
                            117, 
                            140
                        ],
                        &quot;expanded_url&quot; : &quot;https://twitter.com/i/web/status/880805966375202816&quot;,
                        &quot;display_url&quot; : &quot;twitter.com/i/web/status/8…&quot;
                    }
                ]
            },
            &quot;in_reply_to_screen_name&quot; : null,
            &quot;id_str&quot; : &quot;880805966375202816&quot;,
            &quot;retweet_count&quot; : 2,
            &quot;in_reply_to_user_id&quot; : null,
            &quot;favorited&quot; : false,
            &quot;user&quot; : {
                &quot;follow_request_sent&quot; : null,
                &quot;has_extended_profile&quot; : false,
                &quot;profile_use_background_image&quot; : true,
                &quot;time_zone&quot; : &quot;Pacific Time (US &amp; Canada)&quot;,
                &quot;id&quot; : 1024389338,
                &quot;default_profile&quot; : true,
                &quot;verified&quot; : true,
                &quot;profile_text_color&quot; : &quot;333333&quot;,
                &quot;profile_image_url_https&quot; : &quot;https://pbs.twimg.com/profile_images/489757746669944832/qL0j6UB1_normal.jpeg&quot;,
                &quot;profile_sidebar_fill_color&quot; : &quot;DDEEF6&quot;,
                &quot;is_translator&quot; : false,
                &quot;geo_enabled&quot; : true,
                &quot;entities&quot; : {
                    &quot;url&quot; : {
                        &quot;urls&quot; : [ 
                            {
                                &quot;url&quot; : &quot;http://t.co/h6TDPEl3jy&quot;,
                                &quot;indices&quot; : [ 
                                    0, 
                                    22
                                ],
                                &quot;expanded_url&quot; : &quot;http://www.FloridaBar.org&quot;,
                                &quot;display_url&quot; : &quot;FloridaBar.org&quot;
                            }
                        ]
                    },
                    &quot;description&quot; : {
                        &quot;urls&quot; : []
                    }
                },
                &quot;followers_count&quot; : 10418,
                &quot;protected&quot; : false,
                &quot;id_str&quot; : &quot;1024389338&quot;,
                &quot;default_profile_image&quot; : false,
                &quot;listed_count&quot; : 498,
                &quot;lang&quot; : &quot;en&quot;,
                &quot;utc_offset&quot; : -25200,
                &quot;statuses_count&quot; : 75802,
                &quot;description&quot; : &quot;Statewide professional organization of lawyers that serves as an advocate &amp; intermediary for attorneys, the court &amp; the public. Retweets are not endorsements.&quot;,
                &quot;friends_count&quot; : 2001,
                &quot;profile_link_color&quot; : &quot;1DA1F2&quot;,
                &quot;profile_image_url&quot; : &quot;http://pbs.twimg.com/profile_images/489757746669944832/qL0j6UB1_normal.jpeg&quot;,
                &quot;notifications&quot; : null,
                &quot;profile_background_image_url_https&quot; : &quot;https://abs.twimg.com/images/themes/theme1/bg.png&quot;,
                &quot;profile_background_color&quot; : &quot;C0DEED&quot;,
                &quot;profile_banner_url&quot; : &quot;https://pbs.twimg.com/profile_banners/1024389338/1377117432&quot;,
                &quot;profile_background_image_url&quot; : &quot;http://abs.twimg.com/images/themes/theme1/bg.png&quot;,
                &quot;name&quot; : &quot;The Florida Bar&quot;,
                &quot;is_translation_enabled&quot; : false,
                &quot;profile_background_tile&quot; : false,
                &quot;favourites_count&quot; : 54326,
                &quot;screen_name&quot; : &quot;theflabar&quot;,
                &quot;url&quot; : &quot;http://t.co/h6TDPEl3jy&quot;,
                &quot;created_at&quot; : &quot;Thu Dec 20 14:46:06 +0000 2012&quot;,
                &quot;contributors_enabled&quot; : false,
                &quot;location&quot; : &quot;Tallahassee, Florida&quot;,
                &quot;profile_sidebar_border_color&quot; : &quot;C0DEED&quot;,
                &quot;translator_type&quot; : &quot;none&quot;,
                &quot;following&quot; : null
            },
            &quot;geo&quot; : null,
            &quot;in_reply_to_user_id_str&quot; : null,
            &quot;possibly_sensitive&quot; : false,
            &quot;lang&quot; : &quot;en&quot;,
            &quot;created_at&quot; : &quot;Fri Jun 30 15:11:21 +0000 2017&quot;,
            &quot;in_reply_to_status_id_str&quot; : null,
            &quot;place&quot; : null,
            &quot;metadata&quot; : {
                &quot;iso_language_code&quot; : &quot;en&quot;,
                &quot;result_type&quot; : &quot;recent&quot;
            }
        },
        &quot;entities&quot; : {
            &quot;symbols&quot; : [],
            &quot;user_mentions&quot; : [],
            &quot;hashtags&quot; : [],
            &quot;urls&quot; : [ 
                {
                    &quot;url&quot; : &quot;https://t.co/2vxXe3VnTU&quot;,
                    &quot;indices&quot; : [ 
                        39, 
                        62
                    ],
                    &quot;expanded_url&quot; : &quot;https://twitter.com/theflabar/status/880805966375202816&quot;,
                    &quot;display_url&quot; : &quot;twitter.com/theflabar/stat…&quot;
                }
            ]
        },
        &quot;in_reply_to_screen_name&quot; : null,
        &quot;id_str&quot; : &quot;880957463801057281&quot;,
        &quot;retweet_count&quot; : 2,
        &quot;in_reply_to_user_id&quot; : null,
        &quot;favorited&quot; : false,
        &quot;user&quot; : {
            &quot;follow_request_sent&quot; : null,
            &quot;has_extended_profile&quot; : false,
            &quot;profile_use_background_image&quot; : false,
            &quot;time_zone&quot; : &quot;Eastern Time (US &amp; Canada)&quot;,
            &quot;id&quot; : NumberLong(2680494548),
            &quot;default_profile&quot; : false,
            &quot;verified&quot; : false,
            &quot;profile_text_color&quot; : &quot;000000&quot;,
            &quot;profile_image_url_https&quot; : &quot;https://pbs.twimg.com/profile_images/821370669573275649/SOQ1xHS3_normal.jpg&quot;,
            &quot;profile_sidebar_fill_color&quot; : &quot;000000&quot;,
            &quot;is_translator&quot; : false,
            &quot;geo_enabled&quot; : true,
            &quot;entities&quot; : {
                &quot;url&quot; : {
                    &quot;urls&quot; : [ 
                        {
                            &quot;url&quot; : &quot;http://t.co/pTHhl5lG9P&quot;,
                            &quot;indices&quot; : [ 
                                0, 
                                22
                            ],
                            &quot;expanded_url&quot; : &quot;http://www.thefloridabarfoundation.org&quot;,
                            &quot;display_url&quot; : &quot;thefloridabarfoundation.org&quot;
                        }
                    ]
                },
                &quot;description&quot; : {
                    &quot;urls&quot; : [ 
                        {
                            &quot;url&quot; : &quot;http://t.co/65UE4Zk0tC&quot;,
                            &quot;indices&quot; : [ 
                                94, 
                                116
                            ],
                            &quot;expanded_url&quot; : &quot;http://bit.ly/13JbjCY&quot;,
                            &quot;display_url&quot; : &quot;bit.ly/13JbjCY&quot;
                        }
                    ]
                }
            },
            &quot;followers_count&quot; : 1533,
            &quot;protected&quot; : false,
            &quot;id_str&quot; : &quot;2680494548&quot;,
            &quot;default_profile_image&quot; : false,
            &quot;listed_count&quot; : 41,
            &quot;lang&quot; : &quot;en&quot;,
            &quot;utc_offset&quot; : -14400,
            &quot;statuses_count&quot; : 2012,
            &quot;description&quot; : &quot;The mission of The Florida Bar Foundation is to provide greater access to justice in Florida. http://t.co/65UE4Zk0tC&quot;,
            &quot;friends_count&quot; : 532,
            &quot;profile_link_color&quot; : &quot;0084B4&quot;,
            &quot;profile_image_url&quot; : &quot;http://pbs.twimg.com/profile_images/821370669573275649/SOQ1xHS3_normal.jpg&quot;,
            &quot;notifications&quot; : null,
            &quot;profile_background_image_url_https&quot; : &quot;https://abs.twimg.com/images/themes/theme1/bg.png&quot;,
            &quot;profile_background_color&quot; : &quot;000000&quot;,
            &quot;profile_banner_url&quot; : &quot;https://pbs.twimg.com/profile_banners/2680494548/1484665070&quot;,
            &quot;profile_background_image_url&quot; : &quot;http://abs.twimg.com/images/themes/theme1/bg.png&quot;,
            &quot;name&quot; : &quot;FloridaBarFoundation&quot;,
            &quot;is_translation_enabled&quot; : false,
            &quot;profile_background_tile&quot; : false,
            &quot;favourites_count&quot; : 2002,
            &quot;screen_name&quot; : &quot;FL_Bar_Found&quot;,
            &quot;url&quot; : &quot;http://t.co/pTHhl5lG9P&quot;,
            &quot;created_at&quot; : &quot;Fri Jul 25 21:17:50 +0000 2014&quot;,
            &quot;contributors_enabled&quot; : false,
            &quot;location&quot; : &quot;Florida&quot;,
            &quot;profile_sidebar_border_color&quot; : &quot;000000&quot;,
            &quot;translator_type&quot; : &quot;none&quot;,
            &quot;following&quot; : null
        },
        &quot;geo&quot; : null,
        &quot;in_reply_to_user_id_str&quot; : null,
        &quot;possibly_sensitive&quot; : false,
        &quot;lang&quot; : &quot;en&quot;,
        &quot;created_at&quot; : &quot;Sat Jul 01 01:13:21 +0000 2017&quot;,
        &quot;quoted_status_id_str&quot; : &quot;880805966375202816&quot;,
        &quot;in_reply_to_status_id_str&quot; : null,
        &quot;place&quot; : {
            &quot;country_code&quot; : &quot;US&quot;,
            &quot;url&quot; : &quot;https://api.twitter.com/1.1/geo/id/00d511d335cd9fb6.json&quot;,
            &quot;country&quot; : &quot;United States&quot;,
            &quot;place_type&quot; : &quot;city&quot;,
            &quot;bounding_box&quot; : {
                &quot;type&quot; : &quot;Polygon&quot;,
                &quot;coordinates&quot; : [ 
                    [ 
                        [ 
                            -81.2445014, 
                            28.489488
                        ], 
                        [ 
                            -81.1256316, 
                            28.489488
                        ], 
                        [ 
                            -81.1256316, 
                            28.568794
                        ], 
                        [ 
                            -81.2445014, 
                            28.568794
                        ]
                    ]
                ]
            },
            &quot;contained_within&quot; : [],
            &quot;full_name&quot; : &quot;Alafaya, FL&quot;,
            &quot;attributes&quot; : {},
            &quot;id&quot; : &quot;00d511d335cd9fb6&quot;,
            &quot;name&quot; : &quot;Alafaya&quot;
        },
        &quot;metadata&quot; : {
            &quot;iso_language_code&quot; : &quot;en&quot;,
            &quot;result_type&quot; : &quot;recent&quot;
        }
    },
    &quot;user&quot; : {
        &quot;follow_request_sent&quot; : null,
        &quot;has_extended_profile&quot; : false,
        &quot;profile_use_background_image&quot; : true,
        &quot;time_zone&quot; : &quot;Eastern Time (US &amp; Canada)&quot;,
        &quot;id&quot; : 493169878,
        &quot;default_profile&quot; : false,
        &quot;verified&quot; : false,
        &quot;profile_text_color&quot; : &quot;333333&quot;,
        &quot;profile_image_url_https&quot; : &quot;https://pbs.twimg.com/profile_images/872490334655270916/jxMbCTKe_normal.jpg&quot;,
        &quot;profile_sidebar_fill_color&quot; : &quot;F3F3F3&quot;,
        &quot;is_translator&quot; : false,
        &quot;geo_enabled&quot; : true,
        &quot;entities&quot; : {
            &quot;url&quot; : {
                &quot;urls&quot; : [ 
                    {
                        &quot;url&quot; : &quot;https://t.co/6sIP0DbThb&quot;,
                        &quot;indices&quot; : [ 
                            0, 
                            23
                        ],
                        &quot;expanded_url&quot; : &quot;http://www.legalaidocba.org&quot;,
                        &quot;display_url&quot; : &quot;legalaidocba.org&quot;
                    }
                ]
            },
            &quot;description&quot; : {
                &quot;urls&quot; : [ 
                    {
                        &quot;url&quot; : &quot;https://t.co/8HiQPlRDyv&quot;,
                        &quot;indices&quot; : [ 
                            133, 
                            156
                        ],
                        &quot;expanded_url&quot; : &quot;https://vimeo.com/190166320&quot;,
                        &quot;display_url&quot; : &quot;vimeo.com/190166320&quot;
                    }
                ]
            }
        },
        &quot;followers_count&quot; : 447,
        &quot;protected&quot; : false,
        &quot;id_str&quot; : &quot;493169878&quot;,
        &quot;default_profile_image&quot; : false,
        &quot;listed_count&quot; : 5,
        &quot;lang&quot; : &quot;en&quot;,
        &quot;utc_offset&quot; : -14400,
        &quot;statuses_count&quot; : 3362,
        &quot;description&quot; : &quot;Development, fundraiser, communications, photographer. Breakfast of Champions boc@legalaidocba.org Retweets do not imply endorsement https://t.co/8HiQPlRDyv&quot;,
        &quot;friends_count&quot; : 2161,
        &quot;profile_link_color&quot; : &quot;990000&quot;,
        &quot;profile_image_url&quot; : &quot;http://pbs.twimg.com/profile_images/872490334655270916/jxMbCTKe_normal.jpg&quot;,
        &quot;notifications&quot; : null,
        &quot;profile_background_image_url_https&quot; : &quot;https://abs.twimg.com/images/themes/theme7/bg.gif&quot;,
        &quot;profile_background_color&quot; : &quot;EBEBEB&quot;,
        &quot;profile_banner_url&quot; : &quot;https://pbs.twimg.com/profile_banners/493169878/1496917809&quot;,
        &quot;profile_background_image_url&quot; : &quot;http://abs.twimg.com/images/themes/theme7/bg.gif&quot;,
        &quot;name&quot; : &quot;Donna Haynes&quot;,
        &quot;is_translation_enabled&quot; : false,
        &quot;profile_background_tile&quot; : false,
        &quot;favourites_count&quot; : 1997,
        &quot;screen_name&quot; : &quot;lasocba&quot;,
        &quot;url&quot; : &quot;https://t.co/6sIP0DbThb&quot;,
        &quot;created_at&quot; : &quot;Wed Feb 15 14:26:11 +0000 2012&quot;,
        &quot;contributors_enabled&quot; : false,
        &quot;location&quot; : &quot;Orlando, Florida&quot;,
        &quot;profile_sidebar_border_color&quot; : &quot;DFDFDF&quot;,
        &quot;translator_type&quot; : &quot;none&quot;,
        &quot;following&quot; : null
    },
    &quot;geo&quot; : null,
    &quot;in_reply_to_user_id_str&quot; : null,
    &quot;possibly_sensitive&quot; : false,
    &quot;lang&quot; : &quot;en&quot;,
    &quot;created_at&quot; : &quot;Sat Jul 01 13:42:30 +0000 2017&quot;,
    &quot;quoted_status_id_str&quot; : &quot;880805966375202816&quot;,
    &quot;in_reply_to_status_id_str&quot; : null,
    &quot;place&quot; : null,
    &quot;metadata&quot; : {
        &quot;iso_language_code&quot; : &quot;en&quot;,
        &quot;result_type&quot; : &quot;recent&quot;
    }
}
</pre>

### Summary [table id=5 /] 

Happy coding!

<div style="padding-bottom:20px; padding-top:10px;" class="hupso-share-buttons">
  <!-- Hupso Share Buttons - https://www.hupso.com/share/ -->
  
  <a class="hupso_toolbar" href="https://www.hupso.com/share/"><img src="http://static.hupso.com/share/buttons/share-medium.png" style="border:0px; padding-top: 5px; float:left;" alt="Share Button" /></a><!-- Hupso Share Buttons -->
</div>