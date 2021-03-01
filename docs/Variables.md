# A Formal Introduction

> This reference is structured so that it can be read from top to bottom, if you like. Later sections use ideas and syntax previously introduced. Familiarity with JavaScript is assumed.

Like many programming languages such as JS, Eliph uses significant use of **curly braces** `{}` to delimit blocks of code, rather than indentation.

Semicolons are optional and are mainly used to fit multiple expressions onto a single line, and in basic `for` and `till`-loops like below.

```dart
for i = 0; i < 10; i++ { console.log(i); }
till i = 0; i == 10; i++ { console.log(i); } // till is the opposite of for
```

Function calls must require parentheses, as in many other programming languages. **Statements** such as `break`, `continue` and `goto`, and **unary operators** such as `len` and `size` do not require parentheses, since they are not functions.

```dart
echo sys.inspect(e) // echo is a statement
```

When invoking functions as arguments to methods, such as in `map` and `filter` operations, you can leave out the parentheses.

```dart
[1, 2, 3, 4, 5].map { $ * 2 }.filter { $ % 3 == 0 }
```

Valid variable or identifier names with a letter, underscore `_` or **any Unicode character** that is not punctuation or symbols. All other characters can include digits, `-` and `$`.

Note: On using `-` as part of variable names, make sure to surround every `-` with spaces (you should also do the same with all infix operators). Leading `-` is parsed as a unary negation operator.

If you need to give a constant or variable the same name as a reserved Eliph keyword, prefix `$`. Use `$$` in place of `$`. This is because a single `$` is considered a **topical identifier**.

The following are a list of all the **keywords** of the language in Eliph:

```dart
var let const def
if unless then elif elun else
for till own in of when break continue
while until loop repeat pass
switch case where rise fall
try throw catch raise except finally
do return yield label goto guard
import export default from as
args this it debugger
get set async await

// Contextual keywords
at to til by with skip
ext impl pub pvt prot read fin mut stat

// Declarations
func gen infix unary
class | type | interface
struct | package | namespace

// Operators
and nand or nor xor xnor not
super len ctor size typeof instof del void

// Statements
print puts echo assert debug info warn error

// Types
any unknown other never
num int float deci frac comp
str char bool sym
tuple array record object
set map weakset weakmap regex

// Constants
true yes on | false no off
null | undef | infin | nan

// Browser constants
document event navigator performance screen window

// Node constants
console module native global require exports
```

You can declare `let` and `var` variables on their own. The `const` keyword is only used when declaring variables in loops.

```dart
let i;
var j;
for const i in [0::len array] {}
```

All variables when declared with the `=` assignment operator are automatically assigned a `let` declaration in the compiled output, the first time they appear.

Likewise, `const` variables are always initialized with `:=`, and **cannot be modified**.

```dart
i = 3;  // let i = 3
j .= 4; // var j = 4
k := 5; // const k = 5
```

Non-local or `var` variables are declared with `.=`, and you are required to use `.=` whenever you refer to the same variable in upper scopes, such as outside functions.

```dart
x .= 10 // declared as `var x`
do { x = 5 } // 10 => creates a temporary variable called x
do { x .= 2 } // 2 => modifies `var x`
```

You can declare multiple constants or multiple variables on a single line, separated by commas:

```dart
x = 0.0, y := 0.0, z .= 0.0;
```

or assign different types of variables the same value.

```dart
x = y := z .= 0.0;
```

`// line comments` and `/* block comments */` work the same way as in JavaScript.

```dart
/* hooray for nested comments */
/**
 * @param hooray for nested comments
 */
```

You can destructure from tuples, arrays, objects, records and maps, like in Swift, Reason or JavaScript:

```dart
(x, y, , z) = (0, 0, 1, 0);
[x, y, , z] = [0, 0, 1, 0];
{x, y, z} = {x: 0, y: 0, z: 0, a: 1};

{| 'x': x, 'y': y, 'z': z |} = {| 'x': 0, 'y': 0, 'z': 0 |};
```
