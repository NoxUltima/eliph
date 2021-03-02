# A Formal Introduction

> This reference is structured so that it can be read from top to bottom, if you like. Later sections use ideas and syntax previously introduced. Familiarity with JavaScript is assumed.

This reference is structured so that it can be read from top to bottom, if you like. Later sections use ideas and syntax previously introduced. Familiarity with JavaScript is assumed.

First, the basics: CoffeeScript uses significant whitespace to delimit blocks of code. You don't need to use semicolons `;` to terminate expressions, ending the line will do just as well (although semicolons can still be used to fit multiple expressions onto a single line).

Instead of using curly braces `{ }` to surround blocks of code in functions, `if`-statements, `switch`, and `try`/`catch`, use indentation.

You don't need to use parentheses to invoke a function if you're passing arguments. The implicit call wraps forward to the end of the line or block expression.

`console.log sys.inspect object` → `console.log(sys.inspect(object));`

To further clear things up, you can omit the parentheses when calling a function.

```coffee
add 2, 3
```

And comments are:

```coffee
# from here to the end of the line.
```

Lisp hackers, you may be pleased to know that you can use dashes in the name of your variables and functions. The names are equivalent to, and are compiled to, camel case. Eg. `my-value = 42` == `myValue = 42`.

Note: On using `-` as part of variable names, make sure to surround every `-` with spaces on **both sides**---try to do the same with all operators.

If you need to give a constant or variable the same name as a reserved Eliph keyword, prefix `$`. Use `$$` in place of `$`. This is because a single `$` is considered a **topical identifier**. `#` is used for comments.

The file extension for Eliph is `.el`.

The following are a list of all the **keywords** of the language in Eliph:

```coffee
var let const def
if unless then elif elun else
for till own in of when lest
break continue while until loop repeat pass
switch case where rise fall
try throw catch raise except finally
do return yield label goto guard
import export default from as
args this it debugger
get set async await

# Contextual keywords
at to til by with skip
ext impl pub pvt prot read fin mut stat

# Declarations
func gen infix unary
class | type | interface
struct | package | namespace

# Operators
and nand or nor xor xnor not
super len ctor size typeof instof del void

# Statements
print puts echo assert debug info warn error

# Types
any unknown other never
num int float deci frac comp
str char bool sym
tuple array record object
set map weakset weakmap regex

# Constants
true yes on | false no off
null | undef | infin | nan

# Browser constants
document event navigator performance screen window

# Node constants
console module native global require exports
```

## the Basics

Valid variable or identifier names with a letter, underscore `_` or **any Unicode character** that is not punctuation or symbols. All other characters can include digits, `-` and `$`.

Basic assignment is as you would expect, `variable = value`, and there is no need for variable declarations with `var`, `let` or `const` as they are built into the operators.

However, you must use `.=` to modify variables in upper scopes, regardless if they were declared with `var` or `let`.

```coffee
x: int = 10 # type declaration

do -> x = 5
x # 10

do -> x .= 2
x # 2
```

Almost everything is an expression, which means you can do things like:

```coffee
x = if 2 + 2 == 4 then 10 else 0
x # 10
```

Things such as loops, switch statements, and even try/catch statements are all expressions.

If you want to simply declare a variable and not initialize it, you can use `let`. Alternatively, use `var` which behaves similar to JS 'var'.

```coffee
let x
```

You can also declare constants in LiveScript using `constant := value`. They are checked at compile time - the compiled JS adds a `const` for you.

Attempting to compile the following:

```coffee
const x = 10
x = 0
```

## Literals

### Booleans, Void, Undefined

Boolean values have two possible values, `true` and `false`, but those have their own aliases.

```coffee
true == on == yes # true
false == off == no # false
```

In JavaScript, "undefined" or `undef` can be redefined, so it is prudent to use the `void` operator which produces the undefined value, always.

```coffee
undef
x = void 0 # undefined
null
```

### Numbers

`int` literals have no `.`, whereas `float`s have. `int`s also can end in `n`, of which explicitly tell the compiler it is a `bigint`.

```coffee
42 # int

17.34 # float
0.4 # float
4. # float
.4 # float
```

Radix literals can be created using prefixes `0x`, `0o`, `0b`.

```coffee
dec = 6.
hex = 0xf00d
binary = 0b1010
octal = 0o744
```

Underscores, leading 0s and appended letters are ignored.

```coffee
distance = 064_000km
```

Bases 2 to 64 can be used, as long as they contain any combination of the below digits, are surounded in backticks and suffixed with the base.

```
0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$&
```

```coffee
i = `105`6 # 41
```

### Strings

Characters, of type `char`, enclosed in ` `` `, are strings of length 1. They are compatible with strings.

```coffee
a: char = `a`;
```

You can use double or single quotes for strings `str`.

```coffee
'a string'
"a string"
```

Characters and single-quote strings have special escape syntax, as shown below.

```coffee
'\''         # single quote
'\"'         # double quote
'\`'         # backtick
'\\'         # literal backslash
'\a'         # alert
'\b'         # backspace
'\e'         # escape
'\f'         # form feed
'\n'         # newline
'\r'         # carriage return
'\t'         # tab
'\v'         # vertical tab
'\x30'       # ASCII character
'\uFFFF'     # BMP Unicode character
'\u{10FFFF}' # non-BMP Unicode character
```

