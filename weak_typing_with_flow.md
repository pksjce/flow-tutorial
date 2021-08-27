A gradual typed system is as strong as your typing. If you provide a weak or broad type, it will fail to identify errors.

For eg

```javascript
function bar(x: Object) {
  x.y();
  if (x.hasOwnProperty("y")) {
    x.y();
  }
  if (x.hasOwnProperty("z")) {
    x.z();
  }
}
```

By typing `x: Object`, we see that flow can make no guess as to what it might contain. While this maybe convenient for libraries that implement broad apis and patterns, your code probably needs stricter typing which guarantees presence and type of `x.y`

Not exact typing

For eg

```javascript
//@flow

type Obj = { x: number };

const a: Obj = { x: 1, y: 1, z: 2 };
```

The above will not throw any error.

For these kind of inconsistencies to be uncovered, you will have to type the objects exactly.

```javascript
//@flow

type Obj = $Exact<{ x: number }>;

const a: Obj = { x: 1, y: 1 };
```

will throw the following looking error

```
5: const a:Obj = {x: 1, y:1}                 ^ Cannot assign object literal to `a` because property `y` is missing in `Obj` [1] but exists in object literal [2].
References:
5: const a:Obj = {x: 1, y:1}
           ^ [1]
5: const a:Obj = {x: 1, y:1}                 ^ [2]
```

Also further safety of the `const a` could be acheived through

```javascript
//@flow

type Obj = $ReadOnly<$Exact<{ x: number }>>;

const a: Obj = { x: 1 };
a.x = 2; // will throw error
```
