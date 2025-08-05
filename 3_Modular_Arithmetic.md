# 🔢 Modular Arithmetic

Modular arithmetic is a system of arithmetic for integers, where numbers "wrap around" when reaching a certain value—the **modulus**. A classic example is a 12-hour clock; if it's 10 o'clock and you add 4 hours, it becomes 2 o'clock, not 14. This is `(10 + 4) % 12 = 2`. This concept is crucial for handling calculations that might result in numbers too large to fit in standard data types.

---

## 📜 Key Formulae

Here are the fundamental properties of modular arithmetic. Let `M` be the modulus.

### 1. Addition `➕`
The modulus of a sum is the modulus of the sum of the individual moduli.
```cpp
(a + b) % M = ((a % M) + (b % M)) % M
```

### 2. Multiplication `✖️`
The modulus of a product is the modulus of the product of the individual moduli.
```cpp
(a * b) % M = ((a % M) * (b % M)) % M
```

### 3. Subtraction `➖`
To handle potential negative results from `(a % M) - (b % M)` (as the `%` operator in C++ can yield negative results for negative inputs), we add `M` before taking the final modulus. This ensures the result is always a positive integer within the range `[0, M-1]`.

```cpp
// Correct way to handle modular subtraction to avoid negative results
(a - b) % M = ((a % M) - (b % M) + M) % M
```

### 4. Division `➗`
Modular division is not as straightforward as the other operations. To compute `(a / b) % M`, we must multiply `a` by the **modular multiplicative inverse** of `b` (denoted as `b⁻¹`). The modular multiplicative inverse is a number such that `(b * b⁻¹) % M = 1`.

The division formula is then transformed into a multiplication:
```cpp
(a / b) % M = ((a % M) * (b⁻¹) % M) % M
```
**Important:** The modular multiplicative inverse of `b` exists only if `b` and `M` are coprime (their greatest common divisor is 1). This is a key reason why a prime modulus is often chosen.

---

## 🎯 The Choice of Modulus (M) in Competitive Programming

In competitive programming, you'll frequently see problems requiring you to output an answer modulo a large number. The most common choice is **`10^9 + 7`**.

### Why `10^9 + 7`?

1.  **It's a Prime Number:** As mentioned above, using a prime modulus ensures that the modular multiplicative inverse exists for all numbers from `1` to `M-1`. This makes modular division possible for all these numbers, which is essential for many algorithms.

2.  **It Avoids Overflow:**
    *   `10^9 + 7` fits comfortably within a standard 32-bit signed integer (which can typically hold values up to `2 * 10^9`).
    *   More importantly, when performing intermediate calculations like `(a % M) * (b % M)`, the result can be up to `(M-1) * (M-1)`, which is approximately `10^18`. This value fits within a 64-bit integer type (`long long` in C++), preventing overflow before the final modulus is taken. This is a common source of bugs if not handled carefully.