Strings can be written with a preceding backslash instead of quotes. Backslash strings can't contain `, : ; ] ) }` or whitespace.

```coffee
\word
func \word, \word;
(func \word)
[\word]
{prop: \word}
```

Double quoted strings allow interpolation. Single quoted strings are passed through as-is. Simple variables can be interpolated without curly braces.

```coffee

"The answer is #{2 + 2}"
'As #{is}'

variable = "world"
"Hello #variable"
```

Multiline strings (can also do the same but with double quotes for use with interpolation):

```coffee
multiline = 'string can be multiline \
            and go on and on \
            beginning whitespace is \
            ignored'
heredoc = '''
            string can be multiline
            with newlines
            and go on and on
            beginning whitespace is
            ignored
'''
nospaces = 'deadbeef
            deadbeef'
```

### Objects

Braces are optional:

```coffee
obj = {prop: 1, thing: 'moo'}

person =
  age:      23
  eye-color: 'green'
  height:   180cm

oneline = color: 'blue', heat: 4
```

Property access:

```coffee
obj = {}
obj.key = 'val'
obj.'key1' = 'val' # similar to TOML
obj['key2'] = 'val'

obj # { key: 'val', key1: 'val', key2: 'val' }
```

Dynamic keys:

```coffee
obj =
  "#variable": 234
  (person.eye-color): false
```

Property setting shorthand - easily set properties with variables if you want the property name to be the same as the variable name.

```coffee
x = 1
y = 2
obj = {x, y}
```

Flagging shorthand - easily set boolean properties.

```coffee
{+debug, -live}
```

This - no need to use a dot `.` to access properties.

```coffee
@ # this
@location # this.location
@'location' # this.'location'
@['location'] # this['location]
```

### Arrays

Arrays work the same way as in JavaScript.

```coffee
[1, person.age, 'French Fries']
```

Implicit arrays created with an indented block. They need at least two items for it to work. If you have only one item, you can add a splat `...` to force the implicit list.

```coffee
my-list =
  32 + 1
  person.height
  'beautiful'

one-item =
  1
  ...
```

When implicitly listing, you can use an asterisk `*` to disambiguate structures such as arrays and objects. The asterisk does not denote an item of the list, but merely sets aside an implicit structure so that it is not muddled with the other ones being listed.

```coffee
tree =
  * 1
    * 2
      3
    4
  * 5
    6
    * 7
      8
      * 9
        10
    11

obj-list =
  * name: 'tessa'
    age:  23
  * name: 'kendall'
    age:  19

obj =
  * name: 'tessa'
    age:  23

obj-one-list =
  * name: 'tessa'
    age:  23
  ...
```

Lists of words:

```coffee
[* list of words *]
```

#### Tuples, Sets and Maps

Tuples, sets and maps are created the same way as in objects, or with constructor functions.

```coffee
set = [| 1, 2, 3 |] # Map literal

set = new Set
  1
  2
  3

map = {| 1: 2, 3: 4 |} # Map literal

map = new Map
  * 1, 2
  * 3, 4

tuple = (1, 2, 3) # Tuple literal

tuple = new Tuple
  1
  2
  3

record = (| key: val |) # Record literal

record = new Record
  key: val
```

### Ranges

Ranges can be:

- individual numbers or characters, separated by `,`
- ranges or classes of characters, separated by combinations of `:` or `<>` (angle brackets exclude either start or end)
- \+ variable steps, separated by colons: `2:3:4`

`0`s or spaces ` ` are added implicitly wherever needed.

| Operator         | Meaning                           |
| ---------------- | --------------------------------- |
| `a,b`            | `a` and `b` only                  |
| `,b,`            | implicit `0` -> `0,b,0`           |
| `a,b:c`          | `a`, then from `b` to `c` by `±1` |
| `a::b`           | from `a` to `b`, inclusive        |
| `a:>b` or `a:<b` | ... excluding `b`                 |
| `a<:b` or `a>:b` | ... excluding `a`                 |
| `a<>b` or `a><b` | ... exclusive                     |
| `a::b:c`         | ... inclusive, step by `c`        |
| `a::b:c:d`       | ... step by `c`, then `d`\*       |

In `[a::b:c:d]`:

- Range alternates between adding `c` and `d` to `a`, until reaching/hitting `b`.
- Algebraically: `[a, a+c, a+c+d, a+2c+d, a+2c+2d, a+3c+2d, a+3c+3d ... b]`

You can also specify literal characters, as either `char` literals or single-character strings.

Some things to note:

- If the range counts **out of bounds**, it will coerce that to count in the right direction.
- So, if `c + d > 0 && a > b || c + d < 0 && a < b`, then all numbers following `a` and `b` will be negated: `c` would be `-c` and `d` would be `-d`.

````coffee
[1,2,3] # [1, 2, 3]
[1::10] # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[1::10:2] # [1, 3, 5, 7, 9]
[-1,0::10:1:2] # [0, 1, 3, 4, 6, 7, 9, 10]

# String literals
['a'::'j'] # ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
['a'::'f':2] # ['a', 'c', 'e']
``

