---
title: " "
comments: false
type: "top"
---
<div id="top"></div>
<script src="https://cdn1.lncld.net/static/js/av-core-mini-0.6.4.js"></script>
<script>AV.initialize("E7vwwiWpiaeLTwLBS8GGfbHX-gzGzoHsz", "gvN94Bk9as8RRGeuQGqeHazh");</script>
<script type="text/javascript">
  var time=0
  var title=""
  var url=""
  var query = new AV.Query('Counter');
  query.notEqualTo('id',0);
  query.descending('time');
  query.limit(1000);
  query.find().then(function (todo) {
    for (var i=0;i<1000;i++){
      var result=todo[i].attributes;
      time=result.time;
      title=result.title;
      url=result.url;
      var content="<center>"+"<a href='"+"https://yfygoing.com"+url+"'>"+"<font size= 4>"+title+"</a>"+"</center>"+"<center>"+"<font size= 2 color='#555'>"+"Times of Reading："+time+"</font>"+"<br />" + "<div style='border-top:2px dotted #0052d4;'></div>"+"</center>";
      document.getElementById("top").innerHTML+=content
    }
  }, function (error) {
    console.log("error");
  });
</script>

<style>.post-description { display: none; }<style>
