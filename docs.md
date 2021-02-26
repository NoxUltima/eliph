# An Informal Introduction

> This reference is structured so that it can be read from top to bottom, if you like. Later sections use ideas and syntax previously introduced. Familiarity with JavaScript is assumed.

Like many programming languages such as JS, Eliph uses significant use of **curly braces** `{}` to delimit blocks of code, rather than indentation.

Semicolons are optional and are mainly used to fit multiple expressions onto a single line, and in basic `for` and `til`-loops like below.

```coffee
for i = 0; i < 10; i++ { console.log(i); }
til i = 0; i == 10; i++ { console.log(i); } // til is the opposite of for
```

Function calls must require parentheses, as in many other programming languages. Statements such as `break`, `continue` and `goto`, and unary operators such as `not`, `len` and `size` do not require parentheses, since they are not functions.

```coffee
echo sys.inspect(e) // echo is a statement
```

When invoking functions as arguments to methods, such as in `map` and `filter` operations, you can leave out the parentheses.

```coffee
[1, 2, 3, 4, 5].map { $ * 2 }.filter { $ % 3 == 0 }
```

## Variables

Valid variable or identifier names with a letter, underscore `_` or **any Unicode character** that is not punctuation or symbols. All other characters can include digits, `-` and `$`.

If you need to give a constant or variable the same name as a reserved Eliph keyword, prefix `$`. Use `$$` in place of `$`. This is because a single `$` is considered a **topical identifier**.

The following are a list of all the **keywords** of the language in Eliph:

```coffee
var let const def
if unless then elif elun else
for own in of when break continue
while until loop repeat pass
switch case where other fallthru
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

```coffee
let i;
var j;
for const i in [0::len array] {}
```

All variables when declared with the `=` assignment operator are automatically assigned a `let` declaration in the compiled output, the first time they appear.

Likewise, `const` variables are always initialized with `:=`, and **cannot be modified**.

```coffee
i = 3;  // let i = 3
j .= 4; // var j = 4
k := 5; // const k = 5
```

Non-local or `var` variables are declared with `.=`, and you are required to use `.=` whenever you modify the same variable in upper scopes, such as outside functions.

```coffee
x .= 10 // declared as `var x`
do { x = 5 } // 10 => creates a new variable called x
do { x .= 2 } // 2 => modifies `var x`
```

You can declare multiple constants or multiple variables on a single line, separated by commas:

```coffee
x = 0.0, y := 0.0, z .= 0.0;
```

or assign different types of variables the same value.

```coffee
x = y := z .= 0.0;
```

`// line comments` and `/* block comments */` work the same way as in JavaScript.

```coffee
/* hooray for nested comments */
/**
 * @param hooray for nested comments
 */
```

You can destructure from tuples, arrays, objects, records and maps, like in Swift, Reason or JavaScript:

```coffee
(x, y, , z) = (0, 0, 1, 0);
[x, y, , z] = [0, 0, 1, 0];
{x, y, z} = {x: 0, y: 0, z: 0, a: 1};

{| 'x': x, 'y': y, 'z': z |} = {| 'x': 0, 'y': 0, 'z': 0 |};
```

## Data types

In addition to the JavaScript basic types, such as `bool`, `str`, and `float` (all `number`s in JavaScript are `float`), we do provide a few more.

You can add an annotation that goes right before the variable name, similar to C# and Java.

```coffee
let int count;
var int count;
```

Because `count` has a type the compiler knows what we are and are not allowed to do with its value:

```coffee
// Allowed: addition
nextCount = count + 1

// Error: count is not of the type any()|any[]
x = count.map => 3
```

You can cast (convert a value from one type to another) with the `as` keyword or constructor function.

```coffee
someValue = "this is a string"; // assigned 'str'
int strLength = len (someValue as str);
```

Another is through using constructor functions:

```coffee
someValue = "this is a string";
int strLength = len str(someValue);
```

### Null and Undefined

#### Void, Null and Undefined

Both `undef` and `null` actually have their **own** types, but they’re not extremely useful on their own.

`undef` is the default value assigned to a variable, or the value returned from function calls, while `null` is the value which you assign explicitly.

```coffee
// Not much else we can assign to these variables!
undef u = undef;
null n = null;
```

`void` is a type alias, and `void == null | undef`.

```coffee
void warnUser() {
  print "This is my warning message";
}
```

So declaring variables of type `void` is not useful because you can only assign `null` or `undef` to them:

```coffee
void unusable = undef;
unusable = null;
```

### Boolean

A boolean is either one of two values, `true` and `false`, and has the type `bool`. As in YAML, `on` `and` yes are the same as boolean `true`, while `off` and `no` are boolean `false`.

```coffee
bool isDone := false;
```

Logical and comparison operators such as `!`, `&&`, `||`, `<`, `>`, `<=`, `>=` are retained.

```coffee
!true // false
true && false // false
true || false // true
```

We do provide a few more, such as the xor operator `^^`.

`&&`, `||` and `^^`, and their infix forms `and`, `or` and `xor`, have their own inverses: `!&`/`nand`, `!|`/`nor` and `!^`/`xnor`.

```coffee
false ^^ true  // true
false ^^ false // false
1 ^^ 0         // 1
1 ^^ 1         // false
```

`==` and `!=` in Eliph compile to `===` and `!==` in JavaScript.

If you really want to use JavaScript's `==` and `!=`, use the _fuzzy equality_ operators `=~` and `!~` instead.

### Numbers

In JavaScript, all numbers are either floating point values or (big) integers. These floating point numbers get the type `float`, while integers simply get `int`.

