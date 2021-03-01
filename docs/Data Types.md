# Data types

In addition to the JavaScript basic types, such as `bool`, `str`, and `float` (all `number`s in JavaScript are `float`), we do provide a few more.

You can add a type annotation that goes atfer the variable name, similar to how you would do it in Swift and TypeScript:

```dart
let count: int;
var count: int;
```

Because `count` has a type the compiler knows what we are and are not allowed to do with its value:

```dart
// Allowed: addition
nextCount = count + 1;

// Error: count is not of the type any()|any[]
x = count.map { 3; };
```

You can cast (convert a value from one type to another) with the `as` keyword or constructor function.

```dart
someValue = "this is a string"; // assigned 'str'
strLength: int = len (someValue as str);
```

Another is through using constructor functions:

```dart
someValue = "this is a string";
strLength: int = len str(someValue);
```

## Null and Undefined

### Void, Null and Undefined

Both `undef` and `null` actually have their **own** types, but they’re not extremely useful on their own.

`undef` is the default value assigned to a variable, or the value returned from function calls, while `null` is the value which you assign explicitly.

```dart
// Not much else we can assign to these variables!
u: undef = undef;
n: null = null;
```

`void` is a type alias, and `void == null | undef`.

```dart
warnUser(): void {
  print "This is my warning message";
}
```

So declaring variables of type `void` is not useful because you can only assign `null` or `undef` to them:

```dart
unusable: void = undef;
unusable = null;
```

## Boolean

A boolean is either one of two values, `true` and `false`, and has the type `bool`. As in YAML, `on` `and` yes are the same as boolean `true`, while `off` and `no` are boolean `false`.

```dart
isDone: bool := false;
```

Logical and comparison operators such as `!`, `&&`, `||`, `<`, `>`, `<=`, `>=` are retained.

```dart
!true // false
true && false // false
true || false // true
```

We do provide a few more, such as the xor operator `^^`.

`&&`, `||` and `^^`, and their infix forms `and`, `or` and `xor`, have their own inverses: `!&`/`nand`, `!|`/`nor` and `!^`/`xnor`.

```dart
false ^^ true  // true
false ^^ false // false
1 ^^ 0         // 1
1 ^^ 1         // false
```

`==` and `!=` in Eliph compile to `===` and `!==` in JavaScript.

If you really want to use JavaScript's `==` and `!=`, use the _fuzzy equality_ operators `=~` and `!~` instead.

## Numbers

In JavaScript, all numbers are either floating point values or (big) integers. These floating point numbers get the type `float`, while integers simply get `int`.

`int` literals have no `.`, whereas `float`s have. `int`s also can end in `n`, of which explicitly tell the compiler it is a `bigint`.

The basic operations `+`, `-`, `*` and `/` work the same way as in JS, and you can use parentheses `()` in grouping your expressions:

```dart
2 + 2 // 4
50 - 5 * 6 // 20
(50 - 5 * 6) / 4 // 5.0
8 / 5 // 1.6
```

Regular division with `/` will evaluate to a `float`, but floor division with `~/` will return `int`. Operators with mixed type operands convert the evaluated result to `float`:

```dart
4 * 3.75 - 1;
```

```dart
17 / 3; // 5.666666666666667
17 ~/ 3; // 5
17 % 3; // 2
5 * 3 + 2; // 17
```

Bitwise operations such as unary `~`, infix `&`, `|` and `^` (and their inverses `~&`, `~|`, `~^`), and shift operators `<<`, `>>` and `>>>` will evaluate into `int`, no matter the type.

```dart
5 & 1; // 1
5 | 1; // 5
5 ^ 1; // 4
~5; // 10
5 << 1; // 10
5 >> 1; // 2
5 >>> 1; // 2
```

`%%` provides dividend-dependent modulo:

```dart
-7 % 5 == -2; // The remainder of 7 / 5
-7 %% 5 == 3; // n %% 5 is always between 0 and 4
```

Radix literals can be created using prefixes `0x`, `0o`, `0b`. Literals can be broken up using the `_` character which will be ignored. Leading 0s are also ignored.

