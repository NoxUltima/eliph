# An Informal Introduction

> This reference is structured so that it can be read from top to bottom, if you like. Later sections use ideas and syntax previously introduced. Familiarity with JavaScript is assumed.

Like many programming languages such as JS, Eliph uses significant use of **curly braces** `{}` to delimit blocks of code, rather than indentation.

Semicolons are optional and are mainly used to fit multiple expressions onto a single line, and in basic `for` and `till`-loops like below.

```res
for i = 0; i < 10; i++ { console.log(i); }
till i = 0; i == 10; i++ { console.log(i); } // till is the opposite of for
```

Function calls must require parentheses, as in many other programming languages. Statements such as `break`, `continue` and `goto`, and unary operators such as `not`, `len` and `size` do not require parentheses, since they are not functions.

```res
echo sys.inspect(e) // echo is a statement
```

When invoking functions as arguments to methods, such as in `map` and `filter` operations, you can leave out the parentheses.

```res
[1, 2, 3, 4, 5].map { $ * 2 }.filter { $ % 3 == 0 }
```

## Variables

Valid variable or identifier names with a letter, underscore `_` or **any Unicode character** that is not punctuation or symbols. All other characters can include digits, `-` and `$`.

If you need to give a constant or variable the same name as a reserved Eliph keyword, prefix `$`. Use `$$` in place of `$`. This is because a single `$` is considered a **topical identifier**.

The following are a list of all the **keywords** of the language in Eliph:

```res
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

```res
let i;
var j;
for const i in [0::len array] {}
```

All variables when declared with the `=` assignment operator are automatically assigned a `let` declaration in the compiled output, the first time they appear.

Likewise, `const` variables are always initialized with `:=`, and **cannot be modified**.

```res
i = 3;  // let i = 3
j .= 4; // var j = 4
k := 5; // const k = 5
```

Non-local or `var` variables are declared with `.=`, and you are required to use `.=` whenever you modify the same variable in upper scopes, such as outside functions.

```res
x .= 10 // declared as `var x`
do { x = 5 } // 10 => creates a new variable called x
do { x .= 2 } // 2 => modifies `var x`
```

You can declare multiple constants or multiple variables on a single line, separated by commas:

```res
x = 0.0, y := 0.0, z .= 0.0;
```

or assign different types of variables the same value.

```res
x = y := z .= 0.0;
```

`// line comments` and `/* block comments */` work the same way as in JavaScript.

```res
/* hooray for nested comments */
/**
 * @param hooray for nested comments
 */
```

You can destructure from tuples, arrays, objects, records and maps, like in Swift, Reason or JavaScript:

```res
(x, y, , z) = (0, 0, 1, 0);
[x, y, , z] = [0, 0, 1, 0];
{x, y, z} = {x: 0, y: 0, z: 0, a: 1};

{| 'x': x, 'y': y, 'z': z |} = {| 'x': 0, 'y': 0, 'z': 0 |};
```

## Data types

In addition to the JavaScript basic types, such as `bool`, `str`, and `float` (all `number`s in JavaScript are `float`), we do provide a few more.

You can add an annotation that goes right before the variable name, similar to C# and Java.

```res
let int count;
var int count;
```

Because `count` has a type the compiler knows what we are and are not allowed to do with its value:

```res
// Allowed: addition
nextCount = count + 1

// Error: count is not of the type any()|any[]
x = count.map => 3
```

You can cast (convert a value from one type to another) with the `as` keyword or constructor function.

```res
someValue = "this is a string"; // assigned 'str'
int strLength = len (someValue as str);
```

Another is through using constructor functions:

```res
someValue = "this is a string";
int strLength = len str(someValue);
```

### Null and Undefined

#### Void, Null and Undefined

Both `undef` and `null` actually have their **own** types, but they’re not extremely useful on their own.

`undef` is the default value assigned to a variable, or the value returned from function calls, while `null` is the value which you assign explicitly.

```res
// Not much else we can assign to these variables!
undef u = undef;
null n = null;
```

`void` is a type alias, and `void == null | undef`.

```res
void warnUser() {
  print "This is my warning message";
}
```

So declaring variables of type `void` is not useful because you can only assign `null` or `undef` to them:

```res
void unusable = undef;
unusable = null;
```

### Boolean

A boolean is either one of two values, `true` and `false`, and has the type `bool`. As in YAML, `on` `and` yes are the same as boolean `true`, while `off` and `no` are boolean `false`.

```res
bool isDone := false;
```

Logical and comparison operators such as `!`, `&&`, `||`, `<`, `>`, `<=`, `>=` are retained.

