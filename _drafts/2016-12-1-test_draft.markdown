---
layout: post
title:  "webspider"
date:   2016-12-1 18:00:00 -0400
---

### Scala web spider with Jsoup

The scala web spider can be used, as in this simple example, to parse then list links from HTML at a URL.

{% highlight scala %}
// Define a starting link                                                                             
val startingLink = "http://imgur.com/r/cats"                                                          

// Only buffer links from imgur.com                                                                   
val buffer = Spider.Buffer("imgur.com")                                                               

// Start crawling a URL with the spider                                                               
Spider.Crawl("http://imgur.com/r/cats", 1, buffer, Seq("href", "src") : _*)                           

// Create media and link result values, both are URLs as lists of strings                             
println( buffer.listMedia.mkString("\nMedia gathered: " + buffer.sizeMedia + " [\n", "\n", "\n]"))     
println( buffer.listLinks.mkString("\nLinks gathered: " + buffer.sizeLinks + " [\n", "\n", "\n]"))     
{% endhighlight %}

***Spider Crawl***

*First argument:*
URL to start at

*Second argument:*
Number of times to recursively search gathered links (max index for the list of gathered links to search from),
 in this case 1 means we will only scan the first argument, therefore gathering all links and media URLs
on that first link's HTML.

*Third argument:*
Pass a buffer object for the crawl to fill as a side-effect .

*Fourth argument:*
A sequence of types to look for.

*Output:* (From running above code assuming Spider is imported already.)

{% highlight bash %}
Starting...

0                                                  100%
--------------------------------------------------
Media gathered: 73 [
http://s.imgur.com/min/gallery.js?1480634721
http://i.imgur.com/s5rB1fub.jpg
.
.
.  ]

Links gathered: 102 [
http://imgur.com/r/cats
http://imgur.com/r/cats/3QTBGjAA
.
.
.  ]
{% endhighlight %}

Most of the links were removed from the output for the sake of brevity, but the actual output shows the entire list.

*Note:* Some media is not an image type.

***Dead link checker***

Use the dead link checker to find 404 links on your website.

{% highlight scala %}
val buffer = Spider.Buffer("http://www.myWebsite.com")                                           
Spider.Crawl("http://www.myWebsite.com/", 20, buffer, Seq("href", "src") : _*)           
println( buffer.listDeadLinks.mkString("\ndead links gathered: " + buffer.sizeDeadLinks + " [\n", "\n", "]\n"))
println( buffer.listLinks.mkString("\nLinks gathered: " + buffer.sizeLinks + " [\n", "\n", "\n]")) 
{% endhighlight %}

This prints the following:

{% highlight bash %}
Starting...

0                                                  100%
----------------------------------------------------
dead links gathered: 1 [
http://www.myWebsite.com/empty
]

Links gathered: 15 [
http://www.myWebsite.com/
http://www.myWebsite.com/legal/shipping.html
http://www.myWebsite.com/legal/return.html
http://www.myWebsite.com/legal/privacy.html
http://www.myWebsite.com/legal/payment.html
http://www.myWebsite.com/clinics.php
http://www.myWebsite.com/emergencies.php
http://www.myWebsite.com/housecalls.php
http://www.myWebsite.com/pharmacy.php
http://www.myWebsite.com/fees.php
http://www.myWebsite.com/services.php
http://www.myWebsite.com/index.php
http://www.myWebsite.com/current.php
http://www.myWebsite.com/new.php
http://www.myWebsite.com/empty
]
{% endhighlight %}

*Note:* Sometimes it may produce false negatives, so try running a dead link scan a few times to be sure of results.

In the above example, I changed to domain of the website displayed and also the empty link is pointing to a directory that does not exist.
