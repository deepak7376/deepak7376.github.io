---
layout: post
title:  "Python Data Structures and Algorithms (DSA)"
date:   2019-01-25 00:04:58 +0530
categories: dsa
summary: Contains advance python DSA concepts.
---

## Python Data Structures and Algorithms (DSA)

### Table of Contents
1. **Data Structures**
    - Arrays
    - Linked Lists
    - Stacks
    - Queues
    - Trees
    - Graphs
    - Hash Tables
    - Heaps

2. **Algorithms**
    - Sorting
    - Searching
    - Recursion
    - Dynamic Programming
    - Greedy Algorithms
    - Backtracking
    - Graph Algorithms

---

### 1. Data Structures

#### Arrays
- **Definition**: An array is a collection of items stored at contiguous memory locations.
- **Operations**: Insertion, Deletion, Traversal
- **Code Example**:
    ```python
    # 1. Accessing Elements
    my_list = [10, 20, 30, 40, 50]

    # Indexing
    first_element = my_list[0]
    print("First element:", first_element)

    # Slicing
    sublist = my_list[1:4]
    print("Sublist:", sublist)

    # 2. Modifying Lists
    # Assignment
    my_list[0] = 100
    print("After assignment:", my_list)

    # Append
    my_list.append(60)
    print("After append:", my_list)

    # Insert
    my_list.insert(2, 'x')
    print("After insert:", my_list)

    # Extend
    my_list.extend([70, 80])
    print("After extend:", my_list)

    # Remove
    my_list.remove(30)
    print("After remove:", my_list)

    # Pop
    popped_element = my_list.pop(2)
    print("After pop:", my_list, "Popped element:", popped_element)

    # Clear
    my_list.clear()
    print("After clear:", my_list)

    # 3. Querying Lists
    my_list = [10, 20, 20, 30, 40]

    # Count
    count_20 = my_list.count(20)
    print("Count of 20:", count_20)

    # Index
    index_30 = my_list.index(30)
    print("Index of 30:", index_30)

    # 4. Sorting and Reversing
    # Sort
    my_list = [40, 10, 30, 20]
    my_list.sort()
    print("Sorted list:", my_list)

    # Sorted (creates a new list)
    sorted_list = sorted([50, 10, 30, 20])
    print("Sorted list using sorted():", sorted_list)

    # Reverse
    my_list.reverse()
    print("Reversed list:", my_list)

    # Reversed (creates an iterator)
    reversed_list = list(reversed(my_list))
    print("Reversed list using reversed():", reversed_list)

    # 5. Aggregations
    # Length
    length = len(my_list)
    print("Length of the list:", length)

    # Sum
    total_sum = sum(my_list)
    print("Sum of elements:", total_sum)

    # Min
    min_element = min(my_list)
    print("Minimum element:", min_element)

    # Max
    max_element = max(my_list)
    print("Maximum element:", max_element)

    # 6. Copying Lists
    # Shallow Copy
    shallow_copy = my_list.copy()
    print("Shallow copy:", shallow_copy)

    # Deep Copy (for nested lists)
    import copy
    nested_list = [[1, 2], [3, 4]]
    deep_copy = copy.deepcopy(nested_list)
    print("Deep copy:", deep_copy)

    # 7. List Comprehension
    doubled = [x * 2 for x in my_list]
    print("Doubled list using comprehension:", doubled)

    # 8. Membership
    is_20_in_list = 20 in my_list
    print("Is 20 in the list?", is_20_in_list)

    # 9. Iteration
    print("Elements in the list:")
    for x in my_list:
        print(x)

    # 10. Joining and Splitting
    # Joining
    string_list = ['a', 'b', 'c']
    joined_string = ''.join(string_list)
    print("Joined string:", joined_string)

    # Splitting
    split_list = "a,b,c".split(',')
    print("Split list:", split_list)
    ```

---

