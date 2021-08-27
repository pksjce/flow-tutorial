In a class, flow can help you extend and use the right properties from the parent

```javascript
/* @flow */

class A {
  prop: string;
  method(): string {
    return "A";
  }
}

class B {
  test(): string {
    if (super.prop) {
      return super.prop;
    }
    return "B";
  }
}
```

The error will be

```
12:     if (super.prop) {
            ^ property `prop` is missing in super of `B` [1].
References:
10: class B {
          ^ [1]
13:       return super.prop;
                 ^ Cannot return `super.prop` because property `prop` of unknown type [1] is incompatible with string [2].
References:
12:     if (super.prop) {
            ^ [1]
11:   test(): string {
              ^ [2]

```