### Miscellaneous

Labels (useful for nested loops):

```coffee
label l: 4 + 2
````

Constructor shorthand.

```coffee
@@
@@x
x@@y
```

## Operators

### Boolean

Logical and comparison operators such as `!`, `&&`, `||`, `<`, `>`, `<=`, `>=` are retained.

```coffee
!true # false
true && false # false
true || false # true
```

You can do chained comparison with `<`, `>`, `<=`, `>=`:

```coffee
1 < 2 < 4        # true
1 < 2 == 4/2 > 0 # true
```

We also add the xor operator `^^`.

`&&`, `||` and `^^`, and their infix forms `and`, `or` and `xor`, have their own inverses: `!&`/`nand`, `!|`/`nor` and `!^`/`xnor`.

```coffee
false ^^ true  # true
false ^^ false # false
1 ^^ 0         # 1
1 ^^ 1         # false
```

Because the `==` operator frequently causes undesirable coercion, is intransitive, and has a different meaning than in other languages, CoffeeScript compiles `==` into `===,` and `!=` into `!==`. In addition, `is` compiles into `===,` and `isnt` into `!==`.

If you really want to use JavaScript's `==` and `!=`, use the _fuzzy equality_ operators `=~` and `!~`, or aliases `sim` or `diff` instead.

### Numeric

The basic operations `+`, `-`, `*` and `/` work the same way as in JS, and you can use parentheses `()` in grouping your expressions:

```coffee
2 + 2 # 4
50 - 5 * 6 # 20
(50 - 5 * 6) / 4 # 5.0
8 / 5 # 1.6
```

Regular division with `/` will evaluate to a `float`, but floor division with `//` will return `int`. Operators with mixed type operands convert the evaluated result to `float`:

```coffee
4 * 3.75 - 1;
```

```coffee
17 / 3 # 5.666666666666667
17 // 3 # 5
17 % 3 # 2
5 * 3 + 2 # 17
```

Bitwise operations such as unary `~`, infix `&`, `|` and `^` (and their inverses `~&`, `~|`, `~^`), and shift operators `<<`, `>>` and `>>>` will evaluate into `int`, no matter the type.

```coffee
14 & 9   # 8
14 | 9   # 15
14 ^ 9   # 7
~9       # -10
9  << 2  # 36
-9 >> 2  # -3
-9 >>> 2 # 1073741821
```

`%%` provides dividend-dependent modulo:

```coffee
-7 % 5 == -2 # The remainder of 7 / 5
-7 %% 5 == 3 # n %% 5 is always between 0 and 4
```

The minimum/maximum operators `<?` and `>?`, which return the smaller or larger of the two operands.

```coffee
3 <? 10 # 3
3 >? 10 # 10
```

PHP's "spaceship" operator `<=>`, returns either `1`, `0` or `-1` depending on whether the number on the left is greater than, equal to or lesser than the right.

```coffee
3 <=> 1 # 1
1 <=> 3 # -1
2 <=> 2 # 0
```

Casting to a number:

```coffee
+'4' #  4
-'3' # -3
```

Use `in` to check if an element is in a list; use `of` to check if a key is in an object.

```coffee
list = [7, 8, 9]
2 in [1, 2, 3, 4, 5]             # true
3 in list                    # false
\id of id: 23, name: \rogers # true
```

Use the `len` operator to retrieve the length of a string, array or tuple, use `size` to check for the number of keys or elements in an object, record, map and set:

```coffee
strLen: int = len 'hello' # 5
arrLen: int = len  [1, 2, 3, 4, 5] # 5
tupleLen: int = len (1, 2, 3, 4, 5) # 5

objSize: int = size {| 0, 1, 2, 3, 4 |} # 5
setSize: int = size [| 0, 1, 2, 3, 4 |] # 5
recSize: int = size {- 0: 0, 1: 1, 2: 2, 3: 3, 4: 4 -} # 5
mapSize: int = size {| 0: 0, 1: 1, 2: 2, 3: 3, 4: 4 |} # 5
```

Strings, tuples and arrays can be concatenated `+`, replaced `-`, repeated `*`, or sliced/split `/` with arithmetic operators.

Use `*` to join strings back from arrays `[]` or tuples `()`, where the right operand is the delimiter, converting whatever non-string into strings.

```coffee
s: str = 'Hello'

# Concatenating strings together
s = 'Hello' + 'World!' # 'Hello World!'
s = 'Hello'

# Repeating strings
s = 'hello ' * 3 # 'hello hello hello '

# Replacing with substring or regex
s = 'Hello' - `l` # 'Heo'
s = 'Hello' - (/llo$/, 'lp me') # 'Help me'
# (calls String.replace() with the right operand)

# Splitting
t: str[] = s / 1 # ['H', 'e', 'l', 'l', 'o']
t = s / [2, 3] # ['He', 'llo']
t = s / '' # ['H', 'e', 'l', 'l', 'o']

# Splitting
c: char[] = [...s] # [`h`, `e`, `l`, `l`, `o`]
```

Tuples can be concatenated `+`, filtered `-`, repeated `*`, or sliced/split `/` with arithmetic operators.

