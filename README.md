# This is Zenith.

A new language extending the features of JavaScript, and compiles to JS, expanded and modified with lots of new shorthands and alternative syntaxes, and borrowing a few concepts from languages such as TypeScript, Python, Java, Flow, F# and Haskell.

## History of the language

The language first started out as a mixture of JS and Python. I used to develop algorithms during my free time using Python at the time but eventually switched to JS and proceeded to translate them by hand in JS, hoping to use them in my web development projects in college.

However, I found out that many of the functions and features which Python had, such as the `random` and `string` libraries, `range()`, tuples and array comprehensions, did not exist in JS. And since these are completely different languages designed for different goals in mind, so I had to painstakingly figure out how to produce exactly the same code in either language, which I resorted to doing in Stack Overflow.

I wanted to create a new way to produce an entire library to bring Python functions to be used in the JS context. But since I have gotten used to web development and hence JS programming a lot, I wanted to create a new language that would get the best of both worlds, as well as combining features which I had liked from different languages, so that seasoned programmers in these languages won't have a steep learning curve.

## Basics

### Sample boilerplate code

Straight outta Python. Just a simple Hello World program.

```js
print('Hello world!')
> Hello world!
```

### Hybrid Typing

Zenith is dynamically typed, just like Python and JS, in order to save time typing. Zenith also has the type identifiers from Java and the C family, which is used for assigning explicit typing standards for certain variables and prevent them from being reassigned a value of a different type.

There are four ways of declaring constants and variables - in the same way as JS:

- `const` is a signal that the identifier won't be reassigned.
- `let` is a signal that the variable may be reassigned, such as a counter in a loop, or a value swap in an algorithm. It also signals that the variable will be used only in the block it's defined in, which is not always the entire containing function.
- `var` is now the weakest signal available when you define a variable in JavaScript. The variable may or may not be reassigned, and the variable may or may not be used for an entire function, or just for the purpose of a block or loop.
- A variable without any of the above prefixes are considered global and therefore will be modified by any function or method.

The variable types are from TypeScript, which are:

- `number`, `string`, `boolean`, `enum`, `void`, `null`, `undefined`/`none`, `any`, `never`, `array`, `object` and `tuple`.

and subtypes as in Java or C#:

- `char` under `string`,
- `byte`, `short`, `int`, `long`, `decimal` and `double` and `float` under `number`.

Here's this in action:

```js
var f: number = 255
typeof f
> number
f = (long) f -> casting
typeof f
> long
```

As in JavaScript, functions, methods, variables and class names can contain Unicode characters, must contain only a single word. They can contain any character, but must not begin or end with the following characters:

| Characters |          What they stand for           |
| :--------: | :------------------------------------: |
| `()[]{}<>` |     Parentheses, brackets & braces     |
|   `. ,`    |          Dot/full stop, comma          |
|   `+-*/`   |  Arithmetic and assignment operators   |
| `&ǀ!?:~^`  | Boolean, logical and bitwise operators |

You can declare and assign multiple variables as in Python:

```js
// Python way
var width, height = 20, 30
width * height
> 600
```

And you can swap and reassign the values of the variables in one line like so:

```js
var width = 20,
  height = 30;
width, (height = height), width;
width, height > 30, 20;
```

### Comments

Comments work the same as in most languages like the C family, Java and JS. No comment on that (pun intended.)

```js
// This is a single-line comment
/* This is a multi-line comment */
/**
 * This is a documentation comment
 * @param | is cool
 */
```

## Literals

### Numbers

Numbers operate in the same way as in JavaScript, however it also supports duodecimal (base 12).

```js
var binary = 0b1010
var octal = 0o12
var decimal = 10
var duodecimal = 0zx // (0123456789xe, 0123456789te or 0123456789ab)
var hexadecimal = 0xa
```

Underscores and appended letters are ignored. Letters can also be used inside literals

```js
64_000 -> 64
640km -> 64
64_000km -> 64000
64e3 -> 64000 // (exponent)
64n -> 64n // (BigInt)
```

There is also a shorthand way of writing numbers (only integers) in bases from 2 to 64. Bases from 10 to 36 use the decimal numerals appended with letters from the English alphabet, and can be written in mixed case, while bases higher than 36 use the Greek alphabet (with four extra symbols), where each non-numeral digit has to be lowercase.

The base 64 digits are: `0123456789abcdefghijklmnopqrstuvwxyzαβγδεζηθικλμνξπρσςτυφχψωϙϛϝϸ`

```js
Digit Chart
[
  '0:0',  '1:1',  '2:2',  '3:3',  '4:4',  '5:5',
  '6:6',  '7:7',  '8:8',  '9:9',  '10:a', '11:b',
  '12:c', '13:d', '14:e', '15:f', '16:g', '17:h',
  '18:i', '19:j', '20:k', '21:l', '22:m', '23:n',
  '24:o', '25:p', '26:q', '27:r', '28:s', '29:t',
  '30:u', '31:v', '32:w', '33:x', '34:y', '35:z',
  '36:α', '37:β', '38:γ', '39:δ', '40:ε', '41:ζ',
  '42:η', '43:θ', '44:ι', '45:κ', '46:λ', '47:μ',
  '48:ν', '49:ξ', '50:π', '51:ρ', '52:σ', '53:ς',
  '54:τ', '55:υ', '56:φ', '57:χ', '58:ψ', '59:ω',
  '60:ϙ', '61:ϛ', '62:ϝ', '63:ϸ'
]
```

```js
1000001b1 -> 65
41b16 -> 65
1tb36 -> 65
15b60 -> 65
11b64 -> 65

akalib36 -> 17743014
13θπγb64 -> 17743014
```

For any base larger than 64, digits are either separated by dots or underscores.

```js
1_3_43_50_38b64 -> 17743014
1.3.43.50.38b64 -> 17743014
```

Numbers can be exponentiated:

```js
1e5 -> 100000
1.3e4 -> 13000
2.3e4 ->
```

Similar to algebra, a number before a variable multiples that variable.

```js
3'30' == 3 * '30' == '303030'
var k = 3; 3k == 3*3 == 9
```

### Booleans, null, void, undefined and other type aliases

See the correspondence table below.

|             Alias              | Compilation value |
| :----------------------------: | :---------------: |
|      `true`, `yes`, `on`       |      `true`       |
|      `false`, `no`, `off`      |      `true`       |
|   `void` (compiles to none)    |    `undefined`    |
| `undefined` (can be redefined) |    `undefined`    |
|         `null`, `none`         |      `null`       |
|           `infinity`           |    `Infinity`     |
|             `nan`              |       `NaN`       |

### Strings

Zenith can also manipulate strings, which can be expressed in several ways. They can be enclosed in single quotes `'...'` (evaluated by default in the console) or double quotes `"..."`. The backslash `\` is used to escape quotes, other characters and itself.

```js
// single quotes
"spam eggs" == "spam eggs";
// use \' to escape the single quote or use double quotes instead
"doesn't" == "doesn't";
// Why not both?
'"Yes," they said.' == '"Yes," they said.';
'"Isn\'t," they said.' == '"Isn\'t", they said.';
```

This is a list of escape characters.

- Horizontal tab: `\t`
- Vertical tab: `\v`
- Null char: `\0`
- Backspace: `\b`
- Form feed: `\f`
- Newline: `\n`
- Carriage return: `\r`
- Single quote: `\'`
- Double quote: `\"`
- Backslash: `\\`
- Unicode characters:`\4-digit codepoint` or `\{5/6-digit codepoint}`, such as `\ud83d`, or `\u{1f680}`

