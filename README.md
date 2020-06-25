# This is Zenith.

A new language based on JavaScript (JS) and Python, and compiles to JS, expanded and modified with lots of new shorthands and alternative syntaxes inspired by newer programming languages such as Haskell, Elixir, Swift, Scala, Go and Dart, including those which compile to JavaScript, such as CoffeeScript, LiveScript and more.

## History of the language

The language first started out as a mixture of JS and Python. I used to develop algorithms during my free time using Python at the time but eventually switched to JS and proceeded to translate them by hand in JS, hoping to use them in my web development projects in college.

However, I found out that many of the functions and features which Python had, such as the `random` and `string` libraries, `range()`, tuples and array comprehensions, did not exist in JS. And since these are completely different languages designed for different goals in mind, so I had to painstakingly figure out how to produce exactly the same code in either language, which I resorted to doing in Stack Overflow.

I wanted to create a new way to produce an entire library to bring Python functions to be used in the JS context. But since I have gotten used to web development and hence JS programming a lot, I wanted to create a new language that would get the best of both worlds, as well as combining features which I had liked from different languages, so that seasoned programmers in these languages won't have a steep learning curve.

## Basics

### Sample boilerplate code

Straight outta Python. Just a simple Hello World program.

```
print('Hello world!')
> Hello world!
```

### Hybrid Typing

Zenith is dynamically typed, just like Python and JS, in order to save time typing. Zenith also has the type identifiers from Java and the C family, which is used for assigning explicit typing standards for certain variables and prevent them from being reassigned a value of a different type.

The common data types in TypeScript, are:

- `number`, `string`, `boolean`, `enum`, `void`, `null`, `undefined`/`none`, `any`, `never`, `array`, `object` and `tuple`.

and their equivalent categories in Java:

- `char` under `string`,
- `byte`, `short`, `int`, `long`, `decimal` and `double` and `float` under `number`.

Here's this in action:

```
var f: byte = 255
typeof f
> byte
f = (long) f
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

```
// Python way
var width, height = 20, 30
width * height
> 600
```

And you can swap and reassign the values of the variables in one line like so:

```
var width = 20, height = 30
width, height = height, width
width, height > 30, 20
```

### Comments

Comments work the same as in most languages like the C family, Java and JS. No comment on that (pun intended.)

```
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

```
var binary = 0b1010
var octal = 0o12
var decimal = 10
var duodecimal = 0zx // (0123456789xe, 0123456789te or 0123456789ab)
var hexadecimal = 0xa
```

Underscores and appended letters are ignored. Letters can also be used inside literals

```
64_000 -> 64
640km -> 64
64_000km -> 64000
64e3 -> 64000
```

There is also a shorthand way of writing numbers (only integers) in bases from 2 to 64. Bases from 10 to 36 use the decimal numerals appended with letters from the English alphabet, and can be written in mixed case, while bases higher than 36 use the Greek alphabet (with four extra symbols), where each non-numeral digit has to be lowercase.

The base 64 digits are: `0123456789abcdefghijklmnopqrstuvwxyzαβγδεζηθικλμνξπρσςτυφχψωϙϛϝϸ`

```
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

```
1000001b1 -> 65
41b16 -> 65
1tb36 -> 65
15b60 -> 65
11b64 -> 65

akalib36 -> 17743014
13θπγb64 -> 17743014
```

For any base larger than 64, digits are either separated by dots or underscores.

```
1_3_43_50_38b64 -> 17743014
1.3.43.50.38b64 -> 17743014
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

```
// single quotes
'spam eggs' == "spam eggs"
// use \' to escape the single quote
// or use double quotes instead
'doesn\'t' == "doesn't"
// Why not both?
'"Yes," they said.' == "\"Yes,\" they said."
'"Isn\'t," they said.' == "\"Isn't\", they said."
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

```
> 'hell\u{6f}'
'hello'
```

If you don't want characters prefaced by \ to be interpreted as special characters, you can use raw strings by encasing your string in backticks (``), like this.

```
> print(`Hello,
world!`)
'Hello,\nworld!'
> print("Hello," + '\nworld!')
'Hello,\nworld!'
```

Two or more strings next to each other are automatically concatenated. Strings can span multiple lines, however are read as one continuous string when there is a backslash at the end of a line.

```
> 'This is already boring. \
Can I take a nap?'
'This is already boring. Can I take a nap?'
```

Strings can be concatenated with the `+` operator, and repeated with `*`:

```
> 'un' * 3 + 'ium'
'unununium'
```

You can merge two strings encased in different quotes: `'Hello ' + "world!" == 'Hello world!'`
If you want to concatenate string variables or a variable and a string, use `+`:

```
> var zen = 'Zen'
> zen + 'ith'
'Zenith'
> var zen = 'Zen'
> zen 'ith'
SyntaxError
```

String interpolation is a way to construct a new string from a mix of constants, variables, literals, and expressions by including their values inside a string literal. All three types of strings, including single and double quoted strings can be interpolated. The syntax for interpolation can be `#{}`, `#[]`, `[]#`, `#[]#` or `${}`.

```
var m = 3, message = "#{m} times 2.5 is #{m * 2.5}"
'3 times 2.5 is 7.5'
```

Characters and strings are not differentiated. Strings and arrays can be indexed as in JS. Operating with strings and arrays are much like Python, including the use of negative indices and string/array slicing or splicing.

```
> var word = 'Zenith'
> word[0] == word[-6] == 'Z'
> word[5] == word[-1] == 'h'
```

Characters from position 0 (included) to 2 (excluded):

```
> word[0:2]
'Ze'
```

