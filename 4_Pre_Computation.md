# 🧠 Pre-Computation in Competitive Programming

Pre-computation is a powerful optimization technique where we compute results beforehand and store them to answer multiple queries quickly. This is particularly useful when the same calculations are repeated across different test cases.

---

## ❓ The Problem

Let's consider a classic problem to understand this technique.

**Question:** You are given `T` test cases. In each test case, you receive a number `N`. Your task is to print the factorial of `N` modulo `M` for each test case.

**Given:**
- Modulo `M = 10^9 + 7`

**Constraints:**
- `1 <= T <= 10^5`
- `1 <= N <= 10^5`

---

## 🐢 Generic (Naive) Approach

The most straightforward way is to calculate the factorial for each given `N` inside the test case loop.

This approach involves a loop from 1 to `N` for every single test case `T`.

### Time Complexity Analysis
The complexity for a single test case is `O(N)`. Since there are `T` test cases, the total time complexity becomes **O(T * N)**.

Given the constraints:
- `10^5 (T) * 10^5 (N) = 10^10` operations.

This is a very large number of operations and will certainly lead to a **Time Limit Exceeded (TLE)** error on most online judges.

### Code (Naive)

```cpp
#include<iostream>

using namespace std;

const int M = 1e9 + 7;

int main() {
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        long long fact = 1;

        for (int i = 1; i <= n; i++) {
            fact = (fact * i) % M;
        }

        cout << fact << endl;
    }
    return 0;
}
```

---

## 🚀 The Optimized Approach: Pre-Computation

Notice that the values of `N` can be repeated across test cases, and the maximum value of `N` is fixed at `10^5`. Instead of re-calculating `N!` every time, we can pre-compute all factorials from 1 to `10^5` *once* and store them in an array. Then, for each query, we can retrieve the answer in constant time.

### Time Complexity Analysis
1.  **Pre-computation:** We loop once from 1 to `10^5` to calculate and store all the factorials. This takes **O(N_max)** time.
2.  **Answering Queries:** For each of the `T` test cases, we just do an array lookup, which takes **O(1)** time. The total time for this part is **O(T)**.

The total time complexity is **O(N_max + T)**.

Given the constraints:
- `10^5 (N_max) + 10^5 (T) ≈ 2 * 10^5` operations.

This is well within the typical limit of `10^7` operations per second and will pass easily.

### Code (Pre-Computation)

```cpp
#include<iostream>

using namespace std;

const int M = 1e9 + 7;
const int MAX_N = 1e5 + 10;

long long fact[MAX_N];

int main() {
    // 0! is defined as 1
    fact[0] = 1;
    
    for (int i = 1; i < MAX_N; i++) {
        fact[i] = (fact[i - 1] * i) % M;
    }

    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        // Answer each query in O(1) time.
        cout << fact[n] << endl; 
    }

    return 0;
}
```