Use `*` to join strings back from arrays `[]` or tuples `()`, where the right operand is the delimiter, converting whatever non-string into strings.

```coffee
s: str = 'Hello'

# Concatenation
a = (1, 2) + (3, 4); #  (1, 2, 3, 4)

# Filtering (all instances of the values will be removed)
a = (1, 2, 3) - 3; #  (1, 2)
a = (1, 3, 2, 3) - 3; #  (1, 2)
a = (1, 3, 2, 3) - (2, 3); #  (1)

# Filtering with functions
a = (1, 3, 2, 4) - (e) => 1 < e < 4 # (1, 4)

# Repeating
a = (1:) * 3 # (1, 1, 1)

# Subdividing
a = (1::10) / 2 # ((1, 2), (3, 4), (5, 6), (7, 8), (9, 10))
a = (1::10) / (1, 2, 3, 4) # ((1), (2, 3), (4, 5, 6), (7, 8, 9, 10))

# Joining
strArr = ['H', 'e', `l`, 'l', 'o']
strArr = strArr * '' # 'Hello'
```

### Piping

Instead of a series of nested function calls, you can pipe values in. `x |> f` and `f <| x` are equivalent to f(x).

```coffee
x = [1, 2, 3] |> reverse |> head # 3
y = reverse <| [1, 2, 3] # [3, 2, 1]
```

Use `$` as a placeholder in pipeline operations. `$` is immutable, established only once per pipeline step.

```coffee
input |> $ - 3 |> -$ |> $ * 2 |> Math.max $, 0 |> print
```

### Existence

The `?` or existence operator can be used in a variety of contexts to check for existence. For completeness:

| Example                         | Definition                                                                                                             |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `a?`                            | tests that `a` is in scope and `a != null`                                                                             |
| `a ? b`                         | returns `a` if `a` is in scope and `a != null`; otherwise, b                                                           |
| `a?.b` or `a?.'b'` or `a?['b']` | returns `a.b` if `a` is in scope and `a != null`; otherwise, `undefined`                                               |
| `a?(b, c) or a? b, c`           | returns the result of calling `a` (with arguments `b` and `c`) if `a` is in scope and callable; otherwise, `undefined` |
| `a ?= b`                        | assigns the value of `b` to `a` if `a` is not in scope or if `a == null`; produces the new value of `a`                |

```coffee
# Conditional existence assignment
solipsism = true if mind? && !world?

# Existence tests with if statement
if window?
  environment = 'browser (probably)'

# Existence assignment
speed = 0
speed ?= 15

# nullish coalescing
footprints = yeti ? "bear"

# Optional chaining
zip = lottery.drawWinner?().'address'?.zipcode
```

### Objects

`instof` (alternative to the long `instanceof`) - list literals to the right get expanded:

```coffee
new Date() instof Date           # true
new Date() instof [Date, Object] # true
```

`typeof` - add a bang for a useful alternative:

```coffee
typeof /^/  # object
typeof! /^/ # RegExp
```

`del` or `delete` returns the value of the deleted item:

```coffee
obj = {one: 1, two: 2}
r = del obj.one
r # 1
```

`del!` is like `del` in JavaScript, and returns `false` only if the property exists and can't be deleted, otherwise returns `true`.

```coffee
obj = {one: 1, two: 2}
delete! obj.one # true
delete! Math.PI # false
```

Property copy - copy enumerable properties, both ways. `<<<` for own properties, `<<<<` for all properties.

```coffee
obj = {one: 1, two: 2}
obj <<< three: 3 # {one: 1, two: 2, three: 3}
three: 3 <<< obj # {one: 1, two: 2, three: 3}
{go: true} <<<< window
window >>>> go: true
```

Clone `^^` - creates a prototypical clone of the operand. It does not create a deep clone of the object, rather the resulting object's prototype is the operand. Remember that prototypes are ignored when serializing to JSON.

```coffee
obj = {one: 1}

obj2 = ^^obj
obj2.two = 2
obj2 # {one: 1, two: 2}
# above includes its prototype's properties
# JSON serialization would be just `{two: 2}`
obj  # {one: 1}
```

The infix `with` (aka the cloneport) combines the clone and property copy operators for easy object creation. It is equivalent to `^^obj <<< obj2`. Remember that the clone operator creates a prototypical clone, and prototypes are not serialized in JSON.

```coffee
girl = {name: \hanna, age: 22}
guy  = girl with name: \john
guy  # {name: 'john',  age: 22}

# the above result includes the object's prototype
# in the result - the actual JSON: {name: 'john'}

girl # {name: 'hanna', age: 22}
```

### Partial Application, Operators as Functions

You can partially apply operators and properties, and use them as functions.

```coffee
(+ 2) 4         # 6
(*) 4 3         # 12

(!) true        # false
(in [1::3]) 2 # true

(.name) name: \Tessa # 'Tessa'
```

By using the `export` operator instead of `exports` you get a more concise way to define modules.

```coffee
export func = ->
export v
export v-a, v-b, v-c

export
  a: 1
  b: -> 123

export class MyClass
```

### Import

Having to require a series of modules results in a lot of cruft. You can get rid of that cruft by using require!, which takes an ID, or a string, array, or object literal.