`int` literals have no `.`, whereas `float`s have. `int`s also can end in `n`, of which explicitly tell the compiler it is a `bigint`.

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

Bitwise operations such as unary `~`, infix `&`, `|` and `^` (and their inverses `~&`, `~|`, `~^`), and shift operators `<<`, `>>` and `>>>` will evaluate into `int`, no matter the type.

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

Radix literals can be created using prefixes `0x`, `0o`, `0b`. Literals can be broken up using the `_` character which will be ignored. Leading 0s are also ignored.

```coffee
dec = 6.;
hex = 0xf00d;
binary = 0b1010;
octal = 0o744;

billion = 1_000_000_000;
```

The minimum/maximum operators `<?` and `>?`, which return the smaller or larger of the two operands.

```coffee
3 <? 10; // 3
3 >? 10; // 10
```

PHP's "spaceship" operator `<=>`, returns either `1`, `0` or `-1` depending on whether the number on the left is greater than, equal to or lesser than the right.

```coffee
3 <=> 1; // 1
1 <=> 3; // -1
2 <=> 2; // 0
```

Bases 2 to 64 can be used, as long as they use these digits below and are surrounded in string literals and suffixed with the base. Bases are not case-sensitive if 36 and below.

```
0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$&
```

```coffee
i = '105'6; // 41
```

### Characters and Strings

Characters, of type `char`, enclosed in ` `` `, are strings of length 1. They can be converted into integers with `int()`, and concatenated with `+` or repeated with `*` to form strings.

```coffee
char a = `a`;
```

As in other languages, we use the type `str` (not `string`) to refer to these textual datatypes. Just like JavaScript, Eliph also uses double quotes `"` or single quotes `'` to surround string data.

```coffee
str color = 'blue';
color = 'red';
```

Both character and single-quoted string literals have special escape syntax, as shown below. Single-quote strings evaluate as-is, and require you to escape some special characters, as shown below:

```coffee
'\''         // single quote
'\"'         // double quote
'\`'         // backtick
'\\'         // literal backslash
'\a'         // alert
'\b'         // backspace
'\e'         // escape
'\f'         // form feed
'\n'         // newline
'\r'         // carriage return
'\t'         // tab
'\v'         // vertical tab
'\x30'       // ASCII character
'\uFFFF'     // BMP Unicode character
'\u{10FFFF}' // non-BMP Unicode character
```

Double-quote strings allow interpolation and embedding of variables of expressions. Embedded variables are of the form `#var`, and interpolated expressions are of the form `#{ expr }`.

You can delimit your string with as many `"` or `'` characters as you want, but each string literal should be surrounded with an **odd** number of the same character.

|                                | `'` | `"` |
| ------------------------------ | --- | --- |
| Ignores indentation/newlines   | Yes | No  |
| Allows interpolating/embedding | No  | Yes |
| Raw, unescaped strings         | Yes | No  |
| Proper Unicode handling        | No  | Yes |

```coffee
author = 'Wittgenstein'
quote = "A picture is a fact. -- #author"
sentence = "#{22 / 7} is a decent approximation of π"
```

In single-quoted strings, lines are joined by a single space unless they end with a backslash. Indentation is ignored.

```coffee
mobyDick = 'Call me Ishmael. Some years ago --
  never mind how long precisely -- having little
  or no money in my purse, and nothing particular
  to interest me on shore, I thought I would sail
  about a little and see the watery part of the
  world...'
```

Strings can be concatenated `+`, replaced `-`, repeated `:`, sliced or split `/` with arithmetic operators.

Use `*` to join strings back from arrays `[]` or tuples `()`, where the right operand is the delimiter. This operation will convert all non-strings (including `char`s) into strings.

```coffee
str s = 'Hello';

// Concatenating strings together
s = 'Hello' + 'World!' // 'Hello World!'
s = 'Hello'

// Replacing strings by substring or regex
s = 'Hello' - `l`; // 'Heo'
s = 'Hello' - (/llo$/, 'lp me'); // 'Help me'
// (calls String.replace() with the right operand)

// Splitting
str[] t = s / 1; // ['H', 'e', 'l', 'l', 'o']
t = s / ''; // ['H', 'e', 'l', 'l', 'o']

// Splitting with spread operator
char[] c = [...s]; // [`h`, `e`, `l`, `l`, `o`]

// Joining
strArr = ['H', 'e', `l`, 'l', 'o'];
strArr = strArr * ''; //  'Hello'
```

Strings can be indexed, and can accept any integer value, but modulo `%%` the length of the string. So given a string `s` of length `5`, `... s[5] == s[0] == s[-4] == s[-9] ...`.

Use the `len` operator to retrieve the length of a string:

```coffee
strLen = len 'hello' // 5
```

Use commas to retrieve individual indices of strings, and combinations of `<>` and `:` to extract ranges of strings from arrays. More on #ranges.

Much like JavaScript objects and maps, arrays and tuples do have keys (their **numeric** index) and values (which are the values you see on the screen), You can use `in` or its inverse `!in` to test whether a substring or character is in a string.

```coffee
'34' in '12345' // true
`3` in '12345' // true

'34' !in '12345' // false
`3` !in '12345' // false
```

`of` returns `true` if and only if the number passed in is between 0 and 1 less than the length of the string.

```coffee
3 of '12345' // true
-1 of '12345' // false
```

### Regular Expressions

Marked as #TODO

### Tuples and Arrays

Marked as #TODO

### Records, Objects, Maps and Frozen Maps

Marked as #TODO

### Sets

Marked as #TODO

## Control Flow

Marked as #TODO

