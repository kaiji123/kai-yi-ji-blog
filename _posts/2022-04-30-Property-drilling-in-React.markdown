---
layout: post
title:  "Property drilling in React"
categories: jekyll update
---


## Introduction
As we have already talked about properties in React, I want to introduce a phenomenon called property drilling in React.

## How Property drilling occurs ?
Suppose we have a grandparent component and grandchild component. How would we pass properties from grandparent to grandchild components ? Well, it would have to first pass properties to its child component and then the child component passes to the grandchild component. From this, we have a created a chain of passing properties around, which is called Property drilling.

## How to resolve Property drilling?
We have two solutions to avoid Property drilling problem. One of them is to use Context API from React and the other one is to use Redux.


## Context API
The context API allows components to use the same values withing the same context. To be able to use the same context you have to provide context to the components. We can do that by firstly creating a ThemeContext.js file in which it will provide context where you can switch themes.

```javascript
import { createContext, useState } from "react";

export const ThemeContext = createContext()


function ThemeProvider(props) {
    const [theme, setTheme] =  useState("dark")
    return (
    <ThemeContext.Provider value = {[theme, setTheme]}>
        {props.children}
    </ThemeContext.Provider>
  );
}

export default ThemeProvider;
```

Let's walk through the code. Firstly, we created context using 
```javascript
export const ThemeContext = createContext()
```
then we defined ThemeProvider function in which there is a theme state using a hook.
```javascript
const [theme, setTheme] =  useState("dark")
``` 
We then passed the state to the provider.
```javascript
    <ThemeContext.Provider value = {[theme, setTheme]}>
        {props.children}
    </ThemeContext.Provider>
```
Notice that we wrapped props.children inside Provider context, this means that all children of this component will be provided the context.

Lastly, we exported ThemeProvider component.

## How to use the context ?
We will need to use our context to be able to access theme state. Suppose you already have App.js in your React project. 

```javascript

import './App.css';
import Navbar from './components/Navbar';
import { useContext, useEffect } from 'react';

//hello
function App() {
  return (
      <div className="App">
        <Navbar />
      </div>
  );
}

export default App;
```
We provide context to App.js like following.

```javascript

import './App.css';
import Navbar from './components/Navbar';
import { useContext, useEffect } from 'react';
import ThemeProvider from './contexts/ThemeContext';

//hello
function App() {
  return (

    <ThemeProvider>
      <div className="App">
        <Navbar />
      </div>
    </ThemeProvider>
  );
}

export default App;
```
This way Navbar component will be able to access all the values in that context. Notice the we had to import ThemeProvider from ThemeContext.jsx file.

```javascript
import "./Navbar.css"
import { useContext, useEffect } from "react";
import ThemeProvider, { ThemeContext } from "../contexts/ThemeContext";
//hello
function Navbar() {

    const [theme, setTheme] = useContext(ThemeContext)
    
    useEffect(function(){
        console.log(theme)
    },[])

    function handleTheme(){
        if (theme == "dark"){
            setTheme("white")
        }
        else{
            setTheme("dark")
        }
    }
    return (
        <nav className="nav-bar">
            <div className="theme">
                <input type="checkbox" checked= {"dark" == theme} onChange = {handleTheme}/>
            </div>
        </nav>
    );
}
export default Navbar;
```


{% include comment.html%}