If you are requiring a module with dashes in its name, you must use a string literal.

You can rename what you are requiring by using an object literal.

You can destructure to get the contents of value.

```coffee
import lib
import 'lib1'

import prelude-ls
import 'prelude-ls'

import [fs, path]
import fs, path

import jQuery: $

import {
  fs
  path
  lib: foo
}
```

You can easily require parts of modules with destructuring.

```coffee
import {
  fs: filesystem
  'prelude-ls': {map, id}
  path: {join, resolve}:p
}
```

Filenames are automatically extracted.

```coffee
import 'lib.js'
import './dir/lib1.js'
```

## Control Flow

### If, Unless and Else

There are several ways to format an `if` statement. (Note that the `if` statement is actually an expression, and be used as such). `=>` is an alias for `then`.

The standard:

```coffee
if 2 + 2 == 4
  'something'
else
  'something else'

if 2 + 2 == 4 then 'something' else 'something else'

if 2 + 2 == 4
then 'something'
else 'something else'
```

The `else` is optional, and further `elif`s can be added.

```coffee
if 2 + 2 == 4
  'something'

if 2 + 2 == 6
  'something'
elif 2 + 2  == 5
  'something else'
else
  'the default'
```

It can be used as an expression:

```coffee
result = if 2 / 2 is 0
         then 'something'
         else 'something else'
```

It can also be used postfix - it has a lower precedence than assignment, making this useful:

```coffee
x = 10
x = 3 if 2 + 2 == 4
x # 3
```

`unless` is the equivalent to `if not`, and `eless` `else if not`.

```coffee
unless 2 + 2 == 5
  'something'
eless 3 + 3 == 6
  'yo'

x = 10
x = 3 unless 2 + 2 == 5
```

`guard` is an alias for `unless`, and must always end with `else`.

```coffee
x = guard 2 + 4 == 5 else
  'something'
x # something
```

`that` refers implicitly to the value of the condition. It will unwrap existence checks.

```coffee
time = days: 365

half-year = that / 2 if time.days
# 182.5

if /^e(.*)/ == 'enter'
  that.1   # 'nter'

if half-year?
  that * 2 # 365
```

### Loops and Comprehensions

There are three basic forms of for loop. One that iterates through a range of numbers, one that iterates through items in a list, and one that iterates through keys and values of an object.

We will first examine the for loop that iterates through a range of numbers. It has the structure of: `for (var|let|const) (VAR) in (RANGE) (when|lest COND)` - (almost everything is optional). By default, `VAR` is implicitly declared `let`.

You previously learnt about ranges in `RANGE`, which are encased in either `()` or `[]`.

`when`, (alias `case`, `|`) is an optional guard, and will evaluate to an `if` statement in the loop. Similarly, `lest` is equivalent to `unless` or `when not`.

If used as an expression, loops will evaluate to a list.

```coffee
i = [for i from 1 to 10 by 3 => i]
# 1, 4, 7, 10
```

`for ... in` loops iterate through a list. They have the structure: `for (var|let|const VAL-VAR), (var|let|const? INDEX-VAR) in EXP (when|lest COND)` - again almost everything is optional.

`VAL-VAR` evaluates to the current value, while `INDEX-VAR` evaluates to the current index of the list. Either one is optional.

`EXP` should evaluate to an array or tuple, which can be indexed.

```coffee
for x in [1, 2, 3]
  x

xs = for let x, i in [1::10] by 2 when x % 3 == 0
  -> i + x
xs[0]! # 5
xs[1]! # 17
```

`for ... of` loops iterate through an object. They have the structure: `for own let (var|let|const KEY-VAR), (var|let|const? VAL-VAR) in EXP (when|lest COND)` - again almost everything is optional.

`own` uses the hasOwnProperty check on the properties, stopping the iteration of properties higher up in the prototype chain.

`KEY-VAR` evaluates to the key of the property, and `VAL-VAR` evaluates to the property value. Either one is optional.

`EXP` should evaluate to an object, or virtually anything with key-value pairs.

```coffee
for k, v of {a: 1, b: 2}
  "#k#v"

xs = for own let key, value of {a: 1, b: 2, c: 3, d: 4} when value % 2 == 0
  -> key + value
xs[0]! # 'b2'
xs[1]! # 'd4'
```

Both `for...in` and `for...of` are interchangeable - the two (optional) key/value variables are switched. The value comes first and then the key in `for...in` loops, whereas the key comes first and then the value in `for...of` loops.

You can omit one or both variables in in/of loops.

```coffee
res = for , i in [1, 2, 3]
  i
res # [0, 1, 2]

for (:>3) then fun!
# calls `fun` three times

[6 for (:>3)] # [6, 6, 6]
```

Regular nested loops will evaluate to a list of lists.

```coffee
result = for x to 3
  for y to 2
    x + y
result # [[0, 1, 2], [1, 2, 3], [2, 3, 4], [3, 4, 5]]
```

List comprehensions always produce a list. Nested comprehensions produce a flattened list.

```coffee
[x + 1 for x in [::10:2] when x != 4]
# [1,3,7,9,11]

["#x#y" for x in [\a, \b] for y in [1, 2]]
# ['a1','a2','b1','b2']
```