```js
> 'hell\u{6f}'
'hello'
```

If you don't want characters prefaced by \ to be interpreted as special characters, you can use raw strings by encasing your string in backticks (``), like this.

```js
> print(`Hello,
world!`)
'Hello,\nworld!'
> print("Hello," + '\nworld!')
'Hello,\nworld!'
```

Two or more strings next to each other are automatically concatenated. Strings can span multiple lines, however are read as one continuous string when there is a backslash at the end of a line.

```js
> 'This is already boring. \
Can I take a nap?'
'This is already boring. Can I take a nap?'
```

Strings can be concatenated with the `+` operator, and repeated with `*`:

```js
> 'un' * 3 + 'ium'
'unununium'
```

You can merge two strings encased in different quotes: `'Hello ' + "world!" == 'Hello world!'`
If you want to concatenate string variables or a variable and a string, use `+`:

```js
> var zen = 'Zen'
> zen + 'ith'
'Zenith'
> var zen = 'Zen'
> zen 'ith'
SyntaxError
```

String interpolation is a way to construct a new string from a mix of constants, variables, literals, and expressions by including their values inside a string literal. All three types of strings, including single and double quoted strings can be interpolated. The syntax for interpolation can be `#{}`, `#[]`, `[]#`, `#[]#` or `${}`.

```js
var m = 3,
  message = "#{m} times 2.5 is #{m * 2.5}";
("3 times 2.5 is 7.5");
```

Characters and strings are not differentiated. Strings and arrays can be indexed as in JS. Operating with strings and arrays are much like Python, including the use of negative indices and string/array slicing or splicing.

```js
> var word = 'Zenith'
> word[0] == word[-6] == 'Z'
> word[5] == word[-1] == 'h'
```

Characters from position 0 (included) to 2 (excluded):

```js
> word[0:2]
'Ze'
```

Characters from position 2 (included) to 5 (excluded):

```js
> word[2:5]
'nit'
```

This is so that `word[:n] + word[n:] == word`

```js
> word[:2] + word[2:]
'Zenith'
> word[:4] + word[4:]
'Zenith'
```

Strings cannot be changed - they are immutable. Therefore, assigning to an indexed position in the string results in an error. If you need a different string, you should create a new one:

```js
> var nadir = 'Nadir' + word[1:]
> nadir
'Nadirenith'
```

The built in property `.len`, `.size` or `.length` returns the length of a string, as well as their equivalent functions `len()`, `size()` or `length()`:

```js
> 'supercalifragilisticexpialidocious'.length
34
```

### Arrays

Arrays work in a similar fashion in Javascript and as lists in Python.

```js
squares = [1, 4, 9, 16, 25] > squares[(1, 4, 9, 16, 25)];
```

Like strings (and all other built-in sequence types), arrays can be indexed and sliced:

```js
> squares[0] // Indexing returns the item
1
> squares[-1]
25
> squares[-3:] // Slicing returns a new array
[9, 16, 25]
```

Arrays can be dequed, and a variety of methods can be used. When removing value(s) from the array, the method would return the removed value(s). The `add()` method functions like `push()` or `append()` when one argument is passed.

|          Method          | Arguments |                       Description                        |
| :----------------------: | :-------: | :------------------------------------------------------: |
|   `push()`,`append()`    |     1     |       appends a new value to the end of the array        |
|         `pop()`          |     0     |        removes the value at the end of the array         |
| `unshift()`, `prepend()` |     1     |        prepends a value to the start of the array        |
|        `shift()`         |     0     |       removes the value at the start of the array        |
|         `add()`          |   1, 2    |            adds an value at a specified index            |
|        `delete()`        |     1     |     deletes and returns a value at a specified index     |
|        `remove()`        |     1     |    deletes and returns the first instance of a value     |
|      `removeLast()`      |     1     |     deletes and returns the last instance of a value     |
|      `removeAll()`       | 1 or more | deletes and returns all instances of a value as an array |
|    `get()`, `index()`    |     1     |          returns the value at a specified index          |
|   `set()`,`replace()`    |     2     |        replaces a value at its index with another        |
|   `clear()`, `empty()`   |     0     |                     empties an array                     |
|         `fill()`         | 1 or more |        overrides an array with the inside values         |
|      `replaceAll()`      |     2     |      replaces all values in the array with another       |
|       `reverse()`        |     0     |               reverses the array in place                |
|       `shuffle()`        |     0     |               shuffles the array in place                |

Many of the built-in array functions in JavaScript remain unchanged in Zenith.

### Lists

Lists function in the same way as tuples in Python (encased in parentheses `()`), and hence, they are immutable.

```js
> squares = (1, 4, 9, 16, 25)
```

## Operators

In most other languages like JavaScript, we use the `=` sign to assign a value to a constant or variable. All these signs can be placed right before the equal sign to reassign it to the variable. Each operator described below also has a keyword.

```js
var val = 4096
val #= 2 // val = val # 2
val += 2 // val = val + 2
> 2050
```

### Numeric Operations

Rounding functions are affected by the base/radix which the number is in. For instance, the hexadecimal value `0x1.7` is rounded down to `0x1.0`.

| Operator |    Type    | Keyword  |                     Description                      |            Example            |
| :------: | :--------: | :------: | :--------------------------------------------------: | :---------------------------: |
|   `+`    | arithmetic |  `plus`  |                       Addition                       |          `1 + 1 = 2`          |
|   `-`    | arithmetic | `minus`  |                     Subtraction                      |          `2 - 1 = 1`          |
|   `*`    | arithmetic | `times`  |                    Multiplication                    |          `3 * 3 = 9`          |
|   `/`    | arithmetic | `divide` |                       Division                       |         `9 / 5 = 1.8`         |
|   `#`    | arithmetic | `fldiv`  |                    Floor division                    |          `7 # 5 = 1`          |
|   `/:`   | arithmetic | `rndiv`  |              _Division with rounding_\*              |   `7 #: 5 = 1, 8 /: 5 = 2`    |
|   `/!`   | arithmetic | `cldiv`  |                   Ceiling division                   |         `7 /! 5 = 2`          |
|   `+.`   | arithmetic |  `pluf`  |               Floating point addition                |        `1 +. 1 = 2.0`         |
|   `-.`   | arithmetic |  `minf`  |              Floating point subtraction              |        `2 -. 1 = 1.0`         |
|   `*.`   | arithmetic |  `timf`  |            Floating point multiplication             |        `3 *. 3 = 9.0`         |
|   `%`    | arithmetic |  `rem`   | Modulus operator - returns remainder of two operands |         `13 % 3 = 1`          |
|   `%/`   | arithmetic | `flmod`  |                    Floor modulus                     |       `12.5 %/ 0.3 = 0`       |
|   `%%`   | arithmetic |  `mod`   |                        Modulo                        |  `a %% b = (a % b + b) % b`   |
|   `++`   | arithmetic |  `incr`  |                    Increment by 1                    |             `a++`             |
|   `--`   | arithmetic |  `decr`  |                    Decrement by 1                    |             `a--`             |
|  `+++`   | arithmetic |  `incr`  |                    Increment by a                    |            `a+++`             |
|  `---`   | arithmetic |  `decr`  |                    Decrement by a                    |            `a---`             |
|   `**`   | arithmetic |  `pow`   |                    Power function                    | `2 ** 3 = 8, 10 ** -1 = 0.1`  |
|  `***`   | arithmetic |  `exp`   |            Scientific shorthand notation             | `2e4 = 2 *** 4 = 2 * 10 ** 4` |
|   `~~`   | arithmetic |  `flr`   |                    Floor function                    |          `~~3.2 = 3`          |
|   `=~`   | arithmetic |  `rnd`   |                  Rounding function                   |    `=~3.4 = 3, =~3.5 = 4`     |
|   `!~`   | arithmetic |  `ceil`  |                   Ceiling function                   |          `!~3.4 = 4`          |
|   `</`   | arithmetic |  `sqrt`  |                    Square root\*                     |           `<*4 = 2`           |
|   `/>`   | arithmetic |  `curt`  |                     Cube root\*                      |           `*>8 = 2`           |
# Zenith

