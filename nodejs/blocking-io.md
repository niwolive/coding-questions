Say we want to read form `file` with nodejs and print out the length of each line (numbers of characters). The following implementation is incorrect. Explain why.

Hint: one of the called functions is missing an argument.

```javascript
const fs = require("fs");
const file_content = fs.readFile('./file', 'utf-8');
const lines = file_content.split('\n');

for (let li of lines)
  console.log(`The length of line:\n
              \t ${li}\n
              \t is ${li.length} characters.`);
```

<details>
  <summary>Answer</summary>

  <!-- FIXME This exlaination needs review, deeper insights. Include another level of <details/> explaining some event loop basic -->

  The code above is assuming that `fs.readFile` is called synchronously. This is not the case, `readfile` is called asynchronously and needs a callback that will be queued in the event loop's callback queue.

Here is a workable solution: 

```javascript
const fs = require("fs");
fs.readFile('./file', 'utf-8', (err,file) => {
  const lines = file.split('\n');

  for (let li of lines)
    console.log(`The length of line:\n
                \t ${li}\n
                \t is ${li.length} characters.`);
});

```
Note that the operations on the file are encapsulated in a callback to the function `readLine`, which makes sure we have finished to read the file from the disk before trying to manipulate it.

## Resources

- [Official documentation of the filesystem module](https://nodejs.org/api/fs.html#fs_fs_readfile_file_options_callback) (`fs`) in NodeJS .
- For more reading on the event loop, which helps understand how asynchronous code is processed, read [this document](https://github.com/nodejs/node/blob/master/doc/topics/event-loop-timers-and-nexttick.md) from the official node repo.
- For more reading on asynchronous coding in node [read this blog article from RisingStack](https://blog.risingstack.com/node-hero-async-programming-in-node-js/)

</details>
