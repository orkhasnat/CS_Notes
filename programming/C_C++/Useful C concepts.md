## Bit-wise Operators

- `&` (AND): Returns 1 if both bits are 1.
- `|` (OR): Returns 1 if at least one bit is 1.
- `^` (XOR): Returns 1 if the bits are different.
- `~` (Bit-wise NOT): Flips each bit.
- `<<` (Left Shift): Shifts bits left (doubles).
- `>>` (Right Shift): Shifts bits right (halves).

## Modulus Operator

- `(a + b) % m = (a % m + b % m) % m`
- Converting char numbers to int numbers and vice-versa:
  - ASCII code for '0' is 48.
  - Adding or subtracting 48 from char ASCII or int value converts it.
  - Example: `char a = '9'; printf("%d", a - 48);` converts '9' to 9 (int).

## Using `&` Instead of Modulus `%`

- `AND (&)` can be used instead of the mod `%` operator for even numbers:
  - `27 % 2` is the same as `27 & 1`.
  - `27 & 2` is not the same as `27 % 3`.

## Using XOR for Odd and Even

- XOR can be used to find odd and even numbers:
  - XORing 1 with an even number increments it by 1.
  - XORing 1 with an odd number decrements it by 1.

## Using XOR to Find Unique Element

- XOR can be used to find if an array has only one element whose frequency is one:
  - XOR properties: `0 ^ N = N`, `N ^ N = 0`.
  - If an element appears an odd number of times, XORing all elements will reveal it.

## Left and Right Shifts as Powers of 2

- Left shifts (`<<`) and right shifts (`>>`) work as exponential/power of 2.
  - `n << a` is equivalent to `n * (2^a)`.

## `static` Keyword

- `static` variables preserve their value across scopes.
- They are not initialized again in a new scope.
- Example: `static int count = 0;`

## Converting Case with `&` and `|`

- To convert ASCII char to upper: `char & 95`.
- To convert ASCII char to lower: `char | 32`.

## Printing Strings Easily

- Use a `typedef` to create string aliases for easier printing:
  - `typedef char* string;`
  - `string str = "some text";`
  - `printf(str);`

## Structure Memory Consumption

- Declare structure members in ascending order by size to save memory.
- Example: Declaring `char`, `int`, `pointer`, `float`, `double`, `array`, etc., in that order can reduce memory usage.

## `printf` Return Type

- `printf` returns the total number of characters successfully printed.

## `scanf` Return Type

- `scanf` returns the total number of inputs scanned successfully.
- Example: `printf("%d", scanf("%s %f"));` will print out 2 if two inputs were successfully scanned.

## `scanf` and Char Input

- When using `scanf` for char input, consider using `' %c'` to handle newline characters in input.
- This prevents newline characters from being read as input.

## Pointers Passed as Function Arguments

- When passing pointers as function arguments, remember that the parameter creates a local variable in the function.
- The argument is copied into this local variable, so changes to the local variable won't affect the original pointer.
- Example: `func(int *h) {*h = (*h) * 5;}` and `func(p)` are not the same; `p` and `h` are distinct variables.

