How to find the source of an error in flow.

Lets consider the following piece of code

```javascript
// @flow

const a = [1, 2, 3, 4];

function getArrayItem(index) {
  return a[index];
}

getArrayItem("5");
```

In the above piece we are calling `getArray` method with a string. Flow will detect this error for you and throw the following

```
6:   return a[index];
            ^ Cannot get `a[index]` because string [1] is not an array index.
References:
9: getArrayItem('5')
            ^ [1]
```

So, what can you do to fix this?
You should specifically annotate the parameters to the `getArrayItem` method as follows

`getArrayItem(index: number){..}`

Now the error changes to

```
9: getArrayItem('5')
            ^ Cannot call `getArray` with `'5'` bound to `index` because string [1] is incompatible with number [2].
References:
9: getArrayItem('5')
            ^ [1]
5: function getArray(index: number){
                            ^ [2]
```

The above error is much more clearer and points to the right annotated rule.
