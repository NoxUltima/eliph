# Disclaimer

This language is but a **concept**. The Standard Library and Compiler and everything else will be released soon (perhaps a few years from now). I just need time to work on it, and get my college and uni settled. I written this document a few months ago.

# Eliph

**Eliph** is a language that compiles to JavaScript. The golden rule is, if it looks like JavaScript, it should work _with_ and _like_ JavaScript, and compiles to short, sweet and readable JavaScript code. So it should be seen as an attempt to expose and extend the good parts of JavaScript in a simple way, powered by the increasingly rampant JavaScript ecosystem and its many packages and modules.

The language borrows and blends elements and concepts from different programming languages&mdash;reactive, object-oriented and functional programming. Alright, let's begin. It is a completely new programming language by itself, so you can write more sophisticated code with tons of syntactic sugar and powerful features and a large standard library.

Eliph has a syntax similar to Swift, Go, Reason, Dart and Scala, features and operators similar to Haskell, F#, LiveScript and CoffeeScript, and with functions and modules based on Python and Ruby.

## History of Eliph

Eliph first began as a side gig in early 2020 when I developed algorithms and programs in Python and JavaScript during my free time, but using the former twice as much. However in order to use my Python command line programs in my web development projects I wanted to rewrite my codes in JS, but having to go over to Stack Overflow and manually searching for the exact functions in my code which uses highly specialised Python functions and libraries unavailable and difficult to find in JS.

Also the functions which JavaScript offers are often too difficult to understand and may often require some further explanation to comprehend, after looking at the documentation. As I grew deeply obsessed with programming in JS due to the idea that one can design and develop everything they imagine using only one language, this lead me to pursue a goal of creating a new language that blends the simplicity and ease of Python with the malleability of JavaScript, along with syntaxes and operations inspired by different programming languages.

## Why Eliph?

Eliph aims to be a more concise cousin to the JavaScript language by introducing new concepts, functions and symbols implemented in other programming languages, thus making it easier to write code, with less characters and more "syntactic sugar". This would make code normally written in tens or hundreds of lines much much more readable and compact, and allows you to write expressive code without any redundant or verbose boilerplate.

A necessary component of the language and its design has to do with its concise syntax: employing a good balance of words and symbols, and minimizing the overuse of brackets, and perhaps all the typable keys in the keyboard. So to simplify things, we do remove a number of things, although they really can be seen as optional.

[coffeescript]: https://coffeescript.org/
[wtfjs]: https://github.com/denysdovhan/wtfjs
[stdlib]: https://stdlib.io/
[npm packages]: https://medium.com/@thomasfuchs/what-if-we-had-a-great-standard-library-in-javascript-52692342ee3f

**Eliph is _lagom_**. Preserving JavaScript's curly brace syntax, so that for people who come from languages like C, Java or even JS developers would be able to learn quickly. However, some of the more unnecessary things that really become a big hassle for developers like me, such as verbosity, word length and excessive use of punctuation, have been removed.

- **Shortened keyword and even function names**: `function -> func`, `instanceof -> instof`, `extends -> from / of`, `implements -> with`
- **Unnecessary punctuation have been removed**, such as semicolons `;`, commas `,`, and parentheses `()` in statements like `if ()` and `for ()` are removed.
- **Everything is an expression**, and can be assigned to variables and returned from functions, which includes control flow statements like `if`, `for` and `try`.
- **Optional declarations** with `var`, `let` or `const` are only allowed when initializing a variable without a value or one in a loop.
- **Implicit returns**: the last statement is automatically returned from a `do`-block (closure) or a function, unless otherwise specified with `return`.

