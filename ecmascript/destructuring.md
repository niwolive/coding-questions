
What is the value of `[cat,dog]` by the end of this program?

``` javascript
let cat = "Fred";
let dog;

[cat="Jim", dog="Will"] = [dog, cat];
```

- A. `["Jim", "Fred"]`
- B. `["Jim", "Will"]`
- C. `[undefined, "Will"]`
- D. `[Fred, "Will"]`

<details>
  <summary>Answer</summary>
  A. is the answer. On the last destructuring assignment `cat` takes its default value since `dog` is undefined. Dog takes `cat`'s value which is "Fred".
</details>