```res
!true // false
true && false // false
true || false // true
```

We do provide a few more, such as the xor operator `^^`.

`&&`, `||` and `^^`, and their infix forms `and`, `or` and `xor`, have their own inverses: `!&`/`nand`, `!|`/`nor` and `!^`/`xnor`.

```res
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

```res
2 + 2 // 4
50 - 5 * 6 // 20
(50 - 5 * 6) / 4 // 5.0
8 / 5 // 1.6
```

Regular division with `/` will evaluate to a `float`, but floor division with `~/` will return `int`. Operators with mixed type operands convert the evaluated result to `float`:

```res
4 * 3.75 - 1;
```

```res
17 / 3; // 5.666666666666667
17 ~/ 3; // 5
17 % 3; // 2
5 * 3 + 2; // 17
```

Bitwise operations such as unary `~`, infix `&`, `|` and `^` (and their inverses `~&`, `~|`, `~^`), and shift operators `<<`, `>>` and `>>>` will evaluate into `int`, no matter the type.

```res
5 & 1; // 1
5 | 1; // 5
5 ^ 1; // 4
~5; // 10
5 << 1; // 10
5 >> 1; // 2
5 >>> 1; // 2
```

`%%` provides dividend-dependent modulo:

```res
-7 % 5 == -2; // The remainder of 7 / 5
-7 %% 5 == 3; // n %% 5 is always between 0 and 4
```

Radix literals can be created using prefixes `0x`, `0o`, `0b`. Literals can be broken up using the `_` character which will be ignored. Leading 0s are also ignored.

```res
dec = 6.;
hex = 0xf00d;
binary = 0b1010;
octal = 0o744;

billion = 1_000_000_000;
```

The minimum/maximum operators `<?` and `>?`, which return the smaller or larger of the two operands.

```res
3 <? 10; // 3
3 >? 10; // 10
```

PHP's "spaceship" operator `<=>`, returns either `1`, `0` or `-1` depending on whether the number on the left is greater than, equal to or lesser than the right.

```res
3 <=> 1; // 1
1 <=> 3; // -1
2 <=> 2; // 0
```

Bases 2 to 64 can be used, as long as they use these digits below and are surrounded in string literals and suffixed with the base. Bases are not case-sensitive if 36 and below.

```
0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$&
```

```res
i = '105'6; // 41
```

### Characters and Strings

Characters, of type `char`, enclosed in ` `` `, are strings of length 1. They can be converted into integers with `int()`, and concatenated with `+` or repeated with `*` to form strings.

```res
char a = `a`;
```

As in other languages, we use the type `str` (not `string`) to refer to these textual datatypes. Just like JavaScript, Eliph also uses double quotes `"` or single quotes `'` to surround string data.

```res
str color = 'blue';
color = 'red';
```

Both character and single-quoted string literals have special escape syntax, as shown below. Single-quote strings evaluate as-is, and require you to escape some special characters, as shown below:

```res
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

```res
author = 'Wittgenstein'
quote = "A picture is a fact. -- #author"
sentence = "#{22 / 7} is a decent approximation of π"
```

In single-quoted strings, lines are joined by a single space unless they end with a backslash. Indentation is ignored.

```res
mobyDick = 'Call me Ishmael. Some years ago --
  never mind how long precisely -- having little
  or no money in my purse, and nothing particular
  to interest me on shore, I thought I would sail
  about a little and see the watery part of the
  world...'
```

Strings can be concatenated `+`, replaced `-`, repeated `:`, sliced or split `/` with arithmetic operators.

Use `*` to join strings back from arrays `[]` or tuples `()`, where the right operand is the delimiter. This operation will convert all non-strings (including `char`s) into strings.

```res
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

```res
strLen = len 'hello' // 5
```

Use commas to retrieve individual indices of strings, and combinations of `<>` and `:` to extract ranges of strings from arrays. More on #Ranges.

Much like JavaScript objects and maps, arrays and tuples do have keys (their **numeric** index) and values (which are the values you see on the screen), You can use `in` or its inverse `!in` to test whether a substring or character is in a string.

```res
'34' in '12345' // true
`3` in '12345' // true

'34' !in '12345' // false
`3` !in '12345' // false
```

`of` returns `true` if and only if the number passed in is between 0 and 1 less than the length of the string.

```res
3 of '12345' // true
-1 of '12345' // false
```

### Regular Expressions

Marked as #TODO

### Tuples and Arrays

```res
a = [1, 2] + [3, 4]; // Concatenation
[x, , ...z] = a // Destructuring
print(x, z); // 1, [3, 4]
$a = [...a, ...a, 4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
$a = a * 2 + [4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
```