Object comprehensions produce an object. You can also perform comprehensions on tuples, sets, maps and records this way too.

```coffee
sample-obj = {key: val * 2 for key, val of {a: 1, b: 2}}
# {a: 2, b: 4}

my-tuple = ("#x#y" for x in (\a, \b) for y in (1, 2))
# Tuple { 'a1', 'a2', 'b1', 'b2' }

squares = {| x: x ** 2 for x in [1::5] |}
# Map { 1: 1, 2: 4, 3: 9, 4: 16, 5: 25 }

random-set = [| x for x in [1::10:2,-3] when x |]
# Set { 2, 4, 6, 8, 10, -3 }
```

`while` loops:

```coffee
i = 0
list = [1::10]
while n < 9
  n = list[++i]
```

`until` is equivalent to `while not`.

`while`/`until` can also accept a when guard, and an optional `else` clause which runs if the loop didn't run at all.

```coffee
i = 1
list = [1 to 10]
until i > 7 when n != 99
  n = list[++i]
else 10
```

`repeat-while` loops, or the JavaScript equivalent of `do-while`:

```coffee
i = 0
list = [1 to 10]
repeat
  i++
while list[i] < 9
```

`while` can also accept an update clause.

```coffee
i = 0
list = [1 to 10]
while list[i] < 9, i++ then i
```

`while true`:

```coffee
i = 0
loop
  \ha
  break if ++i > 20

i = 0
repeat
  \ha
  if ++i > 20 then break
```

### Switch

`break` is automatically inserted, and multiple conditions are allowed.

```coffee
switch 6
  case 1    then \hello
  case 2, 4 then \boom
  case 6
    'here it is'
  default \something
```

If you switch on nothing, you switch on true.

```coffee
switch
  case 5 == 6
    \never
  case false
    'also never'
  case 6 / 2 is 3
    'here'
```

You can use `fall` to stop automatic break insertion. It must be the last expression of the case block. As well, you can use a `switch` statement as an expression.

```coffee
result = switch 6
  case 6
    something = 5
    fall
  case 4
    'this is it'

result # 'this is it'
```

`|` is an `alias` for case, and `=>` is an alias for `then`. `else` and `| =>` are aliases for default.

```coffee
switch 'moto'
  | "some thing"      => \hello
  | \explosion, \bomb => \boom
  | [< the moto ? >]  => 'here it is'
  |                   => \something
```

You can add an optional guard with `where` and `lest` (opposite of `where`), and also declare other variables to check for additional conditions:

```coffee
switch point = (-1, 1)
  | (x, y) where x == y =>
    print "(#x, #y) is on the line x == y"
  | (x, y) lest x != -y =>
    print "(#x, #y) is on the line x == -y"
  | (x, y) =>
    print "(#x, #y) is just some arbitrary point"
```

You can use data structures to test multiple values, in which any variable assigned is automatically destructured in the same switch statement.

Alternatively, leave the structure blank `()` or insert a wildcard placeholder `$`, to match any possible value.

```coffee
switch point = {x: 1.5, y: 1.5}
  | {x: 0, y: 0} =>
    print "#point is at the origin"
  | {x: 0} =>
    print "#point is on the x-axis"
  | {y: 0} =>
    print "#point is on the y-axis"
  | {x: -2 <= x <= 2, y: -2 <= y <= 2} =>
    print "#point is inside the box"
  | {} =>
    print "#point is outside of the box"
```

### Control Transfer Statements

The `continue` statement tells a loop to stop what it's doing and start again at next iteration of the loop.

```coffee
text = "", i;
for i in [1::5]
  if i == 3 => continue
  text += "The number is " + i + "\n"
```

In a switch statement, `continue` stops the execution of the current branch and executes the labelled branch that immediately comes after it.

```coffee
command = 'CLOSED'
switch command
  case 'CLOSED' =>
    continue nowClosed # move to nowClosed without printing
    print command
  nowClosed: case command1 := 'NOW_CLOSED' =>
    print command1
```

The `break` statement ends execution of an entire control flow statement immediately.

```coffee
text = "", i;
for i in [1::5]
  if i == 3 => break
  text += "The number is " + i + "\n"
```

You can mark a statement, such as a `do`-block, with a statement marked with `label`, as long as it doesn't exist at the parent scope. Use `goto` followed by the labeled keyword.

```coffee
i = 0;
func goTo: void
  label runThis: do for j in [1::100]
    i .+= j; return
  print i # 0
  goto runThis
  print i # 5050
  return;

goTo!
goto runThis # Throws an error
```

### Exceptions

You can throw exceptions with the aptly named `throw`. For built-in error types, it is common convention to leave out the `new`.

```coffee
throw Error 'an error has occurred!'
```

You can catch and deal with exceptions with the try catch finally block. Both catch and finally are optional.

The `try` block is attempted. If an exception occurs, the `catch` block is executed. It is supplied with the exception object. If you do not specify the name of this variable it will default to `e`. You can destructure the exception object if you wish.

```coffee
try => ...

try => ...
catch
  2 + 2
  e.message

x = try => ...
catch {message} => message

x # unimplemented
```

