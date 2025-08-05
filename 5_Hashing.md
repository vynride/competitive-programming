# ⛓️ Hashing in C++

Hashing is a powerful technique used to store and retrieve data in an average time complexity of O(1). One of the most common applications is to count the frequencies of elements in a collection.

---

## ❓ Problem: Frequency Counter

Given an array `A` of `N` integers and `Q` queries. In each query, you are given a number `X`, and your task is to print the count of `X` in the array `A`.

### Constraints
*   `1 <= N <= 10^5`
*   `1 <= a[i] <= 10^7`
*   `1 <= Q <= 10^5`

---

## 🐢 Brute-Force Approach

The most straightforward way to solve this is to iterate through the entire array for each query and count the occurrences of the given number `X`.

### Time Complexity Analysis
*   **Reading Input Array:** O(N)
*   **Answering Queries:** For each of the `Q` queries, we iterate through the `N` elements of the array. This takes O(Q * N) time.
*   **Total Complexity:** `O(N + Q * N)`

With `N` and `Q` up to `10^5`, the total number of operations would be in the order of `10^5 * 10^5 = 10^10`, which is too slow and will result in a **Time Limit Exceeded (TLE)** error on most competitive programming platforms.

### C++ Implementation

```cpp
#include<iostream>
#include<vector>

using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }

    int q;
    cin >> q;

    while (q--) {
        int x;
        cin >> x;

        int ct = 0;
        for (int i = 0; i < n; i++) {
            if (a[i] == x) {
                ct++;
            }
        }
        
        cout << ct << endl;
    }
    return 0;
}
```

---

## 🚀 Optimized Approach: Pre-computation with Hashing

We can significantly optimize the process by pre-computing the frequencies of all numbers in the array. We can use a separate array, often called a **hash array** or **frequency array**, to store these counts. The index of the hash array will correspond to the number, and the value at that index will be its frequency.

### Time Complexity Analysis
*   **Pre-computation:** We iterate through the input array `A` once to populate our hash array. This takes O(N) time.
*   **Answering Queries:** For each of the `Q` queries, we can now find the count of `X` in O(1) time by simply looking up the value at `hsh[X]`. This takes a total of O(Q) for all queries.
*   **Total Complexity:** `O(N + Q)`

With `N` and `Q` up to `10^5`, the total operations are around `10^5 + 10^5 = 2 * 10^5`, which is extremely fast and well within the time limits.

### C++ Implementation

```cpp
#include<iostream>
#include<vector>

using namespace std;

const int N = 1e7 + 10;

// Global arrays are automatically initialized to zero in C++.
int hsh[N];

int main() {
    int n;
    cin >> n;

    // Pre-computation: Store frequencies of each element
    for (int i = 0; i < n; i++) {
        int val;
        cin >> val;
        hsh[val]++;
    }

    int q;
    cin >> q;

    while (q--) {
        int x;
        cin >> x;
        
        // Fetching the pre-computed count in O(1)
        cout << hsh[x] << endl;
    }
    
    return 0;
}
```

---

## 💡 Handling Negative Numbers

The array-based hashing approach shown above works only for non-negative indices. If the array can contain negative numbers, we need a different strategy.

### 1. Use C++ STL Maps
The easiest and most flexible way is to use `std::map` or `std::unordered_map`. These data structures can handle any key type, including negative numbers, without any manual index manipulation.

*   `std::unordered_map`: Provides average O(1) time complexity for insertions and lookups. It is generally the preferred choice for frequency counting.
*   `std::map`: Provides O(log N) time complexity as it stores keys in a sorted order.

### 2. Index Shifting / Offsetting
If the range of negative numbers is known and small, you can "shift" the numbers to make them non-negative.

**Example:**
If the numbers in the array `A` are in the range `[-10^3, 10^3]`.

1.  **Create a Hash Array:** Create a hash array large enough to hold the entire range, e.g., `int hsh[2001]`.
2.  **Add an Offset:** Choose an offset that makes the smallest number map to index 0. Here, the offset would be `1000`.
3.  **Store Frequency:** When you encounter a number `a[i]`, you increment the count at `hsh[a[i] + 1000]`.
4.  **Query:** To find the count of a number `x`, you look up the value at `hsh[x + 1000]`.

This method is less flexible than using maps but can be slightly faster if the range is small and fixed.
```
