Consider the following code:

```
for(let i=0;i<100;i++)
  setTimeout(console.log,1000,'.');
```

Which of the following is correct:
- A. 100 dots will be rendered to the standard output after approximately one second
- B. one dot will be rendered to the standard output approximately every second
- C. 100 dots will be rendered to the standard output after approximately 100 seconds

Argument your answer.

<details>
  <summary>Answer</summary>
  A. is correct. 
  
  *Explanation*
  `setTimeout` is asynchronous code. This means the javascript interpreter doesn't wait than its execution finishes to move forward with the loop.

</details>

---
