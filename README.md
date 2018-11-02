I've tested the demo with 3 versions of `esm`. 

And the node version is `10.0.0`. 

The results are much different.

Run:
```shell
$ node -r esm main.js
```

## esm 3.0.0

It works well.

## esm 3.0.18

It'll throw a:
```shell
file:///Users/leiysky/esm-demo/main.js:6
func('a', 'b');

ReferenceError: func is not defined
    at Object.<anonymous> (file:///Users/leiysky/esm-demo/main.js:6:7)
    at Object.<anonymous> (file:///Users/leiysky/esm-demo/main.js:1)
```

And if you exchange the import sequence in `main.js` like:
```js
// source 
import { func } from './util';
import { func1 } from './module';

// after exchanging
import { func1 } from './module';
import { func } from './util';
```
It'll work.

## esm 3.0.84

Just like `3.0.18`, but has different error:
```shell
file:///Users/leiysky/esm-demo/module.js:1
SyntaxError: Missing export name 'func' in ES module: file:///Users/leiysky/esm-demo/main.js
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:689:10)
```

And if you exchange the import sequence like above, it'll work too.