#### Linked Lists
- **Definition**: A linked list is a linear data structure where elements are stored in nodes, with each node pointing to the next.
- **Types**: Singly Linked List, Doubly Linked List
- **Code Example**:
    ```python
    class Node:
        def __init__(self, data):
            self.data = data
            self.next = None

    class LinkedList:
        def __init__(self):
            self.head = None

        def append(self, data):
            new_node = Node(data)
            if not self.head:
                self.head = new_node
                return
            last = self.head
            while last.next:
                last = last.next
            last.next = new_node

        def print_list(self):
            current = self.head
            while current:
                print(current.data)
                current = current.next

    ll = LinkedList()
    ll.append(1)
    ll.append(2)
    ll.append(3)
    ll.print_list()
    ```
---

#### Stacks
- **Definition**: A stack is a linear data structure that follows the LIFO (Last In, First Out) principle.
- **Operations**: Push, Pop, Peek
- **Code Example**:
    ```python
    stack = []

    # Push
    stack.append(1)
    stack.append(2)
    stack.append(3)

    # Pop
    stack.pop()  # 3

    # Peek
    print(stack[-1])  # 2
    ```
---

#### Queues
- **Definition**: A queue is a linear data structure that follows the FIFO (First In, First Out) principle.
- **Operations**: Enqueue, Dequeue
- **Code Example**:
    ```python
    from collections import deque

    queue = deque()

    # Enqueue
    queue.append(1)
    queue.append(2)
    queue.append(3)

    # Dequeue
    queue.popleft()  # 1
    ```
---

#### Trees
- **Definition**: A tree is a hierarchical data structure with nodes, where each node has zero or more children.
- **Types**: Binary Tree, Binary Search Tree (BST), AVL Tree
- **Code Example (BST)**:
    ```python
    class TreeNode:
        def __init__(self, key):
            self.left = None
            self.right = None
            self.val = key

    def insert(root, key):
        if root is None:
            return TreeNode(key)
        else:
            if root.val < key:
                root.right = insert(root.right, key)
            else:
                root.left = insert(root.left, key)
        return root

    def inorder(root):
        if root:
            inorder(root.left)
            print(root.val)
            inorder(root.right)

    root = TreeNode(50)
    root = insert(root, 30)
    root = insert(root, 20)
    root = insert(root, 40)
    root = insert(root, 70)
    root = insert(root, 60)
    root = insert(root, 80)

    inorder(root)
    ```
---

#### Graphs
- **Definition**: A graph is a collection of nodes (vertices) and edges connecting them.
- **Representations**: Adjacency Matrix, Adjacency List
- **Code Example (Adjacency List)**:
    ```python
    from collections import defaultdict

    class Graph:
        def __init__(self):
            self.graph = defaultdict(list)

        def add_edge(self, u, v):
            self.graph[u].append(v)

        def dfs_util(self, v, visited):
            visited.add(v)
            print(v, end=' ')
            for neighbour in self.graph[v]:
                if neighbour not in visited:
                    self.dfs_util(neighbour, visited)

        def dfs(self, v):
            visited = set()
            self.dfs_util(v, visited)

    g = Graph()
    g.add_edge(0, 1)
    g.add_edge(0, 2)
    g.add_edge(1, 2)
    g.add_edge(2, 0)
    g.add_edge(2, 3)
    g.add_edge(3, 3)

    g.dfs(2)
    ```
---

#### Hash Tables
- **Definition**: A hash table is a data structure that maps keys to values using a hash function.
- **Operations**: Insertion, Deletion, Search
- **Code Example**:
    ```python
    hash_table = {}

    # Insertion
    hash_table['key1'] = 'value1'
    hash_table['key2'] = 'value2'

    # Deletion
    del hash_table['key1']

    # Search
    print(hash_table['key2'])  # value2
    ```

- **Code Example**:
    ```python
    # Example dictionary with counts
    count_dict = {'apple': 3, 'banana': 2, 'orange': 1}
    for key in count_dict.keys():
        print(key)

    for value in count_dict.values():
        print(value)

    for key, value in count_dict.items():
        print(f"{key}: {value}")
    ```

