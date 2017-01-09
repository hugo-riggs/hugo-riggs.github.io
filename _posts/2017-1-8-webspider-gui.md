---
layout: post
title:  "Webspider GUI"
date:   2016-12-1 18:00:00 -0400
---

### Web spider with GUI 

Hugo Riggs
webspider, 2017

Using Webspider Gui

The gui application of my webspider program can be quite effective at certian tasks that can 
be preformed on html content. For example you could check for dead links on your
website. Alternitively you could use the application to download particular media files, because the regular expression language acceptors are provided for links to content. To use the regex fields follow
the [Java Pattern](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html). Below 
explains some methods of use, with instructional screen shots. The application is
available through [dropbox](https://www.dropbox.com/s/ogy8sj8649ct33z/guispider-1.5.zip?dl=0)

I tried the program on this website as I work with jekyll locally:

An initial scan of the webspite, I changed no default options, except for the URL.
![Initial Scan]({{site.url}}/assets/webspider-gui-images/initialScan.png )

Adding a missing link to the website, now this link shows up under the same crawl.
![After Adding ML]({{site.url}}/assets/webspider-gui-images/afterAddingML.png )

Now click the dead links check box and scan again, notice the missing link is found in three files.
Note: jekyll is automatically adding the html code with the `MISSINGLINK` to each post, so it is
added to three files.
![Detected missing link]({{site.url}}/assets/webspider-gui-images/missingLink.png )

Use the java pattern for regular expression creation, this can help you find specific links.
Note: (?i) mean case insensitivity. Add more iterations for a better chance to get content.
![Regex and Root]({{site.url}}/assets/webspider-gui-images/regexAndRoot.png )

Also download content with the download checkbox, ensure media links is also checked that
makes the crawler find the actual links to image data i.e. (jpg, gif, png, mp4, etc). The
javascript checkbox is an option because some websites dynamically link to url's from inside
the javascript of the webpage, so you can scrape that data as well with the checkbox selected.
Find titles is used to gather titles of webpages, this can give you more information about
what an ambigious url might contain Note: it will only return as many titles as iterations set.
**Make sure to end your download path with a `/` in unix systems and `\` in windows systems.**
![Started Imgur]({{site.url}}/assets/webspider-gui-images/downloadingMedia.png )
