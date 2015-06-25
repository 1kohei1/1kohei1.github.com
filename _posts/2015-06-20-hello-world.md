---
layout: post
permalink: Filter-md-autocomplete-items-without-function
title: "Filter md-autocomplete items without function"
description: "This is about filtering items without function in the controller."
category: 
tags: [AngularJS, Angular Material]
---
{% include JB/setup %}
This is about filtering items without function in the controller.

{% highlight html %}
<md-autocomplete md-selected-item="ctrl.sampleValue" 
                 md-search-text="searchText" 
                 md-items="item in ctrl.items | filter:searchText"
                 md-item-text="item.value">
  <md-item-template>
    <span md-highlight-text="searchText">{{ item.value }}</span>
  </md-item-template>
</md-autocomplete>
{% endhighlight %}

That's it! You do not need any code for filtering items when searchText changes. `filte` takes care of everything!

If you want to work more, Code pen is provided below.

<p data-height="268" data-theme-id="0" data-slug-hash="QbqLqq" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/QbqLqq/'>md-autocomplete preselected when object is passed</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>