Marked as #TODO

### Records, Objects and Maps

Marked as #TODO

### Sets

Marked as #TODO

### Ranges

There are also range literals, like in CoffeeScript, Kotlin or Swift, for example, `[1,2,3]` or `[1:100:1]`.

Ranges are short, sweet and very powerful, evaluating to tuples or arrays containing numeric values, depending on the brackets.

A range literal can either contain individual numeric elements separated by commas, or subranges of the form `start::end:step`, implicitly adding `0` wherever needed.

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

- Each iteration alternates between adding `c`and`d`to`a`, until reaching and hitting `b`.
- Algebraically, this is equivalent to `[a, a + c, a + c + d, a + 2c + d, a + 2c + 2d, a + 3c + 2d, a + 3c + 3d ... b]`

Some things to note:

- If the range counts **out of bounds**, it will coerce that to count in the right direction. `c + d > 0 && a > b || c + d < 0 && a < b`, then all numbers following `a` and `b` will be negated: `c` would be `-c` and `d` `-d`.

**Slicing and splicing** allow you to retrieve and override elements in tuples and arrays, or individual `char`s in strings, using the same notation above.

Slice syntax is always enclosed in `[]` immediately after the literal or variable, like how we would access arrays or objects in JS.

The placeholder `$` stands for the length of the array or string it refers to, and remains constant.

```res
c = 'hello'; // Slicing
s = c[1]; // e
s = c[1,2]; // el (specific indices)
s = c[:>$]; // hello (string cloning)
s = c[$>:]; // olleh (specific indices)
```

When splicing, each individual index must be assigned a literal value, and for subranges a tuple of values.

- `a=1,b=2` - Assign `1` to index `a` and `2` to `b`.
- `a::b:c=<1,2>` - Assign to every index evaluated by the range expression `a::b:c`, alternating between values `1, 2`, in order of appearance.

```res
t = (1, 2, 3); // Splicing
t = t + (4, 5); // (1, 2, 3, 4, 5)
t = t * 2; // (1, 2, 3, 4, 5, 1, 2, 3, 4, 5)
t = (1, 2, 3, 4, 5)[$>:];   // (5, 4, 3, 2, 1)
t = (1, 2, 3, 4, 5)[-1='5']; // (1, 2, 3, 4, '5')
```

## Control Flow

Control flow statements can be written without the use of parentheses. As with functions and other block expressions, multi-line conditionals are delimited inside curly braces.

```res
if y <= 15 { x = 10; print x; }
```

If you have only one statement on a line then you can use `then` or move the statement postfix:

```res
if y <= 15 then print y;
print if y <= 15;
```

In Eliph, **everything is an expression**, which means that they can be assigned to variables and returned from functions.

It's common to insert a closure wrapper in order to ensure that all variables are closed over, and all the generated functions don't share the final values. The `do` keyword, immediately invokes a passed function, forwarding any arguments.

```res
res = do factorial(n) int {
  if n < 0 then -1
  else if n == 0 then 1
  else n * factorial(n - 1);
}
```

When control flow statements are used as expressions, the value of the last statement of all bodies (enclosed in curly braces) is implicitly returned, unless explicitly specified with `return`. More on functions in the next section.

```res
res = 3 if true else 0;

res = if 2 & 3 ^^ 3 + 2 != 4 {
  res + 3;
} elun "#{4}" < "30" {
  4;
} else 5;

x = 2
res = switch {
  case x == 3, x == 4 -> 3;
  case x in [4, 5, 6] -> 4;
  case x % 2 == 0 -> 2;
  else -> 0;
};

y = 'string'
res = try {
  parseInt(i);
} catch {
  error 'unknown';
} finally {
  4;
};
```

You can mark a statement, such as a `do`-block, with a statement marked with `label`. Use `goto` followed by the labeled keyword. This is similar to calling functions without arguments. You can `goto` outside `labels` from inside other scopes, but you cannot do so the other way around.

```res
i = 0;
func goTo() void {
  label runThis: do for j in [1::100] {
    i .+= j; return;
  }
  print i; // 0
  goto runThis; // will modify the i variable 100 times
  print i; // 5050
  return;
}
goTo();
goto runThis; // Throws an error
```

### If-Else

`if` statements are compiled either into JavaScript expressions, using the ternary operator when possible, and closure wrapping otherwise.

There is no explicit ternary statement in Eliph — you simply use a regular `if` statement on a single line. The `else` and `elif` (not `else if`) blocks are optional.

```res
temp = 28
if (temp <= 15)
  print "It's very cold. Consider wearing a scarf.";
elif (temp >= 30)
  print "It's really warm. Don't forget to wear sunscreen.";
else
  print "It's not that cold. Wear a t-shirt.";
```

