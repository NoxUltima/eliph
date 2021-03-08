# Disclaimer

This language is but a **concept**. The Standard Library and Compiler and everything else will be released soon (perhaps a few years from now). I need time to work on it and get my college and uni settled. I wrote this document a few months ago.

# Eliph

**Eliph** is the language for folks who don't necessarily love JavaScript, but who still acknowledge its importance in the ecosystem.
It embraces the full feature set of JavaScript, and also extends it with new and improved features, so to improve the readability and brevity of traditional JavaScript code.

It compiles to the highest quality of clean, readable and performant JS, directly runnable in browsers and Node. This means you can pick up Eliph and access the vast JS ecosystem and tooling as if you've known it for a long time!

If you have an existing TypeScript or ReScript codebase, Eliph code can be compiled to both of these languages allowing you to slip it in any codebase almost unnoticed. The output preserves the general code structure, as all of the extra features that go along with Eliph is declared at the bottom of the file. Types would be inserted and inferred whenever necessary.

```coffee
query = select user.id from user
  where user.name == 'boom' && user.id == 1
    || user.name == 'bang' && user.id == 2
```

Eliph has:

- a syntax similar to Nim, Ruby, OCaml, LiveScript, CoffeeScript, Bash, Julia and Elixir;
- semantics, features and operators similar to F#, Crystal, Haskell, PureScript and Elm;
- functions and modules based mostly on JavaScript (NPM such as Lodash, Ramda, Math.JS and more), as well as core and community libraries from Python and Ruby.

## Why Eliph?

Eliph aims to be a more concise cousin to the JavaScript language by introducing new concepts, functions and symbols implemented in other programming languages, making it easier to write code with fewer characters and more "syntactic sugar". This would make code typically written in tens or hundreds of lines much more readable and compact and allows you to write expressive code without redundant or verbose boilerplate.

A necessary component of the language and its design has to do with its concise syntax: employing the right balance of words and symbols and minimizing the overuse of brackets and perhaps all the typable keys in the keyboard. So to simplify things, we do remove a number of things, although they really can be seen as optional.

[coffeescript]: https://coffeescript.org/
[wtfjs]: https://github.com/denysdovhan/wtfjs
[stdlib]: https://stdlib.io/
[npm packages]: https://medium.com/@thomasfuchs/what-if-we-had-a-great-standard-library-in-javascript-52692342ee3f

**_Lagom_**. We deem curly braces, semicolons and even commas as unnecessary. Sometimes that applies too for parentheses. The only times you would need them are when you want to cram things into a single line. Some of the more unnecessary things that really become a big hassle for developers like me, such as verbosity, word length and excessive use of punctuation, have been removed.

- **Shortened keyword and function names**: `function -> func`, `instanceof -> instof`, `extends -> from / of`, `implements -> with`
- **Unnecessary punctuation have been removed**, such as semicolons `;`, commas `,`, and parentheses `()` in statements like `if ()` and `for ()`.
- **Everything is an expression**, and can be assigned to variables and returned from functions, which includes control flow statements like `if`, `for` and `try`.
- **Optional declarations** with `var`, `let` or `const` are only allowed when initializing a variable without a value or one in a loop.
- **Implicit returns**: the last statement is automatically returned from a `do`-block (closure) or a function, unless otherwise specified with `return`.

**Static and robust**. JavaScript has a complete lack of types. It's also notorious for its [peculiar runtime behaviour][wtfjs], which can lead to unexpected and sometimes annoying side effects. TypeScript kind of _solves_ this, by adding static and inferred types to the language, but this doesn't change the fact that it inherits all of JavaScript's problems.

- Types in Eliph are **automatically inferred.** You don't need to explicitly assign a type to a variable. Use `any` or `dyn` to disable type-checking.
- You can annotate **anywhere** within your code, such as the types of variables and function parameters, object values, return types, and even within expressions, so you can assure yourself that you really know what you're doing.
- **A type should not change into another.** In JavaScript, your variable's type might change when the code runs, hence causing a wide range of side-effects.
- **A type system that is sometimes incorrect can be dangerous** due to expectation mismatches.
- **Types are erased after compilation** and don't exist at runtime. They are detected at compile time and will get reported in your IDE.

