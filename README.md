# Basics

1. tc39 is the team that handles changes in java script.
2. JS is 100% backward compatable. We if write code now, it will for sure work anytime in future.
3. Knowing how things are implemented in previous versions helps understand how latest features are implemented as most of them are just wrappers of the old functions

# Compilation vs Polifilling

`Compilation` - Takes the latest code and compiles it to older versions of javascript. Babel is an example

`Polifilling` - It is like a node package. Import and use it for same syntax

```
import Promise from 'promise-polyfill'
var Promise = requrie('promise-polyfill').default;
```

# use strict

1. add `"use strict"` at the top of js file
2. add `"use strict"` at the start of a function. This makes sure that only code that is inside that function is strict
```
// not strict
function hello() {
    "use strict"
    // strict mode
}
```

## uses of "use strict"

1. prevents accidental globals
```
var theVal = 0;
thVal = 1; // this not "theVal", it is "thVal". If we use strict mode, this will throw an error.
if(theVal > 0){
    console.log("greater than 0");
}
```
2. Does not spill values present in eval statement
```
"use strict"
var a = 2;
eval("var a = 1");
console.log(a); // If not strict, a will become 1
```
3. Cannot delete variables and functions when strict
```
"use strict";
var a = 2;
delete a; // throws an error

var foo = function(){}
delete foo; // throws an error
```
