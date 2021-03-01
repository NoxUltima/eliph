# Control Flow

Control flow statements can be written without the use of parentheses. As with functions and other block expressions, multi-line conditionals are delimited inside curly braces.

```dart
if y <= 15 { x = 10; print x; }
```

If you have only one statement on a line then you can use `then` or move the statement postfix:

```dart
if y <= 15 then print y;
print if y <= 15;
```

In Eliph, **everything is an expression**, which means that they can be assigned to variables and returned from functions.

It's common to insert a closure wrapper in order to ensure that all variables are closed over, and all the generated functions don't share the final values. The `do` keyword, immediately invokes a passed function, forwarding any arguments.

```dart
res = do 36; // 36
res = do { 36; }; // 36
res = do (~a = 6, ~b = 6) { a * b; }; // 36

res = do factorial(n = 3): int {
  if n < 0 then nan
  else if n == 0 then 1
  else n * factorial(n - 1);
} // 6
```

When control flow statements are used as expressions, the value of the last statement of most statements, sometimes enclosed in curly braces is implicitly returned, unless explicitly specified with `return`.

These include:

- `do`-blocks
- `if`, `unless`, `elif`, `elun`, `else` in decision trees
- `for`, `til`, `while`, `until`, and `repeat` blocks in `repeat-while/until` loops
- Every `case` or `else` statement in `switch` expressions.
- `catch` and `finally`.

Functions will be explained in later topics.

```dart
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

```dart
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

## If-Else

`if` statements are compiled either into JavaScript expressions, using the ternary operator when possible, and closure wrapping otherwise.

There is no explicit ternary statement in Eliph — you simply use a regular `if` statement on a single line. The `else` and `elif` (not `else if`) blocks are optional.

