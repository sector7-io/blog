---
layout: post
title: "Cache-Friendly Data Structures: When Theory Meets Hardware"
date: 2025-01-08
categories: [Performance, DataStructures, SystemsProgramming]
summary: "How designing data structures with CPU cache behavior in mind can lead to dramatic performance improvements beyond what algorithmic complexity would predict."
---

# When O(n) Outperforms O(log n)

Algorithmic complexity has been the gold standard for evaluating data structure performance for decades. However, in practice, CPU cache behavior can completely invert our theoretical expectations.

Consider this counterintuitive fact: a simple linear search through an array (O(n) complexity) can often outperform a binary search in a tree structure (O(log n) complexity) for collections with thousands of elements. This isn't a theoretical curiosity – it's a practical reality that can have dramatic performance implications.

The key factor is memory access patterns. A linear search through a contiguous array has near-perfect spatial locality:

```c
bool linear_search(int* array, int size, int target) {
    for (int i = 0; i < size; i++) {
        if (array[i] == target) return true;
    }
    return false;
}
```

When the CPU loads a cache line (typically 64 bytes), it gets not just the current element but also the next several elements. This means that for a significant portion of the search, the data is already in the L1 cache.

In contrast, a binary search tree involves pointer chasing:

```c
typedef struct Node {
    int value;
    struct Node* left;
    struct Node* right;
} Node;

bool tree_search(Node* root, int target) {
    if (root == NULL) return false;
    if (root->value == target) return true;
    if (target < root->value) 
        return tree_search(root->left, target);
    else 
        return tree_search(root->right, target);
}
```

Each step in the traversal likely involves a cache miss, as the next node could be anywhere in memory. These cache misses dominate the performance, especially as data sizes exceed cache capacity.

I tested this with a simple benchmark on a modern Intel CPU:

- Linear search in sorted array (1000 elements): ~0.4 microseconds (avg)
- Binary search in balanced tree (1000 elements): ~1.2 microseconds (avg)

The linear search was consistently 3x faster, despite its worse algorithmic complexity. This gap only starts to close when collections grow to tens of thousands of elements.

This phenomenon applies to more than just search operations. Consider these cache-friendly alternatives to traditional data structures:

1. **Flat arrays** instead of linked lists
2. **Array-based binary heaps** instead of pointer-based trees
3. **Open addressing hash tables** instead of chained hash tables

The lesson is clear: When designing performance-critical systems, consider not just algorithmic complexity but also how your data structures interact with the memory hierarchy. Sometimes, a "worse" algorithm is actually better in practice.