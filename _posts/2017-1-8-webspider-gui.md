---
layout: post
title:  "Webspider GUI"
date:   2016-12-1 18:00:00 -0400
---

### Web spider with GUI 

Hugo Riggs
webspider, 2017

Scala GUI webspider is effective at certian tasks. For example you could check for dead links on your
website. Alternitively you could use the application to download particular media files. Regular expression patterns are used as filters. Use the [Java Pattern](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html). Application on [dropbox](https://www.dropbox.com/s/ogy8sj8649ct33z/guispider-1.5.zip?dl=0)

I tried the program on this website as I work with jekyll locally:

After adding a missing link to the website, now I select the dead links check box and crawl. The missing link is found in three files.
Note: jekyll is automatically adding the html code with the `MISSINGLINK` to each post, so it is
added to three files.
![Detected missing link]({{site.url}}/assets/webspider-gui-images/missingLink.png )

Use the java pattern for regular expression creation, this can help you find specific links.
Note: (?i) mean case insensitivity. Add more iterations for a better chance to get content.
<!-- ![Regex and Root]({{site.url}}/assets/webspider-gui-images/regexAndRoot.png ) -->

Also download content with the download checkbox, ensure media links is also checked that
makes the crawler find the actual links to image data i.e. (jpg, gif, png, mp4, etc). The
javascript checkbox is an option because some websites dynamically link to url's from inside
the javascript of the webpage, so you can scrape that data as well with the checkbox selected.
Find titles is used to gather titles of webpages, this can give you more information about
what an ambigious url might contain Note: it will only return as many titles as iterations set.
**Make sure to end your download path with a `/` in unix systems and `\` in windows systems.**
![Started Imgur]({{site.url}}/assets/webspider-gui-images/downloadingMedia.png )

Downloading cartoons example:
<iframe width="560" height="315" src="https://www.youtube.com/embed/8ToQnOWmVkQ" frameborder="0" allowfullscreen></iframe>
