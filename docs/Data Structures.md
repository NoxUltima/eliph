# Data Structures

## Tuples and Arrays

Tuples are used to store multiple items in a single variable. A tuple is a collection which is ordered and unchangeable. Tuples are written inside parentheses and the elements are separated by either commas or new lines.

```dart
thistuple = (1, 2, 3);
print thistuple;
```

Like strings, tuples can be indexed (modulo its length), and also can be concatenated `+`, filtered `-`, repeated `*`, sliced or split `/` with arithmetic operators.

```dart
// Concatenation
a = (1, 2) + (3, 4); // (1, 2, 3, 4)

// Filtering (all instances of the values will be removed)
a = (1, 2, 3) - 3; // (1, 2)
a = (1, 3, 2, 3) - 3; // (1, 2)
a = (1, 3, 2, 3) - (2, 3); // (1)

// Repeating
a = tuple(1) * 3 // (1, 1, 1)

// Subdividing
a = (1::10) / 2 // ((1, 2), (3, 4), (5, 6), (7, 8), (9, 10))
a = (1::10) / (1, 2, 3, 4) // ((1), (2, 3), (4, 5, 6), (7, 8, 9, 10))
```

```dart
a = [1, 2] + [3, 4]; // Concatenation
[x, , ...z] = a // Destructuring
print(x, z); // 1, [3, 4]
$a = [...a, ...a, 4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
$a = a * 2 + [4]; // [1, 2, 3, 4, 1, 2, 3, 4, 5]
```

Marked as #TODO

## Records, Objects and Maps

Marked as #TODO

## Sets

Marked as #TODO
