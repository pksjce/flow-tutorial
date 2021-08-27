Consider the following comparison

```javascript
// @flow
function example(x, y) {
  if (x == y) {
  }
  if (x === y) {
  }
}

example("a", 1);
```

Here, flow faithfully throws an error for `==` comparison as

```
3:     if (x == y) {}
           ^ Cannot compare string [1] to number [2].
References:
7: example('a', 1);
           ^ [1]
7: example('a', 1);
                ^ [2]
```