- **Code Example**:
    ```python
    from collections import defaultdict

    # Sample data: tuples of (key, value)
    data = [('fruits', 'apple'), ('fruits', 'banana'), ('fruits', 'orange'),
            ('vegetables', 'carrot'), ('vegetables', 'spinach'), ('grains', 'rice')]

    # Initialize defaultdict with list as the default_factory
    grouped_dict = defaultdict(list)

    # Group elements by key
    for key, value in data:
        grouped_dict[key].append(value)

    # Iterate over the dictionary and print key-value pairs
    for key, values in grouped_dict.items():
        print(f"{key}: {values}")

    fruits: ['apple', 'banana', 'orange']
    vegetables: ['carrot', 'spinach']
    grains: ['rice']

    from collections import defaultdict

    # Custom default factory
    def default_value():
        return {'count': 0, 'items': []}

    custom_dict = defaultdict(default_value)
    custom_dict['a']['count'] += 1
    custom_dict['a']['items'].append('apple')
    custom_dict['b']['count'] += 2
    custom_dict['b']['items'].append('banana')

    print(custom_dict)
    # Output: defaultdict(<function default_value at 0x...>, {'a': {'count': 1, 'items': ['apple']}, 'b': {'count': 2, 'items': ['banana']}})
    ```

---

#### Heaps
- **Definition**: A heap is a special tree-based data structure that satisfies the heap property.
- **Types**: Min-Heap, Max-Heap
- **Code Example (Min-Heap)**:
    ```python
    import heapq

    heap = []

    # Insertion
    heapq.heappush(heap, 1)
    heapq.heappush(heap, 3)
    heapq.heappush(heap, 5)
    heapq.heappush(heap, 2)
    heapq.heappush(heap, 4)

    # Deletion
    print(heapq.heappop(heap))  # 1
    ```
---
### 2. Algorithms

#### Sorting
- **Bubble Sort**:
    ```python
    def bubble_sort(arr):
        n = len(arr)
        for i in range(n):
            for j in range(0, n-i-1):
                if arr[j] > arr[j+1]:
                    arr[j], arr[j+1] = arr[j+1], arr[j]
        return arr

    arr = [64, 34, 25, 12, 22, 11, 90]
    print(bubble_sort(arr))
    ```
- **Quick Sort**:
    ```python
    def partition(arr, low, high):
        pivot = arr[high]
        i = low - 1
        for j in range(low, high):
            if arr[j] < pivot:
                i = i + 1
                arr[i], arr[j] = arr[j], arr[i]
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        return i + 1

    def quick_sort(arr, low, high):
        if low < high:
            pi = partition(arr, low, high)
            quick_sort(arr, low, pi - 1)
            quick_sort(arr, pi + 1, high)
        return arr

    arr = [10, 7, 8, 9, 1, 5]
    print(quick_sort(arr, 0, len(arr) - 1))
    ```

#### Searching
- **Binary Search**:
    ```python
    def binary_search(arr, x):
        low = 0
        high = len(arr) - 1
        mid = 0

        while low <= high:
            mid = (high + low) // 2
            if arr[mid] < x:
                low = mid + 1
            elif arr[mid] > x:
                high = mid - 1
            else:
                return mid
        return -1

    arr = [2, 3, 4, 10, 40]
    x = 10
    print(binary_search(arr, x))
    ```

#### Recursion
- **Factorial**:
    ```python
    def factorial(n):
        if n == 0:
            return 1
        else:
            return n * factorial(n-1)

    print(factorial(5))  # 120
    ```

#### Dynamic Programming
- **Fibonacci Sequence**:
    ```python
    def fibonacci(n, memo={}):
        if n in memo:
            return memo[n]
        if n <= 1:
            return n
        memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo)
        return memo[n]

    print(fibonacci(10))  # 55
    ```

### Greedy Algorithms
**Definition**: Greedy algorithms build up a solution piece by piece, always choosing the next piece that offers the most immediate benefit.

#### Coin Change Problem
Given a set of coins and a total amount, find the minimum number of coins needed to make the amount.