Characters from position 2 (included) to 5 (excluded):

```
> word[2:5]
'nit'
```

This is so that `word[:n] + word[n:] == word`

```
> word[:2] + word[2:]
'Zenith'
> word[:4] + word[4:]
'Zenith'
```

Strings cannot be changed - they are immutable. Therefore, assigning to an indexed position in the string results in an error. If you need a different string, you should create a new one:

```
> var nadir = 'Nadir' + word[1:]
> nadir
'Nadirenith'
```

The built in property `.len`, `.size` or `.length` returns the length of a string, as well as their equivalent functions `len()`, `size()` or `length()`:

```
> 'supercalifragilisticexpialidocious'.length
34
```

### Arrays

Arrays work in a similar fashion in Javascript and as lists in Python.

```
squares = [1, 4, 9, 16, 25]
> squares
[1, 4, 9, 16, 25]
```

Like strings (and all other built-in sequence types), arrays can be indexed and sliced:

```
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

```
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
|   `#:`   | arithmetic | `rndiv`  |              _Division with rounding_\*              |   `7 #: 5 = 1, 8 #: 5 = 2`    |
|   `#!`   | arithmetic | `cldiv`  |                   Ceiling division                   |         `7 #! 5 = 2`          |
|   `+.`   | arithmetic |  `pluf`  |               Floating point addition                |        `1 +. 1 = 2.0`         |
|   `-.`   | arithmetic |  `minf`  |              Floating point subtraction              |        `2 -. 1 = 1.0`         |
|   `*.`   | arithmetic |  `timf`  |            Floating point multiplication             |        `3 *. 3 = 9.0`         |
|   `%`    | arithmetic |  `rem`   | Modulus operator - returns remainder of two operands |         `13 % 3 = 1`          |
|   `%/`   | arithmetic | `flmod`  |                    Floor modulus                     |      `12.5 _|_ 0.3 = 0`       |
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
|  `</>`   | arithmetic |  `nrt`   |                       Nth root                       |        `4 <*> 16 = 2`         |
|   `::`   | arithmetic |  `abs`   |                    Absolute value                    |          `::-3 = 3`           |
|   `&`    |  bitwise   |  `land`  |                     Bitwise AND                      |         `5 & 13 = 5`          |
|   `ǀ`    |  bitwise   |  `lor`   |                      Bitwise OR                      |         `5 ǀ 13 = 13`         |
|   `^`    |  bitwise   |  `lxor`  |                     Bitwise XOR                      |         `5 ^ 13 = 8`          |
|   `~`    |  bitwise   |  `lnot`  |                     Bitwise NOT                      |           `~5 = 6`            |
|   `<<`   |  bitwise   |  `lsl`   |                      Left shift                      |         `5 << 3 = 40`         |
|   `>>`   |  bitwise   |  `lsr`   |                  Signed right shift                  |        `40 >> 2 = 10`         |
|  `>>>`   |  bitwise   |  `asr`   |                 Zerofill right shift                 |      `4096 >>> 2 = 256`       |

\*Unary operands. Operators are placed before the operand without space.

### Comparison, Logic and Conditional Operators

These operators produce booleans.

|                              Operator                               |    Type    | Keyword |                Description                 |         Example         |
| :-----------------------------------------------------------------: | :--------: | :-----: | :----------------------------------------: | :---------------------: |
|                                `==`                                 | comparison |  `equ`  |        Equal to (value comparison)         |    `3 == '3': true`     |
|                                `!=`                                 | comparison | `nequ`  |      Not equal to (value comparison)       |     `1 != 3: true`      |
|                                `===`                                | comparison |  `is`   |   Is exactly (value and type comparison)   |     `1 === 3: true`     |
|                                `!==`                                | comparison | `isnt`  | Is not exactly (value and type comparison) |     `2 !== 3: true`     |
|                                `<>`                                 | comparison | `nequ`  |     Not equal to (numeric comparison)      |     `1 <> 3: true`      |
|                                 `<`                                 | comparison |  `lt`   |                 Less than                  |      `1 < 3: true`      |
|                                 `>`                                 | comparison |  `gt`   |                Greater than                |      `3 > 1: true`      |
|                                `<=`                                 | comparison |  `lte`  |           Less than or equal to            |     `3 <= 3: true`      |
|                                `>=`                                 | comparison |  `gte`  |          Greater than or equal to          |     `3 <= 3: true`      |
| `&&`, `/\` | logic | `and` | Logical and | `true && false == false` |
|                             `ǀǀ` , `\/`                             |   logic    |  `or`   |                 Logical or                 | `true ǀǀ false == true` |
|                                 `!`                                 |   logic    |  `not`  |                Logical not                 |    `!true == false`     |
|                               `-ǀǀ-`                                |   logic    |  `not`  |                Logical not                 |   `-ǀtrueǀ- == false`   |

### Template operators

|  Operator  |    Type     |    Keyword     |            Function            |                            Example                            |
| :--------: | :---------: | :------------: | :----------------------------: | :-----------------------------------------------------------: |
|   `? :`    | conditional | `if elif else` | Conditional (ternary) operator |                  `var i = true ? i++ : i--`                   |
| `.= :: .=` | conditional |   `case def`   |          Map operator          |      `var i = 1 .= 'one' :: 2 .= 'two' :: ?. n.toString`      |
| `:= :: :=` | conditional |   `when def`   |        Switch operator         | `var i = 1<i<=3 := 'one' :: 2<2<=3 := 'two' :: ?. n.toString` |

## Functions

## Generators

## Decision-Making

## Loops and Comprehensions

## Property Access

## Classes and Inheritance

## Error-handling

## OOP
