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

We will use javascript reduce function to sum up the bytelength that we need for the final buffer.

{% highlight javascript %}
{
  const Length = inputBuffers.reduce(
    (sum, buff) => sum + buff.byteLength,
    0
  )
{% endhighlight %}

This code will get the required bytelength for the buffer.

Now we create an outputBuffer which will be an Uint8Array. We also need to define offset for next code.

{% highlight javascript %}
  const outputBuffer = new Uint8Array(Length)
  let offset = 0

{% endhighlight %}

Finally, we use the following code.

{% highlight javascript %}
 inputBuffers.forEach((buff) => {
    if (ArrayBuffer.isView(buff)) {
      const { buffer, byteOffset, byteLength } = buff
      outputBuffer.set(new Uint8Array(buffer, byteOffset, byteLength), offset)
    } else {
	console.log(buff)
	console.log(offset)
      outputBuffer.set(new Uint8Array(buff), offset)
    }
    offset += buff.byteLength
  })
   return outputBuffer
{% endhighlight %}

This will iterate through inputBuffers array which we already explained. For every buffer in that array, we check if the buffer is ArrayBuffer View. If it is, then extract properties of that buffer, and set from offset. Otherwise set this buffer from offset directly. Notice that when we iterate through each buffer we increment the offset by that buffers bytelength. This is because whenever we put all elements from that buffer to our outputBuffer we need also to tell the outputBuffer to move to the index when there is not any element. Lastly, we return the outputBuffer.

Now we have the concatenate function. Let's test it using the following code.

{% highlight javascript %}
console.log(concatBuffers(new Uint8Array([1,2,3,58,8]),new Uint8Array([1,5,6,8,5])))
{% endhighlight %}

This will give us
{% highlight javascript %}
Uint8Array(10) [
  1, 2, 3, 58, 8,
  1, 5, 6,  8, 5
]
{% endhighlight %}

which is the concatenation of two buffers.
{% include amazon.html %}
{% include comment.html%}