**Static and robust types**. JavaScript, because of its complete lack of types, resulting in its [peculiar runtime behaviour](https://github.com/denysdovhan/wtfjs), which can lead to unexpected and sometimes annoying side effects. TypeScript aimed to provide better tooling for JavaScript, by adding static typing to the JavaScript language, but inherits all of its problems, and has a much slower build process than modern JavaScript since it always has to be "compiled" by type-checking, hence significantly adding a lot more to the build time.

- Types in Eliph are **automatically inferred.** You don't need to explicitly assign a type to a variable. If you want to disable type checking for a variable whenever you're working with a third-party JavaScript library, you can use the `any` type.
- You can annotate **anywhere** within your code, even within expressions, so you can assure yourself and also other people who will be maintaining your code, that you know what you're doing.
- **A type should not change into another.** In JavaScript, your variable's type might change when the code runs, hence causing a wide range of side-effects. This is an anti-feature; it makes the code much harder to understand when reading or debugging.
- **Types are erased after compilation** and don't exist at runtime. You don't need type info during runtime; so any type errors are automatically reported at compile time so you can catch the bugs earlier.
- **A type system that is sometimes incorrect can be dangerous** due to expectation mismatches. Most type systems make a guess at the type of a value and show you a type in your editor that's sometimes incorrect.

**Dependency-free**. Eliph aims to provide a suite of built-in classes, methods and functions that provide more than what JS can, so there is no need for you to compose your own functions on the fly. At the same time, Eliph should include in and of itself a **standard library** (inspired by languages like Python, Ruby and Go) since the JS ecosystem is littered with dependencies. Shipping the final product inevitably drags in a huge amount of code, most of which the project doesn't actually use.

- Eliph can be used directly on Node.JS and even has its own standalone library with no dependencies, `@eliph/stdlib`, similar to other compile-to-JS languages.
- The Eliph standard library can be used directly on any Node.JS application, even alongside other to-JS languages like TypeScript and CoffeeScript.

**One-to-one mapping**. Unreadable boilerplate JS code generated from other compiled-to-JS languages makes it so that it could be, practically speaking, hard to debug, hard to learn from and hard to integrate with existing handwritten JS. Whereas for Eliph, the compiled output is automatically mapped to one source file, while the code structure is preserved. This is especially important while learning, where users might want to understand how the code's compiled, and to audit for bugs. Eliph does a number of things to remove unnecessary boilerplate code from the compiled output.

- Syntactic sugar, `stdlib` modules and built-in functions such as range literals, fractions and s(p)licing, whenever mentioned in Eliph code, are automatically generated as import statements from `@eliph` in the final output, and map cleanly to regular JavaScript functions.
- Variables and constants are temporary. They are declared `let` by default the moment they first appear. Those with **illegal identifier names**, or the values which are passed onto the `del` statement, are put in a "header" object that exists only on the current scope.

---

## Roadmap

Many programming languages and frameworks often have adequate language support in integrated development environments. Language support is a fancy term for things like code snippets, syntax highlighting, boilerplate, documentation, language references and even a big ecosystem of plugins, packages and Stack Overflow developers.

- Documentation
- Standard library
- Syntax highlighting
- Compiler
- Formatter
- Linter and debugger

### Documentation

The roadmap for developing the language has to start with the documentation, as that would give me a head start on the grammatical and syntactic features of the language. The documentation will be written with Markdown, which would explain the features, grammar, functions and modules in the language and its core library, and explain the similarities and differences between it and other programming languages.

### Syntax Highlighting

The next pattern is to do the syntax highlighting for the language. Syntax highlighting displays text, especially source code, in different colours and fonts according to the category of terms. This feature facilitates writing in a structured language such as a programming language or a markup language as both structures and syntax errors are visually distinct.

Most editors with syntax highlighting allow different colors and text styles to be given to dozens of different lexical sub-elements of syntax. These include keywords, comments, control-flow statements, variables, and other elements. Programmers often heavily customize their settings in an attempt to show as much useful information as possible without making the code difficult to read.

Code is processed through a series of regular expressions, and each match is assigned a scope. These scopes are mapped to colors in stylesheets and themes in code editors and syntax highlighting engines in code editors.

Highlighting can be fine-tuned through the use of custom code, such as highlighting bracket encapsulations or indentation depth, HTML and XML tags and attributes, variable, function or class names, or even allowing for including other languages inside the code.

### Standard Library

While the Eliph Language Reference describes the syntax and semantics and programming of the Eliph programming language, this library reference manual describes the standard library that is distributed in Eliph's module `@eliph/stdlib`.

Eliph's standard library is very extensive, offering a wide range of modules as indicated by this long list below. These modules can also be accessed through that provide standardized solutions for many problems that occur in everyday programming. Some of the modules, are wrappers around other librries such as

---

## Standard Library

1. the Eliph Programming Language
   1. `parser` - Access Eliph parse trees
   2. `ast` - Abstract Syntax Trees
   3. `symtable` - Access to the compiler's symbol tables
   4. `symbol` - Constants used with Eliph parse trees
   5. `token` - Constants used with Eliph parse trees
   6. `keyword` - Testing for Eliph keywords
   7. `tokenize` - Tokenizer for Eliph source code
2. Text Processing `text`
   1. `string` - advanced string manipulation
   2. `regexp` - advanced regular expressions and operations
   3. `textprep` - text preparation modules
   4. `unicode` - Unicode character data
   5. `adobe` - Adobe Glyph List data
3. Mathematical and Numeric Modules (inspired by MathJS)
   1. `math` - mathematical functions
   2. `decimal` - decimal fixed point and floating point arithmetic
   3. `fraction` - rational numbers
   4. `complex` - complex numbers
   5. `algebra` - algebra and polynomials
   6. `random`, `seed` - seeded PRNG and advanced random modules
   7. `radix` - formatting and converting numbers between locales and bases
   8. `units` - unit conversion
   9. `stats` - statistics functions
   10. `money` - currency conversion and manipulation
4. Data Types (inspired by Moment and DateJS)
   1. `datetime` - date parsing, conversion and manipulation
   2. `datetime.timezone` - IANA time zone support
   3. `calendar` - calendar-related functions
   4. `struct` - advanced data structures
5. Data Analysis and Manipulation (inspired by D3 and SciPy)
   1. `transform` - data manipulation and transformation algorithms
   2. `sym` - scientific computing and data analysis tools
   3. `plot` - data visualization tools
6. Reactive Programming (inspired by RxJS)
   1. `observable` - tools for reactive programming
   2. `promise` - asynchronous programming
   3. `reactive` - reactive functional programming
   4. `stream` - tools for working with streams
   5. `callback` - async callback functions
7. Functional Programming (inspired by Ramda, Lodash, Underscore and LazyJS)
   1. `iterator` - functions creating iterators for efficient looping
   2. `function` - higher-order functions and operations on callable objects
   3. `operator` - operators as functions
8. File System and I/O
   1. `glob` - Unix style pathname pattern expansion
   2. `pathlib` - Tools for working with file system paths
   3. `schedule` - Task scheduler
   4. `json`, `yaml`, `toml`, `cson`, `xml`: parsing and serialization
   5. `csv` and `xsl` - CSV and Excel file reading and writing
   6. `binary` - tools for reading/writing binary files
   7. `datagen` - data generation library
9. Image and Audio
   1. `img` - image manipulation and processing tools
   2. `img.gen` - image generation tools
   3. `tts` - text-to-speech
   4. `voice` - voice commands
10. Web Templating and Design

    1. `url` - URL utilities and manipulation

    2. `style` - CSS parsing, conversion and stringing
    3. `style.color` - color manipulation
    4. `html` - HTML manipulation, templating and functions
    5. `html.convert` - templating language conversion (Pug/Jade, HAML, Slim and more)
    6. `minify` - HTML, CSS and JS minifier

11. Security and Cryptography
    1. `crypto` - cryptography and security algorithm and tools
    1. `passhash` - password hashing algorithms
12. Internationalization and Localization
    1. `gettext` - Multilingual i18n services
    2. `locale` - i18n services + numbers, plurals and currencies
13. APIs and web services (inspired by Axios)
    1. `rest` - built-in REST framework
    2. `api` - interacting with web APIs
    3. `doc` - API documentation generator
    4. `graphql` - interacting with GraphQL APIs
    5. `mine` - web scraping and analysis
    6. Clients, like MongoDB, Redis, FaunaDB, PostgreSQL, etc...
    7. `query` - query builder for the aforementioned database clients
14. Machine Learning (inspired by scikit-learn, ml.js and more)
    1. `graphlib` - network analysis tools
    2. `mlkit` - machine learning tools
15. Natural Language Processing (inspired by Gensim, NLTK and Compromise)
    1. `nlp` - textual processing and analysis
    2. `nlp.data` - datasets and corpora
16. Code Analysis and Debugging
    1. `typecheck` - static runtime type checking
    2. `assert` - testing and debugging tools
    3. `format` - code formatter and prettifier
    4. `console` - console logging tools
    5. `command` - command-line utilities

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
