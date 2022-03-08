# I_learned_today
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
