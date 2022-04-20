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

# Pass by value or pass by reference

1. Primitive data types are passed as values.
2. Objects are passed as pass by reference. i.e if we update a value, it will get reflected. But we replace it will not change the object.
```
var x = 1;
var obj1 = { "a": 1}
var obj2 = { "a": 1}
var foo = function(obj1, obj2, x){
    x = 2;
    obj1.["b"] = 2;
    obj2 = { "new" : 10 };
}
foo(obj1,obj2,x);
console.log(x); // 1
console.log(obj1); // { "a": 1, "b": 2}
console.log(obj2); // { "a": 1} // This is not changed
```

# Rest operator
One option to get indefinite number of arguments is using "arguments" keyword inside loop. It is not any array(array methods will not work), but we can itterate over the arguments.

Other option is to use spread operator
- It should be the last argument
- All the remaining arguments will form an array. We can use array operations on this.
```
var foo = function(method, ...options){
    console.log(arguments); // ["a", 1, 2, 3, 4] // Cannot perform array operations on this
    console.log(method); // "a"
    console.log(options); // [1, 2, 3, 4] // Can perform array operations on this
}
foo("a", 1, 2, 3, 4);
```

# Spread Operator
```
var arr1 = [1, 2, 3]
var arr2 = [...arr1]; // We can use this copy an array.
var arr3 = arr1; // This is just passing array as refference not as value.
arr2[0] = 4;
arr3[0] = 4;
console.log(arr1); // [1, 2, 3]
console.log(arr2); // [4, 2, 3]
console.log(arr3); // [4, 2, 3]
console.log(arr1); // [4, 2, 3]

var fun = function (...options) {
    console.log(options);
}
fun(arr1); // The options inside the function will be [[1,2,3]]
fun(...arr1); // The options inside the function will be [1,2,3]
```

# Template String
- Should be inside ``
- javascript code should be inside ${}
- tag\`\`. what ever is inside this \`\` will be passed to the function named tag
```
function h1(strings, ...values) { 
    // strings will contain [ "hell ", ", welcome to ", ""]
    // values will contain [ name, place ] coming from ${}
    var body = "";
    for (var i = 0; i < strings.legth; i++) {
        body += strings[i] + (values[i] || "");
    }
    return `<h1>{body}</h1>`;

}

var name = "MJ";
var place = "world";
console.log(h1`hello ${name}, welcome to ${place}`)
```
