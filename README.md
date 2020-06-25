# This is Zenith.

A new language based on JavaScript (JS) and Python, and compiles to JS, expanded and modified with lots of new shorthands and alternative syntaxes inspired by newer programming languages such as Haskell, Elixir, Swift, Scala, Go and Dart.

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
64_000km -> 64000
64e3 -> 64000
```

There is also a shorthand way of writing numbers (only integers) in bases from 2 to 64. Bases from 10 to 36 use the decimal numerals appended with letters from the English alphabet and can be used to write js functions which can :
Base 64: `0123456789abcdefghijklmnopqrstuvwxyzαβγδεζηθικλμνξπρσςτυφχψωϙϛϝϸ`

```
1000001b1 -> 65
41b16 -> 65
1tb36 -> 65
15b60 -> 65
11b64 -> 65
```

For any base larger than 64, digits are either separated by dots or underscores.

### Strings

Zenith can also manipulate strings, which can be expressed in several ways. They can be enclosed in single quotes `'...'` (evaluated by default) or double quotes `"..."` with the same result 2. The backslash `\` is used to escape quotes.

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
- Unicode characters:`\4-digit codepoint` or `\{5-digit codepoint}`, such as `\ud83d`, or `\u{1f680}`

```
> 'hello' == 'hell\u{6f}'
true
```

If you don't want characters prefaced by \ to be interpreted as special characters, you can use raw strings by encasing your string in backticks, like this. Which means, strings can now span multiple lines. Except `\`.

```
> print(`Hello,
world!`)
`Hello,
World!`
> print("Hello," + '\nworld!')
`Hello,
World!`
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

String interpolation is a way to construct a new string from a mix of constants, variables, literals, and expressions by including their values inside a string literal.

```
var m = 3, message = `${m} times 2.5 is ${m * 2.5}`
'3 times 2.5 is 7.5'
```

Characters and strings are not differentiated.

```
> var word = 'Zenith'
> word[0]
'Z'
> word[5]
'h'
```

Indices may also be negative numbers. Negative indices start from -1.

```
var word = 'Zenith'
word[-6] == 'Z'
word[-1] == 'h'
```

In addition to indexing, slicing is also supported. While indexing is used to obtain individual characters, slicing allows you to obtain substrings:

```
> word[0:2] // Characters from position 0 (included) to 2 (excluded)
'Ze'
> word[2:5] // Characters from position 2 (included) to 5 (excluded)
'nit'
```

Note how the start is always included, and the end always excluded. This makes sure that `s[:i] + s[i:]` is always equal to `s`:

```
> word[:2] + word[2:]
'Zenith'
> word[:4] + word[4:]
'Zenith'
```

Strings cannot be changed - they are immutable. Therefore, assigning to an indexed position in the string results in an error. If you need a different string, you should create a new one:

```
> 'Nadir' + word[1:]
'Nadirenith'
```

The built in property `.len`, `.size` or `.length` returns the length of a string, as well as the functions `len()`, `size()` or `length()`:

```
> 'supercalifragilisticexpialidocious'.length
34
```

### Operators

Expression syntax is straightforward: the operators `+`, `-`, `*` and `/` work just like in most other languages (for example, Pascal or C); parentheses `(())` can be used for grouping. For example:

```py
2 + 2 // 4
50 - 5 * 6 // 20

// Division will only return a float
// regardless of the types
(50 - 5 * 6) / 4 // 5.0
8 / 5 // 1.6
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
<< = bitwise left shift
>> = bitwise right shift
<<< = bitwise unsigned left shift
>>> = bitwise unsigned right shift
~~ = double bitwise NOT, alternative to floor function
```

```
2357 @ 4567 // 2
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

### Arrays

The language knows number of compound data types, used to group together other values. The most versatile is the array, which can be written as a list of comma-separated values (items) between square brackets. Arrays might contain items of different types, but usually the items all have the same type.

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

Arrays can be dequed, and a variety of methods can be used. When removing value(s) from the array, the method would return the removed value(s).

```
var arr = [1, 2, 3, 4, 5]
arr.push(6) or arr.append(6) // adds a new value to the end of the array
> [1, 2, 3, 4, 5, 6]
arr.pop() // removes the last value from the array
> [1, 2, 3, 4, 5]
arr.unshift(0) // adds a new value to the start of the array
> [0, 1, 2, 3, 4, 5]
arr.shift() // removes the first value from the array
> [1, 2, 3, 4, 5]

arr.add('3', 2) // adds an value at a specified index. If the second argument is not passed, the element is added to the end of the array.
> [1, 2, '3', 3, 4, 5]
arr.remove('3') // deletes the first instance of a value
> [1, 2, 3, 4, 5]

var arr = [1, 2, 3, 4, 5]
arr.get('3') // returns the value specified. Returns undefined if value does not exist.
> undefined
arr.index(3) // returns the value specified at its index.
> 4
arr.set(2, '2')) // modifies array in place, replacing element with x
> [1, '2', 3, 4, 5]

arr = [1, 2, 3, 4, 4, 4, 5]
arr.removeAll(4) // deletes all instances of a value
> [1, 2, 3, 5]

arr = [1, 2, 3, 4, 4, 5, 4]
arr.removeLast(4) // deletes the last instance of a value
> [1, 2, 3, 4, 4, 5]

arr = [1, 2, 3, 4, 5, 6, 7]
arr.delete(6) // deletes a value based on its index
> [1, 2, 3, 4, 5, 6]


arr.clear() // clears the entire array
> []

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
