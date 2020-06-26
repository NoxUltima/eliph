Ham / Spider / Khepri

Switch functions - testing for both values or expressions

```js
var dis = 'whoa'
switch (dis) {
  if dis.length == 5: res = 'this'
  if 0, 1, 2, 3, 4: res = 'deez'
  if dis # 3 == dis.length ^^ !Math.randint(0, dis.length): res = 'deez nuts'
  else: res = 'dis'
}
res
```

```
deez

```

which compiles to

```js
var dis = "whoa";
var dis;
var a = Math.floor(dis / 3) == dis.length;
b = !~~(Math.random() * dis.length);
if (dis == 5) res = "this";
else if (dis % 1 == 0 && 0 <= dis && 5 > dis) res = "deez";
else if (!a ^ !b) res = "deez nuts";
else res = "dis";
console.log(res);
```

```
deez
```

| Bitwise | Logical | Boolean  |
| ------- | ------- | -------- |
| `&`     | `&&`    | and      |
| `~&`    | `!&`    | nand     |
| `ǀ`     | `ǀǀ`    | or       |
| `~ǀ`    | `!ǀ`    | nor      |
| `^`     | `^^`    | xor      |
| `@`     | `@@`    | xnor/iff |
| `~`     | `!`     | not      |

Changes to JS

- Screw semicolons! Just kidding, they're optional.
- Optional "return" statements for arrow, anonymous and regular functions. The variable when stated alone is already the return statement
- fn, not function
- Python words like `if`, `elif`, `else`, `and`, `or`, `not`, as well as `then`, `unless`, `until`, `xor`, `xnor`, `nand`, `nor`, `iff`
- `but` and `nor` have the symbols `!&` and `!|`
- print() becomes log()
- No more brackets after most keywords.
- JS is revamped.
- The Python floor division sign `//` is now `#`
- Quick mafs.
- Every arithmetical or bitwise operator can come before the =
- /\ and \/ can be used as `and` and `or`.
- For-looping: `for i: 30, 2, -2` is equivalent to `for (var i=30;i>2;i-=2)`
- Until and do-until loop (negative of while loops)
- Array comprehensions! `[0, 1, 2, 3]` = `[x: 4]` = `[...Array(4).keys()]`
- Array splicing, slicing and spread syntax, negative indices

Function libraries from Python, JS, Swift and some new programming languages out there.

Markup:

- The basic tag is <tag>.
- CSS-like syntax (classes and everything) comes after the tag name.
- Then goes whatever parameters, in quotes
- The content comes before the > sign. This includes any nested tags.

```js
return <Div .message .important #no [class]='msg === "Hello World!" ? HelloWorld : no' n-for='i in msgs'>
        <Div>msg</Div>
    </Div>

<t-icon class="Hey there"></t-icon>
```

You can assign numerals with custom digit sets, and convert strings to numbers this way.

```js
import String from z;

Radix(36) {
    digits: String.digits
        + String.ASCIIUppercase,
    decimal: '.',
    separator: (',', 3)
}
var base36 = r36'A.I' // 10.5
```

which is the same as

```js
var number: float ('A.I', 36)
```

```js
function convertBase(
  str,
  fromBase,
  toBase,
  DIGITS = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ+/"
) {
  const add = (x, y, base) => {
    let z = [];
    const n = Math.max(x.length, y.length);
    let carry = 0;
    let i = 0;
    while (i < n || carry) {
      const xi = i < x.length ? x[i] : 0;
      const yi = i < y.length ? y[i] : 0;
      const zi = carry + xi + yi;
      z.push(zi % base);
      carry = Math.floor(zi / base);
      i++;
    }
    return z;
  };

  const multiplyByNumber = (num, x, base) => {
    if (num < 0) return null;
    if (num == 0) return [];

    let result = [];
    let power = x;
    while (true) {
      num & 1 && (result = add(result, power, base));
      num = num >> 1;
      if (num === 0) break;
      power = add(power, power, base);
    }

    return result;
  };

  const parseToDigitsArray = (str, base) => {
    const digits = str.split("");
    let arr = [];
    for (let i = digits.length - 1; i >= 0; i--) {
      const n = DIGITS.indexOf(digits[i]);
      if (n == -1) return null;
      arr.push(n);
    }
    return arr;
  };

  const digits = parseToDigitsArray(str, fromBase);
  if (digits === null) return null;

  let outArray = [];
  let power = [1];
  for (let i = 0; i < digits.length; i++) {
    digits[i] &&
      (outArray = add(
        outArray,
        multiplyByNumber(digits[i], power, toBase),
        toBase
      ));
    power = multiplyByNumber(fromBase, power, toBase);
  }

  let out = "";
  for (let i = outArray.length - 1; i >= 0; i--) out += DIGITS[outArray[i]];

  return out;
}
```

The above function can be written as:

```js
fn convertBase(str, fromBase, toBase,
    chars = "0123456789abcdefghijklmnopqrstuvwxyz"
    "ABCDEFGHIJKLMNOPQRSTUVWXYZ+/") {

    const add = (x, y, base) => {
        let z, carry, i = [], 0, 0
        const n = max(x.len, y.len)
        while i < n || carry {
            const xi = i < x.len ? x[i] : 0
            const yi = i < y.len ? y[i] : 0
            const zi = carry + xi + yi
            z.push(zi % base)
            carry = zi # base
            i++
        }
        return z
    }

    const multiply = (num, x, base) => {
        if num < 0 return null
        if num == 0 return []

        let result = [], power = x
        while true {
            num & 1 && (result = add(result, power, base))
            num = num >> 1
            if num === 0 break
            power = add(power, power, base)
        }
    }

    const parseDigits = (str, base) => {
        const digits = str.split()
        let arr = []
        for i: digits.length - 1 -> 0 {
            const n = chars.index(digits[i])
            if n == -1 return null
            arr.push(n)
        }
        return arr
    }

    const digits = parseDigits(str, fromBase)
    if digits === null return null

    let outArray, power = [], [1]
    for i: digits.len {
        digits[i] && (
                outArray = add(outArray,
                multiply(digits[i], power, toBase),
                ), toBase
            )
        power = multiply(fromBase, power, toBase)
    }

    let out = ''
    for i: digits.len -> 0
        out += chars[outArray[i]]

    return out
}
```
