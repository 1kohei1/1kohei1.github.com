---
layout: post
title: "Hour and Minute Angular Directive"
description: "Hour and Minute Angular Directive"
category: 
tags: [AngularJS]
---
{% include JB/setup %}
I needed to create directive for hour and minute input. There is input `type="time"`, but my supervisor didn't like to have default colon and dash and whatever. So I was asked to create directive for hour and minute input.

Let's list up the directive specifications:

1. No space, no alphabets. Those are not allowed to enter.
2. Help users enter. Like insert colon after hour. Correct inappropriate value... etc
3. Show errors when the input value is not in correct format.

Anyway, let's look the codepen first!

<p data-height="268" data-theme-id="0" data-slug-hash="ZGqqgq" data-default-tab="result" data-user="1kohei1" class='codepen'>See the Pen <a href='http://codepen.io/1kohei1/pen/ZGqqgq/'>hour minute input directive3</a> by Kohei Arai (<a href='http://codepen.io/1kohei1'>@1kohei1</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

If you want to read the entire html and javascript in nice color syntax, here is the [Github gist](https://gist.github.com/1kohei1/d48461d69782332e6b36)

Let me go through each line of code for my future reference.
{% highlight javascript %}
function ensureHourMinute(value) {
  var nospace = value.replace(/ /g, '');
  var num = nospace.replace(/[^0-9:]/, '');

  var hour = num.split(':')[0].slice(0, 2);
  var minute = '';
  if (num.indexOf(':') >= 0) {
    minute = num.split(':')[1].slice(0, 2);
  }
  var cursorPos = element[0].selectionStart;
{% endhighlight %}
Remove all space, alphabetical characters. Set up the variable for hour and minute. If the passed value has colon in that, set the minute to the second index of num splitted by ":". `cursorPos` is used to set the cursor after the value is renderred.

{% highlight javascript %}
var isTyped = preValue.length < value.length;
var isReplaced = preValue.length === value.length;
var isTimeAlreadySet = num.length - preValue.length > 1;

// Deleted all
if (num.length == 0) {
  return setUpView(hour, minute, cursorPos);
}
{% endhighlight %}
Those variables are to track what users have done to input. When the length of num is zero, that means all the value is deleted, so empty input.

{% highlight javascript %}
// Colon is deleted
if (preValue.indexOf(':') >= 0 && num.indexOf(':') === -1) {
  hour = preValue.split(':')[0].slice(0, 2);
  minute = preValue.split(':')[1].slice(0, 2);
  // When minute is already entered, put colon.
  if (minute.length === 1) {
    minute = '';
    hour += ':';
    cursorPos++;
  } else if (minute.length === 2) {
    hour += ':';
    cursorPos++;
  }
  return setUpView(hour, minute, cursorPos);
}
{% endhighlight %}
This part takes care of when the colon is deleted. When minute is only one digit, delete the minute instead of colon. When minute exists, leave the input value unchanged and set the cursor after colon.

{% highlight javascript %}
// Other case
if (parseInt(hour) > 12) {
  hour = '12:';
  cursorPos = 3;
} else if (parseInt(hour) >= 10) {
  hour += ':';
  if (cursorPos === 1 || cursorPos === 2) {
    cursorPos = 3;
  }
} else if (parseInt(hour) >= 0 && num.indexOf(':') >= 0) {
  hour += ':';
} else if (minute !== '') {
  hour += ':';
}

if (minute > 59) {
  minute = '59';
} else if (minute.length === 1 && parseInt(minute) < 10 && (isTyped || isReplaced) && !isTimeAlreadySet) {
  minute += '0';
}
{% endhighlight %}
This snippet handles all the other case: typed, replaced, and deleted. If hour is over 12, that means it is out of the range. So set the hour to 12 and move to the cursor after colon. If hour is greater than 10 and less than equal to 12, add ":". For this case, there are two cases. 1. User is editing an hour 2. User is editing minute and hour is in that range. If the `cursorPos` is in hour range, that is 1. So move the cursor after the colon.

The same thing for minute too. If the minute is greater than 59, set it to 59. Other than that, if the minute is one number, put zero after that. `!isTimeAlreadySet` is for the case the ng-model value is set at the first call. Without this, the minute behaves strange way when ng-model has the initial value. 

{% highlight javascript %}
function setUpView(hour, minute, cursorPos) {
  preValue = hour + minute;
  
  controller.$setViewValue(preValue);
  controller.$render();
  element[0].setSelectionRange(cursorPos, cursorPos);
  
  return preValue;
}
{% endhighlight %}
Set the `preValue`, change the input view, and set the cursor at appropriate position.

If there is anything unclear, play with [codepen](http://codepen.io/1kohei1/pen/ZGqqgq?editors=001) or [Github gist](https://gist.github.com/1kohei1/d48461d69782332e6b36). Thank you!