# What_I_learned_today
A  casual blog to record things I learned on internet related to programming.


Timeless sources:   
- https://github.com/Asabeneh/30-Days-Of-JavaScript   
- https://github.com/leonardomso/33-js-concepts   
- https://github.com/ossu/computer-science   
- https://github.com/bradtraversy/design-resources-for-developers
- https://cs50.harvard.edu/x/2022/
- https://cs50.harvard.edu/web/2020/


 22/2/2022

- In Node.js, `console.log()` is actually:
 `console.log = function (d) {
  process.stdout.write(d + '\n');
};`

source: https://nodejs.org/docs/v0.3.1/api/process.html#process.stdout

- One can use `alt+shift+I` in `VS Code` to have multiple cursors for all the selected elements.  
Usage example: for formatting all the copy-pasted list of words that are not properly formatted as list items for json.

source: https://www.youtube.com/watch?v=QcXlyriZVa8


24/2/2022

- one can open up a folder in the current VS Code window, which by default opens up a new window, use `-r` as in `code -r [your dir]`   


3/8/2022   
- `if` statement, if not followed by `else` or `else if`, must `return` something within the brackets (or its lexical scope, if we omit the brackets), in order to work. Even if a function, method or any expression would return something, in that lexical scope the `return` keyword is still needed.    
   
- to print a `function` in `console.log()` simply use the inbuilt function object method called `toString()`. `toString()` is also available for Array object.   
   
- `...args` as multiple arguments for a function's parameter requires the 3 dots `...`, whereas within the function no need to add 3 dots `...` and `args` alone is valid.   
Note: however, when passing it within a function, as an argument, to a nested function or a returned function, `...args` syntax must be preserved.
  
    
   
9/3/2022    
- a function that does the deep clone (in contrast to shallow clone `[...x]/{...x}`):   
 ```js
const deepClone = (obj) => {
  if (typeof obj !== 'object' || obj === null) return obj;

  // create an array or object to hold the value
  const newObj = Array.isArray(obj) ? [] : {};

  for (let key in obj) {
    const value = obj[key];
    // recursive call for nested objects and arrays
    newObj[key] = deepClone(value);
  }

  return newObj;
};   
```
   
   
10/3/2022   
- to center an item, without using flex or grid:   
first the html template:   
```html
<div class='outer-box'>
 <div class='inner-box'></div>
</div>
```   
now the version #1 with absolute positionng, which used to be an old, popular way:   
```css
.outer-box {
<!--  styling code -->
  position: relative;
}

.inner-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
<!--  styling code -->
}
```   
Its Codepen link: https://codepen.io/matinsasan/pen/jOagyOX   

Now, using absolute positioning #2, using `inset`, plus `margin: auto`, in CSS:   

```css
<!-- same code as the previous CSS snippet -->

.inner-box {
  position: absolute;
  inset: 0;
  margin: auto;
<!--  styling code -->
}

```   
Its Codepen link: https://codepen.io/matinsasan/pen/GROVrOG   

   
13/3/2022   
- `for...of` loop is for `array`, whereas `for... in` loop is for `object`.   
`.entries()` method gives index and value for array:   
`for (let [index, value] of someArray.entries())`,   
whereas key-value pair for object:   
`for (const [key, value] in someObject.entries())`. 
   
25/3/2022   
- an often used `CSS` shorthand `background` should best be avoided, as it can interfere with, for example, `background-color` and `background-image` to work properly.      
 
29/3/2022   
- React updates state in batches:   
in setState method, for example, updating through `setCount = () => count+1` within a function call multiple times would fail and still use the original, previous state as a reference, while using `setCount = prev => prev+1` by passing the `previous state` as an argument we can accomplish this.
   
4/4/2022   
- Some web events can cause cost performance badly, like input, mousemove, etc. where there might be heavy API usage.   
With the help of `debounce` and `throttle` we can address this issue.   
Link to the gist of how to implement debounce and throttle: https://gist.github.com/MatinSasan/25e7ba3837df68c0cc1d2ebfab8a5552
   
9/4/2022   
- in CSS, whenever we assign `padding` with `width` to an element, we use `box-sizing:border-box` to keep the math as simple as possible.   
- to center with flexbox (will update for grid and some tricks):  
simply add to the parent element, along with `display:flex`, `justify-content:center` to horizontally center as well as `align-items:center` to vertically center.   
Note that in order to make `align-items` work, we have to add `height` to the parent element, which is usually `100vh` (vh: a percentage of the full viewport height).
