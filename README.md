# This is Zenith.

A new language based on JavaScript (JS) and Python, and compiles to JS, expanded and modified with lots of new shorthands and alternative syntaxes inspired by newer programming languages such as Haskell, Elixir, Swift, Scala, Go and Dart, including those which compile to JavaScript, such as CoffeeScript, LiveScript and more.

## History of the language

The language first started out as a mixture of JS and Python. I used to develop algorithms during my free time using Python at the time but eventually switched to JS and proceeded to translate them by hand in JS, hoping to use them in my web development projects in college.

However, I found out that many of the functions and features which Python had, such as the `random` and `string` libraries, `range()`, tuples and array comprehensions, did not exist in JS. And since these are completely different languages designed for different goals in mind, so I had to painstakingly figure out how to produce exactly the same code in either language, which I resorted to doing in Stack Overflow.

This lead me to create a new way to produce an entire library to bring Python functions to be used in the JS context. But since I have gotten used to web development and hence JS programming a lot, I wanted to create a new language that would combine the features of both languages, along with ways to improve interoperability with different paradigms such as mobile and game development.

## An informal introduction

### Sample boilerplate code

```
main() { // main function is optional
    print('Hello world!')
}
> Hello world!
```

## Hybrid Typing

Zenith is dynamically typed, just like Python and JS, in order to save time typing. Zenith also has the type identifier, which is used for assigning explicit typing standards for certain variables and prevent them from being reassigned a value of a different type.

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

There is also a shorthand way of writing numbers (only integers) in bases from 2 to 64. Bases from 10 to 36 use the decimal numerals appended with letters from the English alphabet, and can be written in mixed case, while bases higher than 36 use the Greek alphabet and each digits has to be lowercase:
Base 64: `0123456789abcdefghijklmnopqrstuvwxyzαβγδεζηθικλμνξπρσςτυφχψωϙϛϝϸ`

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

Arrays work in a similar fashion in Javascript and as lists in functions.

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
|      `removeAll()`       |   many    | deletes and returns all instances of a value as an array |
|    `get()`, `index()`    |     1     |          returns the value at a specified index          |
|   `set()`,`replace()`    |     2     |        replaces a value at its index with another        |
|   `clear()`, `empty()`   |     0     |                     empties an array                     |
|         `fill()`         |   many    |          overrides an array with the same value          |
|      `replaceAll()`      |     2     |      replaces all values in the array with another       |
|       `reverse()`        |     0     |               reverses the array in place                |
|       `shuffle()`        |     0     |               shuffles the array in place                |

Many of the built-in array functions in JavaScript remain unchanged in Zenith.

### Operators

Expression syntax is straightforward: the operators `+`, `-`, `*` and `/` work just like in most other languages (for example, Pascal or C); parentheses `(())` can be used for grouping. For example:

```
2 + 2 -> 4
50 - 5 * 6 -> 20
```

Division will only return a float regardless of the operands.

```
(50 - 5 * 6) / 4 -> 5.0
8 / 5 -> 1.6
```

To do floor division and get an integer result, you can use the `#` operator; to calculate the remainder (modulo) you can use `%`:

```
17 / 3 // 5.66666666667
17 # 3 // 5
17 #: 3 // 6 (rounding division)
17 #! 3 // 6 (ceiling division)
17 % 3 // 2
5 * 3 + 2 // 17

// True modulo
a %% b // => (a % b + b) % b
```

Like JS bitwise operators also exist:

```
& = bitwise AND
| = bitwise OR
~ = bitwise NOT
^ = bitwise XOR
@ = bitwise XOR
<< = bitwise left shift
>> = bitwise right shift
<<< = bitwise unsigned left shift
>>> = bitwise unsigned right shift
~~ = double bitwise NOT, alternative to floor function
```

```
2357 ^ 4567 // 2
~4093 // -4094
~~1.3 // 1
```

To calculate exponents you can use the `**` operator:

```
5 ** 2 // 25
2 ** 10 // 1024
```

There is full support for floating point; operators with mixed type operands convert the integer operand to floating point:

```
4 * 3.75 - 1 // 14.0
```

Comparison operators are quite similar to Python, including the use of the `is` operator. They evaluate to boolean functions.

```
== -> equal to
===
<> -> not equal to
< -> less than
> -> greater than
<= -> less than or equal to
>= -> more than or equal to

a < b < c -> equations can be chained like this as well
```

### Comments

Comments work the same as in most languages like the C family, Java and JS, however with some notable differences:

```
    // This is a single-line comment
    /* This is a multi-line comment */
   /**
    * This is a Javadoc comment
    * @param | is cool
    */
```

However other comment types are also permitted:

```
<!-- HTML comments work too here -->
|- This is a single-line comment
|= This is a single-line comment
||- This is a single-line comment
||= This is a single-line comment
|- This is a multi-line comment -|
|= This is also a multi-line comment =|
Comments can also be nested within arrows too,
which are multi-line comments themselves:
<<- This is cool ->>
<<= This is also cool =>>
```

### Loops

```
for () {
    for () {
        for () {
        }
    }
}

for (a = 0, b, c)

while (true) {

}
```

### Mathematical Operations
