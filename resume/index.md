---
layout: default
title: "resume"
---

<center>
<div id="wrapper" style="width: 100%; height: 870px; margin-bottom: 3em;">
<iframe src="resume.pdf" width="100%" height="100%"></iframe>
</div>
</center>


<script>
$(function() {
var w = $(window)
var i = $('wrapper')

i.height(i.width * 1.1);

w.resize(function() {
	i.height(i.width * 1.1)
	})
});

</script>