**Dependency-free**. Eliph aims to provide a suite of built-in classes, methods and functions from its source code on the fly, so there is no need for you to litter your code and ship your product with loads of utility functions and algorithms (unless you're tailoring your own for the job).

That's why we're trying to encode and consolidate these utility functions into a **standard library** (inspired by languages like Python, Ruby and Go). We feel we don't want to drag a lot of our dead code into our final codebase, when we can just take the ones we need.

- Eliph can be used directly on Node.JS and even has its own standalone library with no dependencies, `@eliph/stdlib`. The code is automatically formed or imported from the compiler.
- The standard library also can be used with virtually any language that compiles to javascript, allowing for smooth interop.

**One-to-one mapping**. Unreadable boilerplate JS code generated from other compiled-to-JS languages makes it so that it could be, practically speaking, hard to debug, hard to learn from and hard to integrate with existing JS.

For Eliph, we try to make sure that we preserve much of Eliph's syntax in the output, rather than try to cram boilerplate code in the middle of the output. This is especially important while learning, where users might want to understand how the code's compiled, and to audit for bugs.

- All **JS features** are preserved. Some mappings are less obvious, and may require some reordering of terms. This is all taken care by the compiler.
- **Comments** are always preserved in the final output, even within interpolated strings and block regular expressions.
- **Type annotations** are not "removed" from the output. Mainly, they exist as comments, if the compiled language does not have any types. They are distinguished separately from regular comments.
- **Built-in and standard functions** are generated as prototype methods and functions at the top of the file, along with any import statements.
- **Variables** with illegal identifier names, keyword names or variables that would eventually be deleted with `del`, are declared with an object at the top of its scope (if there are any) and accessed from that object.

---

## History of Eliph

Eliph first began as a side gig in early 2020 when I developed algorithms and programs in Python and JavaScript during my free time. However, as I've gotten used to programming in JavaScript, and previously developed a lot of programs in Python, but having to go over to Stack Overflow and manually searching for the exact functions in my code, which uses highly specialised Python functions and libraries unavailable and difficult to find in JS.

Also, the functions which JavaScript offers are often too difficult to understand and may usually require some further explanation to comprehend after looking at the documentation. As I grew deeply obsessed with programming in JS due to the idea that one can design and develop everything they imagine using only one language, this lead me to pursue a goal of creating a new language that blends the simplicity and ease of Python with the malleability of JavaScript, along with syntaxes and operations inspired by different programming languages.

Many programming languages and frameworks often have adequate language support in integrated development environments. Language support is a fancy term for things like code snippets, syntax highlighting, boilerplate, documentation, language references and even a big ecosystem of plugins, packages and Stack Overflow developers.

## Roadmap

- Documentation
- Standard library
- Syntax highlighting
- Compiler and Formatter
- Linter and debugger

### Documentation

The roadmap for developing the language has to start with the documentation, as that would give me a head start on the grammatical and syntactic features of the language. The documentation will be written with Markdown, which would explain the features, grammar, functions and modules in the language and its core library, and explain the similarities and differences between it and other programming languages.

### Syntax Highlighting

The next pattern is to do the syntax highlighting for the language. Syntax highlighting displays text, especially source code, in different colours and fonts according to the category of terms, while visually distinguishing structures and syntax errors.

Code is parsed through a series of regular expressions, and each match is assigned a scope. These scopes are mapped to colors in stylesheets and themes in code editors and syntax highlighting engines in code editors.

Highlighting can be fine-tuned through the use of custom code, such as highlighting bracket encapsulations or indentation depth, HTML/XML tags and attributes, variable, function or class names, or even allowing for including other languages inside the code.

---

# Table of Contents

[awesomejs]: https://github.com/sorrycc/awesome-javascript/
[awesomenode]: https://github.com/sindresorhus/awesome-nodejs
[awesomepy]: https://github.com/vinta/awesome-python

1. A Formal Introduction
2. The Basics
   1. Your First Program
   2. Code Structure
   3. Comments
   4. Keywords
   5. Embedding Raw Code
3. Variables
   1. `var`, `let`, `const`
   2. Shorthands
4. Constants and literals
   1. Basic data types
   2. `null` and `undef`
   3. Booleans `bool` and their operations
   4. Numbers
      1. Integers `int` and floating points `float`
      2. Arithmetic and bitwise operations
      3. Fractions `frac`
      4. Decimals `deci`
      5. Complex Numbers `comp`
   5. Strings `str` and characters `char`
      1. String Operations
      2. Templates
      3. Basic and Extended Slicing
   6. Regular Expressions
   7. Ranges, Sequences and Comprehensions
      1. Literals `[a<:b:c,d]`
      2. Array and Object Comprehensions
5. Data Structures
   1. Tuples `()` and Arrays `[]`
   2. Objects `{}` and Records `(| |)`
   3. Maps `{| |}` and Sets `[| |]`
   4. Weak Sets `#[]` and Maps `#{}`
   5. Destructuring assignment
6. Control Flow
   1. The `do` block, closures and `pass`
   2. Decision Making
      1. `if`, `elif`, `else`, `unless`, `elun`
      2. `guard-else`
   3. Loops
      1. Range, `for-in`, `for-of` and `for-from`
      2. `break` and `continue`
      3. `while` and `until`; `repeat-while` and `repeat-until`
      4. Infinite `loop`
   4. Switch
      1. Basic (conditional) `switch`
      2. Multiple cases and half-expressions
      3. `break` and `fallthru`
      4. Pattern matching
   5. Error handling
      1. `try-catch-finally`
      2. Multiple `catch` statements
   6. `label` and `goto`
7. Functions
   1. `func` declaration
   2. Recursion
   3. Generators
   4. First-class functions
   5. Composition
   6. Piping
   7. Currying
8. Types
   1. `any`, `void`, `unknown`, `other` and `never`
   2. Type aliases
   3. Literal types
   4. Unions and intersection types
   5. Interfaces
   6. `enum`
      1. Default
      2. Ranged Values
      3. Non-Numeric Values
9. Classes
   1. Constructors and instances
   2. Methods and attributes
   3. Inheritance and mixins
   4. Access modifiers
10. Modules
    1. Import and export
    2. Using NPM modules
    3. Namespaces
