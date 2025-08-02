# 📜 C++ Basics

## 📋 Table of Contents

1.  [🚀 Getting Started](#-getting-started)
    *   [Basic Program Structure](#basic-program-structure)
    *   [Standard Headers](#standard-headers)
2.  [🔢 Data Types & Variables](#-data-types--variables)
    *   [Primary Data Types](#primary-data-types)
    *   [Type Truncation](#type-truncation)
    *   [Boolean Logic](#boolean-logic)
3.  [🧮 Operators & Expressions](#-operators--expressions)
    *   [Arithmetic Operators](#arithmetic-operators)
    *   [Increment Operators (`++`)](#increment-operators-)
    *   [Type Casting & ASCII Values](#type-casting--ascii-values)
    *   [Type Promotion in Calculations](#type-promotion-in-calculations)
    *   [Operator Precedence](#operator-precedence)
4.  [📈 Data Limits & Overflow](#-data-limits--overflow)
    *   [Integer Limits](#integer-limits)
    *   [Handling Overflow](#handling-overflow)
    *   [Floating-Point Precision](#floating-point-precision)
5.  [⌨️ Input & Output](#-input--output)
    *   [Basic Input with `cin`](#basic-input-with-cin)
    *   [Reading a Full Line with `getline`](#reading-a-full-line-with-getline)
6.  [⛓️ C++ Strings](#-c-strings)
    *   [Appending to a String](#appending-to-a-string)
    *   [Converting Character to Integer](#converting-character-to-integer)
7.  [📦 Arrays](#-arrays)
    *   [Array Size Limitations](#array-size-limitations)
    *   [Arrays in Functions (Pass by "Reference")](#arrays-in-functions-pass-by-reference)
8.  [🔗 References](#-references)
    *   [Pass by Reference vs. Pass by Value](#pass-by-reference-vs-pass-by-value)

---

## 🚀 Getting Started

### Basic Program Structure

A fundamental C++ program includes the `main` function, which is the entry point of execution. The `cout` object is used to print output to the console.

```cpp
#include<iostream> // For input/output operations like cout
#include<cmath>    // For math functions like sqrt

// The 'using namespace std;' line allows us to use names for objects
// and variables from the standard library without the std:: prefix.
using namespace std;

int main() {
    cout << "Hello " << "I'm Vivian" << '\n';
    cout << "The square root of 16 is: " << sqrt(16) << endl;
    return 0; // Indicates successful execution
}
```

### Standard Headers

The header `<bits/stdc++.h>` is a non-standard header file often used in competitive programming to include all standard library headers at once, saving time from including each one individually.

> **⚠️ Note:** While convenient, using `<bits/stdc++.h>` is not portable and may not be available on all compilers (like MSVC). It's generally better practice in software development to include only the specific headers you need.

---

## 🔢 Data Types & Variables

### Primary Data Types

These are the most common built-in data types in C++.

*   `char`: Stores a single character (e.g., `'a'`).
*   `int`: Stores whole numbers (e.g., `3`, `-5`).
*   `float`: Stores single-precision floating-point numbers (numbers with decimals).
*   `double`: Stores double-precision floating-point numbers (more precise than `float`).
*   `bool`: Stores a boolean value (`true` or `false`).
*   `long long`: Stores very large whole numbers.

```cpp
char c = 'a';
int a = 3;
double b = 3.5;
```

### Type Truncation

When a value is assigned to a variable of a less precise type, the value is truncated (cut off), not rounded.

```cpp
// The fractional part (.5) is discarded.
int k = 4.5; // k will be 4
```

### Boolean Logic

In C++, boolean values are represented numerically in output and can be assigned from numbers.

*   `false` is equivalent to `0`.
*   `true` is equivalent to any non-zero number.

```cpp
// Printing booleans
bool d = false;
cout << d << endl; // Output: 0

// Assigning from numbers
bool f = 0; // f is false
bool e = 3; // e is true
```

---

## 🧮 Operators & Expressions

### Arithmetic Operators

The modulo operator (`%`) gives the remainder of a division.

```cpp
int remainder = 10 % 3; // remainder will be 1
```

### Increment Operators (`++`)

*   **Post-increment (`a++`)**: The variable's original value is used in the expression first, and *then* the variable is incremented.
*   **Pre-increment (`++a`)**: The variable is incremented first, and *then* its new value is used in the expression.

```cpp
int a = 5;
cout << a++ << endl; // Prints 5, then a becomes 6.
cout << ++a << endl; // a becomes 7, then prints 7.
```
**Output:**
```
5
7
```

### Type Casting & ASCII Values

You can explicitly convert a value from one type to another. This is often used to see the integer ASCII value of a character.

```cpp
char c = 'c';
cout << (int)c << endl;
```
**Output:**
```
99
```

### Type Promotion in Calculations

When an operation involves different data types, C++ automatically promotes the "lower" type to the "higher" type before performing the calculation. The result will have the higher data type.

**Hierarchy of Promotion:** `double` > `float` > `long long` > `int` > `char`

```cpp
// The integer 7 is promoted to a double (7.0) before division.
cout << 7 / 2.0 << endl; // Output: 3.5

// The char 'c' (ASCII 99) is promoted to an int before adding 1.
// The result is an integer.
cout << 'c' + 1 << endl;
```
**Output:**
```
100
```

#### Nuances of Truncation

The type of the variable where the result is stored matters greatly. The calculation is performed first, and *then* the result is assigned.

```cpp
int a = 3 / 2;     // Integer division: 3 / 2 = 1. Result is 1.
double b = 3 / 2;  // Integer division: 3 / 2 = 1. The int 1 is then converted to a double 1.0 and stored in b.
double c = 3 / 2.0; // Floating-point division: 3 / 2.0 = 1.5. Result is 1.5.

cout << a << endl;
cout << b << endl;
cout << c << endl;
```
**Output:**
```
1
1.0
1.5
```

### Operator Precedence

Operator precedence determines the order in which operations are performed. Operators with the same precedence are typically evaluated from left to right.

![Operator Precedence Table](/images/precedence-table.png)

```cpp
// Example 1: Left-to-right evaluation
cout << 7 / 2 * 3 << endl;
// 1. (7 / 2) is calculated first -> 3 (integer division)
// 2. 3 * 3 is calculated -> 9

// Example 2: Left-to-right evaluation
cout << 3 * 7 / 2 << endl;
// 1. (3 * 7) is calculated first -> 21
// 2. 21 / 2 is calculated -> 10 (integer division)
```
**Output:**
```
9
10
```

---

## 📈 Data Limits & Overflow

### Integer Limits

Each integer data type has a maximum and minimum value it can hold.

*   `int`: approx. **-2 * 10⁹ to +2 * 10⁹**
*   `long int`: (Often the same as `int`, but can be larger) approx. **-2 * 10⁹ to +2 * 10⁹** or **-9 * 10¹¹ to +9 * 10¹¹**
*   `long long int`: approx. **-9 * 10¹⁸ to +9 * 10¹⁸**

### Handling Overflow

Overflow occurs when a calculation produces a result that is outside the range of the variable's data type, leading to an incorrect, "wrapped-around" value.

```cpp
int a = 100000;
int b = 100000;

// This calculation overflows because 100,000 * 100,000 = 10^10, which is larger than max int.
// The result will be an unexpected, incorrect number.
int c = a * b;
cout << c << endl;

// The constant INT_MAX stores the maximum value for an int.
// Adding 1 to it will cause it to wrap around to a large negative number.
int mx = INT_MAX;
cout << mx + 1 << endl;
```

Even if the result is stored in a larger data type, overflow can still happen *during* the calculation if the operands are of a smaller type.

```cpp
// Incorrect: a * b is calculated first as an int, overflows, and THEN
// the incorrect result is stored in the long long.
long long int c = a * b;
```

**Correct way:** Promote one of the operands to a `long long` *before* the calculation. Multiplying by `1LL` (a long long literal) is a common trick.

```cpp
// Correct: a is promoted to long long, so the entire multiplication
// is done using long long arithmetic, preventing overflow.
long long int c = a * 1LL * b;
```

### Floating-Point Precision

#### Scientific Notation
By default, `cout` may print very large or very small `double` values in scientific notation.

```cpp
double a = 100000;
double b = 100000;
double c = a * b;

cout << c << endl; // Output might be: 1e+10
```

To display the number in full, use the `fixed` manipulator.

```cpp
// The 'fixed' manipulator forces decimal notation.
cout << fixed << c << endl; // Output: 10000000000.000000
```

#### Setting Precision
You can control the number of digits after the decimal point using `setprecision()` from the `<iomanip>` header.

```cpp
#include <iomanip> // Required for setprecision

// ...
double c = a * b;
cout << fixed << setprecision(2) << c << endl; // Output: 10000000000.00
```

#### Precision Errors
`double` has a limited precision (about 15-17 decimal digits). It cannot accurately store numbers that require more precision, which can lead to small errors.

```cpp
double big_num = 1e24;
cout << fixed << big_num << endl;
// The output is imprecise because 10^24 requires more precision than a double can offer.
// Output might be: 999999999999999983222784.000000
```

---

## ⌨️ Input & Output

### Basic Input with `cin`

The `cin` object reads input from the console. It stops reading when it encounters whitespace (a space, tab, or newline).

```cpp
int a;
double b;
cin >> a >> b; // Reads an int, skips whitespace, then reads a double.
```

### Reading a Full Line with `getline`

To read an entire line of text, including spaces, use the `getline` function.

```cpp
string str;
getline(cin, str);
cout << str << endl;
```

#### The `getline` and `cin` Problem

A common issue arises when mixing `cin >>` with `getline`. When you enter a number for `cin >> t;` and press Enter, `cin` reads the number, but the newline character (`\n`) is left in the input buffer. The subsequent `getline` call reads this leftover newline as its input, resulting in an empty string and skipping the intended input.

```cpp
int t;
cin >> t;

// The first getline reads the '\n' left by cin >> t
while (t--) {
    string s;
    getline(cin, s);
    cout << s << endl; // The first line printed will be empty
}
```

**Solution:** Use `cin.ignore()` to discard the leftover newline character from the input buffer before calling `getline`.

```cpp
int t;
cin >> t;
cin.ignore(); // Consume the leftover '\n'

while (t--) {
    string s;
    getline(cin, s);
    cout << s << endl;
}
```

---

## ⛓️ C++ Strings

### Appending to a String

While you can use the `+` operator to append characters, it can be inefficient as it may create a new string each time. Using `push_back()` or `+=` is generally more performant.

```cpp
string str1 = "hello";
char ch = '!';

// Inefficient for single characters in a loop
str1 = str1 + ch;

// Better alternatives
str1.push_back(ch);
str1 += ch;
```

### Converting Character to Integer

To convert a numeric character (e.g., `'7'`) to its integer value (e.g., `7`), you can subtract the ASCII value of `'0'`.

```cpp
string s = "12345";
int first_digit = s[0] - '0'; // '1' - '0' -> 49 - 48 = 1
cout << first_digit << endl; // Output: 1
```

---

## 📦 Arrays

### Array Size Limitations

The maximum size of an array depends on where it is declared due to memory allocation differences (stack vs. static/global).

*   **Local Array (in `main` or a function):** Allocated on the stack, which has limited memory. A typical limit is around **10⁵ to 10⁶** elements.
*   **Global/Static Array:** Allocated in a different memory segment with much more space. A typical limit is around **10⁷ to 10⁸** elements.

> **⚠️ Note:** When declaring a global or static array, its size must be a `const` expression known at compile time.

```cpp
// Global array declaration
const int N = 1e7; // 1 followed by 7 zeros = 10,000,000
int global_arr[N];

int main() {
    // Local array declaration
    const int M = 1e5; // 100,000
    int local_arr[M];
    return 0;
}
```

### Arrays in Functions (Pass by "Reference")

When you pass a C-style array to a function, you are not passing the entire array by value. Instead, the array "decays" into a pointer to its first element. This pointer is passed by value, but since it points to the original array's memory, any modifications made inside the function will affect the original array. This *behaves* like pass-by-reference.

```cpp
// arr is a pointer to the first element of the original array
void modify_array(int arr[]) {
    arr[0] = 77; // This modifies the original array
}

int main() {
    int my_arr[] = {1, 2, 3};
    cout << "Before: " << my_arr[0] << endl; // Output: 1

    modify_array(my_arr);

    cout << "After: " << my_arr[0] << endl; // Output: 77
    return 0;
}
```

> **💡 Competitive Programming Tip:** As your notes mention, it's a common strategy in competitive programming to declare large arrays globally to avoid stack size limits and the complexity of passing multi-dimensional arrays. This makes the array accessible from any function.

---

## 🔗 References

### Pass by Reference vs. Pass by Value

*   **Pass by Value:** A *copy* of the variable is passed to the function. Changes inside the function do not affect the original variable.
*   **Pass by Reference (`&`):** An *alias* (or reference) to the original variable is passed. Changes inside the function directly modify the original variable. This is more efficient for large objects like strings as it avoids making a copy.

```cpp
// n1 is passed by reference, n2 is passed by value
void increment(int &n1, int n2) {
    n1++;
    n2++;
}

// s is passed by reference
void clear_string(string &s) {
    s = "";
}

int main() {
    int a = 3;
    int b = 3;
    increment(a, b);
    // a was passed by reference, so it was changed.
    // b was passed by value, so the original was not changed.
    cout << a << " " << b << endl;

    string my_str = "some text";
    clear_string(my_str);
    cout << "My string is now: '" << my_str << "'" << endl;
    return 0;
}
```
**Output:**
```
4 3
My string is now: ''
```
