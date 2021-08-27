Typing a function's return type, helps you avoid the function returning anything that cant be consumed. This works very well when there are conditionals in your function.

For eg

```
/* @flow */

function foo(text: string | number): string {
  switch (typeof text) {
    case 'string':
      return text;
    case 'number':
      return text; // error, should return string
    default:
      return 'wat';
  }
}
```
