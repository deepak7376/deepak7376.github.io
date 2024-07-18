---
layout: post
comments: true
title:  "Interview Coding Patterns Cheatsheet"
date:   2024-07-05 00:04:58 +0530
categories: general
description: Interview Coding Patterns Cheatsheet.
---

---

## Interview Coding Patterns Cheatsheet

### 1. Two Pointers
Used for problems involving pairs in an array or linked list.

**Example Problem**: Find two numbers in a sorted array that add up to a target sum.

```python
def two_sum(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        current_sum = nums[left] + nums[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return []

nums = [1, 2, 3, 4, 6]
target = 6
print(two_sum(nums, target))  # Output: [1, 3]
```

### 2. Sliding Window
Used for problems involving a contiguous subarray.

**Example Problem**: Find the maximum sum of a subarray of size `k`.

```python
def max_sum_subarray(nums, k):
    max_sum = current_sum = sum(nums[:k])
    for i in range(k, len(nums)):
        current_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, current_sum)
    return max_sum

nums = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(nums, k))  # Output: 9
```

### 3. Fast and Slow Pointers
Used for problems involving cycles in linked lists or arrays.

**Example Problem**: Detect a cycle in a linked list.

```python
class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next

def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

# Creating a cycle for testing
node1 = ListNode(1)
node2 = ListNode(2)
node3 = ListNode(3)
node4 = ListNode(4)
node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node2

print(has_cycle(node1))  # Output: True
```

### 4. Merge Intervals
Used for problems involving overlapping intervals.

**Example Problem**: Merge overlapping intervals.

```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    for current in intervals[1:]:
        last = merged[-1]
        if current[0] <= last[1]:
            last[1] = max(last[1], current[1])
        else:
            merged.append(current)
    return merged

intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
print(merge_intervals(intervals))  # Output: [[1, 6], [8, 10], [15, 18]]
```

### 5. Cyclic Sort
Used for problems involving numbers in a given range.

**Example Problem**: Find the missing number in an array containing `n` distinct numbers taken from 0 to `n`.

```python
def find_missing_number(nums):
    i, n = 0, len(nums)
    while i < n:
        j = nums[i]
        if j < n and nums[i] != nums[j]:
            nums[i], nums[j] = nums[j], nums[i]
        else:
            i += 1
    for i in range(n):
        if nums[i] != i:
            return i
    return n

nums = [4, 0, 3, 1]
print(find_missing_number(nums))  # Output: 2
```

### 6. In-place Reversal of a Linked List
Used for problems involving reversing the nodes of a linked list in place.

**Example Problem**: Reverse a linked list.

```python
def reverse_list(head):
    prev = None
    while head:
        next_node = head.next
        head.next = prev
        prev = head
        head = next_node
    return prev

# Creating a linked list for testing
node1 = ListNode(1)
node2 = ListNode(2)
node3 = ListNode(3)
node4 = ListNode(4)
node1.next = node2
node2.next = node3
node3.next = node4

reversed_head = reverse_list(node1)
while reversed_head:
    print(reversed_head.value, end=" ")
    reversed_head = reversed_head.next  # Output: 4 3 2 1
```

### 7. Tree Traversal
Used for problems involving tree traversals.

**Example Problem**: Perform in-order traversal of a binary tree.

```python
class TreeNode:
    def __init__(self, value=0, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

def inorder_traversal(root):
    result = []
    def traverse(node):
        if not node:
            return
        traverse(node.left)
        result.append(node.value)
        traverse(node.right)
    traverse(root)
    return result

# Creating a binary tree for testing
root = TreeNode(1)
root.right = TreeNode(2)
root.right.left = TreeNode(3)

print(inorder_traversal(root))  # Output: [1, 3, 2]
```

### 8. Subsets
Used for problems involving subsets of a set.

**Example Problem**: Generate all subsets of a given set.

```python
def subsets(nums):
    result = []
    def backtrack(start, current):
        result.append(list(current))
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()
    backtrack(0, [])
    return result

nums = [1, 2, 3]
print(subsets(nums))  # Output: [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```

### 9. Topological Sort
Used for problems involving directed acyclic graphs (DAGs).

**Example Problem**: Find a topological ordering of a given graph.

```python
from collections import defaultdict, deque

def topological_sort(vertices, edges):
    graph = defaultdict(list)
    in_degree = {i: 0 for i in range(vertices)}
    for u, v in edges:
        graph[u].append(v)
        in_degree[v] += 1
    queue = deque([k for k in in_degree if in_degree[k] == 0])
    sorted_order = []
    while queue:
        vertex = queue.popleft()
        sorted_order.append(vertex)
        for neighbor in graph[vertex]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    return sorted_order if len(sorted_order) == vertices else []

vertices = 6
edges = [(5, 2), (5, 0), (4, 0), (4, 1), (2, 3), (3, 1)]
print(topological_sort(vertices, edges))  # Output: [4, 5, 2, 0, 3, 1]
```

### 10. Dynamic Programming
Used for problems involving overlapping subproblems and optimal substructure.

**Example Problem**: Find the length of the longest increasing subsequence.

```python
def length_of_lis(nums):
    if not nums:
        return 0
    dp = [1] * len(nums)
    for i in range(len(nums)):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)

nums = [10, 9, 2, 5, 3, 7, 101, 18]
print(length_of_lis(nums))  # Output: 4 (2, 3, 7, 101)
```

---
