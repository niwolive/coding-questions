Consider the following code:

```javascript
let x;
for(x of [1,2,3,4,5])
 setTimeout(() => console.log(x),1000);
```

Once the program has finished its execution, which is correct:
- A. 5 is diplayed 5 times on the screen
- B. numbers from 1 to 5 are displayed on the screen

How would you change modify this program to get the other answer?

<details>
  <summary>Answer</summary>
  Topic: closures,scope,asynchronicity

  A. is correct. 
  
  *Explanation*
  Iterating over the defined array of numbers will call setTimout 5 times, creating a distinct anonymous function each time. However all of these anonymous function will refer to the same only existing variable x in the scope, which has long time been incremented to 5 when any of the setTimeout triggers.

---

  To get numbers from 1 to 5 displayed on the screen, we could have done any of the following: 

```javascript
for(let x of [1,2,3,4,5])
 setTimeout(() => console.log(x),1000);
```
Here, we declare the variable inside the for loop construct. The interpreter will create a new variable binding in a separate lexical environment for each of the iteration. The closure `() => console.log(x)` will thus be executed in a different environment for each of the iteration, with different (incrementing) values for x.

---

```javascript
let x;
for(x of [1,2,3,4,5])
  setTimeout(console.log,1000,x); // or setTimeout(console.log.bind(null,x),1000);
```
Here, x is passed as an argument to setTimeout. It is thus bound to the environment of this specific call setTimeout call.

---

```javascript
let x;
const logx = num => function(){console.log(num)}; 
// or const logx = num => console.log.bind(null, num);
for(x of [1,2,3,4,5])
  setTimeout(logx(x),1000);
```
Similarly here, we use a function `logx` that returns a function that uses `num`, which is the value of `x` passed to `logx` at each iteration. The anonymous function within `logx` is thus a closure.  

Note: I am not using an arrow function for the return value of `logx`, as `logx` itself uses one. This is just to improve readability (try replacing the function return value by an arrow function and it might make sense).

---

  *Resources*
  - [MDN Guide on Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
  - [https://davidwalsh.name/for-and-against-let](https://davidwalsh.name/for-and-against-let)
<!-- FIXME read David Walsh's article, it seems to dig quite deep -->
<!-- FIXME find a few more good references for that -->
</details>

