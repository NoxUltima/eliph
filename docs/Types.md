# Types

### Interfaces

Interfaces are structures used for storing data in named fields, and work the same way as in TypeScript. In order to use a interface, you must first declare one. An interface is basically an type that describes compound data types such as `map`s and `obj`s.

```dart
interface Person {
  string name;
  int age;
};

// or alternatively:
Person = interface {
  string name;
  int age;
};
```

From this point on the `Person` interface can be created and the correct type will be inferred. It does not have to be annotated:

```dart
alice: Person = {
  name: "Alice",
  age: 42,
};
```

Fields can be optional:

```dart
Person = interface {
  string name;
  int age?; // declared as optional
}
```

or "read-only", by prefixing `read` before the property type. FIelds marked as read-only will throw an error if you attempt to modify or change the object in question.

Variables use `const` or `:=` whereas properties use `read`.

```dart
Person = interface {
  read string name;
  read int age;
}
```

To describe a **function type** with an interface, we give the interface a call signature. This is like a function declaration with only the parameter list and return type given. Each parameter in the parameter list requires both name and type.

Once defined, we can use this function type interface like we would other interfaces. The names of the parameters do not need to match, as long as the argument order matches that of the interface.

```dart
interface SearchFunc {
  bool (str source, str substr);
}

mySearch SearchFunc = func (src: str, sub: str): bool {
  result = src.search(sub);
  result > -1;
};
```

We can also describe **index types** that we can "index into" like `a[10]`, or `ageMap["daniel"]`, particularly if we are dealing with maps, arrays, tuples or objects.

```dart
interface StringArray {
  str [int index];
}

StringArray myArray = ["Bob", "Fred"];
str myStr = myArray[0];
```

### Destructuring

When you assign an array or object literal to a value, Zenith breaks up and matches both sides against each other, assigning the values on the right to the variables on the left. In the simplest case, it can be used for parallel assignment:

```dart
coordinates = [10, 20, 30];
[x] = 10;
print x // 10

theBait   = 1000
theSwitch = 0

[theBait, theSwitch] = [theSwitch, theBait]
```

But it’s also helpful for dealing with functions that return multiple values.

```dart
// Make an Ajax request to fetch the weather...
weatherReport = (location) => {
  return [location, 72, "Mostly Sunny"];
};

[city, temp, forecast] = weatherReport("Berkeley, CA");
```

Destructuring assignment can be used with any depth of array and object nesting, to help pull out deeply nested properties.

```dart
futurists := {
  sculptor: "Umberto Boccioni",
  painter: "Vladimir Burliuk",
  poet: {
    name: "F.T. Marinetti",
    address: ["Via Roma 42R", "Bellagio, Italy 22021"]
  }
};

{sculptor} = futurists;

{
  poet: {
    name,
    address: [street, city]
  }
} = futurists;
```

Expansion can be used to retrieve elements from the end of an array without having to assign the rest of its values. It works in function parameter lists as well.

Destructuring assignment can even be combined with splats.

```dart
tag = "<impossible>"

[open, contents..., close] = tag.split("")
```

Marked as #TODO
