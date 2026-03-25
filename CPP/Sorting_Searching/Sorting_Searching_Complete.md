# 🔍 SORTING & SEARCHING — Complete Guide + Problems
### Master the Core Interview Algorithms | Zero → Hero 🚀

---

## 📌 TABLE OF CONTENTS

### PART A — SEARCHING ALGORITHMS
1. [Linear Search (O(N))](#1-linear-search-on)
2. [Binary Search (O(log N))](#2-binary-search-olog-n)
3. [STL Searching Methods (`find`, `binary_search`)](#3-stl-searching-methods)
4. [STL Lower Bound & Upper Bound](#4-stl-lower-bound--upper-bound)

### PART B — SORTING ALGORITHMS (Implementations)
5. [Bubble Sort (O(N²))](#5-bubble-sort-on)
6. [Selection Sort (O(N²))](#6-selection-sort-on)
7. [Insertion Sort (O(N²))](#7-insertion-sort-on)
8. [Merge Sort (O(N log N))](#8-merge-sort-on-log-n)
9. [Quick Sort (O(N log N))](#9-quick-sort-on-log-n)
10. [STL Sorting (`sort`, Custom Comparators)](#10-stl-sorting-custom-comparators)

### PART C — SORTING & SEARCHING PROBLEMS
11. [Find First and Last Occurrence of Element](#11-find-first-and-last-occurrence-of-element)
12. [Search in Rotated Sorted Array](#12-search-in-rotated-sorted-array)
13. [Find Minimum in Rotated Sorted Array](#13-find-minimum-in-rotated-sorted-array)
14. [Square Root using Binary Search](#14-square-root-using-binary-search)
15. [Peak Index in a Mountain Array](#15-peak-index-in-a-mountain-array)
16. [Sort Array of 0s, 1s, and 2s (Dutch National Flag)](#16-sort-array-of-0s-1s-and-2s-dutch-national-flag)
17. [Merge Intervals](#17-merge-intervals)
18. [Count Inversions (Merge Sort Trick)](#18-count-inversions-merge-sort-trick)
19. [Aggressive Cows / Book Allocation (Binary Search on Answer)](#19-aggressive-cows--book-allocation-binary-search-on-answer)

---

# ═══════════════════════════════════
# PART A — SEARCHING ALGORITHMS
# ═══════════════════════════════════

## 1. Linear Search (O(N))

Checks every element one by one. Works on **unsorted** arrays.

### ✅ Solution
```cpp
int linearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) return i;  // Found! Return index
    }
    return -1;  // Not found
}
```

---

## 2. Binary Search (O(log N))

Halves the search space every step. **MUST BE SORTED!**

### ✅ Solution (Iterative - Best Practice)
```cpp
int binarySearch(int arr[], int n, int target) {
    int left = 0, right = n - 1;

    while (left <= right) {
        // Prevent integer overflow: left + (right - left) / 2
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) return mid;         // Found
        else if (arr[mid] < target) left = mid + 1; // Search right half
        else right = mid - 1;                       // Search left half
    }
    return -1; // Not found
}
```

---

## 3. STL Searching Methods

C++ provides built-in functions for both linear and binary search!

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Required!
using namespace std;

int main() {
    vector<int> v = {10, 20, 30, 40, 50};

    // ── 1. STL LINEAR SEARCH (find) ──
    auto it = find(v.begin(), v.end(), 30);
    if (it != v.end()) {
        cout << "Found at index: " << (it - v.begin()) << "\n";
    }

    // ── 2. STL BINARY SEARCH (returns true/false) ──
    bool exists = binary_search(v.begin(), v.end(), 40);
    cout << "40 exists? " << (exists ? "Yes" : "No") << "\n";

    return 0;
}
```

---

## 4. STL Lower Bound & Upper Bound

Crucial tools for Competitive Programming and TCS NQT.
*   **`lower_bound(X)`**: Iterator to **first element ≥ X**
*   **`upper_bound(X)`**: Iterator to **first element > X**

```cpp
vector<int> v = {10, 20, 30, 30, 30, 40, 50};

// Find first element >= 30
auto lb = lower_bound(v.begin(), v.end(), 30);
cout << "Lower bound index: " << (lb - v.begin()) << "\n"; // Index 2

// Find first element > 30
auto ub = upper_bound(v.begin(), v.end(), 30);
cout << "Upper bound index: " << (ub - v.begin()) << "\n"; // Index 5

// Count occurrences of 30!
int count = ub - lb; // 5 - 2 = 3
```

---

# ═══════════════════════════════════
# PART B — SORTING ALGORITHMS
# ═══════════════════════════════════

## 5. Bubble Sort (O(N²))
Swaps adjacent elements if they are in the wrong order. Heaviest elements "bubble" to the end.

```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false; // Optimization
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break; // Array is sorted!
    }
}
```

---

## 6. Selection Sort (O(N²))
Selects the minimum element from the unsorted part and swaps it to the front.

```cpp
void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr[i], arr[minIndex]);
    }
}
```

---

## 7. Insertion Sort (O(N²))
Places each element into its correct position in the left (sorted) part. Great for small or mostly sorted arrays.

```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // Shift elements right to make room
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

---

## 8. Merge Sort (O(N log N))
Divide & Conquer. Halves the array, sorts the halves recursively, and merges them.

```cpp
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    vector<int> L(n1), R(n2);

    for (int i = 0; i < n1; i++) L[i] = arr[left + i];
    for (int j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];

    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int left, int right) {
    if (left >= right) return;
    int mid = left + (right - left) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}
```

---

## 9. Quick Sort (O(N log N))
Divide & Conquer. Picks a "pivot", places smaller elements to the left, larger to the right, and recurses.

```cpp
int partition(int arr[], int low, int high) {
    int pivot = arr[high]; // Choosing last element as pivot
    int i = low - 1;

    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1; // Final position of pivot
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

---

## 10. STL Sorting (`sort`, Custom Comparators)

**Never write sorting algorithms manually in an interview unless specifically asked.** Always use `std::sort()`!

```cpp
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> v = {50, 20, 40, 10, 30};

    // ── 1. ASCENDING SORT (O(N log N)) ──
    sort(v.begin(), v.end());  // 10 20 30 40 50

    // ── 2. DESCENDING SORT ──
    sort(v.begin(), v.end(), greater<int>()); // 50 40 30 20 10

    // ── 3. CUSTOM LAMBDA SORT (Sort by last digit) ──
    vector<int> nums = {45, 12, 89, 21};
    sort(nums.begin(), nums.end(), [](int a, int b) {
        return (a % 10) < (b % 10); // Sort by ones place
    });
    // output: 21, 12, 45, 89
}
```

---

# ═══════════════════════════════════
# PART C — SORTING & SEARCHING PROBLEMS
# ═══════════════════════════════════

## 11. Find First and Last Occurrence of Element

### 📝 Problem
Given a sorted array containing duplicates, find the first and last occurrence index of a specific element.

### 🧪 Test Cases
`[1, 2, 2, 2, 2, 3, 4, 7 ,8 ,8]`, Target `2` -> First: 1, Last: 4

### ✅ Solution (Binary Search - O(log N))
```cpp
int firstOccurrence(vector<int>& v, int target) {
    int left = 0, right = v.size() - 1, ans = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (v[mid] == target) {
            ans = mid;        // Record answer
            right = mid - 1;  // Keep looking left for earlier occurrences!
        } else if (v[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return ans;
}

int lastOccurrence(vector<int>& v, int target) {
    int left = 0, right = v.size() - 1, ans = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (v[mid] == target) {
            ans = mid;        // Record answer
            left = mid + 1;   // Keep looking right for later occurrences!
        } else if (v[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return ans;
}
```

### ✅ Solution (Using STL Lower/Upper Bound)
```cpp
void firstAndLastSTL(const vector<int>& v, int target) {
    auto lb = lower_bound(v.begin(), v.end(), target);
    auto ub = upper_bound(v.begin(), v.end(), target);

    if (lb == v.end() || *lb != target) {
        cout << "-1 -1"; // Not found
    } else {
        int first = lb - v.begin();
        int last = (ub - v.begin()) - 1;  // ub points to NEXT element
        cout << "First: " << first << " Last: " << last;
    }
}
```

---

## 12. Search in Rotated Sorted Array

### 📝 Problem
Array is sorted, but rotated at some pivot. `[4, 5, 6, 7, 0, 1, 2]`. Find target `0`. Use O(log N) time.

### ✅ Solution (Binary Search Trick)
```cpp
int searchRotated(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;

        // Check if LEFT half is properly sorted
        if (nums[left] <= nums[mid]) {
            // Is target inside the sorted left half?
            if (target >= nums[left] && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;

        // Check if RIGHT half is properly sorted
        } else {
            // Is target inside the sorted right half?
            if (target > nums[mid] && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }
    return -1;
}
```

---

## 13. Find Minimum in Rotated Sorted Array

### 📝 Problem
Find the minimum element in `[4, 5, 6, 7, 0, 1, 2]`. Ans: `0`.

### ✅ Solution (Binary Search)
```cpp
int findMin(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;

    // If already sorted without rotation
    if (nums[left] <= nums[right]) return nums[left];

    while (left < right) {
        int mid = left + (right - left) / 2;

        // If mid element is greater than rightmost element, min must be in right half (rotation is there)
        if (nums[mid] > nums[right]) {
            left = mid + 1;
        } else {
            // Min is at mid, or in the left half
            right = mid;
        }
    }
    return nums[left];
}
```

---

## 14. Square Root using Binary Search

### 📝 Problem
Find `floor(sqrt(x))` without using `sqrt()`.

### ✅ Solution
```cpp
int mySqrt(int x) {
    if (x == 0 || x == 1) return x;

    int left = 1, right = x, ans = 0;
    while (left <= right) {
        int mid = left + (right - left) / 2;

        // Check mid * mid <= x (use x/mid to prevent int overflow!)
        if (mid <= x / mid) {
            ans = mid;      // Safe answer
            left = mid + 1; // Look for higher perfectly safe answer
        } else {
            right = mid - 1;
        }
    }
    return ans;
}
```

---

## 15. Peak Index in a Mountain Array

### 📝 Problem
`[0, 1, 0]` -> Peak is index 1. `[0, 2, 1, 0]` -> Peak is index 1. Array goes strictly UP then strictly DOWN.

### ✅ Solution
```cpp
int peakIndexInMountainArray(vector<int>& arr) {
    int left = 0, right = arr.size() - 1;

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] < arr[mid + 1]) {
            // Climbing the mountain, peak is on the right
            left = mid + 1;
        } else {
            // Walking down, peak is at mid or on the left
            right = mid;
        }
    }
    return left;
}
```

---

## 16. Sort Array of 0s, 1s, and 2s (Dutch National Flag)

### 📝 Problem
Given an array of only 0s, 1s, and 2s. Sort without `sort()` in O(N).

### ✅ Solution (3-Pointer Approach)
```cpp
void sortColors(vector<int>& nums) {
    int low = 0, mid = 0, high = nums.size() - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++; mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else { // It's a 2
            swap(nums[mid], nums[high]);
            high--; // Do NOT mid++, newly swapped element needs to be checked!
        }
    }
}
```

---

## 17. Merge Intervals

### 📝 Problem
`[[1,3], [2,6], [8,10], [15,18]]` -> `[[1,6], [8,10], [15,18]]`

### ✅ Solution (Sort + Iterate)
```cpp
vector<vector<int>> mergeIntervals(vector<vector<int>>& intervals) {
    if (intervals.empty()) return {};

    // 1. Sort based on starting times
    sort(intervals.begin(), intervals.end());

    vector<vector<int>> merged;
    merged.push_back(intervals[0]); // Push first interval

    for (int i = 1; i < intervals.size(); i++) {
        // If current interval overlaps with the last added interval
        if (intervals[i][0] <= merged.back()[1]) {
            // Extend the end time
            merged.back()[1] = max(merged.back()[1], intervals[i][1]);
        } else {
            // No overlap, push to result
            merged.push_back(intervals[i]);
        }
    }
    return merged;
}
```

---

## 18. Count Inversions (Merge Sort Trick)

### 📝 Problem
How many pairs `(i, j)` exist such that `i < j` and `arr[i] > arr[j]`?

### ✅ Solution
Modify the Merge step of Merge Sort!

```cpp
int mergeAndCount(vector<int>& arr, int left, int mid, int right) {
    int i = left, j = mid + 1, inv_count = 0;
    vector<int> temp;

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp.push_back(arr[i++]);
        } else {
            temp.push_back(arr[j++]);
            // MAGIC LINE: All remaining elements in left half (i to mid) are > arr[j]
            inv_count += (mid - i + 1);
        }
    }
    while (i <= mid) temp.push_back(arr[i++]);
    while (j <= right) temp.push_back(arr[j++]);

    for (int k = left; k <= right; k++) arr[k] = temp[k - left];
    return inv_count;
}

int mergeSortAndCount(vector<int>& arr, int left, int right) {
    int inv_count = 0;
    if (left < right) {
        int mid = left + (right - left) / 2;
        inv_count += mergeSortAndCount(arr, left, mid);
        inv_count += mergeSortAndCount(arr, mid + 1, right);
        inv_count += mergeAndCount(arr, left, mid, right);
    }
    return inv_count;
}
```

---

## 19. Aggressive Cows / Book Allocation (Binary Search on Answer)

### 📝 Problem Overview
**"Minimizing the maximum"** or **"Maximizing the minimum"** problems.
E.g. Place 3 cows in 5 stalls `[1,2,8,4,9]` so the minimum distance between cows is as large as possible.

### ✅ Solution (Binary Search on Possible Answers)
```cpp
bool canPlaceCows(vector<int>& stalls, int n, int cows, int minDist) {
    int cowCount = 1;
    int lastPos = stalls[0];

    for (int i = 1; i < n; i++) {
        if (stalls[i] - lastPos >= minDist) { // Can we place it here?
            cowCount++;
            lastPos = stalls[i];
        }
        if (cowCount == cows) return true;
    }
    return false;
}

int aggressiveCows(vector<int>& stalls, int cows) {
    sort(stalls.begin(), stalls.end()); // Crucial!
    int n = stalls.size();

    int left = 1; // Min possible distance
    int right = stalls[n-1] - stalls[0]; // Max possible distance
    int ans = 0;

    // Binary Searching the DISTANCE
    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (canPlaceCows(stalls, n, cows, mid)) {
            ans = mid;      // Valid distance, let's try a LARGER one
            left = mid + 1;
        } else {
            right = mid - 1; // Invalid distance, must try a SMALLER one
        }
    }
    return ans;
}
```

---
*Sorting & Searching Guide | The Ultimate Prep Toolkit*
