---
layout: post
title: "Binary Search Doesn’t Need a Sorted Array?"
date: 2026-05-30 19:00:00 +0000
categories: [blog, cp]
tags: [cp]
---

# Binary Search on a Mountain Array

I used to think binary search only worked on sorted (non-decreasing) arrays. 
Recently, I found an interesting application: binary search can also be used to find the peak of a mountain array.

A mountain array is an array that first increases and then decreases.

Formally,

$$
a_1 \le a_2 \le a_3 \le \cdots \le a_{peak}
\ge \cdots \ge a_{n-2} \ge a_{n-1} \ge a_n
$$

Consider the following array:

`1, 2, 3, 4, 4, 5, 6, 7, 7, 7, 4, 3, 3, 2, 2`

The peak value is `7`.

The key observation is that if we compare two consecutive elements:

- If `a[mid] >= a[mid - 1]`, we are still on the increasing part (or at the plateau of the peak), so we can move right.
- Otherwise, we are on the decreasing part, so we move left.

```cpp
int lft = 0, rgt = n - 1;
int ans = 0;

while (lft <= rgt) 
{
    int mid = lft + (rgt - lft) / 2;

    int a = arr[mid - 1];
    int b = arr[mid];

    if (b >= a) 
    {
        ans = b;
        lft = mid + 1;
    } 
    else 
    {
        rgt = mid - 1;
    }
}
```

The idea is simple: compare two consecutive elements and determine whether the sequence is still increasing. This allows binary search to locate the peak in logarithmic time.

---

Related resources:

- Related problem: https://codeforces.com/contest/2232/problem/C2
- My solution: https://codeforces.com/contest/2232/submission/376757771
- Editorial: https://codeforces.com/blog/entry/154128