The `finally` block is executed after the `try` or `catch`, regardless of what has happened.

```coffee
try => ...
catch => handleException e
finally => doSomething!

try => ...
finally => doSomething!
```


## Functions

Functions are defined by an optional list of parameters in parentheses, an arrow, and the function body. The empty function looks like this: `->`

```coffee
(x, y) -> x + y

-> # an empty function

# multiple lines, and be assigned to
# a let like in JavaScript
times = (x, y) ->
  x * y
```

As you see, function definitions are considerably shorter! You may also have noticed that we have omitted return. In Eliph, almost everything is an expression and the last one reached is automatically returned.

However, you can still use `return` to force returns if you want, or you can add a bang `!` before the arrow to suppress auto-returning: `no-ret = (x) !->`, or add an implicit `return` at the end.

You can also strongly type your arguments. In this case, `void` is used as a type, and `void` is the union of `undef` and `null`.

```coffee
times = (x: num, y: num): num -> x * y
nothing = (): void -> undef
```

You can omit the parentheses when calling a function, and you can omit the comma separating the arguments if the preceding item is not callable, just like in arrays.

```coffee
x = 4
Math.pow x, 3 # 64
Math.pow 2 3  # 8
```

If you are calling the function with no arguments, you can use a bang ! - as well you don't need to use a dot when chaining banged functions.

```coffee
f!
[1, 2, 3].reverse!slice 1 # [2,1]
```

and, or, xor, spaced . or ?. all close implicit calls - allowing for parentheses free chaining.

`and`, `or`, `xor`, `nand`, `nor`, `xnor`, as well as ` .` and `?.` all close implicit calls, while `&&`, `||`, `^^`, `!&`, `!|`, `!^` do not.

```coffee
even 0 and 3 # even(0) && 3
even 0 &&  3 # even(0 && 3)

$$ \h1 .find \a .text! # Hello world!
```

You can use `do` to call functions with no arguments:

```coffee
do 3 + 2 # 5
```

and pass arguments to them right after the `do`:

```coffee
x = 3, y = 2
do x + y # 5
```

If you use do on a named function, when the do is not used as an expression, the named function will remain a function statement.

```coffee
i = 0
f 9 # 9
i   # 1
do func f x
  ++i; x
i   # 2
```

You can't call a function with an implicit object, if you want to do that you can use `do`:

```coffee
f do
  a: 1
  b: 2
```

`do` allows you to do many things without adding extra parentheses.

```coffee
pow do
  1
  2

h 1 do
  a: 2
  b: 5
```

You can also call functions infix using backticks `` ` ``.

```coffee
add = (x, y) -> x + y
3 `add` 4 # 7
```

Calling a function with bare splats ... implies calling it with the arguments of the current function. Especially useful when calling `super`.

```coffee
add = (x, y) -> x + y
g = (a, b) -> add ...
g 3, 4 # 7
```

### Parameters

Extended parameters:

```coffee
setPersonParams = (
  person # target object to set params
  person.age
  person.height
) -> person

person = setPersonParams {}, 21, 180 cm
# => {age: 21, height: 180}
```

This is especially useful with `this`.

```coffee
set-text = (@text) -> this
```

You can set default arguments:

```coffee
add = (x = 4, y = 3) -> x + y
add 1, 2 # 3
add 1    # 4
add!     # 7
```

...or indeed use any operator (in parameters, `x = 2` is just `x ? 2`):

```coffee
add = (x && 4, y || 3) -> x + y
add 1, 2 # 6
add 2, 0 # 7
```

You can also destructure the arguments:

```coffee
setCoords = ({x, y}) -> "#x,#y"
setCoords y: 2, x: 3 # '3,2'
```

...and even set defaults (or use any logic) on those destructured parameters, functioning like Python's keyword arguments.

```coffee
setCoords = (~x = 1, ~y = 3) -> "#x, #y"
setCoords y = 2, x = 3 # '3,2'
setCoords x = 2 # '2,3'
setCoords y = 7 # '1,7'
setCoords! # '1,3'

# Alternatively,
setCoords = ({x = 1, y = 3} = {}) -> "#x,#y"
setCoords y: 2, x: 3 # '3,2'
setCoords x: 2 # '2,3'
setCoords y: 7 # '1,7'
setCoords! # '1,3'
```

You can also use splats in your parameters:

```coffee
f = (x, ...ys) -> x + ys.1
f 1, 2, 3, 4 # 4
```

You can even use unary operators in your parameters. You could use + and `!!` to cast your parameters to a number or boolean respectively, or use the clone operator `^^` to make sure any changes you make to the object are not reflected in the original. You can still use extended parameters, eg. `(!!x.x) ->`.

```coffee
f = (!!x) -> x
f 'truthy string' # true

g = (+x) -> x
g '' # 0

obj = prop: 1
h = (^^x) ->
  x.prop = 99; x
h obj
obj.prop # 1
```

### Bound Functions

Defined using the wavy arrow `~>`. Use the long wavy arrow for curried and bound functions `~~>`. Prepend a ~ to named functions to make them bound.

Bound functions have `this` lexically bound, not dynamically bound as normally. This means that it does not matter in which context they are called, the value of this in their body will always be the value of this where they were defined.

```coffee
obj = new
  @x      = 10
  @normal = -> @x
  @bound  = ~> @x

