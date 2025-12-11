# Complete DSA Tutorial for LeetCode (Python)

## Table of Contents
1. [Python Essentials for DSA](#1-python-essentials-for-dsa)
2. [Time & Space Complexity](#2-time--space-complexity)
3. [Arrays & Strings](#3-arrays--strings)
4. [Linked Lists](#4-linked-lists)
5. [Stacks & Queues](#5-stacks--queues)
6. [Hash Tables](#6-hash-tables)
7. [Trees](#7-trees)
8. [Graphs](#8-graphs)
9. [Heaps](#9-heaps)
10. [Sorting & Searching](#10-sorting--searching)
11. [Recursion & Backtracking](#11-recursion--backtracking)
12. [Dynamic Programming](#12-dynamic-programming)
13. [Common Patterns](#13-common-patterns)
14. [Problem-Solving Strategy](#14-problem-solving-strategy)

---

## 1. Python Essentials for DSA

### Key Data Types
```python
# Lists (Dynamic Arrays)
arr = [1, 2, 3]
arr.append(4)           # O(1)
arr.pop()               # O(1)
arr.insert(0, 0)        # O(n)
arr.remove(2)           # O(n)

# Strings (Immutable)
s = "hello"
s += "world"            # O(n) - creates new string
chars = list(s)         # Convert to list for mutations

# Tuples (Immutable)
t = (1, 2, 3)

# Sets (Hash-based, unordered)
s = {1, 2, 3}
s.add(4)                # O(1)
s.remove(2)             # O(1)

# Dictionaries (Hash Maps)
d = {"key": "value"}
d["new"] = 123          # O(1)
d.get("key", default)   # O(1)
```

### Essential Built-in Functions
```python
# Math
abs(-5)                 # Absolute value
min(1, 2, 3)           # Minimum
max(1, 2, 3)           # Maximum
pow(2, 3)              # Power: 2^3 = 8

# Collections
len(arr)               # Length
sorted(arr)            # Returns new sorted list
arr.sort()             # In-place sort
reversed(arr)          # Returns iterator
sum(arr)               # Sum of elements
all([True, True])      # All true?
any([False, True])     # Any true?

# String methods
s.split()              # Split by whitespace
s.strip()              # Remove leading/trailing whitespace
s.lower(), s.upper()   # Case conversion
s.isalnum()            # Alphanumeric check
s.isdigit()            # Digit check
```

### List Comprehensions
```python
# Basic
squares = [x**2 for x in range(10)]

# With condition
evens = [x for x in range(10) if x % 2 == 0]

# Nested
matrix = [[i+j for j in range(3)] for i in range(3)]
```

### Slicing
```python
arr = [0, 1, 2, 3, 4, 5]
arr[1:4]       # [1, 2, 3] - from index 1 to 3
arr[:3]        # [0, 1, 2] - first 3
arr[3:]        # [3, 4, 5] - from index 3 onwards
arr[-1]        # 5 - last element
arr[::-1]      # [5, 4, 3, 2, 1, 0] - reverse
arr[::2]       # [0, 2, 4] - every 2nd element
```

### Important Imports
```python
from collections import defaultdict, Counter, deque
from heapq import heappush, heappop, heapify
import bisect
import math
```

---

## 2. Time & Space Complexity

### Big O Notation
- **O(1)** - Constant: Hash table access, array index access
- **O(log n)** - Logarithmic: Binary search, balanced tree operations
- **O(n)** - Linear: Single loop, linear search
- **O(n log n)** - Linearithmic: Efficient sorting (merge sort, heap sort)
- **O(n²)** - Quadratic: Nested loops, bubble sort
- **O(2ⁿ)** - Exponential: Recursive Fibonacci, subsets
- **O(n!)** - Factorial: Permutations

### Common Operations Complexity
```python
# List
arr[i]          # O(1)
arr.append(x)   # O(1) amortized
arr.pop()       # O(1)
arr.insert(0,x) # O(n)
x in arr        # O(n)

# Dictionary/Set
d[key]          # O(1) average
key in d        # O(1) average
d[key] = val    # O(1) average

# String
s[i]            # O(1)
s + t           # O(n+m)
s in t          # O(n*m) worst case
```

---

## 3. Arrays & Strings

### Two Pointers Technique
```python
# Remove duplicates from sorted array
def removeDuplicates(nums):
    if not nums: return 0
    i = 0
    for j in range(1, len(nums)):
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]
    return i + 1

# Two sum (sorted array)
def twoSum(numbers, target):
    l, r = 0, len(numbers) - 1
    while l < r:
        curr = numbers[l] + numbers[r]
        if curr == target:
            return [l+1, r+1]
        elif curr < target:
            l += 1
        else:
            r -= 1
```

### Sliding Window
```python
# Maximum sum subarray of size k
def maxSumSubarray(arr, k):
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

# Longest substring without repeating characters
def lengthOfLongestSubstring(s):
    char_set = set()
    l = 0
    max_len = 0
    
    for r in range(len(s)):
        while s[r] in char_set:
            char_set.remove(s[l])
            l += 1
        char_set.add(s[r])
        max_len = max(max_len, r - l + 1)
    
    return max_len
```

### Prefix Sum
```python
# Range sum query
class NumArray:
    def __init__(self, nums):
        self.prefix = [0]
        for num in nums:
            self.prefix.append(self.prefix[-1] + num)
    
    def sumRange(self, left, right):
        return self.prefix[right + 1] - self.prefix[left]
```

---

## 4. Linked Lists

### Node Definition
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### Common Operations
```python
# Reverse linked list
def reverseList(head):
    prev = None
    curr = head
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    return prev

# Detect cycle (Floyd's Algorithm)
def hasCycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

# Merge two sorted lists
def mergeTwoLists(l1, l2):
    dummy = ListNode(0)
    curr = dummy
    
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    
    curr.next = l1 or l2
    return dummy.next

# Find middle of linked list
def middleNode(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

---

## 5. Stacks & Queues

### Stack (LIFO)
```python
# Using list
stack = []
stack.append(1)     # Push
stack.pop()         # Pop
stack[-1]           # Peek

# Valid parentheses
def isValid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in mapping:
            if not stack or stack[-1] != mapping[char]:
                return False
            stack.pop()
        else:
            stack.append(char)
    
    return not stack
```

### Queue (FIFO)
```python
from collections import deque

# Using deque (efficient)
queue = deque()
queue.append(1)        # Enqueue
queue.popleft()        # Dequeue
queue[0]               # Peek

# Moving average
class MovingAverage:
    def __init__(self, size):
        self.queue = deque()
        self.size = size
        self.sum = 0
    
    def next(self, val):
        self.queue.append(val)
        self.sum += val
        
        if len(self.queue) > self.size:
            self.sum -= self.queue.popleft()
        
        return self.sum / len(self.queue)
```

### Monotonic Stack
```python
# Next greater element
def nextGreaterElement(nums):
    result = [-1] * len(nums)
    stack = []  # Stores indices
    
    for i in range(len(nums)):
        while stack and nums[i] > nums[stack[-1]]:
            idx = stack.pop()
            result[idx] = nums[i]
        stack.append(i)
    
    return result
```

---

## 6. Hash Tables

### Dictionary Operations
```python
# Frequency counter
from collections import Counter
nums = [1, 2, 2, 3, 3, 3]
freq = Counter(nums)  # {1: 1, 2: 2, 3: 3}

# Two sum
def twoSum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i

# Group anagrams
def groupAnagrams(strs):
    anagrams = defaultdict(list)
    for s in strs:
        key = ''.join(sorted(s))
        anagrams[key].append(s)
    return list(anagrams.values())
```

### DefaultDict
```python
from collections import defaultdict

# Graph adjacency list
graph = defaultdict(list)
graph[1].append(2)  # No KeyError even if key doesn't exist

# Counting
count = defaultdict(int)
count['a'] += 1  # Starts at 0
```

---

## 7. Trees

### Tree Node Definition
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### Tree Traversals
```python
# Inorder (Left, Root, Right) - gives sorted order for BST
def inorderTraversal(root):
    result = []
    def inorder(node):
        if not node:
            return
        inorder(node.left)
        result.append(node.val)
        inorder(node.right)
    inorder(root)
    return result

# Preorder (Root, Left, Right)
def preorderTraversal(root):
    result = []
    def preorder(node):
        if not node:
            return
        result.append(node.val)
        preorder(node.left)
        preorder(node.right)
    preorder(root)
    return result

# Postorder (Left, Right, Root)
def postorderTraversal(root):
    result = []
    def postorder(node):
        if not node:
            return
        postorder(node.left)
        postorder(node.right)
        result.append(node.val)
    postorder(root)
    return result

# Level-order (BFS)
def levelOrder(root):
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)
    
    return result
```

### Common Tree Problems
```python
# Maximum depth
def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))

# Validate BST
def isValidBST(root):
    def validate(node, low=float('-inf'), high=float('inf')):
        if not node:
            return True
        if not (low < node.val < high):
            return False
        return (validate(node.left, low, node.val) and 
                validate(node.right, node.val, high))
    return validate(root)

# Lowest Common Ancestor
def lowestCommonAncestor(root, p, q):
    if not root or root == p or root == q:
        return root
    
    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)
    
    if left and right:
        return root
    return left or right
```

---

## 8. Graphs

### Graph Representations
```python
# Adjacency List (most common)
graph = defaultdict(list)
graph[1] = [2, 3]
graph[2] = [1, 4]

# Adjacency Matrix
n = 5
graph = [[0] * n for _ in range(n)]
graph[1][2] = 1  # Edge from 1 to 2
```

### DFS (Depth-First Search)
```python
# Recursive
def dfs(graph, node, visited):
    if node in visited:
        return
    visited.add(node)
    print(node)
    for neighbor in graph[node]:
        dfs(graph, neighbor, visited)

# Iterative
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]
    
    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            print(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)
```

### BFS (Breadth-First Search)
```python
def bfs(graph, start):
    visited = set([start])
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        print(node)
        
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

### Common Graph Problems
```python
# Number of Islands (DFS)
def numIslands(grid):
    if not grid:
        return 0
    
    rows, cols = len(grid), len(grid[0])
    islands = 0
    
    def dfs(r, c):
        if (r < 0 or r >= rows or c < 0 or c >= cols or 
            grid[r][c] == '0'):
            return
        grid[r][c] = '0'  # Mark as visited
        dfs(r+1, c)
        dfs(r-1, c)
        dfs(r, c+1)
        dfs(r, c-1)
    
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                islands += 1
                dfs(r, c)
    
    return islands

# Course Schedule (Cycle Detection)
def canFinish(numCourses, prerequisites):
    graph = defaultdict(list)
    for course, prereq in prerequisites:
        graph[course].append(prereq)
    
    visiting = set()
    visited = set()
    
    def hasCycle(course):
        if course in visiting:
            return True
        if course in visited:
            return False
        
        visiting.add(course)
        for prereq in graph[course]:
            if hasCycle(prereq):
                return True
        visiting.remove(course)
        visited.add(course)
        return False
    
    for course in range(numCourses):
        if hasCycle(course):
            return False
    return True
```

---

## 9. Heaps

### Heap Operations (Min Heap by default)
```python
import heapq

# Create heap
heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)

# Convert list to heap
nums = [3, 1, 4, 1, 5]
heapq.heapify(nums)  # O(n)

# Pop minimum
min_val = heapq.heappop(heap)

# Peek minimum
min_val = heap[0]

# Max heap (use negative values)
max_heap = []
heapq.heappush(max_heap, -5)
max_val = -heapq.heappop(max_heap)
```

### Common Heap Problems
```python
# Kth Largest Element
def findKthLargest(nums, k):
    # Min heap of size k
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap[0]

# Merge K Sorted Lists
def mergeKLists(lists):
    heap = []
    dummy = ListNode(0)
    curr = dummy
    
    # Initialize heap with first node of each list
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))
    
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    
    return dummy.next

# Top K Frequent Elements
def topKFrequent(nums, k):
    count = Counter(nums)
    return [num for num, freq in count.most_common(k)]
```

---

## 10. Sorting & Searching

### Binary Search
```python
# Standard binary search
def binarySearch(arr, target):
    l, r = 0, len(arr) - 1
    
    while l <= r:
        mid = (l + r) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            l = mid + 1
        else:
            r = mid - 1
    
    return -1

# Find first occurrence
def firstOccurrence(arr, target):
    l, r = 0, len(arr) - 1
    result = -1
    
    while l <= r:
        mid = (l + r) // 2
        if arr[mid] == target:
            result = mid
            r = mid - 1  # Continue searching left
        elif arr[mid] < target:
            l = mid + 1
        else:
            r = mid - 1
    
    return result

# Using bisect module
import bisect
arr = [1, 2, 4, 4, 5]
idx = bisect.bisect_left(arr, 4)   # Leftmost position
idx = bisect.bisect_right(arr, 4)  # Rightmost position
```

### Sorting Algorithms
```python
# Quick Sort
def quickSort(arr):
    if len(arr) <= 1:
        return arr
    
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    return quickSort(left) + middle + quickSort(right)

# Merge Sort
def mergeSort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = mergeSort(arr[:mid])
    right = mergeSort(arr[mid:])
    
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

---

## 11. Recursion & Backtracking

### Recursion Basics
```python
# Fibonacci
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

# Factorial
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n-1)
```

### Backtracking Template
```python
def backtrack(path, choices):
    if is_goal(path):
        result.append(path[:])  # Make a copy
        return
    
    for choice in choices:
        if is_valid(choice):
            path.append(choice)        # Make choice
            backtrack(path, choices)   # Explore
            path.pop()                 # Undo choice
```

### Common Backtracking Problems
```python
# Permutations
def permute(nums):
    result = []
    
    def backtrack(path, remaining):
        if not remaining:
            result.append(path[:])
            return
        
        for i in range(len(remaining)):
            backtrack(path + [remaining[i]], 
                     remaining[:i] + remaining[i+1:])
    
    backtrack([], nums)
    return result

# Subsets
def subsets(nums):
    result = []
    
    def backtrack(start, path):
        result.append(path[:])
        
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    
    backtrack(0, [])
    return result

# Combination Sum
def combinationSum(candidates, target):
    result = []
    
    def backtrack(start, path, total):
        if total == target:
            result.append(path[:])
            return
        if total > target:
            return
        
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            backtrack(i, path, total + candidates[i])
            path.pop()
    
    backtrack(0, [], 0)
    return result
```

---

## 12. Dynamic Programming

### DP Approach
1. Identify if problem has optimal substructure
2. Define the state (what does dp[i] represent?)
3. Write recurrence relation
4. Implement with memoization or tabulation

### Top-Down (Memoization)
```python
# Fibonacci with memoization
def fib(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    
    memo[n] = fib(n-1, memo) + fib(n-2, memo)
    return memo[n]
```

### Bottom-Up (Tabulation)
```python
# Fibonacci with tabulation
def fib(n):
    if n <= 1:
        return n
    
    dp = [0] * (n + 1)
    dp[1] = 1
    
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]
```

### Common DP Problems
```python
# Climbing Stairs
def climbStairs(n):
    if n <= 2:
        return n
    
    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2
    
    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    
    return dp[n]

# Coin Change
def coinChange(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    
    for i in range(1, amount + 1):
        for coin in coins:
            if i - coin >= 0:
                dp[i] = min(dp[i], dp[i - coin] + 1)
    
    return dp[amount] if dp[amount] != float('inf') else -1

# Longest Common Subsequence
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]

# House Robber
def rob(nums):
    if not nums:
        return 0
    if len(nums) == 1:
        return nums[0]
    
    prev2 = nums[0]
    prev1 = max(nums[0], nums[1])
    
    for i in range(2, len(nums)):
        curr = max(prev1, prev2 + nums[i])
        prev2 = prev1
        prev1 = curr
    
    return prev1
```

---

## 13. Common Patterns

### 1. Two Pointers
**When to use:** Sorted arrays, palindromes, pairs with target sum
```python
# Container with most water
def maxArea(height):
    l, r = 0, len(height) - 1
    max_area = 0
    
    while l < r:
        area = min(height[l], height[r]) * (r - l)
        max_area = max(max_area, area)
        
        if height[l] < height[r]:
            l += 1
        else:
            r -= 1
    
    return max_area
```

### 2. Sliding Window
**When to use:** Contiguous subarrays, substrings
```python
# Minimum window substring
def minWindow(s, t):
    if not s or not t:
        return ""
    
    need = Counter(t)
    have = defaultdict(int)
    required = len(need)
    formed = 0
    
    l = 0
    min_len = float('inf')
    result = ""
    
    for r in range(len(s)):
        char = s[r]
        have[char] += 1
        
        if char in need and have[char] == need[char]:
            formed += 1
        
        while formed == required:
            if r - l + 1 < min_len:
                min_len = r - l + 1
                result = s[l:r+1]
            
            have[s[l]] -= 1
            if s[l] in need and have[s[l]] < need[s[l]]:
                formed -= 1
            l += 1
    
    return result
```

### 3. Fast & Slow Pointers
**When to use:** Linked list cycles, middle of list
```python
# Find duplicate number
def findDuplicate(nums):
    slow = fast = nums[0]
    
    # Find intersection point
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    
    # Find entrance to cycle
    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
    
    return slow
```

### 4. Merge Intervals
**When to use:** Overlapping intervals
```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    
    return merged
```

### 5. Top K Elements
**When to use:** Finding K largest/smallest elements
```python
def topKFrequent(nums, k):
    count = Counter(nums)
    return heapq.nlargest(k, count.keys(), key=count.get)
```

### 6. Binary Search Variations
**When to use:** Search in sorted/rotated arrays, finding boundaries
```python
# Search in rotated sorted array
def search(nums, target):
    l, r = 0, len(nums) - 1
    
    while l <= r:
        mid = (l + r) // 2
        if nums[mid] == target:
            return mid
        
        # Left half is sorted
        if nums[l] <= nums[mid]:
            if nums[l] <= target < nums[mid]:
                r = mid - 1
            else:
                l = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[r]:
                l = mid + 1
            else:
                r = mid - 1
    
    return -1
```

---

## 14. Problem-Solving Strategy

### Step-by-Step Approach

1. **Understand the Problem**
   - Read carefully, identify inputs/outputs
   - Ask clarifying questions
   - Consider edge cases

2. **Examples**
   - Work through 2-3 examples manually
   - Include edge cases

3. **Brute Force**
   - Think of the simplest solution first
   - Analyze time/space complexity

4. **Optimize**
   - Can you use a hash table?
   - Can you sort the data?
   - Can you use two pointers or sliding window?
   - Would binary search work?
   - Is there a DP pattern?

5. **Code**
   - Write clean, readable code
   - Use meaningful variable names
   - Add comments for complex logic

6. **Test**
   - Test with examples
   - Test edge cases: empty input, single element, duplicates
   - Test large inputs mentally

### Common Edge Cases
```python
# Always check:
- Empty input: [], "", None
- Single element: [1], "a"
- Two elements: [1, 2]
- All same elements: [5, 5, 5]
- Negative numbers: [-1, -2, -3]
- Duplicates: [1, 2, 2, 3]
- Already sorted: [1, 2, 3, 4]
- Reverse sorted: [4, 3, 2, 1]
- Large numbers: 10^9
```

### Time Complexity Goals
- **n ≤ 10**: O(n!)
- **n ≤ 20**: O(2ⁿ)
- **n ≤ 500**: O(n³)
- **n ≤ 5000**: O(n²)
- **n ≤ 10⁶**: O(n log n)
- **n > 10⁶**: O(n) or O(log n)

### Useful Python Tricks
```python
# Swap variables
a, b = b, a

# Multiple comparisons
if a < b < c:

# Ternary operator
result = x if condition else y

# Enumerate
for i, val in enumerate(arr):

# Zip
for a, b in zip(list1, list2):

# Any/All
if any(x > 0 for x in arr):
if all(x > 0 for x in arr):

# Default dictionary
from collections import defaultdict
d = defaultdict(int)  # Default value 0
d = defaultdict(list)  # Default value []

# Counter
from collections import Counter
freq = Counter(arr)
most_common = freq.most_common(k)

# Infinity
pos_inf = float('inf')
neg_inf = float('-inf')

# String to int array
digits = [int(d) for d in str(num)]

# Deep copy
import copy
new_list = copy.deepcopy(old_list)
```

---

## Practice Roadmap

### Beginner (Easy Problems)
1. Two Sum
2. Valid Parentheses
3. Merge Two Sorted Lists
4. Best Time to Buy and Sell Stock
5. Valid Palindrome
6. Maximum Subarray
7. Climbing Stairs
8. Reverse Linked List
9. Binary Search
10. Majority Element

### Intermediate (Medium Problems)
1. Longest Substring Without Repeating Characters
2. Container With Most Water
3. 3Sum
4. Product of Array Except Self
5. Group Anagrams
6. Longest Palindromic Substring
7. Number of Islands
8. Course Schedule
9. Coin Change
10. LRU Cache

### Advanced (Hard Problems)
1. Median of Two Sorted Arrays
2. Trapping Rain Water
3. Word Ladder
4. Merge K Sorted Lists
5. Largest Rectangle in Histogram
6. Serialize and Deserialize Binary Tree
7. Word Search II
8. Longest Consecutive Sequence

---

## Final Tips

1. **Consistency is key** - Practice daily, even if just 1 problem
2. **Understand, don't memorize** - Focus on patterns and techniques
3. **Review solutions** - Even if you solve it, check others' solutions
4. **Time yourself** - Practice under time pressure
5. **Learn from mistakes** - Understand why your solution failed
6. **Start simple** - Begin with easy problems, gradually increase difficulty
7. **Mock interviews** - Practice explaining your thought process
8. **Use debugger** - Step through code to understand flow

Good luck with your LeetCode journey! 🚀