**Zenith** is how (I think) JavaScript should be like. The golden rule is, if it looks like JavaScript, it should work _with_ and _like_ JavaScript, and compiles to short, sweet and readable JavaScript code. So it should be seen as an attempt to expose and extend the good parts of JavaScript in a simple way, powered by the increasingly rampant JavaScript ecosystem and its many packages and modules.

Zenith is a new programming language designed to combat JavaScript's:

- inexplicable runtime semantics and cost
- unexpected runtime errors
- disorganized syntactic features
- complete lack of a robust and sturdy type system
- lack of a "standard library" (that is, its own modules which one can import)
- hard interoperability with existing JS code

It is a completely new programming language by itself, so you can write more sophisticated code with tons of syntactic sugar and powerful advanced features. The language borrows and blends elements and concepts from different programming languages&mdash;reactive, object-oriented and functional programming.

Inspired by: JavaScript, TypeScript, Ruby, Python, F#, Nim, Haskell, LiveScript, CoffeeScript, PHP, Rust, Go, Swift, Kotlin, C++, C#, Objective-C, Java, Go, Dart, Haxe, Perl, ReScript/Reason, and Mint.

Alright, let's begin.

---

## Differences from TypeScript

TypeScript should be respected very much given that it's a positive force in the JavaScript ecosystem. Zenith shares some of the same goals as TypeScript. TypeScript's (admittedly noble) goal is to cover the entire JavaScript feature set and more, but Azurite is **not** a superset of JavaScript nor TypeScript, but rather its own programming language that descends from JavaScript.

Consequently, TypeScript's type system is necessarily complex, pitfalls-ridden, potentially requires tweaking, sometimes slow, and requires quite a bit of noisy annotations that often feel like manual bookkeeping rather than clear documentation. In contrast, ReScript's type system:

- Is deliberately curated to be a simple subset most folks will have an easier time to use.
- Has no pitfalls, aka the type system is "sound" (the types will always be correct). Or if you're willing to stop type-checking a variable, when using a third-party library, you can simply use `any`.
- Doesn't need type annotations. Annotate as much or as little as you'd like. The types are inferred by the language.

### Readable Output & Great Interop

Unreadable JavaScript code generated from other compiled-to-js languages makes it so that it could be, practically speaking:

ReScript's JS output is very readable. This is especially important while learning, where users might want to understand how the code's compiled, and to audit for bugs.

This characteristic, combined with a fully-featured JS interop system, allows ReScript code to be inserted into an existing JavaScript codebase almost unnoticed.

## Preservation of Code Structure

ReScript maps one source file to one JavaScript output file. This eases the integration of existing tools such as bundlers and test runners. You can even start writing a single file without much change your build setup. Each file's code structure is approximately preserved, too.

## An Informal Introduction

Zenith provides its own versions of all JavaScript and TypeScript types, including `int` and `float` as JavaScript `number` and `bigint`, `bool` for `boolean` and `str` as `string`.

In addition to familiar types, Swift introduces advanced types not found in JavaScript, such as tuples. Tuples enable you to create and pass around groupings of values. You can use a tuple to return multiple values from a function as a single compound value.

First, the basics. Like many programming languages from Swift to Scala to Rust to TypeScript, Zenith uses significant use of curly braces to delimit blocks of code. So it looks more like JavaScript.

As for semicolons, you don't _actually_ need to use them unless you want to fit multiple expressions onto a single line. Commas are also entirely optional in compound data types, when each property is listed on its own line. The only compulsory thing you need is the outer brackets or braces.

As for function calls, they do require parentheses but there are also other ways you can write them.

```coffee
print(sys.inspect(e)) // This is okay
print (sys.inspect e) // This is also fine
print sys.inspect e   // Nice
```

You can also chain methods without parentheses by spacing them out. Note the function syntax on the right.

```coffee
[1, 2, 3, 4, 5].slice 10 * 3 .filter { $ % 3 == 0 }
[1, 2, 3, 4, 5].slice(10 * 3).filter((i) => i % 3 == 0)
```

This tutorial introduces various features of the Zenith language through examples, beginning with simple expressions, statements and data types, through functions and modules, and finally touching upon advanced concepts like errors and user-defined classes.

Zenith has a lot of keywords, most of which you are familiar with. Let's go through them in a bit of detail here:

```coffee
// Control flow
var let const declare define infix
if unless then elif elun else
for own in of when break continue goto
while until loop repeat pass
with skip at from to til by
switch case label other fall
try throw catch raise except finally
do begin end start stop return yield
import export default as

// Constants
true yes on | false no off
null | undef | infin | nan
document | event | navigator | performance | screen | window
console | module | native | global | require | exports
args | this | it | ctor | debugger

// Data types and declarations
any | never | unknown | auto
num | int | float | dec | frac | comp
str | char | bool | sym
tuple | arr | rec | obj | set | map | weakset | weakmap | regex | date
func | gen
class | type | enum | interface | struct | namespace | package

// Do not use these keywords at all!
byte | ushort | uint | ulong | sbyte | short | long | double | bigint | bigdeci

// Built-in data types
Array ArrayBuffer Atomics BigInt BigInt64Array BigUint64Array Boolean DataView Date Float32Array Float64Array Function Generator GeneratorFunction Int8Array Int16Array Int32Array Intl Map Number Object Proxy Reflect RegExp Set SharedArrayBuffer SIMD String Symbol TypedArray Uint8Array Uint16Array Uint32Array Uint8ClampedArray WeakMap WeakSet Math JSON

// Operators
super len size typeof instof delete void
and nand or nor xor xnor not
lt gt lte gte leg is isnt eq ne sim diff

// Built-in console statements
print puts echo assert debug info warn error

// LINQ syntax
select join group add remove | alias | order asc desc | where into | get set | async await

// Access modifiers (are defined when they are)
ext impl
pub pvt prot read fin mut
defer refer stat dyn check uncheck
abst over dele lock sync
part sealed trans vol unsafe
```

