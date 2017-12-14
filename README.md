Voronezh webperf tools talk stuff.

# Links
## Tools
### Synthetic
- [Google PageSpeed](https://developers.google.com/speed/pagespeed/insights/) and here's a [shiny version for your boss](https://testmysite.withgoogle.com/intl/en-gb)
- [GTmetrix](https://gtmetrix.com/)
- [Pingdom](https://tools.pingdom.com/)
- [WebPageTest](https://www.webpagetest.org/) (WPT)
  - Built on top of WPT: [SpeedCurve](https://speedcurve.com/) and [MachMetrics](https://www.machmetrics.com/) (disc: me and MM do webperf case studies together)

### RUM (Real User Monitoring/Measurements)
- [Google Analytics](https://analytics.google.com/analytics/web/#report/content-site-speed-overview/)
- [New Relic](https://newrelic.com/)
- [AppOptics](https://www.appoptics.com/)
- [Taki](https://takiapp.com/) (disc: I'm on the team 🙋🏻)

# Slides
TBD

# Other links
[Critical rendering path Udacity course by Ilya Grigorik](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/)

# Snippets
## Enable 100% sampling for RUM in GA
<pre>
// This is your generic GA snippet 
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create',
  'UA-xxxxxx', // Your Universal Analytics ID
<b>  {'siteSpeedSampleRate': 100} // <- this is the magic 🌝</b>
);
ga('send', 'pageview');
</pre>

## Insert non-critical CSS and JS on Request Animation Frame
```
<noscript id="deferred-resources">
  <!-- Here you place non-critical resources -->
  <link rel="stylesheet" href="/style.css">
  <script src="//cdn.example.com/javaskripte.js" integrity="sha384-HeyTC39"></script>
  <!-- Google Fonts can go here too -->
</noscript>

<script>
  // Here we load'em
  var loadDeferredStyles = function() {
  var addStylesNode = document.getElementById("deferred-resources");
  var replacement = document.createElement("div");
  replacement.innerHTML = addStylesNode.textContent;
  document.body.appendChild(replacement)
    addStylesNode.parentElement.removeChild(addStylesNode);
  };

  var raf = requestAnimationFrame || mozRequestAnimationFrame ||
    webkitRequestAnimationFrame || msRequestAnimationFrame;
  if (raf) raf(function() { window.setTimeout(loadDeferredStyles, 0); });
  else window.addEventListener("load", function() { window.setTimeout(loadDeferredStyles, 0)});
</script>
```

# Reach out
- [Twitter](https://twitter.com/fast_wordpress)
- [Email](mailto:hom3chuk+perf@gmail.com)
- [Damn Fast WordPress: the Book](https://damnfastwordpress.com/the-book/)
- Telegram `hom3chuk`
