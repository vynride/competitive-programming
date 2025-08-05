# 🚀 Time Complexity Analysis

A crucial aspect of writing efficient code, especially in competitive programming, is understanding its time complexity. This determines how the runtime of your algorithm scales with the size of the input.

![Time Complexity Chart](images/time-complexity-chart.jpg)

---

## 📈 Common Time Complexities

Here are some of the most common time complexities you'll encounter, along with code examples.

### O(1) - Constant Time
An algorithm has constant time complexity if its execution time does not depend on the input size. The operation is performed in a fixed number of steps.

**Example:**
Accessing an array element or a simple variable assignment are O(1) operations.

```cpp
// This operation takes the same amount of time regardless of any 'n'
int y = 10;
```

### O(n) - Linear Time
The runtime grows linearly with the size of the input (`n`). If the input size doubles, the runtime roughly doubles.

**Example:**
A simple `for` loop that iterates from 0 to `n`.

```cpp
// This loop runs 'n' times.
for (int i = 0; i < n; i++) {
    cout << i << endl;
}
```

### O(log n) - Logarithmic Time
The runtime grows logarithmically with the input size. These algorithms are very efficient because the number of operations increases much slower than the input size. Typically, this occurs when the problem size is halved in each step.

**Example:**
The `while` loop below cuts `n` in half at each iteration.

```cpp
int count = 0;
while (n > 0) {
    n = n / 2;
    count++;
}
```

### O(n²) - Quadratic Time
The runtime is proportional to the square of the input size. This is common in algorithms that involve nested iterations over the input data.

**Example:**
A nested loop where the inner loop's iterations depend on the outer loop.

> **_Editor's Note:_** Your original note mentioned the complexity as `(n * (n + 1)) / 2`. For the code provided (`for j < i`), the exact number of inner loop iterations is the sum `0 + 1 + 2 + ... + (n-1)`, which equals `(n * (n-1)) / 2`. While the formula is slightly different, the overall time complexity is still correctly classified as **O(n²)**, as we discard constants and lower-order terms in Big O notation.

```cpp
// The outer loop runs 'n' times.
// The inner loop runs 0, 1, 2, ... up to (n-1) times.
// Total operations are approximately n²/2, which is O(n²).
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        count++;
    }
}
```

---

## 💻 Analyzing Constraints in Competitive Programming

On most competitive programming platforms, a modern CPU can perform roughly **10⁷ to 10⁸ operations per second**. You must analyze the problem's constraints to determine if your algorithm is fast enough.

### Scenario 1: Standard Nested Loops

Let's analyze a typical problem structure with test cases (`T`).

**Constraints:**
*   `1 <= T <= 1000`
*   `1 <= N <= 1000`
*   `1 <= a[i] <= 1000`

**Analysis:**
The code will run the inner loop `N` times for each of the `T` test cases.
*   **Total Iterations:** `T * N` = `1000 * 1000` = `10⁶` iterations.
*   **Conclusion:** Since `10⁶` is well within the `10⁷` to `10⁸` limit, this solution will pass within the time limit (typically 1 second).

```cpp
// T test cases
while (T--) {
    int count = 0;
    // Loop runs N times for each test case
    for (int i = 0; i < N; i++) {
        count++;
    }
}
```

### Scenario 2: The "Sum of N" Constraint (Special Case)

Sometimes, the constraints might look daunting at first glance, but a special condition changes everything.

**Constraints:**
*   `1 <= T <= 100000`
*   `1 <= N <= 100000`
*   `1 <= a[i] <= 1000`
*   **Crucial Detail:** **Sum of N over all Test cases is < 10⁷**

**Analysis:**
A naive calculation would be `T * N` = `10⁵ * 10⁵` = `10¹⁰`, which is far too slow. However, the special constraint tells us the *total* number of iterations of the inner loop across *all* test cases combined.
*   **Total Iterations:** The total work is the sum of `N` for each test case, which is given as `< 10⁷`.
*   **Conclusion:** The total number of operations is less than `10⁷`, which will comfortably pass within the time limit. This constraint is common and allows for O(N) solutions per test case, even with a high number of test cases.

```cpp
// Even with many test cases (T), the total work is manageable.
while (T--) {
    int n; // n can be different for each test case
    cin >> n;
    int count = 0;
    // The sum of all 'n's across all T iterations is < 10^7
    for (int i = 0; i < n; i++) {
        count++;
    }
}
```
---