There are really only two types of comments: `// line comments` and `/* block comments */`. Both can be nested. You can also use the familiar `/** JSDoc comment syntax */` (which is basically just a block comment with an extra asterisk) if you like as well.

```coffee
/* hooray for nested comments */
/**
 * @param hooray for nested comments
 */
```

### Variables

Constants and variables must be declared before they're used. You declare constants with the `const` keyword and variables with the `let` keyword. You can also declare non-local variables with the `var` keyword. The value of a constant can't be changed once it's set, whereas a variable can be set to a different value in the future.

You can declare `let` and `var` variables with a value. They can be seen and referenced by code that comes after them.

```coffee
let i;
var j;
for const i in [0::len array] {}
```

By default, all variables when declared with the `=` assignment operator are automatically assigned a `let` declaration.

Constants are always initialized with `:=`.

```coffee
i = 3;  // let i = 3
j .= 4; // var j = 4
k := 5; // const k = 5
```

You can declare non-local variables with `var` using `.=`, and you are required to use `.=` all the time whenever you modify the same variable in upper scopes, such as outside functions and class methods.

```coffee
x .= 10 // declared as `var x`
do { x = 5 } // 10 => creates a new variable called x
do { x .= 2 } // 2 => modifies `var x`
```

Once you've declared a constant or variable of a certain type, you can't declare it again with the same name, or change it to store values of a different type. Nor can you change a constant into a variable or vice versa.

