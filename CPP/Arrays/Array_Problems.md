# 🧩 ARRAY PROBLEMS — Most Important Questions
### Each Problem: 5 Test Cases + Solution Without STL + Solution With STL

---

## 📌 TABLE OF CONTENTS
1. [Find Maximum & Minimum](#1-find-maximum--minimum)
2. [Reverse an Array](#2-reverse-an-array)
3. [Find Second Largest Element](#3-find-second-largest-element)
4. [Find Duplicates in Array](#4-find-duplicates-in-array)
5. [Two Sum (Find pair with given sum)](#5-two-sum-find-pair-with-given-sum)
6. [Sort an Array](#6-sort-an-array)
7. [Rotate Array by K positions](#7-rotate-array-by-k-positions)
8. [Maximum Subarray Sum (Kadane's Algorithm)](#8-maximum-subarray-sum-kadanes-algorithm)
9. [Find Missing Number (1 to N)](#9-find-missing-number-1-to-n)
10. [Move Zeros to End](#10-move-zeros-to-end)
11. [Merge Two Sorted Arrays](#11-merge-two-sorted-arrays)
12. [Remove Duplicates from Sorted Array](#12-remove-duplicates-from-sorted-array)
13. [Find Majority Element (> N/2 times)](#13-find-majority-element--n2-times)
14. [Subarray with Given Sum](#14-subarray-with-given-sum)
15. [Leaders in an Array](#15-leaders-in-an-array)

---

## 1. Find Maximum & Minimum

### 📝 Problem
Given an array, find the **maximum** and **minimum** element.

### 🧪 Test Cases
| # | Input | Max | Min |
|---|---|---|---|
| 1 | `{3, 1, 4, 1, 5, 9, 2, 6}` | 9 | 1 |
| 2 | `{-5, -1, -3, -9}` | -1 | -9 |
| 3 | `{42}` | 42 | 42 |
| 4 | `{7, 7, 7, 7}` | 7 | 7 |
| 5 | `{0, -1, 100, 50, -50}` | 100 | -50 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void findMinMax(int arr[], int n) {
    int maxVal = arr[0];    // Assume first element is max
    int minVal = arr[0];    // Assume first element is min

    for (int i = 1; i < n; i++) {
        if (arr[i] > maxVal) maxVal = arr[i];   // Update max
        if (arr[i] < minVal) minVal = arr[i];   // Update min
    }

    cout << "Max = " << maxVal << endl;
    cout << "Min = " << minVal << endl;
}

int main() {
    int arr[] = {3, 1, 4, 1, 5, 9, 2, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    findMinMax(arr, n);
    return 0;
}
```

```
Output:
Max = 9
Min = 1
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {3, 1, 4, 1, 5, 9, 2, 6};

    int maxVal = *max_element(v.begin(), v.end());   // Returns iterator → dereference
    int minVal = *min_element(v.begin(), v.end());

    cout << "Max = " << maxVal << endl;   // 9
    cout << "Min = " << minVal << endl;   // 1

    // Get both at once
    auto [mn, mx] = minmax_element(v.begin(), v.end());
    cout << "Min = " << *mn << ", Max = " << *mx << endl;

    return 0;
}
```

> 💡 **Key Insight:** STL `max_element()` returns an **iterator**, so dereference with `*`.

---

## 2. Reverse an Array

### 📝 Problem
Reverse the elements of an array **in-place**.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{1, 2, 3, 4, 5}` | `{5, 4, 3, 2, 1}` |
| 2 | `{10, 20}` | `{20, 10}` |
| 3 | `{7}` | `{7}` |
| 4 | `{1, 1, 2, 2}` | `{2, 2, 1, 1}` |
| 5 | `{9, 8, 7, 6, 5, 4}` | `{4, 5, 6, 7, 8, 9}` |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void reverseArray(int arr[], int n) {
    int left = 0, right = n - 1;

    while (left < right) {
        // Swap arr[left] and arr[right]
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    reverseArray(arr, n);

    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    // Output: 5 4 3 2 1
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};

    reverse(v.begin(), v.end());    // In-place O(n)

    for (int x : v) cout << x << " ";
    // Output: 5 4 3 2 1
    return 0;
}
```

> 💡 **Key Insight:** Two-pointer approach is the classic manual method. STL `reverse()` does exactly that internally.

---

## 3. Find Second Largest Element

### 📝 Problem
Find the **second largest** element in an array (distinct elements).

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{12, 35, 1, 10, 34, 1}` | 34 |
| 2 | `{10, 5, 10}` | 5 |
| 3 | `{1, 2}` | 1 |
| 4 | `{9, 9, 8, 7}` | 8 |
| 5 | `{100, 200, 300, 400}` | 300 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
#include <climits>
using namespace std;

int secondLargest(int arr[], int n) {
    int first = INT_MIN, second = INT_MIN;

    for (int i = 0; i < n; i++) {
        if (arr[i] > first) {
            second = first;      // Old first becomes second
            first = arr[i];      // New first found
        }
        else if (arr[i] > second && arr[i] != first) {
            second = arr[i];     // Update second (not equal to first)
        }
    }

    return second;
}

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Second Largest = " << secondLargest(arr, n);
    // Output: 34
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <set>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {12, 35, 1, 10, 34, 1};

    // Method 1: Using set (stores unique, sorted)
    set<int> s(v.begin(), v.end());    // {1, 10, 12, 34, 35}
    auto it = s.end();
    --it;    // Points to 35 (max)
    --it;    // Points to 34 (second max)
    cout << "Second Largest = " << *it << endl;    // 34

    // Method 2: Sort + traverse backwards
    sort(v.begin(), v.end(), greater<int>());    // {35,34,12,10,1,1}
    int second = INT_MIN;
    for (int x : v) {
        if (x < v[0]) { second = x; break; }
    }
    cout << "Second Largest = " << second << endl;    // 34

    return 0;
}
```

> 💡 **Key Insight:** Using `set` automatically handles duplicates and gives sorted order.

---

## 4. Find Duplicates in Array

### 📝 Problem
Find all elements that appear **more than once**.

### 🧪 Test Cases
| # | Input | Output (Duplicates) |
|---|---|---|
| 1 | `{4, 3, 2, 7, 8, 2, 3, 1}` | `2, 3` |
| 2 | `{1, 1, 2}` | `1` |
| 3 | `{1, 2, 3}` | `(none)` |
| 4 | `{5, 5, 5, 5}` | `5` |
| 5 | `{1, 2, 2, 3, 3, 4}` | `2, 3` |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void findDuplicates(int arr[], int n) {
    // Manual frequency count using extra array
    int freq[1001] = {0};    // Assuming values 0-1000

    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    cout << "Duplicates: ";
    for (int i = 0; i <= 1000; i++) {
        if (freq[i] > 1)
            cout << i << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {4, 3, 2, 7, 8, 2, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    findDuplicates(arr, n);
    // Output: Duplicates: 2 3
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

int main() {
    vector<int> v = {4, 3, 2, 7, 8, 2, 3, 1};

    unordered_map<int, int> freq;
    for (int x : v) freq[x]++;    // Count frequency

    cout << "Duplicates: ";
    for (auto &[val, cnt] : freq) {
        if (cnt > 1) cout << val << " ";
    }
    cout << endl;
    // Output: Duplicates: 2 3

    return 0;
}
```

> 💡 **Key Insight:** `unordered_map` gives O(1) average frequency count. Much cleaner and handles any value range.

---

## 5. Two Sum (Find Pair with Given Sum)

### 📝 Problem
Find **indices of two numbers** that add up to a target sum.

### 🧪 Test Cases
| # | Input Array | Target | Output (indices) |
|---|---|---|---|
| 1 | `{2, 7, 11, 15}` | 9 | `[0, 1]` (2+7=9) |
| 2 | `{3, 2, 4}` | 6 | `[1, 2]` (2+4=6) |
| 3 | `{3, 3}` | 6 | `[0, 1]` |
| 4 | `{1, 5, 3, 7}` | 8 | `[1, 2]` (5+3=8) |
| 5 | `{-3, 4, 1, 2}` | 1 | `[0, 2]` (-3+4=1)... or [0,2] (-3+1=-2?) → `[0,1]` (-3+4=1) ✓ |

---

### ✅ Solution WITHOUT STL (Brute Force — O(n²))

```cpp
#include <iostream>
using namespace std;

void twoSum(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] + arr[j] == target) {
                cout << "Indices: [" << i << ", " << j << "]" << endl;
                cout << "Values: " << arr[i] << " + " << arr[j] << endl;
                return;
            }
        }
    }
    cout << "No pair found!" << endl;
}

int main() {
    int arr[] = {2, 7, 11, 15};
    twoSum(arr, 4, 9);
    // Output: Indices: [0, 1]
    return 0;
}
```

---

### ✅ Solution WITH STL (Hash Map — O(n))

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

void twoSum(vector<int>& v, int target) {
    unordered_map<int, int> seen;   // value → index

    for (int i = 0; i < v.size(); i++) {
        int complement = target - v[i];   // What we need

        if (seen.count(complement)) {     // Already seen it?
            cout << "Indices: [" << seen[complement] << ", " << i << "]" << endl;
            cout << "Values: " << complement << " + " << v[i] << endl;
            return;
        }
        seen[v[i]] = i;    // Store current number with its index
    }
    cout << "No pair found!" << endl;
}

int main() {
    vector<int> v = {2, 7, 11, 15};
    twoSum(v, 9);
    // Output: Indices: [0, 1]
    return 0;
}
```

> 💡 **Key Insight:** For each element, check if `target - element` was already seen. O(n) instead of O(n²)!

---

## 6. Sort an Array

### 📝 Problem
Sort an array in **ascending and descending** order.

### 🧪 Test Cases
| # | Input | Ascending | Descending |
|---|---|---|---|
| 1 | `{5, 2, 8, 1, 9}` | `{1,2,5,8,9}` | `{9,8,5,2,1}` |
| 2 | `{3, 3, 1, 1, 2}` | `{1,1,2,3,3}` | `{3,3,2,1,1}` |
| 3 | `{-5, 0, 3, -1}` | `{-5,-1,0,3}` | `{3,0,-1,-5}` |
| 4 | `{1}` | `{1}` | `{1}` |
| 5 | `{9, 8, 7, 6}` | `{6,7,8,9}` | `{9,8,7,6}` |

---

### ✅ Solution WITHOUT STL (Bubble Sort — O(n²))

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (!swapped) break;    // Optimized: stop if no swap
    }
}

int main() {
    int arr[] = {5, 2, 8, 1, 9};
    int n = 5;
    bubbleSort(arr, n);
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    // Output: 1 2 5 8 9
    return 0;
}
```

---

### ✅ Solution WITH STL (O(n log n))

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {5, 2, 8, 1, 9};

    // Ascending
    sort(v.begin(), v.end());
    cout << "Ascending: ";
    for (int x : v) cout << x << " ";    // 1 2 5 8 9
    cout << endl;

    // Descending
    sort(v.begin(), v.end(), greater<int>());
    cout << "Descending: ";
    for (int x : v) cout << x << " ";    // 9 8 5 2 1
    cout << endl;

    return 0;
}
```

> 💡 **Key Insight:** STL `sort()` uses IntroSort (Quicksort + Heapsort + Insertion sort) → extremely fast in practice!

---

## 7. Rotate Array by K Positions

### 📝 Problem
Rotate array to the **right by K positions**.

### 🧪 Test Cases
| # | Input | K | Output |
|---|---|---|---|
| 1 | `{1,2,3,4,5}` | 2 | `{4,5,1,2,3}` |
| 2 | `{1,2,3}` | 1 | `{3,1,2}` |
| 3 | `{1,2,3,4,5}` | 5 | `{1,2,3,4,5}` (full rotation) |
| 4 | `{-1,-100,3,99}` | 2 | `{3,99,-1,-100}` |
| 5 | `{1,2,3,4,5}` | 7 | `{4,5,1,2,3}` (K%n = 2) |

---

### ✅ Solution WITHOUT STL (Reversal Algorithm — O(n))

```cpp
#include <iostream>
using namespace std;

void reverse(int arr[], int left, int right) {
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++; right--;
    }
}

void rotateRight(int arr[], int n, int k) {
    k = k % n;              // Handle k > n
    reverse(arr, 0, n-1);   // Step 1: Reverse entire array
    reverse(arr, 0, k-1);   // Step 2: Reverse first k elements
    reverse(arr, k, n-1);   // Step 3: Reverse remaining elements
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    rotateRight(arr, 5, 2);
    for (int i = 0; i < 5; i++) cout << arr[i] << " ";
    // Output: 4 5 1 2 3
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    int k = 2;
    int n = v.size();
    k = k % n;

    // Rotate right by k: rotate begin to (n-k)
    rotate(v.begin(), v.begin() + (n - k), v.end());

    for (int x : v) cout << x << " ";
    // Output: 4 5 1 2 3
    return 0;
}
```

> 💡 **Key Insight:** `rotate(first, new_begin, last)` — the element at `new_begin` becomes the first element.

---

## 8. Maximum Subarray Sum (Kadane's Algorithm)

### 📝 Problem
Find the **contiguous subarray** with the **maximum sum**.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{-2,1,-3,4,-1,2,1,-5,4}` | 6 (subarray `{4,-1,2,1}`) |
| 2 | `{1}` | 1 |
| 3 | `{-1,-2,-3}` | -1 (least negative) |
| 4 | `{5,4,-1,7,8}` | 23 (all elements) |
| 5 | `{-2,-1}` | -1 |

---

### ✅ Solution WITHOUT STL (Kadane's — O(n))

```cpp
#include <iostream>
#include <climits>
using namespace std;

int maxSubarraySum(int arr[], int n) {
    int maxSum = INT_MIN;    // Handles all-negative arrays
    int currentSum = 0;

    for (int i = 0; i < n; i++) {
        currentSum += arr[i];

        if (currentSum > maxSum)
            maxSum = currentSum;     // Update best

        if (currentSum < 0)
            currentSum = 0;          // Reset — negative prefix hurts!
    }

    return maxSum;
}

int main() {
    int arr[] = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    cout << "Max Subarray Sum = " << maxSubarraySum(arr, 9);
    // Output: 6
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <numeric>
#include <climits>
using namespace std;

int main() {
    vector<int> v = {-2, 1, -3, 4, -1, 2, 1, -5, 4};

    int maxSum = INT_MIN, currSum = 0;

    for (int x : v) {                    // Range-based for loop (STL iterator style)
        currSum = max(x, currSum + x);   // STL max for current decision
        maxSum  = max(maxSum, currSum);   // STL max for running best
    }

    cout << "Max Subarray Sum = " << maxSum;
    // Output: 6

    return 0;
}
```

> 💡 **Key Insight:** Kadane's is O(n) — optimal. The core idea: restart from current element if adding previous sum makes it worse.

---

## 9. Find Missing Number (1 to N)

### 📝 Problem
Given array of `n-1` numbers from 1 to N, find the **missing number**.

### 🧪 Test Cases
| # | N | Input | Missing |
|---|---|---|---|
| 1 | 5 | `{1,2,4,5}` | 3 |
| 2 | 6 | `{1,2,3,5,6}` | 4 |
| 3 | 3 | `{1,3}` | 2 |
| 4 | 4 | `{2,3,4}` | 1 |
| 5 | 5 | `{1,2,3,4}` | 5 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

int findMissing(int arr[], int n) {
    // Expected sum of 1 to n = n*(n+1)/2
    int expectedSum = n * (n + 1) / 2;

    int actualSum = 0;
    for (int i = 0; i < n - 1; i++)
        actualSum += arr[i];

    return expectedSum - actualSum;   // Missing = expected - actual
}

int main() {
    int arr[] = {1, 2, 4, 5};   // Missing 3 from 1..5
    int n = 5;
    cout << "Missing = " << findMissing(arr, n);
    // Output: Missing = 3
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <numeric>
using namespace std;

int main() {
    vector<int> v = {1, 2, 4, 5};
    int n = 5;

    int expectedSum = n * (n + 1) / 2;
    int actualSum = accumulate(v.begin(), v.end(), 0);   // STL sum

    cout << "Missing = " << expectedSum - actualSum;
    // Output: Missing = 3

    return 0;
}
```

> 💡 **Key Insight:** Sum formula `n*(n+1)/2` avoids sorting. XOR trick also works: XOR all 1..N with all array elements.

---

## 10. Move Zeros to End

### 📝 Problem
Move all **zeros to the end** while maintaining relative order of non-zero elements.

### 🧪 Test Cases
| # | Input | Output |
|---|---|---|
| 1 | `{0,1,0,3,12}` | `{1,3,12,0,0}` |
| 2 | `{0,0,0}` | `{0,0,0}` |
| 3 | `{1,2,3}` | `{1,2,3}` |
| 4 | `{0,1}` | `{1,0}` |
| 5 | `{4,0,0,0,9,0,1}` | `{4,9,1,0,0,0,0}` |

---

### ✅ Solution WITHOUT STL (Two Pointer — O(n))

```cpp
#include <iostream>
using namespace std;

void moveZeros(int arr[], int n) {
    int insertPos = 0;    // Position to place next non-zero

    // Place all non-zeros at front
    for (int i = 0; i < n; i++) {
        if (arr[i] != 0) {
            arr[insertPos++] = arr[i];
        }
    }

    // Fill rest with zeros
    while (insertPos < n) arr[insertPos++] = 0;
}

int main() {
    int arr[] = {0, 1, 0, 3, 12};
    moveZeros(arr, 5);
    for (int i = 0; i < 5; i++) cout << arr[i] << " ";
    // Output: 1 3 12 0 0
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {0, 1, 0, 3, 12};

    // stable_partition: keep non-zeros at front (stable = preserve order)
    stable_partition(v.begin(), v.end(), [](int x){ return x != 0; });

    for (int x : v) cout << x << " ";
    // Output: 1 3 12 0 0
    return 0;
}
```

> 💡 **Key Insight:** `stable_partition` keeps relative order. Manually, track `insertPos` and write non-zeros first.

---

## 11. Merge Two Sorted Arrays

### 📝 Problem
Merge two sorted arrays into a single sorted array.

### 🧪 Test Cases
| # | Array 1 | Array 2 | Merged |
|---|---|---|---|
| 1 | `{1,3,5}` | `{2,4,6}` | `{1,2,3,4,5,6}` |
| 2 | `{1,2,3}` | `{4,5,6}` | `{1,2,3,4,5,6}` |
| 3 | `{1}` | `{2}` | `{1,2}` |
| 4 | `{}` | `{1,2,3}` | `{1,2,3}` |
| 5 | `{1,1,2}` | `{1,3,4}` | `{1,1,1,2,3,4}` |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

void mergeArrays(int a[], int m, int b[], int n, int result[]) {
    int i = 0, j = 0, k = 0;

    while (i < m && j < n) {
        if (a[i] <= b[j])
            result[k++] = a[i++];
        else
            result[k++] = b[j++];
    }
    while (i < m) result[k++] = a[i++];   // Remaining of a
    while (j < n) result[k++] = b[j++];   // Remaining of b
}

int main() {
    int a[] = {1, 3, 5};
    int b[] = {2, 4, 6};
    int result[6];
    mergeArrays(a, 3, b, 3, result);
    for (int i = 0; i < 6; i++) cout << result[i] << " ";
    // Output: 1 2 3 4 5 6
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> a = {1, 3, 5};
    vector<int> b = {2, 4, 6};
    vector<int> result(a.size() + b.size());

    // Merge two sorted ranges into result
    merge(a.begin(), a.end(), b.begin(), b.end(), result.begin());

    for (int x : result) cout << x << " ";
    // Output: 1 2 3 4 5 6
    return 0;
}
```

> 💡 **Key Insight:** Two-pointer approach is O(m+n) — optimal. Always compare front elements of both arrays.

---

## 12. Remove Duplicates from Sorted Array

### 📝 Problem
Remove duplicates **in-place** from a sorted array and return new length.

### 🧪 Test Cases
| # | Input | Output Array | New Length |
|---|---|---|---|
| 1 | `{1,1,2}` | `{1,2}` | 2 |
| 2 | `{0,0,1,1,1,2,2,3,3,4}` | `{0,1,2,3,4}` | 5 |
| 3 | `{1}` | `{1}` | 1 |
| 4 | `{1,2,3,4}` | `{1,2,3,4}` | 4 |
| 5 | `{5,5,5,5}` | `{5}` | 1 |

---

### ✅ Solution WITHOUT STL

```cpp
#include <iostream>
using namespace std;

int removeDuplicates(int arr[], int n) {
    if (n == 0) return 0;

    int insertPos = 1;    // Position for next unique element

    for (int i = 1; i < n; i++) {
        if (arr[i] != arr[i - 1]) {    // New unique element found
            arr[insertPos++] = arr[i];
        }
    }

    return insertPos;   // New length
}

int main() {
    int arr[] = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};
    int n = 10;
    int newLen = removeDuplicates(arr, n);
    for (int i = 0; i < newLen; i++) cout << arr[i] << " ";
    // Output: 0 1 2 3 4
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};

    // unique() moves duplicates to end, returns iterator to new end
    auto newEnd = unique(v.begin(), v.end());
    v.erase(newEnd, v.end());    // Actually erase them

    cout << "New length = " << v.size() << endl;    // 5
    for (int x : v) cout << x << " ";               // 0 1 2 3 4
    return 0;
}
```

> 💡 **Key Insight:** `unique()` only removes **consecutive** duplicates — so array MUST be sorted first!

---

## 13. Find Majority Element (> N/2 times)

### 📝 Problem
Find element appearing **more than N/2 times** (Moore's Voting Algorithm).

### 🧪 Test Cases
| # | Input | Majority Element |
|---|---|---|
| 1 | `{3,2,3}` | 3 |
| 2 | `{2,2,1,1,1,2,2}` | 2 |
| 3 | `{1}` | 1 |
| 4 | `{1,2,1,2,1}` | 1 |
| 5 | `{6,6,6,3,3}` | 6 |

---

### ✅ Solution WITHOUT STL (Moore's Voting — O(n))

```cpp
#include <iostream>
using namespace std;

int majorityElement(int arr[], int n) {
    // Phase 1: Find candidate
    int candidate = arr[0], count = 1;

    for (int i = 1; i < n; i++) {
        if (arr[i] == candidate)
            count++;
        else
            count--;

        if (count == 0) {
            candidate = arr[i];
            count = 1;
        }
    }

    // Phase 2: Verify candidate (skip if guaranteed)
    int verify = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] == candidate) verify++;

    return (verify > n / 2) ? candidate : -1;
}

int main() {
    int arr[] = {2, 2, 1, 1, 1, 2, 2};
    cout << "Majority = " << majorityElement(arr, 7);
    // Output: Majority = 2
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {2, 2, 1, 1, 1, 2, 2};
    int n = v.size();

    unordered_map<int, int> freq;
    for (int x : v) freq[x]++;

    for (auto &[val, cnt] : freq) {
        if (cnt > n / 2) {
            cout << "Majority = " << val << endl;
            return 0;
        }
    }
    cout << "No majority element" << endl;
    return 0;
}
```

> 💡 **Key Insight:** Moore's Voting is O(n) time O(1) space — optimal! Frequency map is O(n) space.

---

## 14. Subarray with Given Sum

### 📝 Problem
Find a **contiguous subarray** with sum equal to target (non-negative numbers).

### 🧪 Test Cases
| # | Input | Target | Found Range |
|---|---|---|---|
| 1 | `{1,2,3,7,5}` | 12 | indices [1,3] (2+3+7=12) |
| 2 | `{1,2,3,4,5}` | 9 | indices [1,4] (2+3+4=9)? → [2,4] (3+4+5-no) → 2+3+4=9 yes [1,3] |
| 3 | `{1,4,20,3,10,5}` | 33 | indices [2,4] |
| 4 | `{15,2,4,8,9,5,10,23}` | 23 | indices [1,4] |
| 5 | `{5,5,5,5}` | 10 | indices [0,1] |

---

### ✅ Solution WITHOUT STL (Sliding Window — O(n))

```cpp
#include <iostream>
using namespace std;

void subarrayWithSum(int arr[], int n, int target) {
    int left = 0, currSum = 0;

    for (int right = 0; right < n; right++) {
        currSum += arr[right];

        // Shrink window from left if sum exceeds target
        while (currSum > target && left <= right)
            currSum -= arr[left++];

        if (currSum == target) {
            cout << "Found! Indices [" << left << ", " << right << "]" << endl;
            return;
        }
    }
    cout << "Not found!" << endl;
}

int main() {
    int arr[] = {1, 2, 3, 7, 5};
    subarrayWithSum(arr, 5, 12);
    // Output: Found! Indices [1, 3]
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> v = {1, 2, 3, 7, 5};
    int target = 12;

    int left = 0, currSum = 0;

    for (int right = 0; right < (int)v.size(); right++) {
        currSum += v[right];

        while (currSum > target && left <= right)
            currSum -= v[left++];

        if (currSum == target) {
            cout << "Found! Indices [" << left << ", " << right << "]" << endl;
            // Subarray elements:
            for (int i = left; i <= right; i++) cout << v[i] << " ";
            return 0;
        }
    }
    cout << "Not found!" << endl;
    return 0;
}
```

> 💡 **Key Insight:** Sliding window avoids nested loops → O(n). Works only for **non-negative** numbers.

---

## 15. Leaders in an Array

### 📝 Problem
An element is a **leader** if it is greater than all elements to its right.

### 🧪 Test Cases
| # | Input | Leaders |
|---|---|---|
| 1 | `{16,17,4,3,5,2}` | `17, 5, 2` |
| 2 | `{1,2,3,4,5}` | `5` |
| 3 | `{5,4,3,2,1}` | `5,4,3,2,1` (all are leaders) |
| 4 | `{7}` | `7` |
| 5 | `{3,3,3,2,1}` | `3,3,2,1` (first = not leader, depends on strict >) |

---

### ✅ Solution WITHOUT STL (Right to Left — O(n))

```cpp
#include <iostream>
using namespace std;

void findLeaders(int arr[], int n) {
    int maxFromRight = arr[n - 1];   // Last element is always a leader
    cout << maxFromRight << " ";

    // Traverse from second-last to first
    for (int i = n - 2; i >= 0; i--) {
        if (arr[i] >= maxFromRight) {
            cout << arr[i] << " ";
            maxFromRight = arr[i];
        }
    }
    cout << endl;
}

int main() {
    int arr[] = {16, 17, 4, 3, 5, 2};
    cout << "Leaders: ";
    findLeaders(arr, 6);
    // Output: Leaders: 2 5 17  (right to left order)
    return 0;
}
```

---

### ✅ Solution WITH STL

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {16, 17, 4, 3, 5, 2};
    vector<int> leaders;

    int maxRight = v.back();
    leaders.push_back(maxRight);

    for (int i = (int)v.size() - 2; i >= 0; i--) {
        if (v[i] >= maxRight) {
            maxRight = v[i];
            leaders.push_back(v[i]);
        }
    }

    reverse(leaders.begin(), leaders.end());   // Restore original order

    cout << "Leaders: ";
    for (int x : leaders) cout << x << " ";
    // Output: Leaders: 17 5 2
    return 0;
}
```

> 💡 **Key Insight:** Traverse from RIGHT to LEFT — the running maximum from right tells you if current is a leader.

---

## 📘 Quick Reference — All Patterns

| Problem | Technique | Time | Space |
|---|---|---|---|
| Max/Min | Linear scan | O(n) | O(1) |
| Reverse | Two pointers | O(n) | O(1) |
| Second Largest | Two variables | O(n) | O(1) |
| Duplicates | Hash map | O(n) | O(n) |
| Two Sum | Hash map | O(n) | O(n) |
| Sort | Bubble/STL sort | O(n²)/O(n log n) | O(1) |
| Rotate | Reversal trick | O(n) | O(1) |
| Max Subarray | Kadane's | O(n) | O(1) |
| Missing Number | Sum formula | O(n) | O(1) |
| Move Zeros | Two pointers | O(n) | O(1) |
| Merge Sorted | Two pointers | O(m+n) | O(m+n) |
| Remove Duplicates | Two pointers | O(n) | O(1) |
| Majority Element | Moore's Voting | O(n) | O(1) |
| Subarray Sum | Sliding window | O(n) | O(1) |
| Leaders | Right scan | O(n) | O(n) |

---

## 🚨 Common Array Mistakes to AVOID

| Mistake ❌ | Correct ✅ |
|---|---|
| Array index starting at 1 | C++ arrays are **0-indexed**: `arr[0]` to `arr[n-1]` |
| `sizeof(arr)` gives element count | `sizeof(arr)/sizeof(arr[0])` gives count |
| Accessing `arr[n]` | Valid indices: `0` to `n-1` only |
| Modifying while iterating | Use a copy or index carefully |
| Integer overflow in sum | Use `long long` for large sums |
| `int/int` loses decimal | Cast: `(double)sum/count` |

---
*Array Problems Guide | TCS NQT & Competitive Programming | With & Without STL*
