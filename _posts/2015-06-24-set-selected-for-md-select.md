---
layout: post
permalink: set-Default-option-of-md-select
title: "Set Default Option of md-select"
description: "This is about setting an option of md-select when ng-model is an object."
category: 
tags: [AngularJS, Angular Material]
---
{% include JB/setup %}
This is about setting an option of md-select when ng-model is an object.<br />
If ng-model is a simple primitive data type, Angular Material selects and highlight the value. But when ng-model is an object, the object is not selected nor highlighted.

[This](https://github.com/angular/material/issues/2862) Github issue represents what I want to achieve, but the [code pen](http://codepen.io/myagoo/pen/Qbddzg?editors=101) in the link does not let you change the option. So this is how your html should look like.

{% highlight html %}
  <md-select ng-model="ctrl.number">
    <md-select-label>{% raw %}{{ ctrl.number.value }}{% endraw %}</md-select-label>
    <md-option ng-repeat="n in ctrl.numbers" ng-value="n" selected="{% raw %}{{ n.value === ctrl.number.value ? 'selected' : '' }}{% endraw %}">{% raw %}{{ n.value }}{% endraw %}</md-option>
  </md-select>
{% endhighlight %}

For forks who are interested in the entire code, I embedded the codepen here. Feel free to play around.

<p data-height="268" data-theme-id="0" data-slug-hash="gpXdjQ" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/gpXdjQ/'>Set Default option for md-select</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>