```python
def min_coins(coins, amount):
    coins.sort(reverse=True)
    count = 0
    for coin in coins:
        while amount >= coin:
            amount -= coin
            count += 1
    return count

coins = [1, 2, 5, 10, 20, 50, 100, 200]
amount = 289
print(min_coins(coins, amount))  # Output: 4 (200 + 50 + 20 + 10 + 5 + 2 + 2)
```

#### Activity Selection Problem
Given a set of activities with start and finish times, select the maximum number of activities that don't overlap.

```python
def activity_selection(activities):
    activities.sort(key=lambda x: x[1])
    selected = [activities[0]]
    for i in range(1, len(activities)):
        if activities[i][0] >= selected[-1][1]:
            selected.append(activities[i])
    return selected

activities = [(1, 3), (2, 5), (4, 6), (6, 7), (5, 8)]
print(activity_selection(activities))  # Output: [(1, 3), (4, 6), (6, 7)]
```

### Backtracking
**Definition**: Backtracking is a general algorithm for finding all (or some) solutions to computational problems by incrementally building candidates to the solutions and abandoning a candidate as soon as it determines that the candidate cannot possibly be completed to a valid solution.

#### N-Queens Problem
Place N queens on an N×N chessboard so that no two queens threaten each other.

```python
def is_safe(board, row, col, n):
    for i in range(col):
        if board[row][i] == 1:
            return False
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
    for i, j in zip(range(row, n, 1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
    return True

def solve_nqueens(board, col, n):
    if col >= n:
        return True
    for i in range(n):
        if is_safe(board, i, col, n):
            board[i][col] = 1
            if solve_nqueens(board, col + 1, n):
                return True
            board[i][col] = 0
    return False

def nqueens(n):
    board = [[0 for _ in range(n)] for _ in range(n)]
    if not solve_nqueens(board, 0, n):
        return "No solution"
    return board

n = 4
solution = nqueens(n)
for row in solution:
    print(row)
```

#### Subset Sum Problem
Find a subset of a given set that sums to a given value.

```python
def subset_sum(arr, target):
    result = []
    def backtrack(start, current_sum, current_list):
        if current_sum == target:
            result.append(list(current_list))
            return
        for i in range(start, len(arr)):
            if current_sum + arr[i] > target:
                continue
            current_list.append(arr[i])
            backtrack(i + 1, current_sum + arr[i], current_list)
            current_list.pop()
    arr.sort()
    backtrack(0, 0, [])
    return result

arr = [3, 34, 4, 12, 5, 2]
target = 9
print(subset_sum(arr, target))  # Output: [[4, 5]]
```

### Graph Algorithms
**Definition**: Graph algorithms are a set of instructions that traverse (visit nodes of a) graph.

#### Depth-First Search (DFS)
DFS is an algorithm for traversing or searching tree or graph data structures. It starts at the root and explores as far as possible along each branch before backtracking.

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start, end=' ')
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

dfs(graph, 'A')  # Output: A B D E F C
```

#### Breadth-First Search (BFS)
BFS is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root and explores all nodes at the present depth level before moving on to the nodes at the next depth level.

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)
    while queue:
        vertex = queue.popleft()
        print(vertex, end=' ')
        for neighbor in graph[vertex]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)

graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

bfs(graph, 'A')  # Output: A B C D E F
```

#### Dijkstra's Algorithm
Dijkstra's algorithm is used for finding the shortest paths between nodes in a graph.

```python
import heapq

def dijkstra(graph, start):
    pq = [(0, start)]
    distances = {node: float('infinity') for node in graph}
    distances[start] = 0
    while pq:
        current_distance, current_node = heapq.heappop(pq)
        if current_distance > distances[current_node]:
            continue
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(pq, (distance, neighbor))
    return distances

graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'C': 2, 'D': 5},
    'C': {'A': 4, 'B': 2, 'D': 1},
    'D': {'B': 5, 'C': 1}
}

print(dijkstra(graph, 'A'))  # Output: {'A': 0, 'B': 1, 'C': 3, 'D': 4}
```