`unless` can be used in place of `if`, and refers to `if not`. Likewise, `elun` (not `else unless`) can be used in place of `elif`, and refers to `else if not`.

There are a handful of ways to write if statements. Note that there is no ternary operator `a ? b : c` in Eliph, as a regular `if` statement would suffice.

```res
x = if (condition) a else b;
x = a if condition else b; // Python postfix if statement
```

```res
// Implicit statement, make sure that there is an else
x = a if condition;
```

A `guard` statement is similar to an `if-else` statement without an `if` body.

```res
func greet({[str x]: str} person) {
  guard let name = person.name else return;
  print "Hello \(name)!";
  guard let location = person.location else {
    print "I hope the weather is nice near you.";
    return;
  }
  print "I hope the weather is nice in \(location)."
}

greet(person: {name: "John"});
// Prints "Hello John!" "I hope the weather is nice near you."
greet(person: {name: "Jane", location: "Cupertino"});
// Prints "Hello Jane!" "I hope the weather is nice in Cupertino."
```

### Loops

Typically, you would write down a `for`-loop like this in JavaScript, which is very confusing to most developers. Also note the compulsory parentheses following the `for` keyword.

```js
for (let i = 1; i <= 10; i++) {}
```

Whereas in Eliph, you can either leave out the brackets following the `for`:

```res
for i = 1; i <= 10; i++ {}
```

We also provide an opposite for the for-loop, the `till` loop, which is basically the direct opposite of the tripartite for-loop. It runs until the second, conditional statement is `true`.

```res
till i = 1; i > 10; i++ {}
```

You can iterates over the items in a sequence, such as items in an array, ranges of numbers, or characters in a string using the `for-in` loop.

```res
for i in [1::100] {
  // actual code goes here
}
```

You can pass in a second parameter which represents the **keys**, that is, indices of whatever you are iterating over.

```res
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

You use the `for-of` loop to iterate over an object or map's keys. The keys are assigned to a variable named `child`, and the values are assigned to `age`.

```res
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

To put it in another way, `for value, key in object` is equivalent to `for key, value of object`.

If you would like to iterate over just the keys that are defined on the object itself (by adding a `hasOwnProperty()` check), use `for own key, value of object`.

To iterate values over a generator function, use `for-from`.

```res
gen fibonacci(): int {
  (a, b) = (0, 1);
  loop {
    (a, b) = (b, a + b);
    yield b;
  }
}

func getFibonacciNumbers(int length) int[] {
  results = [1], fibSeq = fibonacci();
  for n from fibSeq {
    results += [n];
    break if len results == length;
  }
  results;
}
```

A `while` loop performs a set of statements until evaluating a condition. `while` evaluates its condition at the start of each pass through the loop, until the condition is `false`. `repeat-while` (not `do-while`) evaluates its condition at the end of each pass through the loop, until the condition is `false`.

```res
while i < 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```res
repeat {
  text += "The number is " + i;
  print text;
  i++;
} while i < 10;
```

`until` and `repeat-until` are like `while`, except the loop runs until its condition is `true`.

```res
until i == 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```res
repeat {
  text += "The number is " + i;
  print text;
  i++;
} until i == 10;
```

`loop` runs its body forever **unless** there is a `break` statement somewhere.

```res
loop {
  text += "The number is " + i;
  print text;
  i++;
  break if i == 10;
}
```

The `switch` statement works a bit differently than its JavaScript cousin. You need to remember to `break` at the end of every case statement to avoid accidentally falling through to the default case.

If no argument is supplied, the branch conditions are simply boolean expressions, and a branch is executed when its condition is true.

```res
x = 1;
switch {
  case x == 1 -> print 1;
  case x in [2, 3] -> print [2, 3];
  else -> print 4;
}
```

The switch statement can also match against primitive values, but this is highly disrecommended.

```res
x = 3; x += 2;
switch 5 {
  case x -> print "x == #x";
  else -> { print ''; break; };
}
```

The switch finds the first pattern that matches the input, and then executes the code that the pattern points to `->`. Code for a single branch case can be a single expression, or a block of statements.

Like an `if` statement, each case is a separate branch of code execution. The `switch` statement determines which branch should be selected. Only one branch is executed by default.

```res
char z = `z`;
switch someCharacter {
  case `a` -> print "The first letter";
  case `z` -> print "The last letter";
  else -> print "Some other letter";
}
```

The entire `switch` statement finishes its execution as soon as the first matching case is completed, without requiring an explicit `break` statement.