```dart
dec = 6.;
hex = 0xf00d;
binary = 0b1010;
octal = 0o744;

billion = 1_000_000_000;
```

The minimum/maximum operators `<?` and `>?`, which return the smaller or larger of the two operands.

```dart
3 <? 10; // 3
3 >? 10; // 10
```

PHP's "spaceship" operator `<=>`, returns either `1`, `0` or `-1` depending on whether the number on the left is greater than, equal to or lesser than the right.

```dart
3 <=> 1; // 1
1 <=> 3; // -1
2 <=> 2; // 0
```

Bases 2 to 64 can be used, as long as they contain any combination of the below digits, are surounded in brackets and suffixed with the base.

```
0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ$&
```

```dart
i = '105'6; // 41
```

## Characters and Strings

Characters, of type `char`, enclosed in ` `` `, are strings of length 1. They can be converted into integers with `int()`, and concatenated with `+` or repeated with `*` to form strings.

```dart
a: char = `a`;
```

As in other languages, we use the type `str` (not `string`) to refer to these textual datatypes. Just like JavaScript, Eliph also uses double quotes `"` or single quotes `'` to surround string data.

```dart
color: str = 'blue';
color = 'red';
```

Both character and single-quoted string literals have special escape syntax, as shown below. Single-quote strings evaluate as-is, and require you to escape some special characters, as shown below:

```dart
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

```dart
author = 'Wittgenstein'
quote = "A picture is a fact. -- #author"
sentence = "#{22 / 7} is a decent approximation of π"
```

In single-quoted strings, lines are joined by a single space unless they end with a backslash. Indentation is ignored.

```dart
mobyDick = 'Call me Ishmael. Some years ago --
  never mind how long precisely -- having little
  or no money in my purse, and nothing particular
  to interest me on shore, I thought I would sail
  about a little and see the watery part of the
  world...'
```

Strings can be concatenated `+`, replaced `-`, repeated `*`, sliced or split `/` with arithmetic operators.

Use `*` to join strings back from arrays `[]` or tuples `()`, where the right operand is the delimiter. This operation will convert all non-strings (including `char`s) into strings.

```dart
s: str = 'Hello';

// Concatenating strings together
s = 'Hello' + 'World!' // 'Hello World!'
s = 'Hello'

// Replacing strings by substring or regex
s = 'Hello' - `l`; // 'Heo'
s = 'Hello' - (/llo$/, 'lp me'); // 'Help me'
// (calls String.replace() with the right operand)

// Splitting
t: str[] = s / 1; // ['H', 'e', 'l', 'l', 'o']
t = s / [2, 3]; // ['He', 'llo']
t = s / ''; // ['H', 'e', 'l', 'l', 'o']

// Splitting with spread operator
c: char[] = [...s]; // [`h`, `e`, `l`, `l`, `o`]

// Joining
strArr = ['H', 'e', `l`, 'l', 'o'];
strArr = strArr * ''; //  'Hello'
```

Use the `len` operator to retrieve the length of a string:

```dart
strLen = len 'hello' // 5
```

Strings are **modulo and zero-indexed**. Basically, indices can go on forever, but this does **not** mean the string has infinite length.

When accessing **integer** indices in a string (or other sequential data structure such as arrays and tuples), they always are accessed modulo `%%` the length of the string.

- `0` is the first index, `1` is the second, and so on
- Indices can count backward: `-1` is the last, `-2` is second last and so on

So given a string `s` of length `5`,

| False index | -7  | -6  | -5  | -4  | -3  | -2  | -1  | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| True index  | 3   | 4   | 0   | 1   | 2   | 3   | 4   | 0   | 1   | 2   | 3   | 4   | 0   | 1   | 2   |

or to put it more simply, `... s[5] == s[0] == s[-4] == s[-9] ...`.

Use commas to retrieve individual indices of strings, and combinations of `<>` and `:` to extract ranges of substrings from strings. More on #Ranges. This means, you can repeat substrings multiple times until a certain length.

Much like JavaScript objects and maps, arrays and tuples do have keys (their **numeric** index) and values (which are the values you see on the screen), You can use `in` or its inverse `!in` to test whether a substring or character is in a string.

```dart
'34' in '12345' // true
`3` in '12345' // true

