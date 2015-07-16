---
layout: post
title: "Use ng-messages without form"
description: ""
category: 
tags: [AngularJs, Angular Material]
---
{% include JB/setup %}

One day, when I was using an Angular Material, I faced an issue about the ng-messages. I wanted to show required ng-messages, but somehow `FORM_NAME.ELEMENT_NAME.$error` did not work as expected. I tried to show error messages by all possible means, but I couldn't find it.

Then, I came up with this: passing an object to `ng-messages` directly. The good point about this is that it is simple and easy to use. Also, it does not require form tag and name directive.

I really like this. I recommend this approach in the case you want to show error messages, but not part of form. 

<p data-height="268" data-theme-id="0" data-slug-hash="NqBryQ" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/NqBryQ/'>ng-messages without form</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>