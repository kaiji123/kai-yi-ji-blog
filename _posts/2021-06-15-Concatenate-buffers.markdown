---
layout: post
title:  "Concatenating buffers"
date:   2021-06-15 04:54:10 +0200
categories: jekyll update
---
In this post I will show you have to concatenate buffers in javascript using Uint8Array.

First, we need to create a function that concatenates buffers. Let's name it `concatBuffers`. 

{% highlight javascript %}
function concatBuffers(
  ...inputBuffers
) 
{% endhighlight %}

Notice that the function has inputBuffers which has `...` in front of it. This means the inputBuffers will be an array with all arguments in it. For example, if we call `concatBuffers(buffer1,buffer2,buffer3)` then inputBuffers will be `[buffer1,buffer2,buffer3]` 

{% include adsense.html %}