'34' !in '12345' // false
`3` !in '12345' // false
```

`of` returns `true` if and only if the number passed in is a **non-negative integer** and between 0 and the last index (1 less than the length of the string).

```dart
3 of '12345' // true
-1 of '12345' // false
```

Similarly, the `index()` function, similar to `indexOf()` in JavaScript, will always return a **non-negative integer** between 0 and the last index.

```dart
str = '12345'
str.index(4) // 5
```

## Regular Expressions

A regular expression is an object that describes a pattern of characters. Regular expressions have the type `regex` are used to perform pattern-matching and "search-and-replace" functions on text.

You construct a regular expression in one of two ways:

Using a regular expression literal, which consists of a pattern enclosed between slashes, as follows:

```dart
patt: regex = /w3schools/i
```

or surround your pattern in a set of slashes, to turn it into a **block regular expression**. `/\/`. You can interpolate and transform variables and embed code and expressions, by using the hash interpolation syntax `#{expression}` and `#variable` described earlier.

```dart
patt: regex = /\/
w3schools
/\/i
```

Eliph (aims to) natively support(s) the regex definitions in XRegExp, which is a superset of JavaScript regular expressions, as well as most of the features as described in [RegularExpressions.info](https://www.regular-expressions.info/). The following tables below is actually a cheat sheet and is taken from [this Perl documentation](https://perldoc.perl.org/perlre), but with some edits.

```
           PURPOSE                                  WHERE
\   Escape the next character                    Always, except when
                                                 escaped by another \
^   Match the beginning of the string            Not in []
      (or line, if /m is used)
^   Complement the [] class                      At the beginning of []
.   Match any single character except newline    Not in []
      (under /s, includes newline)
$   Match the end of the string                  Not in [], but can
      (or before newline at the end of the       mean interpolate a
      string; or before any newline if /m is     scalar
      used)
|   Alternation                                  Not in []
()  Grouping                                     Not in []
[   Start Bracketed Character class              Not in []
]   End Bracketed Character class                Only in [], and
                                                   not first
*   Matches the preceding element 0 or more      Not in []
      times
+   Matches the preceding element 1 or more      Not in []
      times
?   Matches the preceding element 0 or 1         Not in []
      times
{   Starts a sequence that gives number(s)       Not in []
      of times the preceding element can be
      matched
{   when following certain escape sequences
      starts a modifier to the meaning of the
      sequence
}   End sequence started by {
-   Indicates a range                            Only in [] interior
//  Beginning of comment, extends to line end    Only with /x modifier
/*  Beginning of end comment                     Only with /x modifier
*/  End of block comment                         Only with /x modifier
```

Quantifiers

```* Match 0 or more times
+           Match 1 or more times
?           Match 1 or 0 times
{n}         Match exactly n times
{n,}        Match at least n times
{n,m}       Match at least n but not more than m times

*?        Match 0 or more times, not greedily
+?        Match 1 or more times, not greedily
??        Match 0 or 1 time, not greedily
{n}?      Match exactly n times, not greedily (redundant)
{n,}?     Match at least n times, not greedily
{n,m}?    Match at least n but not more than m times, not greedily

*+     Match 0 or more times and give nothing back
++     Match 1 or more times and give nothing back
?+     Match 0 or 1 time and give nothing back
{n}+   Match exactly n times and give nothing back (redundant)
{n,}+  Match at least n times and give nothing back
{n,m}+ Match at least n but not more than m times and give nothing back
Characters

\t          tab                   (HT, TAB)
\n          newline               (LF, NL)
\r          return                (CR)
\f          form feed             (FF)
\a          alarm (bell)          (BEL)
\e          escape (think troff)  (ESC)
\cK         control char          (example: VT)
\x{}, \x00  character whose ordinal is the given hexadecimal number
\N{name}    named Unicode character or character sequence
\N{U+263D}  Unicode character     (example: FIRST QUARTER MOON)
\o{}, \000  character whose ordinal is the given octal number
\l          lowercase next char (think vi)
\u          uppercase next char (think vi)
\L          lowercase until \E (think vi)
\U          uppercase until \E (think vi)
\Q          quote (disable) pattern metacharacters until \E
\E          end either case modification or quoted section, think vi
```

Character Classes

```
Sequence   Description
[...]      Match a character according to the rules of the
              bracketed character class defined by the "...".
              Example: [a-z] matches "a" or "b" or "c" ... or "z"
[[:...:]]  Match a character according to the rules of the POSIX
              character class "..." within the outer bracketed
              character class.  Example: [[:upper:]] matches any
              uppercase character.
(?[...])    Extended bracketed character class
\w          Match a "word" character (alphanumeric plus "_", plus
              other connector punctuation chars plus Unicode
              marks)
\W          Match a non-"word" character
\s          Match a whitespace character
\S          Match a non-whitespace character
\d          Match a decimal digit character
\D          Match a non-digit character
\pP         Match P, named property.  Use \p{Prop} for longer names
\PP         Match non-P
\X          Match Unicode "eXtended grapheme cluster"
\1          Backreference to a specific capture group or buffer.
              1 may actually be any positive integer.
\g1         Backreference to a specific or previous group,
\g{-1}      The number may be negative indicating a relative
              previous group and may optionally be wrapped in
              curly brackets for safer parsing.
\g{name}    Named backreference
\k<name>    Named backreference (ES6 syntax)
\K          Keep the stuff left of the \K, don't include it in $&
\N          Any character but \n.  Not affected by /s modifier
\v          Vertical whitespace
\V          Not vertical whitespace
\h          Horizontal whitespace
\H          Not horizontal whitespace
\R          Linebreak
Assertions

\b{}   Match at Unicode boundary of specified type
\B{}   Match where corresponding \b{} doesn't match
\b     Match a \w\W or \W\w boundary
\B     Match except at a \w\W or \W\w boundary
\A     Match only at beginning of string
\Z     Match only at end of string, or before newline at the end
\z     Match only at end of string
\G     Match only at pos() (e.g. at the end-of-match position
       of prior m//g)
```

## Ranges

There are also range literals, like in swiftScript, Kotlin or Swift, for example, `[1,2,3]` or `[1:100:1]`.

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

- Each iteration alternates between adding `c` and `d` to `a`, until reaching and hitting `b`.
- Algebraically, this is equivalent to `[a, a + c, a + c + d, a + 2c + d, a + 2c + 2d, a + 3c + 2d, a + 3c + 3d ... b]`

Some things to note:

- If the range counts **out of bounds**, it will coerce that to count in the right direction. `c + d > 0 && a > b || c + d < 0 && a < b`, then all numbers following `a` and `b` will be negated: `c` would be `-c` and `d` `-d`.

**Slicing and splicing** allow you to retrieve and override elements in tuples and arrays, or individual `char`s in strings, using the same notation above.

Slice syntax is always enclosed in `[]` immediately after the literal or variable, like how we would access arrays or objects in JS.

The placeholder `$` stands for the length of the array or string it refers to.

```dart
c = 'hello'; // Slicing
s = c[1]; // e
s = c[1,2]; // el (specific indices)
s = c[:>$]; // hello (string cloning)
s = c[$>:]; // olleh (specific indices)
```

When splicing, each individual index must be assigned a literal value, and for subranges a tuple of values.

- `a=1,b=2` - Assign `1` to index `a` and `2` to `b`.
- `a::b:c=<1,2>` - Assign to every index evaluated by the range expression `a::b:c`, alternating between values `1, 2`, in order of appearance.

```dart
t = '123'; // Splicing
t = t + '45'; // '12345'
t = t * 2; // '1234512345'
t = '12345'[$>:]; // '54321'
t = '12345'[-1='6']; // '123456'
```
