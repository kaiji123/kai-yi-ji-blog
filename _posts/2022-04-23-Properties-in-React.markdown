---
layout: post
title:  "Properties in React"
categories: jekyll update
---


## Introduction
To understand the use of properties , we first need to understand what a component in React framework.

## Components 
Components are reusable entities in react that enables you to manage states, define hooks and arrange code more cleanly. There are some rules such as you should define 
components as functions and not classes (in modern React). The return of each components should be jsx elements (React version of js). Sometimes you want to pass some arguments to components from a parent and to do that we have properties.

## What is a property ?
Think property as an argument that you want to pass to components. The syntax for this should be :

`<Component prop1={arg1} prop2={arg2}/>`

and to access those properties in a component

{% highlight javascript %}
function Component(props){
    const prop1 = props.prop1;
    const prop2 = props.prop2;
    return(
        <div>
        <div>
    )
}
{% endhighlight%}


However, sometimes it is easier to wrap all properties as a single object and pass it as a single property to the component.


{% highlight javascript %}
let object = {
    prop1 : value1,
    prop2 : value2
}
<Component prop={object} />

{% endhighlight%}

This will reduce the amount of arguments you need to pass to the component object.

{% include comment.html%}
