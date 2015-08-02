---
layout: post
title: "A Function to Diff Two JSONs"
description: "A Function to Diff Two JSONs"
category: 
tags: [Javascript]
---
{% include JB/setup %}

I needed to compare two JSONs to check the equality of production JSON and JSON in development system. So here is one function to do so.
I assume one JSON is in correct format and check if the other is in correct format. Also, the function uses [lodash](https://lodash.com/), a JavaScript utility library delivering consistency, modularity, performance, & extras.

The function does:

1. Print out missing property.
2. Print out if the data type is different.
3. Prunt out if the value is different.
4. Print out if an object in array is missing

Here is the code on [Github gist](https://gist.github.com/1kohei1/80806b9eef17c9d7b140). I also put code in this blog just in case if you want to take a look.
{% highlight javascript %}
/**
 * Print out diff of two JSON
 * @param jsonA The correct JSON
 * @param jsonB JSON you want to check diff
 * @param keys Necessary for the function. Just pass ''
 * @param objectKeys Objects to find unique objects in array.
 * @param excludedKeys Array of keys that doesn't have to be checked.
 */
function compareTwoJSON(jsonA, jsonB, keys, objectKeys, excludedKeys) {
  for (var key in jsonA) {
    if (jsonB.hasOwnProperty(key)) {
      if (jsonA[key] === null && jsonB[key] === null) {
        // Ignore null first because typeof null is object
      } else if (typeof jsonA[key] === typeof jsonB[key]) { // Check the data type
        if (Array.isArray(jsonA[key])) { // If the data type is array
          keys = '[' + key + ']';
          var jsonAArray = jsonA[key];
          var jsonBArray = jsonB[key];

          for (var i = 0; i < jsonAArray.length; i++) { // Find the same item in jsonB[key] by iterating jsonA[key]
            var jsonAItem = jsonAArray[i];
            var jsonBItem = '';
            var objectKey = objectKeys[key];
            if (typeof jsonAItem === 'object') {
              // If it is an array of objects, find the equal object by property
              jsonBItem = _.find(jsonBArray, function(obj) {
                return obj[objectKey] === jsonAItem[objectKey];
              });
            } else {
              jsonBItem = _.find(jsonBArray, function(obj) {
                return obj === jsonAItem;
              });
            }
            if (jsonBItem) { // Check if the same item is found in jsonB[key]
              if (keys && keys.indexOf('.') >= 0) {
                keys = keys.split('.').splice(0, 1);
              }
              keys += '.' + jsonAItem[objectKey];
              compareTwoJSON(jsonAItem, jsonBItem, keys, objectKeys, excludedKeys); // Iterate again to compare item in jsonA and jsonB
            } else {
              var missingItem = typeof jsonAItem === 'object' ? jsonAItem[objectKey] : jsonAItem;
              console.log('1. Dev is missing [' + key + '].' + missingItem);
            }
          }
        } else if (typeof jsonA[key] === 'object') {
          if (keys && keys.indexOf('.') >= 0) {
            keys = keys.split('.').splice(0, 1);
          }
          var objectKey = objectKeys[key];
          keys += _.isUndefined(objectKey) ? key : objectKey;
          compareTwoJSON(jsonA[key], jsonB[key], keys, objectKeys, excludedKeys);
        } else if (!_.isEqual(jsonA[key], jsonB[key])) {
          if (excludedKeys.indexOf(key) === -1) {
            console.log('2. Dev has different value at ' + keys + '.' + key);
          }
        }
      } else {
        console.log('3. Dev has different data type at ' + keys + '.' + key);
      }
    } else {
      console.log('4. Dev is missing property ' + keys + '.' + key);
    }
  }
}
{% endhighlight %}
You can play with this on [codepen](http://codepen.io/1kohei1/pen/xGQydz?editors=001).

`objectKeys` is used to detect an object in array of objects. Because JSON is likely to have random order of objects, the function needs a property to find out the same object in array. It takes property containing array in key and property name to compare objects in value.

`excludedKeys`, any property name in this array does not check the equality of the values. It **does** check missing property and different data type though. 

On a side note, there are nice [npm package](https://www.npmjs.com/package/json-diff) and [online checker](http://tlrobinson.net/projects/javascript-fun/jsondiff/). Try them first. If they do not work as expected, it is the time to start writing your own function. I don't think my function answers all of what you want to do. But it should give you some hook to start with. If you find any bugs or unexpected behaviors, just let me know via email: koheiarai.1[at]]gmail.com