obj2 = x: 5
obj2.normal = obj.normal
obj2.bound  = obj.bound

obj2.normal! # 5
obj2.bound!  # 10
```

### Named Functions

You can create named functions whose definition is hoisted to the top of the scope - this is useful for defining utility functions at the end of the file instead of the top. Name functions are constants, and can't be redefined.

```coffee
util!  # 'available above declaration'
util2! # 2

func util(): str => 'available above declaration'
func util2 => 2
```

You can prepend the function definition with a `~` to make it a bound function.

```coffee
~func add(x: num, y: num): void
  @result = x + y
```

You can prepend it with a bang `!` to suppress returning.

```coffee
util! # nothing
!function util x => x
```

### Currying

Curried functions are very powerful. Essentially, when called with less arguments than defined with, they return a partially applied function. This means that it returns a function whose arguments are those which you didn't supply, with the values for what you did supply already bound. They are defined in LiveScript using the long arrow. Perhaps an example will make things more clear:

```coffee
times = (x, y) --> x * y
times 2, 3       # 6 (normal use works as expected)
double = times 2
double 5         # 10
```

You can define bound curried functions with a long wavy arrow: `~~>` If you call a curried function with no arguments, it will evaluate as is, allowing you to use default arguments.

```coffee
f = (x = 5, y = 10) ~~> x + y
f! # 15
g = f 20
g 7 # 27
g!  # 30
```

### Access/Call Function Shorthand

There are especially useful for higher order functions like `map` and `filter`.

`(.prop)` is short for `(x) -> x.prop`.

```coffee
[< hello there you >].map (.length),
# [5, 5, 3]

[< hello there you >].filter (.length < 4)
# ['you']
```

`(unary-op)` is short for `(x) -> unary-op(x)`.

```coffee
[< hello there you >].map (len)
# [5, 5, 3]

[< hello there you >].filter (len < 4)
# ['you']
```

You can also use this to call methods:

```coffee
[[1, 2, 3], [7, 8, 9]].map (.join \|)
# ['1|2|3', '7|8|9']
```

`(obj.)` is short for `(x) -> obj[x]`.

```coffee
obj = one: 1, two: 2, three: 3
[< one three >].map (obj.)
# [1, 3]
```

### Backcalls

Backcalls are very useful. They allow you to unnest callbacks. They are defined using arrows pointed to the left. All the syntax is the same as regular arrows for defining bound functions (`<~`), curried functions (`<--`, `<~~`), suppressing return (`<-!`) - except that it is just pointing the other way.

```coffee
<- $
alert 'boom'
```

They can take arguments, and you can specify a placeholder `$` for where you want it to go.

```coffee
x <- map $, [1::3]
x * 2
# [2, 4, 6]
```

If you wish to have further code after your backcalls, you can set them aside with a do statement.

```coffee
do
  data <-! $.get 'ajaxtest'
  $ '.result' .html data
  processed <-! $.get 'ajaxprocess', data
  $ '.result' .append processed

alert 'hi'
```

### Async and Await

If you will be running your compiled code on a platform that supports the async and await JavaScript keywords, then you can write true asynchronous functions in LiveScript. To mark a function as async, either add an extra `>` to the function arrow (`->>`, `~>>`, `-->>`, etc.), or write `async func` instead of `func` for named functions. Inside an `async` function, you can use the `await` keyword as you would in JavaScript.

```coffee
f1 = (x) ->> await x

async function f2 x
a = await f1 x
```

### Partial Application

You can partially apply functions using the underscore `_` as a placeholder. Sometimes, the function you want to deal with isn't curried, or if it is the arguments are not in a good order. In these cases partial application is very useful.

```coffee
filter-nums = filter _, [1 to 5]
filter-nums even # [2,4]
filter-nums odd # [1,3,5]
filter-nums (< 3) # [1,2]
```

If you call a partially applied function with no arguments, it will execute as is instead of returning itself, allowing you to use default arguments.

Partially applied functions are also really useful for piping if the functions you are using don't have a nice argument order and aren't curried (like in underscore.js for instance).

```coffee
[1, 2, 3] |> _.map $, (* 2) |> _.reduce $, (+), 0
# 12
```

### Arguments

If you have only one argument, you can use `it` to access it without having to define an argument.

```coffee
f = -> it + 2
f 3 # 5
```

You can access the arguments object with the shorthand `&`. The first argument is `&.0`, the second `&.1`, and so on. `&` alone is arguments as a whole.

```coffee
add-three-numbers = -> &.0 + &.1 + &.2
add-three-numbers 1, 2, 3 # 6
```

Note that currying won't work in that situation, as the number of declared arguments in add-three-numbers is 0.

### Generator Functions

You can use generators and yield, as well! A brief rundown:

```coffee
func* f
  yield "foo"

g = ->*
  yield* f!
  yield "bar"

h = g!
h.next!.value + h.next!.value # "foobar"
```

You can create generators by either appending a star `*` to the function keyword, or appending it to the arrow notation. This works with the variety of function arrows we have.

`yield` and `yield*` is simply the same as in JavaScript.