You can change the value of an existing variable to another value, as long as it is of the same type (though you can reuse a variable name when you initialize it to be `any`. In this example, the value of friendlyWelcome is changed from "Hello!" to "Bonjour!":

```coffee
friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

Unlike a variable, the value of a constant can’t be changed after it’s set. Attempting to do so is reported as an error when your code is compiled:

```coffee
languageName := "Swift"
languageName = "Swift++"
// This is a compile-time error: languageName cannot be changed.
```

Constant and variable names can contain almost any character, including Unicode characters:

```coffee
π = 3.14159
你好 = "你好世界"
🐶🐮 = "dogcow"
```

Constant and variable names can't contain whitespace characters, mathematical symbols, arrows, private-use Unicode scalar values, or line- and box-drawing characters. Nor can they begin with a number, although numbers may be included elsewhere within the name.

> Note: If you need to give a constant or variable the same name as a reserved Zenith keyword, surround the keyword with a string literal and prefix a `$` when using it as a name. However, avoid using keywords as names unless you have absolutely no choice.

Within expressions, you can change and assign variables directly. This is because a value assigned will return its value backward.

The expression `i += 2` is shorthand for `i = i + 2`. Effectively, the addition and the assignment are combined into one operator that performs both tasks at the same time.

```coffee
// In this example, both i and j are declared with the value 3
i = j := 3; i += 2 // i == 5
j // j == 3
```

## Data Types

For programs to be useful, we need to be able to work with some of the simplest units of data: numbers, strings, structures, boolean values, and the like. In Zenith, we support the same types as you would expect in JavaScript, plus a few more thrown in to help things along.

This declaration is named `count`, was declared with `let`, is of type `int`, and has a value of `42`. Its type was inferred, we did not explicitly write down that it was an `int`.

```coffee
count = 42;
```

Types can be explicitly added with an annotation, that goes right before the variable name.

```coffee
let int i;
var int j;
```

Because `count` has a type the compiler knows what we are and are not allowed to do with its value:

```coffee
// Allowed: addition
nextCount = count + 1

// Error: count is not of the type any()|any[]
x = count.map => 3
```

### Casting

Sometimes we want to convert a type of a value into something we already know. Casting performs no special checking or restructuring of data. It has no runtime impact and is used purely by the compiler. Zenith assumes that you have performed any special checks you need. Type casting has three forms.

One is the `as`-syntax:

```coffee
unknown someValue = "this is a string";
int strLength = len (someValue as str);
```

Another is the constructor function syntax:

```coffee
unknown someValue = "this is a string";
int strLength = len str(someValue);
```

The other version is the "angle-bracket" syntax:

```coffee
unknown someValue = "this is a string";
int strLength = len <str>someValue;
```

The two samples are equivalent. Using one over the other is mostly a choice of preference; however, when using JSX, only `as`-style and constructor assertions are allowed.

### Boolean

A boolean is either one of two values, `true` and `false`, and has the type `bool`. `true` can have the aliases `yes` and `on` while `false` can have the aliases `no` and `off`.

```coffee
bool isDone := false;
```

The regular boolean operations have been preserved:

- logical operators `!`, `&&`, `||`, and their infix aliases `not`, `and`, `or`;
- comparison operators `<`, `>`, `<=`, `>=`;

```coffee
!true // false
true && false // false
true || false // true
```

We do provide a few more, such as the `^^` or `xor` logical operator, which returns `true` as long as both operands are distinct. It functions roughly same way as `!==`. <small>Note any operators that doesn't have a JavaScript counterpart automatically compile to private functions.</small>

```coffee
xor = (a, b) => !a !== !b && (a || b);
```

```coffee
false ^^ true  // true
false ^^ false // false
1 ^^ 0         // 1
1 ^^ 1         // false
```

`&&`, `||` and `^^`, and their infix forms `and`, `or` and `xor`, have their own inverses: `!&`/`nand`, `!|`/`nor` and `!^`/`xnor`.

`==` and `!=` in Zenith compile to `===` and `!==` in JavaScript. If you really want to use JavaScript's `==` and `!=`, use the _fuzzy equality_ operators `=~` and `!~` instead.

### Numbers

As in JavaScript, all numbers are either floating point values or (big) integers. These floating point numbers get the type `float`, while integers simply get `int`.

The integer numbers (e.g. `2`, `4`, `20`) have type `int`, the ones with a fractional part or with a dot `.` (e.g. `5.0`, `1.6`) have type `float`. `int`s also can end in `n`, of which explicitly tell the compiler it is a `bigint`.

```coffee
dec := 6.;
hex := 0xf00d;
binary := 0b1010;
dctal := 0o744;
```

The basic operations `+`, `-`, `*` and `/` work the same way as in JS, and you can use parentheses `()` in grouping your expressions:

```coffee
2 + 2 // 4
50 - 5 * 6 // 20
(50 - 5 * 6) / 4 // 5.0
8 / 5 // 1.6
```

Regular division with `/` will evaluate to a `float`, but floor division with `~/` will return `int`. Operators with mixed type operands convert the evaluated result to `float`:

```coffee
4 * 3.75 - 1;
```

```coffee
17 / 3; // 5.666666666666667
17 ~/ 3; // 5
17 % 3; // 2
5 * 3 + 2; // 17
```

Bitwise operations such as `&`, `|` and `^` (and their inverses `~&`, `~|`, `~^`), unary `~` and bitwise shift operators `<<`, `>>` and `>>>` will evaluate into `int`.

```coffee
5 & 1; // 1
5 | 1; // 5
5 ^ 1; // 4
~5; // 10
5 << 1; // 10
5 >> 1; // 2
5 >>> 1; // 2
```

`%%` provides dividend-dependent modulo:

```coffee
-7 % 5 == -2; // The remainder of 7 / 5
-7 %% 5 == 3; // n %% 5 is always between 0 and 4
```

Radix literals can be created using prefixes `0x`, `0o`, `0b`. Literals can be broken up using the `_` character which will be ignored:

```coffee
decimal = 11256099;
hexadecimal = 0xABC123;
octal = 0o52740443;
binary = 0b101010111100;
billion = 1_000_000_000;
```

The minimum/maximum operators `<?` and `>?`, which return the smaller or larger of the two operands.

```coffee
3 <? 10; // 3
3 >? 10; // 10
```

PHP's "spaceship" operator `<=>`, returns either `1`, `0` or `-1` depending on whether the number on the left isgreater than, equal to or lesser than the right.

```js
leg = (a, b) => (a < b ? -1 : a > b ? 1 : 0);
```

```coffee
3 <=> 1; // 1
1 <=> 3; // -1
2 <=> 2; // 0
```

Besides the very common `int` and `float`, there are three more types `frac`, `deci` and `comp` types refer to arbitrary-precision fractional, rational and complex numbers respectively.

- Fractions, withr `frac` end in `f`, and can be of the form:
  - `(x,y)f`, where `x` is the numerator and `y` is the denominator.
  - `x.k(d)?f`, where `x` is the integer part, `k` is the non-repeating fractional part and `d` is the repeating fractional part.
- `deci`, whether with a `.` or not, always end in `m`. Alternatively it can also be expressed as a mathematical formula before the `m`, such as `(5**(1/2))n`.
- `comp` of the form `(k,x)j`, where `k` is the real part and `x` is the imaginary part.

`num` is a superset of `int`, `float`, `frac`, `deci`, and `comp`, and for expressions with mixed-type operands, any type lower in the hierarchy is always coerced to a higher superset type.

```coffee
i = 1; // int
i += 1.; // float
i += 1f; // frac
i += 1m; // deci
i += (1,0)j; // comp
```

Bases 2 to 64 can be used, as long as they use these digits and are surrounded in string literals and suffixed with the base: `0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$&`.

```coffee
i = '105'6; // 41
```

Note:

- All `_` and leading `0`s are ignored
- Any numeric literal not ending in `f`, `j`, `m` or `n` will throw an error.

```coffee
040; // 40
04k; // ERROR: Literal shound end in digits or either of f, j, m or n
```

You can type-cast with the use of constructor functions, similar to how `Number()`, `String()` and `Boolean()` usually work.

```coffee
int rounded = int(round(1.3f)); // 1
```

### Strings

As in other languages, we use the type `str` (not `string`) to refer to these textual datatypes. Just like JavaScript, TypeScript also uses double quotes (`"`) or single quotes (`'`) to surround string data.

```coffee
str color = 'blue';
color = 'red';
```

Template strings, of the form `""`, which can span multiple lines and have embedded variables and expressions. These strings are surrounded by the double quote (`"`) character. Embedded variables are of the form `#var`, and interpolated expressions are of the form `#{ expr }`. The difference between `"` and `'`-delimited strings can be summed up in this short table below.

|                             | `'` | `"` |
| --------------------------- | --- | --- |
| Single-line evaluation      | Yes | No  |
| Interpolating and embedding | No  | Yes |
| `\`-escaping (except `#`)   | Yes | No  |
| Proper Unicode handling     | No  | Yes |

```coffee
str fullName = "Bob Bobbington";
int age = 37;
str sentence = "Hello, my name is #fullName.
I'll be #{age + 1} years old next month.";
```

Characters, of type `char`, enclosed in ` `` `, are really just strings of length 1. They don't do anything, really, except they are compatible with `int` operations and can be concatenated to form strings. So, strings basically are arrays of characters.

```coffee
char a = `a`;
```

Strings can be replaced with either a substring or through pattern matching, where the right operand is passed into the arguments of the [`String.replace()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) function.

Strings can be split into tuples of strings or characters with `/`, use casting into `char[]()` or `as char[]` if you want to convert the split result into individual characters. Spreading `[...string]` converts the string into an array of `char`s.

```coffee
str s = 'Hello';

s = 'Hello' - `l`; // 'Heo'
s = 'Hello' - (/llo$/, 'lp me'); // 'Help me'

str[] t = s / 1; // ['H', 'e', 'l', 'l', 'o']

char[] c = char[](s / 1); // [`h`, `e`, `l`, `l`, `o`]

// Alternatively:
char[] c = [...s]
```

Use `%` to join strings back, where the right operand is the delimiter. This operation will convert all non-strings (including `char`s) into strings.

```coffee
strArr = ['H', 'e', `l`, 'l', 'o']
strArr = strArr % '' //  'Hello'
```

### Arrays and Tuples

For array types, you can annotate in one of two ways: the type of the element followed by `[]` to denote an array of that element type. Note arrays work the same way as in JavaScript and are **mutable** in the sense that they can be modified directly by invoking methods such as `push`, `pop`, `shift`, `unshift` and `splice` on it.

```coffee
int[] myList = [1, 2, 3];
myList[1] = 300
myList[1, 3] = [300, 400]; // 300, 400
```

Same thing for tuples; the type followed by `()`. However, they are **immutable** and each operation you perform on it would return a new tuple.

```coffee
int() myTuple = (1, 2, 3);
myTuple[1] = 2 // ERROR: tuple elements cannot be assigned directly.
```

Use the unary `len` operator to retrieve the length of a(n) string/array/tuple:

```coffee
arrLen = len [1, 2, 3, 4, 5] // 5
```

Much like JavaScript objects and maps, arrays and tuples do have keys (their **numeric** index) and values (which are the values you see on the screen), You can use `in` to test for value presence, and `of` to test for key presence.

```coffee
'3' in '12345' // true
3 of '12345' // true
'3' of '12345' // false

'3' in (1, 2, '3', 4, 5) // true
3 of (1, 2, 3, 4, 5) // true
'3' of (1, 2, 3, 4, 5) // false
```

Strings, arrays and tuples can be indexed, concatenated, repeated, sliced and spliced, much the same way as you do with Python. Indices work `%%` the length of the array and are 0-indexed, so given a string/tuple/array `seq` of length `5`, `... seq[5] == seq[0] == seq[-4] == seq[-9] ...`.

Slicing and splicing allow you to retrieve and override elements in tuples and arrays, or individual `char`s in strings. Take note of the slicing syntax:

| Operator         | Meaning                         |
| ---------------- | ------------------------------- |
| `$`              | length of array                 |
| `a,b`            | `a` and `b` only                |
| `,b,`            | implicit `0`: `0,b,0`           |
| `a,b:c`          | `a`, then from `b` to `c`       |
| `a::b`           | from `a` to `b`, inclusive      |
| `a:>b` or `a:<b` | ... excluding `b`               |
| `a<:b` or `a>:b` | ... excluding `a`               |
| `a<>b` or `a><b` | ... exclusive                   |
| `a::b:c`         | ... inclusive, stepping by `c`  |
| `a::b:c:d`       | ... stepping by `c`, then `d`\* |

\* if `c + d > 0 && a > b || c + d < 0 && a < b`, then `c = -c` and `d = -d`.

```coffee
str c = 'hello'; // Slicing
s = c[1]; // e
s = c[1,2]; // el (specific indices)
s = c[:>$]; // hello (string cloning)
s = c[$>:]; // olleh (specific indices)

any() t = (1, 2, 3); // Splicing
t = t + (4, 5); // (1, 2, 3, 4, 5)
t = t * 2; // (1, 2, 3, 4, 5, 1, 2, 3, 4, 5)
t = (1, 2, 3, 4, 5)[$>:];   // (5, 4, 3, 2, 1)
t = (1, 2, 3, 4, 5)[-1='5']; // (1, 2, 3, 4, '5')

any[] a = [1, 2] + [3, 4]; // Concatenation
[x, , ...z] = a // Destructuring
print(x, z); // 1, [3, 4]
$a = [...a, ...a, 4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
$a = a * 2 + [4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
```

Array or tuple types allow you to express a fixed number of elements whose types are known, but need not be the same. For example, you may want to represent a value as a pair of a `str` and `int`.

```coffee
let [str, int] x;

// Initialize it
x = ["hello", 10]; // OK

// Initialize it incorrectly
x = [10, "hello"];
// ERROR: type [int, str] is not assignable to type [str, int]
```

### Objects

\#TODO

### Sets

\#TODO

### Maps

\#TODO

### Other Types

#### Any

To opt-out of type checking when working with existing JS libraries, we label these values with the `any` type:

```coffee
def (str key) => any getValue;
// OK, return value of 'getValue' is not checked
str $str = getValue("myString");
```

The `any` will continue to propagate through your objects:

```coffee
any looselyTyped = {};
let d = looselyTyped.a.b.c.d;
//  ^ = let d: any
```

After all, remember that all the convenience of `any` comes at the cost of losing type safety.

#### Unknown

We may need to describe the type of variables that we do not know when we are writing an application. In these cases, we want to provide a type that tells the compiler and future readers that this variable could be anything, so we give it the `unknown` type.

```coffee
unknown notSure = 4;
notSure = "maybe a string instead";

// OK, definitely a boolean
notSure = false;
```

Also note `def` here is the equivalent of `declare` in TypeScript.

```coffee
def unknown maybe;
// 'maybe' could be a string, object, boolean, undefined, or other types
int anInt := maybe;
// ERROR: Type 'unknown' is not assignable to type 'number'.
```

```coffee
if (typeof maybe == 'bool') {
  // Zenith knows that maybe is a boolean now
  bool aBoolean := maybe;
  // So, it cannot be a string
  str aString := maybe;
// ERROR: Type 'bool' is not assignable to type 'str'.
}
```

```coffee
if (typeof maybe == 'string') {
  // Zenith knows that maybe is a string
  bool aBoolean := maybe;
  // So, it cannot be a boolean
  str aString := maybe;
  // ERROR: Type 'str' is not assignable to type 'bool'.
}
```

Unlike `unknown`, variables of type `any` allow you to access arbitrary properties, even ones that don’t exist. These properties include functions and Zenith will not check their existence or type:

```coffee
any looselyTyped := 4;
looselyTyped.ifItExists(); // OK, ifItExists might exist at runtime
looselyTyped.toFixed(); // OK, toFixed exists (but the compiler doesn't check)

unknown strictlyTyped := 4;
strictlyTyped.toFixed(); // ERROR: Object is of type 'unknown'.
```

#### Void, Null and Undefined

`void` is a little like the opposite of `any`: the absence of having any type at all. `void == null | undef`.

```coffee
void warnUser() {
  print "This is my warning message";
}
```

Declaring variables of type `void` is not useful because you can only assign `null` or `undef` to them:

```coffee
void unusable = undef;
unusable = null;
```

In TypeScript, both `undef` and `null` actually have their **own** types, but they’re not extremely useful on their own. They are considered literal types

```coffee
// Not much else we can assign to these variables!
undef u = undef;
null n = null;
```

#### Other

`other` is a type that represents the **non-primitive** type, i.e. anything that is not `int`, `float`, `str`, `char`, `bool`, `sym`, `void`, `null`, or `undef`.

With object type, APIs like Object.create can be better represented. For example:

```coffee
def func create(other | null) void;

// OK
create({ prop: 0 });
create(null);
create(undef); // Remember, `undef` is not a subtype of `null`
// ERROR: Argument of type 'undef' is not assignable to parameter of type 'other | null'.

create(42);
// ERROR: Argument of type '42' is not assignable to parameter of type 'other | null'.
create("string");
// ERROR: Argument of type '"string"' is not assignable to parameter of type 'other | null'.
create(false);
```

#### Never

The `never` type represents the type of values that **never** occur. For instance, `never` is the return type for a `=>` that always throws an error or one that never returns. Variables also acquire the type `never` when narrowed by any type guards that can never be true.

The `never` type is a subtype of, and assignable to, every type; however, no type is a subtype of, or assignable to, `never` (except never itself). Even `any` isn’t assignable to `never`.

Some examples of functions returning `never`:

```coffee
// Function returning `never` must not have a reachable end point
error (message) never {
  throw Error(message);
}

infiniteLoop() never {
  loop {}
}

// Inferred return type is `never`
fail() {
  error "Something failed";
}
```

### Primitive Constructors

Primitive constructors `Int`, `Float`, `String`, `Char`, `Boolean`, `Symbol`, or `Other` are the same as the lowercase versions recommended above. They almost never should be used. This is not Java.

```coffee
String reverse(String s) => (s / 1).rev() % '';
reverse("hello world");
```

Instead, use the lowercase types.

```coffee
str reverse(str s) => s[#:>0];
reverse("hello world");
```

## Types

Type annotations can appear almost anywhere. They are not often necessary due to type inference, but they can be helpful to confirm your own understanding of the program's types.

`int` and `str` are annotations used throughout these examples.

```coffee
int $5:  = 5;
$9 = (int $5) + (int $4 = 4);
add = (int x, int y) int => x + y;
drawCircle = (int radius) str => "hi";
```

### Aliases

Aliases can be defined for types. This is helpful to attach meaning to simple types and when working with complex types that become long to write down.

```coffee
type seconds = int;
type timeInterval = (seconds, seconds);
```

Using the alias `seconds` it is clear how the sleep function works. If int were used it might not be obvious:

```coffee
sleep = (timeInterval seconds) => { ... }
```

Type aliases are required in some cases, such as working with interfaces, intersections and unions.

## Type Parameters

Types can accept type parameters, which are similar to generics in other languages. Parameterized types are useful when defining structures that work with many types of values. Having a single `arr` type with an argument that can be `int`, `float`, or `str`, is better than having three separate `intArray`, `floatArray`, and `strArray` types.

Parameters are prefixed with a single `#` when defining the type:

```coffee
type arr<#item> = ...
```

When using this type as an annotation the parameter can be filled in with a concrete type:

```coffee
arr<int> x = [1, 2, 3];
arr<str> y = ["one", "two", "three"];
```

Types can have multiple parameters and be nested:

```coffee
type pair<#a, #b> = (#a, #b);

pair(int, str) x = (1, "one");
pair(str, int[]) y = ("123", [1, 2, 3]);
```

Note:

- It is common convention for type parameters to be named `#a`, `#b`, `#c`, etc.
- Type parameters can still be inferred!

### Union Types

As you model more types you find yourself looking for tools which let you compose or combine existing types instead of creating them from scratch. Intersection and Union types are one of the ways in which you can compose types.

A union type describes a value that can be one of several types. We use the vertical bar (`|`) to separate each type, so `int | str | bool` is the type of a value that can be an `int`, a `str` or a `bool`. As you have already heard,

```coffee
type void = null | undef
```

If we have a value that is a union type, we can only access members that are common to all types in the union.

```coffee
interface Bird = { void fly(); void layEggs(); }
interface Fish = { void swim(); void layEggs(); }
def func getSmallPet() Fish | Bird;

pet = getSmallPet();
pet.layEggs(); // will not throw since this property is common

pet.swim(); // will throw
```

Intersection types are closely related to union types, but they are used very differently. An intersection type combines multiple types into one. For example, `Person & Serializable & Loggable` is a type which is all of `Person` and `Serializable` and `Loggable`.

```coffee
interface ErrorHandling {
  bool success;
  { message: str } error?;
}

interface ArtworksData {
  { str title }[] artworks;
}

interface ArtistsData {
  { str name }[] artists;
}

// These interfaces are composed to have
// consistent error handling, and their own data.
type ArtworksResponse = ArtworksData & ErrorHandling;
type ArtistsResponse = ArtistsData & ErrorHandling;
```

### Literal and Conditional Types

A literal is a more concrete sub-type of a collective type. What this means is that `"Hello World"` is a `str`, but a `str` is not `"Hello World"` inside the type system.

When you declare a variable with `.=` or `=`, you are telling the compiler that there is a chance that this variable will change its contents. In contrast, using `:=` to declare a variable will tell the compiler that this object will never change.

The process of going from an infinite number of potential cases to a smaller, finite number of potential case is called narrowing.

```coffee
// We're making a guarantee that this variable
// helloWorld will never change, by using const.

// So, the type of helloWorld is "Hello World", not str
helloWorld := "Hello World";

// On the other hand, a let can change, and so the compiler declares it a string
hiWorld .= "Hi World";
```

#### Strings

In practice string literal types combine nicely with unions, type guards, and type aliases. You can use these features together to get enum-like behavior with strings.

```coffee
type Position = 'before' | 'after';
```

You can pass any of the three allowed strings, but any other string will give the error

```
Argument of type '"ok"' is not assignable to parameter of type "'before' | 'after'"
```

Same thing for characters.

#### Numbers

Numeric literal types act the same as the string literals above. A common case for their use is for describing config values:

```coffee
interface MapConfig {
  float lat, lng;
  (8 | 16 | 32) tileSize
}

setupMap({ lng: -73.935242, lat: 40.73061, tileSize: 16 });
```

#### Booleans

TypeScript also has boolean literal types. You might use these to constrain object values whose properties are interrelated.

```coffee
interface ValidationSuccess {
  true isValid;
  null reason;
}

interface ValidationFailure {
  false isValid;
  str reason;
}

type ValidationResult = ValidationSuccess | ValidationFailure;
```

### Conditional Types

Sometimes you have no choice but to list down all the possible literals a type may have. Enter conditional types, which allow you to explicitly specify which values are valid, without you having to exhaustively write down every single possible value.

```coffee
type Dodecahedron = 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12
```

Specify optional types, variables and then a conditional value or boolean function after the `where` keyword. (`it` is a placeholder for a function with a single argument.)

```coffee
// Both are the same
type Dodecahedron = int where 0 < it <= 12
type Dodecahedron = int i where 0 < i <= 12
```

A conditional is a sub-type of a collective type, but a super-type of a literal. This means that `"Hello World"` is a sub-type of `str a where a in ["Hello World"]`, but the latter is not a subset of the former.

This means you can pass any integer to the `Dodecahedron` type, as long as it is above 0 and at most 12. Any other integer value will produce an error:

```
Argument of type '21' does not satisfy the type "int i where 0 < i <= 12"
```

## Control Flow

There are a couple ways of writing control flow statements, and it's completely up to you to decide how you want it. The formatter tries its best to know exactly how you want your statements to look like so it can be consistent across your code.

The curly braces around the statements are only there to group the statements together so that the code can be compressed into a single line.

A typical statement looks like this:

```coffee
if (y <= 15) { x = 10; print x; }
```

You can remove the parentheses if you so wish:

```coffee
if y <= 15 { x = 10; print x; }
```

If there's only one statement then _that's_ the only time you enclose your expression (or statements) inside parentheses.

```coffee
if (y <= 15) print;
```

Otherwise, you can put your control flow statements (this only works for `if/unless`, `for`, `while` and `until` statements), like Perl:

```coffee
print if y <= 15;
```

In Zenith, **everything is an expression**, which means that they can be assigned to variables and returned from functions:

```coffee
res = 3 if true else 0

res = if 2 & 3 ^^ 3 + 2 != 4 {
  res + 3
} elun "#{4}" < "30" {
  = 4
} else 5

x = 2
res = switch {
  | x == 3, x == 4 => 3;
  | x in [4, 5, 6] => 4;
  | x % 2 == 0 => 2;
  | => 0;
}

y = 'string'
res = try {
  parseInt(i);
} catch {
  error 'unknown error';
} finally {
  4;
}

res = do {
  print 1 + 2 + 3
  print 40
  4
}
```

### If, Else, Unless, and Conditional Assignment

As with functions and other block expressions, multi-line conditionals are delimited by curly braces.

`if` statements are compiled either into JavaScript expressions, using the ternary operator when possible, and closure wrapping otherwise. There is no explicit ternary statement in Zenith — you simply use a regular `if` statement on a single line.

`if` and `else` work the same way as in many other languages, like Java. At its simplest form, it consists of a single `if` statement with a single statement immediately following it or multiple statements enclosed in curly braces.

You can chain multiple `elif` (`else if`) clauses if you wish, or leave a dangling `else` which won't be executed.

```coffee
if (temp <= 15)
  print("It's very cold. Consider wearing a scarf.")
```

```coffee
temp = 28
if (temp <= 15)
  print("It's very cold. Consider wearing a scarf.");
else
  print("It's not that cold. Wear a t-shirt.")
```

```coffee
temp = 28
if (temp <= 15)
  print("It's very cold. Consider wearing a scarf.");
elif (temp >= 30)
  print("It's really warm. Don't forget to wear sunscreen.")
```

```coffee
temp = 28
if (temp <= 15)
  print("It's very cold. Consider wearing a scarf.");
elif (temp >= 30)
  print("It's really warm. Don't forget to wear sunscreen.")
else // don't do anything else
```

```coffee
temp = 28
if (temp <= 15)
  print("It's very cold. Consider wearing a scarf.");
elif (temp >= 30)
  print("It's really warm. Don't forget to wear sunscreen.")
else
  print("It's not that cold. Wear a t-shirt.")
```

`unless` can be used in place of `if`, and refers to `if not`. Likewise, `elun` (`else unless`) can be used in place of `elif`, and refers to `else if not`.

There are a handful of ways to write if statements. Note that there is no ternary operator `a ? b : c` in Zenith, as a regular `if` statement would suffice.

```coffee
if condition { runA(); } else { runB(); }
x = if (condition) a else b;
x = a if condition else b; // Also possible, similar to Python
```

There’s also a handy postfix form, with the `if` or `unless` at the end.

```coffee
x = a if condition;
```

Control flow statements can be written without the use of parentheses (to separate expressions from statements), and/or curly braces (if there is only one statement).

### Loops and Comprehensions

Most of the loops you write are comprehensions over arrays, objects, and ranges. Comprehensions replace (and compile into) `for` loops, with optional `when` clauses and the index. `for` loops are expressions, and can be returned and assigned.

Comprehensions should be able to handle most places where you otherwise would use a loop, `each`/`forEach`, `map`, or `select`/`filter`, for example:

```coffee
shortNames = (for (name in list when len name < 5) name)
```

If you know the start and end of your loop, or would like to step through in fixed **or** variable-size increments, you can use a range to specify the start and end of your comprehension. By default, loops iterate from a starting value up to (and including) the ending value.

Typically, you would write down a `for`-loop like this in JavaScript, which is very confusing to most developers. Also note the compulsory parentheses following the `for` keyword.

```js
for (let i = 1; i <= 10; i++) {}
```

Whereas in Zenith, you can write it out like this:

```coffee
for i in [1::10] {}
```

Note we've just used the range literal (the one used for array and string slicing), which compile to regular arrays of numeric values in JavaScript. Here, `$` is not allowed since there's no sequence to iterate over but we are creating a new array instead.

From the previous chapter we learnt about the slicing and splicing syntax. Range syntax is short, sweet and very powerful.

| Operator         | Meaning                         |
| ---------------- | ------------------------------- |
| `a,b`            | `a` and `b` only                |
| `,b,`            | implicit `0`: `0,b,0`           |
| `a,b:c`          | `a`, then from `b` to `c`       |
| `a::b`           | from `a` to `b`, inclusive      |
| `a:>b` or `a:<b` | ... excluding `b`               |
| `a<:b` or `a>:b` | ... excluding `a`               |
| `a<>b` or `a><b` | ... exclusive                   |
| `a::b:c`         | ... inclusive, stepping by `c`  |
| `a::b:c:d`       | ... stepping by `c`, then `d`\* |

So something as complex as this...

```js
for (let index of [
  1, // Individual elements
  2,
  ...(() => {
    // Start, end and pattern
    const [min, max, patt] = [0, 50, [1, 2, 3, 4]];
    let sum = patt.reduce((a, b) => a + b, 0),
      arr = [min];
    for (let i = min; i <= max; i += sum) {
      let idx = i;
      for (let j of patt) {
        idx += j;
        arr.push(idx);
      }
    }
    // Operator ::, :<, :>, >:, <:, ><, <>
    return arr.filter(i => min <= idx && idx <= max);
  })()
]) {
  // actual code goes here
}
```

...can be simplified into a `for-in` range loop, as shown below. You use the `for-in` loop to iterate over a sequence, such as items in an array, ranges of numbers, or characters in a string.

```coffee
for i in [1,2,::50:1:2:3:4] {
  // actual code goes here
}
```

This example uses a `for-in` loop to iterate over the items in an array. The second element refers to each item's indices.

```coffee
names = ["Anna", "Alex", "Brian", "Jack"];

for name in names {
  print "Hello, #name!";
}
// Hello, Anna! | Hello, Alex! | Hello, Brian! | Hello, Jack!

for name, index in names {
  print "Hello, person #{index + 1}!";
}
// Hello, person 1! | Hello, person 2! | Hello, person 3! | Hello, person 4!
```

You use the `for-of` loop to iterate over an object or map. The keys are assigned to a variable named `child`, and the values are assigned to `age`.

```coffee
yearsOld = { Max: 10, Ida: 9, Tim: 11 };

for child of yearsOld {
  print child;
}
// Max, Ida, Tim

for child, age of yearsOld {
  print "#child is #age";
}
// Max is 10, Ida is 9, Tim is 11
```

If you would like to iterate over just the keys that are defined on the object itself, by adding a `hasOwnProperty()` check to avoid properties that may be inherited from the prototype, use `for own key, value of object`.

To iterate values over a generator function, use `for-from`.

```coffee
genfn fibonacci(): int {
  (a, b) = (0, 1);
  loop {
    (a, b) = (b, a + b);
    yield b;
  }
}

func getFibonacciNumbers(int length) int[] {
  results = [1], fibSeq = fibonacci();
  for n from fibSeq {
    results + [n];
    break if len results is length;
  }
  results;
}
```

A while loop performs a set of statements until a condition becomes `false`. These kinds of loops are best used when the number of iterations isn’t known before the first iteration begins. There are five kinds of while-loops:

- `while` evaluates its condition at the start of each pass through the loop, until the condition is `false`.
- `repeat-while` evaluates its condition at the end of each pass through the loop, until the condition is `false`.

For readability, `until condition` is `while !condition`, `repeat {} until condition` is `repeat {} while condition`, and `loop` which which is equivalent to `while true`.

- `until` and `repeat-until` are like `while`, except the loop runs until the condition is `true`.
- `loop` runs its body forever **unless** there is a `break` statement somewhere.

```coffee
while i < 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```coffee
repeat {
  text += "The number is " + i;
  print text;
  i++;
} while i < 10;
```

```coffee
until i == 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```coffee
repeat {
  text += "The number is " + i;
  print text;
  i++;
} until i == 10;
```

```coffee
loop {}
```

### Switch

Pattern matching provides a way to conditionally execute code when the shape of some data matches a particular pattern. It is similar to `switch-case` statements in other languages, but it can be more expressive and includes some extra safeguards.

```coffee
switch /* some value to consider */ {
  | /* value 1 */ ->
    // respond to value 1
  | /* value 2, value 3 */ ->
    // respond to value 2 or 3
  | ->
    // otherwise, do something else
}
```

The switch finds the first pattern that matches the input, and then executes the code that the pattern points to (the code after the next `->`). Code for a pattern can be a single expression, or a block of statements. The switch statement itself is an expression that can return the value of the code that it executes.

Like the body of an `if` statement, each case is a separate branch of code execution. The `switch` statement determines which branch should be selected.

```coffee
char = `z`
switch someCharacter {
  | `a` -> print "The first letter of the alphabet"
  | `z` -> print "The last letter of the alphabet"
  | -> print "Some other character"
}
```

\#TODO

### Error Handling

\#TODO

### Switch

\#TODO

## Functions and Generator Functions
 
## Property Access

## Classes and Inheritance

## Error-handling

## Types and Object-Oriented Programming