```dart
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

```dart
x = if (condition) a else b;
x = a if condition else b; // Python postfix if statement
```

```dart
// Implicit statement, make sure that there is an else
x = a if condition;
```

A `guard` statement is similar to an `if-else` statement without an `if` body.

```dart
func greet(person: {[str]: str} ) {
  guard name = person.name else return;
  print "Hello \(name)!";
  guard location = person.location else {
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

## Loops

Typically, you would write down a `for`-loop like this in JavaScript, which is very confusing to most developers. Also note the compulsory parentheses following the `for` keyword.

```js
for (let i = 1; i <= 10; i++) {}
```

Whereas in Eliph, you can either leave out the brackets following the `for`:

```dart
for i = 1; i <= 10; i++ {}
```

We also provide an opposite for the for-loop, the `till` loop, which is basically the direct opposite of the tripartite for-loop. It runs until the second, conditional statement is `true`.

```dart
till i = 1; i > 10; i++ {}
```

You can iterate over the items in a sequence, such as items in an array, ranges of numbers, or characters in a string using the `for-in` loop.

```dart
for i in [1::100] {
  // actual code goes here
}
```

You can pass in a second parameter which represents the **keys**, that is, indices of whatever you are iterating over.

```dart
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

```dart
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

```dart
gen fibonacci(): int {
  (a, b) = (0, 1);
  loop {
    (a, b) = (b, a + b);
    yield b;
  }
}

func getFibonacciNumbers(length: int): int[] {
  results = [1], fibSeq = fibonacci();
  for n from fibSeq {
    results += [n];
    break if len results == length;
  }
  results;
}
```

A `while` loop performs a set of statements until evaluating a condition. `while` evaluates its condition at the start of each pass through the loop, until the condition is `false`. `repeat-while` (not `do-while`) evaluates its condition at the end of each pass through the loop, until the condition is `false`.

```dart
while i < 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```dart
repeat {
  text += "The number is " + i;
  print text;
  i++;
} while i < 10;
```

`until` and `repeat-until` are like `while`, except the loop runs until its condition is `true`.

```dart
until i == 10 {
  text += "The number is " + i;
  print text;
  i++;
}
```

```dart
repeat {
  text += "The number is " + i;
  print text;
  i++;
} until i == 10;
```

`loop` runs its body forever **unless** there is a `break` statement somewhere.

```dart
loop {
  text += "The number is " + i;
  print text;
  i++;
  break if i == 10;
}
```

The `switch` statement works a bit differently than its JavaScript cousin. You need to remember to `break` at the end of every case statement to avoid accidentally falling through to the default case.

If no argument is supplied, the branch conditions are simply boolean expressions, and a branch is executed when its condition is true.

```dart
x = 1;
switch {
  case x == 1 -> print 1;
  case x in [2, 3] -> print [2, 3];
  else -> print 4;
}
```

The switch statement can also match against primitive values, but this is highly disrecommended.

```dart
x = 3; x += 2;
switch 5 {
  case x -> print "x == #x";
  else -> { print ''; break; };
}
```

The switch finds the first pattern that matches the input, and then executes the code that the pattern points to `->`. Code for a single branch case can be a single expression, or a block of statements.

Like an `if` statement, each case is a separate branch of code execution. The `switch` statement determines which branch should be selected. Only one branch is executed by default.

```dart
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

```dart
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

```dart
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

```dart
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

```dart
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

```dart
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

```dart
text = "", i;
for i in [1::5] {
  if (i == 3) continue;
  text += "The number is " + i + "\n";
}
```

In a switch statement, `continue` stops the execution of the current branch and executes the labelled branch that immediately comes after it. The code below will skip printing `CLOSED`, and would print `NOW_CLOSED` instead.

```dart
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

```dart
text = "", i;
for i in [1::5] {
  if (i == 3) break;
  text += "The number is " + i + "\n";
}
```

In switch statements, if you really need C-style fallthrough, can opt in to this behavior on a case-by-case basis with the `fallthru` keyword.

```dart
func isPrime(int n) bool { !('1' * n).match(/^1?$|^(11+?)\1+$/) }
```

```dart
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

```dart
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

## Error Handling

Error handling with
The try...catch statement marks a block of statements to try and specifies a response should an exception be thrown.

```dart
try {
  nonExistentFunction();
} catch e {
  error e;
  // expected output: ReferenceError: nonExistentFunction is not defined
  // Note - error messages will vary depending on browser
}
```

The try statement consists of a try-block, which contains one or more statements. {} must always be used, even for single statements. At least one catch-block, or a finally-block, must be present. This gives us three forms for the try statement:

- `try-catch`
- `try-finally`
- `try-catch-finally`

A `catch`-block contains statements that specify what to do if an exception is thrown in the `try`-block. If any statement within the `try`-block (or in a function called from within the `try`-block) throws an exception, control is immediately shifted to the `catch`-block. If no exception is thrown in the `try`-block, the `catch`-block is skipped.

The `finally`-block will always execute after the try-`block` and `catch`-block(s) have finished executing. It always executes, regardless of whether an exception was thrown or caught.

You can nest one or more `try` statements. If an inner `try` statement does not have a `catch`-block, the enclosing `try` statement's `catch`-block is used instead.

When a catch-block is used, the catch-block is executed when any exception is thrown from within the try-block. For example, when the exception occurs in the following code, control transfers to the catch-block.

```dart
try {
  throw 'myException'; // generates an exception
} catch e {
  // statements to handle any exceptions
  logMyErrors(e); // pass exception object to error handler
}
```

The `catch`-block specifies an identifier (`e` in the example above) that holds the value of the exception; this value is only available in the scope of the `catch`-block.

You can create by combining `try-catch` blocks with `switch` structures, like this:

```dart
try {
  myroutine(); // may throw three types of exceptions
} catch e {
  switch instof e {
    case TypeError -> // statements to handle TypeError exceptions
    case RangeError -> // statements to handle RangeError exceptions
    case EvalError -> // statements to handle EvalError exceptions
    // statements to handle any unspecified exceptions
    else -> logMyErrors(e); // pass exception object to error handler
  }
}
```

When an exception is thrown in the try-block, the exception variable (i.e., the e in catch (e)) holds the exception value. You can use this identifier to get information about the exception that was thrown. This identifier is only available in the catch-block's scope. If you don't need the exception value, it could be omitted.

```dart
func isValidJSON(text): bool {
  try {
    JSON.parse(text);
    return true;
  } catch {
    return false;
  }
}
```
