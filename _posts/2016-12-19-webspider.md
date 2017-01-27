---
layout: post
title:  "Scala web spider with Jsoup"
date:   2016-12-1 18:00:00 -0400
---

### Scripting 

The first step to accessing the functionality of *webspider* is by importing the necessary concurrency libraries, and then Crawler object and Class. Now you can define a Crawler value for later use. This can be done through a REPL session as shown below.

{% highlight scala %}
scala> import scala.concurrent.ExecutionContext.Implicits.global
scala> import util.{Success, Failure}
scala> val redditCrawl = Crawler("https://www.reddit.com/r/FifthWorldPics/", 2, Seq("href", "src", "title"): _*)
redditCrawl: spider.Crawler = spider.Crawler@447686d1
{% endhighlight %}

Crawler has a companion object which works as a constructor. The *run()* function of Crawler returns a Future Integer, and that value can be completed, and on success you can import the set-fields of your crawler and access their content. This includes the following data: links within the domain, external links, links to dead content (404), and media links ( .jpg, .png,  .gif, etc. ).

{% highlight scala %}
	scala> redditCrawl.run.onComplete{
	     | case Success(zero) => zero
	     | case Failure(ex) => println(ex)
	     | }

	Crawling…

	scala> redditCrawl.mediaSet.size
	res1: Int = 6

	scala> redditCrawl.localSet.size
	res2: Int = 150

	scala> redditCrawl.mediaSet.size
	res3: Int = 22

	scala> redditCrawl.localSet.size
	res4: Int = 235
{% endhighlight %}


Notice, it is possible to continue with tasks in the REPL, in this case we use the Crawler object’s data fields to check on the status of crawled resources. Each crawl is timed, and this is shown at the end. At this point, because the data fields were imported by our success case code we can begin using the gathered data.

{% highlight scala %}
       scala> 
       Done! (buffer objects filled)
       The crawl took 58 seconds

       scala> mediaSet foreach println
       https://a.thumbs.redditmedia.com/u-_aNnn_68FjNH2zqK3NVKSViwc6BhINZGReTH6_FD8.jpg
       https://b.thumbs.redditmedia.com/Md0EAiGsuUfQOyxhLEf_rIW6pNgwy1M7HhAjHZcev2E.jpg
       https://a.thumbs.redditmedia.com/Mixjq0aUujwDg3WXtNJ8LBI4cfLJ5yo_QueY85HONR8.jpg
       https://b.thumbs.redditmedia.com/pNn4bWxLUvLuA0w0IR9to_vMG0dGjo7PcwysEZ5r7nE.jpg
       https://b.thumbs.redditmedia.com/6r3avQr81jv-OmOG4GUz_5_mjc-35ZjOaNRwVqSdyes.jpg
       https://b.thumbs.redditmedia.com/aj2juGfOO-shfjGE0Egk7CMnvSxRm6fkOzmzGaqZ3JE.jpg
       https://b.thumbs.redditmedia.com/K5hBBFbkpm53CkFEptyX22ack8PK4umjsotwdxBB1_o.jpg
       https://www.redditstatic.com/reddit-init.en.i9drE_f_XYc.js
       https://reddit.com/static/pixel.png
       https://www.redditstatic.com/subscribe-header-thanks.svg
       https://b.thumbs.redditmedia.com/jEensXguO3MevvGMLd_y2c5vUI_gaMYaoYpe4kOqgaI.jpg
       https://b.thumbs.redditmedia.com/qnnkNuLyKCYEwoVn2lYzRA_akhOSWk5AjSTJ7yFr2ho.jpg
       https://b.thumbs.redditmedia.com/rU7GqVMtfNm22HduroF_WC8Qg1g2_rHhhxRkcJ4I0uM.jpg
       https://b.thumbs.redditmedia.com/NkZCxFWDXlWS-bj7s-GhLG_5sw8uLJgGN6mHx8v5eFM.jpg
       https://www.redditstatic.com/reddit.en.rkVCuLkyVtE.js
       https://f.thumbs.redditmedia.com/2Nry3sl-Bh7lC-O_.png
       https://www.redditstatic.com/subscribe-header.svg
       https://b.thumbs.redditmedia.com/o44G2puGuoPOP2uOKb4rIswDYCion94m3woaGk75lFw.jpg
       https://b.thumbs.redditmedia.com/GyMOannsiVJ1_BGFxkmSK0zXHvfnujJxnS_nkrDBXQc.jpg
       https://b.thumbs.redditmedia.com/Uwiuk0cJME4mTJOvF4jhC7E_uQZ14UQwh_TUJ_Vniqg.jpg
       https://b.thumbs.redditmedia.com/y33HBHMorgXzigg1z_ClbOxUZW2GUpk5a41vd2usrjE.jpg
       https://b.thumbs.redditmedia.com/XT_NIqcq_den_XQjYD2enEmrbFm_QJUwggOLnI8jZ8A.jpg

       scala> localSet size
       res5: Int = 240

       scala> externalSet size
       res6: Int = 62
{% endhighlight %}

The crawl was specified to be only two HTML pages wide (breadth first search), and because of the design of Reddit, few image links were gathered, and mostly thumbnails. However, many more inner domain links were discovered, more than can comfortably be displayed here. Also there were 62 external links found. Among the external set of links were links on domains (imgur.com, youtube.com, reddituploads.com, gfycat.com, imzy.com, ceddit.com, rt.com, cruxnow.com, etc.), also no dead links were discovered. For outside of the REPL a program could use these manipulations inside the on success case after the crawler data import. As an example there is the `FunSuite` test below.

{% highlight scala %}
test("test rec script") {
	import spider._
	val crawl = Crawler("https://www.reddit.com/", 1, Seq("href", "src", "title") : _*)
	import crawl._
	crawl.run.onComplete({
		case Success(res) => 
			println(res)
			println("media links:")
			mediaSet foreach (s => println(s))
			println("Title:")
			for((k,v) <- metaDataMap) {
				println(k + ", " + v)
			}
		case Failure(ex) => println(ex)
	})
}

{% endhighlight %}

The metaDataMap will hold crawled content that you request additionally to href or src, and in this case that data is the title from a HTML page. You can also try other tag’s such as (p, div, style), and hopefully the crawler returns adequate data.

*Hugo Riggs
webspider, 2016*