The body of each case must contain **at least one executable statement**.

You can use commas to separate the cases, and combine those into a single

```res
char a = `a`;
switch a {
  case "a", "e", "i", "o", "u" ->
    print "#a is a vowel";
  case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
    "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z" ->
    print "#a is a consonant";
  else ->
    print "#a is neither a vowel nor a consonant";
}
```

In every case statement following the vertical bar, there can be half-expressions, in which the value to compare is inserted as the left operand to the expression. In this case, `in [12:<100]` when used inside a switch expression, is evaluated to `approx in [12:<100]`.

```res
approx = 62;
things = "moons orbiting Saturn";
str count;

count = switch approx {
  case 0 -> "no"; // approx == 0
  case in [1:<5] -> "a few"; // approx in [1:<5], et alii
  case in [5:<12] ->  "several";
  case in [12:<100] -> "dozens of"
  case in [100:<1000] -> "hundreds of";
  else -> "many"; // else (by default), this will run
};

print "There are #count #things.";
// Prints "There are dozens of moons orbiting Saturn."
```

A case can have temporary variables. After they are declared, they can be used within the case's code block. All of the patterns of a compound case have to include **the same set of value bindings**.

```res
point = (9, 0)
switch point {
  case (dist, 0), (0, dist) ->
    print "On an axis, #dist from the origin"
  else ->
    print "Not on an axis"
}
// Prints "On an axis, 9 from the origin"
```

A case can use a `where` clause to check for additional conditions.

```res
point = (-1, 1);
switch point {
  case (x, y) where x == y ->
    print "(#x, #y) is on the line x == y";
  case (x, y) where x == -y ->
    print "(#x, #y) is on the line x == -y";
  case (x, y) ->
    print "(#x, #y) is just some arbitrary point";
}
// Prints "(1, -1) is on the line x == -y"
```

You can use data structures to test multiple values, such as arrays, tuples, records, maps and objects in the same switch statement, where each mentioned value you put in the structure is destructured and tested.

Alternatively, leave the space blank `()` or insert a wildcard placeholder `$`, to match any possible value.

```res
point = {x: 1.5, y: 1.5};
switch point {
  case {x: 0, y: 0} ->
    print "#point is at the origin";
  case {x: 0} ->
    print "#point is on the x-axis";
  case {y: 0} ->
    print "#point is on the y-axis";
  case {x: -2 <= $ <= 2, y: -2 <= $ <= 2} ->
    print "#point is inside the box";
  else ->
    print "#point is outside of the box";
}
// Prints "(1, 1) is inside the box"
```

**Control transfer statements** change the order in which your code is executed, by transferring control from one piece of code to another. There are six control transfer statements in Eliph:

- `continue`
- `break`
- `fall` and `rise`
- `return`
- `goto`
- `throw`

The `continue` statement tells a loop to stop what it's doing and start again at next iteration of the loop.

```res
text = "", i;
for i in [1::5] {
  if (i == 3) continue;
  text += "The number is " + i + "\n";
}
```

In a switch statement, `continue` stops the execution of the current branch and executes the labelled branch that immediately comes after it. The code below will skip printing `CLOSED`, and would print `NOW_CLOSED` instead.

```res
var command = 'CLOSED';
switch (command) {
  case 'CLOSED' -> {
    continue nowClosed; // move to nowClosed without printing
    print command;
  };
  nowClosed: case command1 := 'NOW_CLOSED' -> {
    print command1;
  };
}
```

The `break` statement ends execution of an entire control flow statement immediately. The break statement can be used inside a `switch` or loop statement when you want to terminate the execution of the statement earlier than would otherwise be the case.

```res
text = "", i;
for i in [1::5] {
  if (i == 3) break;
  text += "The number is " + i + "\n";
}
```

In switch statements, if you really need C-style fallthrough, can opt in to this behavior on a case-by-case basis with the `fallthru` keyword.

```res
func isPrime(int n) bool { !('1' * n).match(/^1?$|^(11+?)\1+$/) }
```

```res
integer := 5;
description = "The number #integer is";
switch integer {
  case isPrime($) -> {
    description += " a prime number, and also";
    fall;
  };
  else -> description += " an integer.";
}
print description;
// Prints "The number 5 is a prime number, and also an integer."
```

Similarly, `rise` will execute the branch above it.

```res
integer := 5;
desc = "The number #integer is";
switch integer {
  else -> desc += " an integer.";
  case isPrime($) -> {
    desc += " a prime number, and also";
    rise;
  };
}
print desc;
// Prints "The number 5 is a prime number, and also an integer."
```

### Error Handling

Marked as #TODO
