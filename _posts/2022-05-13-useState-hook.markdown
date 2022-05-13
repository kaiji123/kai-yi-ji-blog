---
layout: post
title:  "useState hook in React"
categories: jekyll update
---

# useState hook in React 
In components we often want manage the state of the objects and correspondingly render our objects on their current states.
In React, we have useState hook to do the job for us.

##  How to use useState ?
The basic implementation of useState hook should look like following
```javascript

import { useState } from 'react';

function Component(props){
    let initialState={}
    [yourState, setYourState] = useState({
        data1: "data1"
        data2: "data2"
    }) 
    function handler(){
        setYourState((previousState) => {...previousState, data1: "Clicked"})
    }
    return (
        <div>
            <button onClick={handler}> Click me ! </button>
            <div>
                {yourState.data1}
            </div>
        </div>
    )

}
```

TODO: ... is spread operator in which it takes all the old data in previousState and puts it in new object state (Be ware the only data1 is changed).

## Deep dive into the code
The above component renders a simple button and the text data in div tag. The text is rendered using yourState variable which is a state defined in useState hook. Therefore, initially the text will be "data1". However, once we click the button, it will trigger handler function.

```javascript
 function handler(){
        setYourState((previousState) => {...previousState, data1: "Clicked"})
    }
```

 Notice that yourState, setYourState are created by using useState hook. Also, see that they are wrapped inside brackets. Well this is because useState will return a list of one state variable and one function that sets your state. We used the above syntax to take out the state function and state variable.

Finally, once it handler is called it triggered, we use the state changer function setYourState to change our state. Notice that the function takes one argument and that argument is ALWAYS going to be your previous state. We used the spread operator to put all the data from previous state to our new state except data1, which will be overwritten to "Clicked" and this will be automatically rendered to the browser


## Conclusion
The useState is an essential part of React framework since it introduces the idea of managing states. This indeed will make the development process easier because it gives you a better abstraction of what states you need to manage.


{% include comment.html%}
