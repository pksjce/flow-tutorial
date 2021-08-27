How union types work.

```
// @flow

type IsDoneWithResult = {
    done: true,
    result: string
}

type IsNotDone =  {
    done: false,
}
function getNew(x: IsDoneWithResult | IsNotDone) {
    if (x.done === true) {
      return x.result;
    }
    return x.result; // error
  }
```

Error

```
14:     return x.result; // error
                 ^ Cannot get `x.result` because property `result` is missing in `IsNotDone` [1].
References:
10: function getNew(x: IsDoneWithResult | IsNotDone) {
                                          ^ [1]
```

In the above code, the object `x` is a union type of `IsDoneWithResult` and `IsNotDone`. While uniting object types, they must have a same object param on which flow will unite the types. Now flow understands that if `x.done === true` then `x.result` must be present. If the result is otherwise, then `x.result` might not be present.
This keeps you safe from accessing undefined parameters.

Another interesting detection that flow does in case of Union types is

```javascript
// @flow
type IsDoneWithResult = {
  status: "DONE",
  result: string
};

type IsLoading = {
  status: "LOADING"
};
function getNew(x: IsDoneWithResult | IsLoading) {
  /* error */
  if (x.status === "LOADED") {
    return x.result;
  }
  return x.result;
}
```

The error is

```
11:     if (x.status === 'LOADED') {
            ^ all branches are incompatible: Either object with property `status` that matches string literal `LOADED` [1] is incompatible with string literal `DONE` [2]. Or object with property `status` that matches string literal `LOADED` [1] is incompatible with string literal `LOADING` [3].
References:
11:     if (x.status === 'LOADED') {
            ^ [1]
3:     status: 'DONE',
               ^ [2]
8:     status: 'LOADING',
               ^ [3]
```

This makes sure that you stick to a strict set of enums while branching over status parameter.
