Given mapWith:
```javascript
const mapWith = (fn, array) => array.map(fn);
```
Consider the following:

```javascript
const row = function () {
  return mapWith(
    (column) => column * arguments[0],
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
  )
};
```

which of the following options in the return value of `row(3)`?

- A. [3,6,9,12,15,18,21,24,27,30,33,36] 
- B. [1,4,9,16,25,36,49,64,81,100,121,144]


<details>
  <summary>Answer</summary>
  **Topic:** environment binding, fat arrow, magic names
  **Right answer:** `A.`

  **Explanation:** `arguments` behaves like `this` in « fat arrow » functions - it is not rebound and the binding from the outer environment will be used. Hence, when calling `mapWith`, `arguments[0]` will refer to any first argument given to the `row`.

  **Note:** if we had used a `function` keyword instead of a « fat arrow », the inner function would have bound `arguments` in its own environment, and `arguments[0]` would have referred to `column`. The answer would have hence been `B.`.
</details>
