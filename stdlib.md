# Standard Library

Welcome to the Nyx Standard Library (`@nyx/nyfti`), a large collection of libraries and modules for Node.JS built around the JS ecosystem. We're trying to encode and consolidate as many functions, classes and modules into a big and powerful **standard library** that represents the best of the JS ecosystem (inspired by languages like Python, Ruby and Go).

Many of the modules from this library are built right into the language, and power many of Nyx's advanced features that do not have a neat JS equivalent. Since the Library is written in JS and JS only, the Standard Library can be used without Nyx.

As your codebase grows, there is a need to extract certain repetitive routines as utility functions, such as making conversions, parsing input and formatting output. But it could be a hard time finding a suitable function that we really need for the job.

---

## Table of Contents

1. [Node.JS Standard Library](https://nodejs.org/docs/latest-v12.x/api/)
2. Nyx Language
   1. `parser` - Access Nyx parse trees
   2. `ast` - Abstract syntax trees
   3. `symtable` - Access to the compiler's symbol tables
   4. `symbol`, `token` - Constants used with Nyx parse trees
   5. `keyword` - Nyx keyword list
   6. `tokenize` - Tokenizer for Nyx source code
   7. `eval` - An evaluator for Nyx expressions
3. Miscellaneous code
   1. `typecheck` - static runtime type checking
   2. `assert` - testing and debugging tools
   3. `format` - code formatter and prettifier
   4. `console` - console logging tools
   5. `command` - command-line utilities
4. Text Processing: Modules for advanced
   1. `string` - string transformation and constants
   2. `regexp` - advanced regular expressions and operations
   3. `textprep` - text preparation modules
   4. `unicode` - Unicode character data
   5. `adobe` - Adobe Glyph List data
5. Mathematical and Numeric Modules (inspired by MathJS)
   1. `math` - mathematical functions
   2. `decimal` - decimal fixed point and floating point arithmetic
   3. `fraction` - rational numbers
   4. `complex` - complex numbers
   5. `algebra` - algebra and polynomials
   6. `seed`, `random` - seeded PRNG and advanced random modules
   7. `radix` - formatting and converting numbers between locales and bases
   8. `units` - unit conversion
   9. `stats` - statistics functions
   10. `money` - currency conversion and manipulation
6. Data Types (inspired by Moment and DateJS)
   1. `datetime` - date parsing, conversion and manipulation
   2. `datetime.zone` - IANA time zone support
   3. `calendar` - calendar-related functions
   4. `struct` - advanced data structures
7. Data Analysis and Manipulation (inspired by D3 and SciPy)
   1. `transform` - data manipulation and transformation algorithms
   2. `sym` - scientific computing and data analysis tools
   3. `plot` - data visualization tools
8. Reactive Programming (inspired by RxJS)
   1. `observable` - tools for reactive programming
   2. `promise` - asynchronous progra
   3. `reactive` - reactive functional programming
   4. `stream` - tools for working with streams
   5. `callback` - async callback functions
9. Functional Programming (inspired by Ramda, Lodash, Underscore and LazyJS)
   1. `iterator` - functions creating iterators for efficient looping
   2. `function` - higher-order functions and operations on callable objects
   3. `operator` - operators as functions
10. File System and I/O
    1. `glob` - Unix style file-system walking
    2. `pathlib` - tools for working with file system paths
    3. `schedule` - task scheduler
    4. `serialize`: JSON, YAML, TOML, CSON and XML parsing and serialization
    5. `csv` and `xsl` - CSV and Excel file reading and writing
    6. `binary` - tools for reading/writing binary files
    7. `datagen` - data generation library
11. Image and Audio
    1. `img` - image manipulation and processing tools
    2. `img.gen` - image generation tools
    3. `audio` - audio processing and manipulation tools
    4. `tts` - text-to-speech utilities
    5. `voice` - voice commands
12. Frontend Utilities
    1. `url` - URL utilities and manipulation
    2. `style` - CSS parsing, manipulation and conversion (CSS, SASS, SCSS, LESS, Stylus)
    3. `style.color` - color parsing and manipulation
    4. `html` - HTML manipulation, templating and functions
    5. `html.convert` - templating language conversion (Pug/Jade, HAML, Slim and more)
    6. `minify` - HTML, CSS and JS minifier
13. Security and Cryptography
    1. `crypto` - cryptography and security algorithm and tools
    2. `passhash` - password hashing algorithms
14. Internationalization and Localization
    1. `intl` - Multilingual i18n services
    2. `locale` - locale-specific utilities: numbers, plurals and currencies
15. Machine Learning (inspired by scikit-learn, ml.js and more)
    1. `graphlib` - network analysis tools
    2. `mlkit` - machine learning tools
16. Natural Language Processing (inspired by Gensim, NLTK and Compromise)
    1. `nlp` - textual processing and analysis
    2. `nlp.data` - datasets and corpora
    3. `chatbot` - chatbot API and framework
17. APIs and web services (inspired by Axios)
    1. `rest` - built-in REST framework
    2. `api` - interacting with web APIs
    3. `doc` - API documentation generator
    4. `graphql` - interacting with GraphQL APIs
    5. `mine` - web scraping and analysis
    6. `query` - query builder for database clients
