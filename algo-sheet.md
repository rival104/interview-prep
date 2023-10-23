From: https://techinterviewhandbook.org

# Array

Note that because both arrays and strings are sequences (a string is an array of characters), most of the techniques here will apply to string problems.

### Sliding window
Master the sliding window technique that applies to many subarray/substring problems. In a sliding window, the two pointers usually move in the same direction will never overtake each other. This ensures that each value is only visited at most twice and the time complexity is still O(n). Examples: Longest Substring Without Repeating Characters, Minimum Size Subarray Sum, Minimum Window Substring

Template
```
1. Initialize two pointers, start and end, both at the 0th index.

2. Initialize any needed variables. For example:
   - max_sum for storing the maximum sum of subarray
   - current_sum for storing the sum of the current window
   - any other specific variables you need

3. Iterate over the array/string using the end pointer:

   while end < length_of_array:
       
       a. Add the current element to current_sum (or perform some operation)

       b. While the current window meets a certain condition (like current_sum exceeds a value, the window has more than a specific number of characters, etc.):
          i. Possibly update max_sum or any other variables
          ii. Remove the element at start pointer from current_sum (or perform the opposite operation)
          iii. Increment the start pointer to make the window smaller

       c. Increment the end pointer

4. After the loop, the answer could be in max_sum or any other variables you used.
```

Example
```javascript
// Find the maximum sum subarray of size `k`:
function maxSumSubarray(arr: number[], k: number): number {
    let start = 0;
    let currentSum = 0;
    let maxSum = Number.NEGATIVE_INFINITY;

    for (let end = 0; end < arr.length; end++) {
        currentSum += arr[end];

        if (end - start + 1 === k) {
            maxSum = Math.max(maxSum, currentSum);
            currentSum -= arr[start];
            start++;
        }
    }

    return maxSum;
}
```

### Two pointers
Two pointers is a more general version of sliding window where the pointers can cross each other and can be on different arrays. Examples: Sort Colors, Palindromic Substrings

When you are given two arrays to process, it is common to have one index per array (pointer) to traverse/compare the both of them, incrementing one of the pointers when relevant. For example, we use this approach to merge two sorted arrays. Examples: Merge Sorted Array

Template
```
1. Initialize two pointers. Depending on the problem:
   - They can start at the beginning and end of the array (`start = 0, end = length_of_array - 1`), which is typical for sorted arrays.
   - Or they can start both at the beginning (`left = 0, right = 1`) or any other positions based on the requirement.

2. Use a loop (typically a while loop) to iterate while the pointers meet the criteria for traversal, e.g., `start < end`.

3. Inside the loop:
   a. Check the current elements at the two pointers.
   b. Based on the problem, decide how to adjust the pointers. Common decisions are:
      i. If the current elements meet some condition, process the current elements and then adjust the pointers (either moving `start` forward or `end` backward or both).
      ii. If the current elements don't meet the condition, adjust one of the pointers (or both) without processing the elements.

4. Continue until the loop ends.

5. The solution might be obtained during the loop's iterations, or after the loop based on the processed elements.
```

Example
```javascript
// In a sorted array, find a pair of elements that sum up to a given target:
function twoSumSorted(arr: number[], target: number): [number, number] | null {
    let start = 0;
    let end = arr.length - 1;

    while (start < end) {
        const currentSum = arr[start] + arr[end];

        if (currentSum === target) {
            return [arr[start], arr[end]];
        } else if (currentSum < target) {
            start++;
        } else {
            end--;
        }
    }

    return null; // No pair found
}
```

### Traversing from the right
Sometimes you can traverse the array starting from the right instead of the conventional approach of from the left. Examples: Daily Temperatures, Number of Visible People in a Queue

### Sorting the array
Is the array sorted or partially sorted? If it is, some form of binary search should be possible. This also usually means that the interviewer is looking for a solution that is faster than O(n).

Can you sort the array? Sometimes sorting the array first may significantly simplify the problem. Obviously this would not work if the order of array elements need to be preserved. Examples: Merge Intervals, Non-overlapping Intervals

### Precomputation
For questions where summation or multiplication of a subarray is involved, pre-computation using hashing or a prefix/suffix sum/product might be useful. Examples: Product of Array Except Self, Minimum Size Subarray Sum, LeetCode questions tagged "prefix-sum"

### Index as a hash key
If you are given a sequence and the interviewer asks for O(1) space, it might be possible to use the array itself as a hash table. For example, if the array only has values from 1 to N, where N is the length of the array, negate the value at that index (minus one) to indicate presence of that number. Examples: First Missing Positive, Daily Temperatures

### Traversing the array more than once
This might be obvious, but traversing the array twice/thrice (as long as fewer than n times) is still O(n). Sometimes traversing the array more than once can help you solve the problem while keeping the time complexity to O(n).

## String

### Counting characters
Often you will need to count the frequency of characters in a string. The most common way of doing that is by using a hash table/map in your language of choice. If your language has a built-in Counter class like Python, ask if you can use that instead.

If you need to keep a counter of characters, a common mistake is to say that the space complexity required for the counter is O(n). The space required for a counter of a string of latin characters is O(1) not O(n). This is because the upper bound is the range of characters, which is usually a fixed constant of 26. The input set is just lowercase Latin characters.

### Anagram
An anagram is word switch or word play. It is the result of rearranging the letters of a word or phrase to produce a new word or phrase, while using all the original letters only once. In interviews, usually we are only bothered with words without spaces in them.

To determine if two strings are anagrams, there are a few approaches:

- Sorting both strings should produce the same resulting string. This takes O(n.log(n)) time and O(log(n)) space.
- If we map each character to a prime number and we multiply each mapped number together, anagrams should have the same multiple (prime factor decomposition). This takes O(n) time and O(1) space. Examples: Group Anagram
- Frequency counting of characters will help to determine if two strings are anagrams. This also takes O(n) time and O(1) space.

### Palindrome
A palindrome is a word, phrase, number, or other sequence of characters which reads the same backward as forward, such as madam or racecar.

Here are ways to determine if a string is a palindrome:

- Reverse the string and it should be equal to itself.
- Have two pointers at the start and end of the string. Move the pointers inward till they meet. At every point in time, the characters at both pointers should match.
- The order of characters within the string matters, so hash tables are usually not helpful.

When a question is about counting the number of palindromes, a common trick is to have two pointers that move outward, away from the middle. Note that palindromes can be even or odd length. For each middle pivot position, you need to check it twice - once that includes the character and once without the character. This technique is used in Longest Palindromic Substring.

- For substrings, you can terminate early once there is no match
- For subsequences, use dynamic programming as there are overlapping subproblems


## Hash Table

- Describe an implementation of a least-used cache, and big-O notation of it.

Template
```
Initialize an LRU Cache with a given capacity:

1. Set cache capacity.
2. Create an empty hashmap that will hold key-value pairs (key -> node in doubly-linked list).
3. Create an empty doubly-linked list (nodes will have key-value pairs).

To GET a value from the cache:

1. If the key is not in the hashmap:
   a. Return "Not Found" or equivalent.
2. If the key is in the hashmap:
   a. Use the hashmap to get the node associated with that key from the doubly-linked list.
   b. Move the accessed node to the head of the doubly-linked list (indicating recent use).
   c. Return the value of the node.

To PUT a value in the cache:

1. If the key is already in the hashmap:
   a. Use the hashmap to get the node associated with that key from the doubly-linked list.
   b. Update the value of the node.
   c. Move the node to the head of the doubly-linked list.
2. If the key is not in the hashmap:
   a. Create a new node with the key-value pair.
   b. Add the node to the head of the doubly-linked list.
   c. Add the key and the node reference to the hashmap.
   d. If the size of the hashmap exceeds the cache capacity:
      i. Remove the node from the tail of the doubly-linked list (least recently used item).
      ii. Remove the corresponding key from the hashmap.

Helper Method - MoveToHead(node):

1. Remove the node from its current position in the doubly-linked list.
2. Add the node to the head of the doubly-linked list.
```

Example
```javascript
class ListNode {
    key: number;
    value: number;
    prev: ListNode | null = null;
    next: ListNode | null = null;

    constructor(key: number, value: number) {
        this.key = key;
        this.value = value;
    }
}

class LRUCache {
    private capacity: number;
    private map: Map<number, ListNode>;
    private head: ListNode;  // Most recently used
    private tail: ListNode;  // Least recently used

    constructor(capacity: number) {
        this.capacity = capacity;
        this.map = new Map();
        this.head = new ListNode(0, 0);
        this.tail = new ListNode(0, 0);
        this.head.next = this.tail;
        this.tail.prev = this.head;
    }

    get(key: number): number {
        if (!this.map.has(key)) return -1;

        const node = this.map.get(key)!;
        this.moveToHead(node);
        return node.value;
    }

    put(key: number, value: number): void {
        if (this.map.has(key)) {
            const node = this.map.get(key)!;
            node.value = value;
            this.moveToHead(node);
        } else {
            const newNode = new ListNode(key, value);
            this.map.set(key, newNode);
            this.addToHead(newNode);

            if (this.map.size > this.capacity) {
                const tailNode = this.removeTail();
                this.map.delete(tailNode.key);
            }
        }
    }

    private moveToHead(node: ListNode): void {
        this.removeNode(node);
        this.addToHead(node);
    }

    private addToHead(node: ListNode): void {
        node.prev = this.head;
        node.next = this.head.next;
        this.head.next!.prev = node;
        this.head.next = node;
    }

    private removeNode(node: ListNode): void {
        node.prev!.next = node.next;
        node.next!.prev = node.prev;
    }

    private removeTail(): ListNode {
        const tailNode = this.tail.prev!;
        this.removeNode(tailNode);
        return tailNode;
    }
}
```

## Recursion

- Always remember to always define a base case so that your recursion will end.
- Recursion is useful for permutation, because it generates all combinations and tree-based questions. You should know how to generate all permutations of a sequence as well as how to handle duplicates.
- Recursion implicitly uses a stack. Hence all recursive approaches can be rewritten iteratively using a stack. Beware of cases where the recursion level goes too deep and causes a stack overflow (the default limit in Python is 1000). You may get bonus points for pointing this out to the interviewer. Recursion will never be O(1) space complexity because a stack is involved, unless there is tail-call optimization (TCO). Find out if your chosen language supports TCO.
- Number of base cases - In the fibonacci recursion, note that one of the recursive calls invoke fib(n - 2). This indicates that you should have 2 base cases defined so that your code covers all possible invocations of the function within the input range. If your recursive function only invokes fn(n - 1), then only one base case is needed.

### Memoization
In some cases, you may be computing the result for previously computed inputs. Let's look at the Fibonacci example again. fib(5) calls fib(4) and fib(3), and fib(4) calls fib(3) and fib(2). fib(3) is being called twice! If the value for fib(3) is memoized and used again, that greatly improves the efficiency of the algorithm and the time complexity becomes O(n).

## Sorting

### Binary search
When a given sequence is in a sorted order (be it ascending or descending), using binary search should be one of the first things that come to your mind.

Template
```
function binarySearch(array, target):
    1. Define two pointers: "left" initialized to 0 and "right" initialized to (length of array - 1).
    
    2. While "left" is less than or equal to "right":
       a. Calculate the middle index: mid = (left + right) / 2.
       b. If array[mid] equals target:
          i. Return mid.
       c. If array[mid] is less than target:
          i. Set left = mid + 1.
       d. Else:
          i. Set right = mid - 1.

    3. Return "Not Found" or an equivalent indicator (like -1).
```

```javascript
function binarySearch(arr: number[], target: number): number {
    let left = 0;
    let right = arr.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (arr[mid] === target) {
            return mid;  // Target value found, return its index
        }

        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    return -1;  // Target value not found in the array
}
```

If you want to find the closest value that's less than the target value in a sorted array, you can modify the binary search algorithm slightly. At the end of the standard binary search loop, the right pointer will indicate the position where the target should be if it were in the array (or before it).

You can use this property to get the closest value less than the target. After the loop ends, the value at `arr[right]` would be the closest value less than the target (if right is within the bounds of the array).

```javascript
// White loop here
while (...)

// Check if 'right' is within bounds
if (right >= 0) {
    return arr[right];
}
```

### Sorting an input that has limited range
Counting sort is a non-comparison-based sort you can use on numbers where you know the range of values beforehand.

Template
```
function countingSort(inputArray, maxValue):
    1. Initialize an array "count" of zeros with a size of (maxValue + 1).
    2. For each element "x" in inputArray:
       a. Increment count[x] by 1.

    3. Initialize an output array "sortedArray" of the same size as inputArray.
    4. Initialize a position variable "pos" to 0.
    5. For each index "i" from 0 to maxValue:
       a. While count[i] is greater than 0:
          i. Place the value "i" in sortedArray[pos].
          ii. Increment pos by 1.
          iii. Decrement count[i] by 1.

    6. Return sortedArray.
```

Example
```javascript
function countingSort(arr: number[], maxValue: number): number[] {
    // Step 1: Initialize count array
    const count: number[] = new Array(maxValue + 1).fill(0);

    // Step 2: Populate count array with frequencies
    for (let num of arr) {
        count[num]++;
    }

    // Step 3-5: Reconstruct the sorted array using the count array
    let sortedIndex = 0;
    const sortedArray: number[] = new Array(arr.length);

    for (let i = 0; i < count.length; i++) {
        while (count[i] > 0) {
            sortedArray[sortedIndex] = i;
            sortedIndex++;
            count[i]--;
        }
    }

    // Step 6: Return the sorted array
    return sortedArray;
}
```

## Matrix

### Create an empty X x M matrix:
```javascript
const matrix = Array(X).fill(undefined).map(() => Array(M).fill(-1)); // Replace -1 for whatever default value you want
```

### Transposing a matrix
The transpose of a matrix is found by interchanging its rows into columns or columns into rows.

Many grid-based games can be modeled as a matrix, such as Tic-Tac-Toe, Sudoku, Crossword, Connect 4, Battleship, etc. It is not uncommon to be asked to verify the winning condition of the game. For games like Tic-Tac-Toe, Connect 4 and Crosswords, where verification has to be done vertically and horizontally, one trick is to write code to verify the matrix for the horizontal cells, transpose the matrix, and reuse the logic for horizontal verification to verify originally vertical cells (which are now horizontal).

```javascript
function transpose(matrix: number[][]): number[][] {
    // Create a new 2D array of size columns x rows of the original matrix
    const transposed: number[][] = Array.from({ length: matrix[0].length }, () => []);
    
    for (let i = 0; i < matrix.length; i++) {
        for (let j = 0; j < matrix[0].length; j++) {
            transposed[j][i] = matrix[i][j];
        }
    }
    
    return transposed;
}
```

### Linked List

### Sentinel/dummy nodes
Adding a sentinel/dummy node at the head and/or tail might help to handle many edge cases where operations have to be performed at the head or the tail. The presence of dummy nodes essentially ensures that operations will never be done on the head or the tail, thereby removing a lot of headache in writing conditional checks to dealing with null pointers. Be sure to remember to remove them at the end of the operation.

Example
```javascript
class ListNode {
    val: number;
    next: ListNode | null = null;

    constructor(val?: number, next?: ListNode | null) {
        this.val = (val === undefined ? 0 : val);
        this.next = (next === undefined ? null : next);
    }
}

function mergeTwoSortedLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    const dummy = new ListNode(-1);  // Sentinel/dummy node
    let current = dummy;  // Pointer to build the merged list

    while (l1 !== null && l2 !== null) {
        if (l1.val < l2.val) {
            current.next = l1;
            l1 = l1.next;
        } else {
            current.next = l2;
            l2 = l2.next;
        }
        current = current.next!;
    }

    // If there are remaining nodes in l1 or l2
    if (l1 !== null) {
        current.next = l1;
    } else {
        current.next = l2;
    }

    return dummy.next;  // Return the next of dummy as the merged list's head
}
```

In the `mergeTwoSortedLists` function, we utilize a dummy node as the head of our merged list. By doing this, we don't have to write special logic to initialize the head of the merged list, because `dummy.next` will naturally point to the start of the merged list at the end of the process. The dummy node serves as a placeholder and helps in simplifying the code.

## Two pointers
Two pointer approaches are also common for linked lists. This approach is used for many classic linked list problems.

- Getting the kth from last node - Have two pointers, where one is k nodes ahead of the other. When the node ahead reaches the end, the other node is k nodes behind
- Detecting cycles - Have two pointers, where one pointer increments twice as much as the other, if the two pointers meet, means that there is a cycle
- Getting the middle node - Have two pointers, where one pointer increments twice as much as the other. When the faster node reaches the end of the list, the slower node will be at the middle

### Using space
Many linked list problems can be easily solved by creating a new linked list and adding nodes to the new linked list with the final result. However, this takes up extra space and makes the question much less challenging. The interviewer will usually request that you modify the linked list in-place and solve the problem without additional storage. You can borrow ideas from the Reverse a Linked List problem.

### Elegant modification operations
As mentioned earlier, a linked list's non-sequential nature of memory allows for efficient modification of its contents. Unlike arrays where you can only modify the value at a position, for linked lists you can also modify the next pointer in addition to the value.

Here are some common operations and how they can be achieved easily:
- Truncate a list - Set the next pointer to null at the last element
- Swapping values of nodes - Just like arrays, just swap the value of the two nodes, there's no need to swap the next pointer
- Combining two lists - attach the head of the second list to the tail of the first list

## Queue

Most languages don't have a built-in Queue class which can be used, and candidates often use arrays (JavaScript) or lists (Python) as a queue. However, note that the dequeue operation (assuming the front of the queue is on the left) in such a scenario will be O(n) because it requires shifting of all other elements left by one. In such cases, you can flag this to the interviewer and say that you assume that there's a queue data structure to use which has an efficient dequeue operation.

## Interval

### Sort the array of intervals by its starting point
A common routine for interval questions is to sort the array of intervals by each interval's starting value. This step is crucial to solving the Merge Intervals question.

### Checking if two intervals overlap
Be familiar with writing code to check if two intervals overlap.

```python
def is_overlap(a, b):
  return a[0] < b[1] and b[0] < a[1]
```
Trick to remember: both the higher pos must be greater then both lower pos.

Merging two intervals
```python
def merge_overlapping_intervals(a, b):
  return [min(a[0], b[0]), max(a[1], b[1])]
```

## Tree

![Tree](https://upload.wikimedia.org/wikipedia/commons/5/5e/Binary_tree_v2.svg)

### Traversals

- In-order traversal - Left -> Root -> Right.<br/>
Result: 2, 7, 5, 6, 11, 1, 9, 5, 9
- Pre-order traversal - Root -> Left -> Right<br/>
Result: 1, 7, 2, 6, 5, 11, 9, 9, 5
- Post-order traversal - Left -> Right -> Root<br/>
Result: 2, 5, 11, 6, 7, 5, 9, 9, 1

Example (Recursive)
```javascript
class TreeNode {
    val: number;
    left: TreeNode | null = null;
    right: TreeNode | null = null;

    constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
        this.val = (val === undefined ? 0 : val);
        this.left = (left === undefined ? null : left);
        this.right = (right === undefined ? null : right);
    }
}

// In-Order Traversal (Left, Root, Right)
function inOrderTraversal(root: TreeNode | null): number[] {
    let result: number[] = [];
    
    function helper(node: TreeNode | null) {
        if (node === null) return;
        
        helper(node.left);
        result.push(node.val);
        helper(node.right);
    }

    helper(root);
    return result;
}

// Pre-Order Traversal (Root, Left, Right)
function preOrderTraversal(root: TreeNode | null): number[] {
    let result: number[] = [];
    
    function helper(node: TreeNode | null) {
        if (node === null) return;

        result.push(node.val);
        helper(node.left);
        helper(node.right);
    }

    helper(root);
    return result;
}

// Post-Order Traversal (Left, Right, Root)
function postOrderTraversal(root: TreeNode | null): number[] {
    let result: number[] = [];

    function helper(node: TreeNode | null) {
        if (node === null) return;

        helper(node.left);
        helper(node.right);
        result.push(node.val);
    }

    helper(root);
    return result;
}
```

Example (Iterative)
```javascript
class TreeNode {
    val: number;
    left: TreeNode | null = null;
    right: TreeNode | null = null;

    constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
        this.val = (val === undefined ? 0 : val);
        this.left = (left === undefined ? null : left);
        this.right = (right === undefined ? null : right);
    }
}

// In-Order Traversal (Left, Root, Right)
function inOrderTraversal(root: TreeNode | null): number[] {
    const result: number[] = [];
    const stack: TreeNode[] = [];
    let current: TreeNode | null = root;

    while (current !== null || stack.length > 0) {
        while (current !== null) {
            stack.push(current);
            current = current.left;
        }

        current = stack.pop()!;
        result.push(current.val);
        current = current.right;
    }

    return result;
}

// Pre-Order Traversal (Root, Left, Right)
function preOrderTraversal(root: TreeNode | null): number[] {
    const result: number[] = [];
    const stack: TreeNode[] = [];
    if (root) stack.push(root);

    while (stack.length > 0) {
        const current = stack.pop()!;
        result.push(current.val);

        if (current.right) stack.push(current.right);
        if (current.left) stack.push(current.left);
    }

    return result;
}

// Post-Order Traversal (Left, Right, Root)
function postOrderTraversal(root: TreeNode | null): number[] {
    const result: number[] = [];
    const stack: TreeNode[] = [];
    let lastVisited: TreeNode | null = null;

    while (root || stack.length > 0) {
        while (root) {
            stack.push(root);
            root = root.left;
        }

        const peekNode = stack[stack.length - 1];

        if (!peekNode.right || peekNode.right === lastVisited) {
            result.push(peekNode.val);
            lastVisited = stack.pop()!;
        } else {
            root = peekNode.right;
        }
    }

    return result;
}
```

### Binary search tree (BST)
In-order traversal of a BST will give you all elements in order.

Be very familiar with the properties of a BST and validating that a binary tree is a BST. This comes up more often than expected.

When a question involves a BST, the interviewer is usually looking for a solution which runs faster than O(n).

**Time complexity**<br/>
Operation	Big-O<br/>
Access	O(log(n))<br/>
Search	O(log(n))<br/>
Insert	O(log(n))<br/>
Remove	O(log(n))

Space complexity of traversing balanced trees is O(h) where h is the height of the tree, while traversing very skewed trees (which is essentially a linked list) will be O(n).

### Use recursion
Recursion is the most common approach for traversing trees. When you notice that the subtree problem can be used to solve the entire problem, try using recursion.

When using recursion, always remember to check for the base case, usually where the node is `null`.

Sometimes it is possible that your recursive function needs to return two values.

### Traversing by level
When you are asked to traverse a tree by level, use breadth-first search.

## Graph

### Graph representations
You can be given a list of edges and you have to build your own graph from the edges so that you can perform a traversal on them. The common graph representations are:

- Adjacency matrix
- Adjacency list
- Hash table of hash tables

Using a hash table of hash tables would be the simplest approach during algorithm interviews. It will be rare that you have to use an adjacency matrix or list for graph questions during interviews.

```javascript
// Let's assume you're given a list of edges as input, where each edge is a tuple of two nodes, e.g., ["A", "B"] means there's an edge between nodes "A" and "B"

type Node = string;
type Graph = Map<Node, Map<Node, boolean>>;

function addEdge(graph: Graph, from: Node, to: Node) {
    if (!graph.has(from)) {
        graph.set(from, new Map<Node, boolean>());
    }
    graph.get(from)!.set(to, true);
}

function buildGraph(edges: [Node, Node][]): Graph {
    const graph = new Map<Node, Map<Node, boolean>>();

    for (const [from, to] of edges) {
        addEdge(graph, from, to);
        addEdge(graph, to, from); // For undirected graph. Remove this for directed graph.
    }

    return graph;
}

// Test
const edges: [Node, Node][] = [
    ["A", "B"],
    ["A", "C"],
    ["B", "D"],
    ["C", "D"],
    ["D", "E"]
];

const graph = buildGraph(edges);

console.log(graph);
```

In algorithm interviews, graphs are commonly given in the input as 2D matrices where cells are the nodes and each cell can traverse to its adjacent cells (up/down/left/right). Hence it is important that you be familiar with traversing a 2D matrix. When traversing the matrix, always ensure that your current position is within the boundary of the matrix and has not been visited before.

```javascript
type Matrix = number[][];


// O(rows * cols) -> time and space
function traverseMatrix(matrix: Matrix): void {
    if (!matrix || matrix.length === 0 || matrix[0].length === 0) {
        return;
    }

    const rows = matrix.length;
    const cols = matrix[0].length;
    const visited: boolean[][] = Array.from({ length: rows }, () => Array(cols).fill(false));

    function isValid(row: number, col: number): boolean {
        return row >= 0 && row < rows && col >= 0 && col < cols && !visited[row][col];
    }

    function dfs(row: number, col: number): void {
        if (!isValid(row, col)) {
            return;
        }

        console.log(matrix[row][col]); // Process the current cell
        visited[row][col] = true;

        // Traverse up/down/left/right
        dfs(row - 1, col); // Up
        dfs(row + 1, col); // Down
        dfs(row, col - 1); // Left
        dfs(row, col + 1); // Right
    }

    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (!visited[i][j]) {
                dfs(i, j);
            }
        }
    }
}

// Test
const matrix: Matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

traverseMatrix(matrix);
```

### 2D Matrix as a graph

Transforming the problem of traversing a 2D matrix into a graph problem involves viewing each cell of the matrix as a node of a graph and the possible movements (e.g., up, down, left, right) from a cell as edges connecting the nodes.

Here's a step-by-step guide on how you can transform the problem:

1. **Nodes Representation**: Each cell in the matrix, identified by its coordinates (i, j), can be treated as a node in the graph.

2. **Edges Representation**: For each cell, consider its adjacent cells. An edge exists between two nodes if you can move from one cell to the adjacent cell. For instance, if movements are restricted to up, down, left, and right, then:
   - The node (i, j) will have an edge to (i-1, j) if (i-1, j) is a valid cell (i.e., moving upwards).
   - The node (i, j) will have an edge to (i+1, j) if (i+1, j) is a valid cell (i.e., moving downwards).
   - The node (i, j) will have an edge to (i, j-1) if (i, j-1) is a valid cell (i.e., moving left).
   - The node (i, j) will have an edge to (i, j+1) if (i, j+1) is a valid cell (i.e., moving right).

3. **Graph Representation**: There are several ways to represent a graph, such as an adjacency list, adjacency matrix, or a hash table of hash tables. In the context of a matrix traversal, an adjacency list is often a good fit. Each node (i.e., matrix cell) would have a list of its adjacent nodes.

4. **Traversal**: With the graph constructed, you can apply standard graph traversal algorithms like DFS or BFS to explore the nodes. 

5. **Special Conditions**: If there are certain cells in the matrix that you cannot traverse (like obstacles), you simply skip adding them as valid edges in the graph representation. 

This transformation is particularly useful when you have more complex conditions for traversal, or when the problem involves finding paths, connected components, etc. It allows you to leverage a wide range of graph algorithms to solve matrix-based problems.

Example
```javascript
type Node = [number, number];
type Graph = Map<string, Node[]>;

function matrixToGraph(matrix: number[][]): Graph {
    const rows = matrix.length;
    const cols = matrix[0].length;
    const graph: Graph = new Map();

    function getNodeKey(node: Node): string {
        return `${node[0]},${node[1]}`;
    }

    function getAdjacentNodes(row: number, col: number): Node[] {
        const directions: Node[] = [[-1, 0], [1, 0], [0, -1], [0, 1]];  // Up, Down, Left, Right
        const adjacentNodes: Node[] = [];

        for (const [dx, dy] of directions) {
            const newRow = row + dx;
            const newCol = col + dy;

            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols) {
                adjacentNodes.push([newRow, newCol]);
            }
        }

        return adjacentNodes;
    }

    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            const node: Node = [i, j];
            const key = getNodeKey(node);
            graph.set(key, getAdjacentNodes(i, j));
        }
    }

    return graph;
}

function traverseGraph(graph: Graph, startNode: Node): void {
    const visited: Set<string> = new Set();

    function dfs(node: Node): void {
        const key = `${node[0]},${node[1]}`;
        if (visited.has(key)) return;

        console.log(node);
        visited.add(key);

        const neighbors = graph.get(key) || [];
        for (const neighbor of neighbors) {
            dfs(neighbor);
        }
    }

    dfs(startNode);
}

// Test
const matrix: number[][] = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

const graph = matrixToGraph(matrix);
traverseGraph(graph, [0, 0]);  // Start traversal from top-left corner
```

### Time complexity
|V| is the number of vertices while |E| is the number of edges.

Algorithm	Big-O<br/>
Depth-first search	O(|V| + |E|)<br/>
Breadth-first search	O(|V| + |E|)<br/>
Topological sort	O(|V| + |E|)<br/>

### Notes
A tree-like diagram could very well be a graph that allows for cycles and a naive recursive solution would not work. In that case you will have to handle cycles and keep a set of visited nodes when traversing.

Ensure you are correctly keeping track of visited nodes and not visiting each node more than once. Otherwise your code could end up in an infinite loop.

### Depth-first search

```python
def dfs(matrix):
  # Check for an empty matrix/graph.
  if not matrix:
    return []

  rows, cols = len(matrix), len(matrix[0])
  visited = set()
  directions = ((0, 1), (0, -1), (1, 0), (-1, 0))

  def traverse(i, j):
    if (i, j) in visited:
      return

    visited.add((i, j))

    # Traverse neighbors.
    for direction in directions:
      next_i, next_j = i + direction[0], j + direction[1]
      if 0 <= next_i < rows and 0 <= next_j < cols:

        # Add in question-specific checks, where relevant.
        traverse(next_i, next_j)

  for i in range(rows):
    for j in range(cols):
      traverse(i, j)
```

### Breadth-first search

```python
from collections import deque

def bfs(matrix):
  # Check for an empty matrix/graph.
  if not matrix:
    return []

  rows, cols = len(matrix), len(matrix[0])
  visited = set()
  directions = ((0, 1), (0, -1), (1, 0), (-1, 0))

  def traverse(i, j):
    queue = deque([(i, j)])
    while queue:
      curr_i, curr_j = queue.popleft()

      if (curr_i, curr_j) not in visited:
        visited.add((curr_i, curr_j))

        # Traverse neighbors.
        for direction in directions:
          next_i, next_j = curr_i + direction[0], curr_j + direction[1]
          if 0 <= next_i < rows and 0 <= next_j < cols:

            # Add in question-specific checks, where relevant.
            queue.append((next_i, next_j))

  for i in range(rows):
    for j in range(cols):
      traverse(i, j)
```

### Topological sorting

A topological sort or topological ordering of a directed graph is a linear ordering of its vertices such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering. Precisely, a topological sort is a graph traversal in which each node v is visited only after all its dependencies are visited.

Topological sorting is most commonly used for scheduling a sequence of jobs or tasks which has dependencies on other jobs/tasks. The jobs are represented by vertices, and there is an edge from x to y if job x must be completed before job y can be started.

Another example is taking courses in university where courses have pre-requisites.

In the context of directed graphs, in-degree of a node refers to the number of incoming edges to that node. In simpler terms, it's a count of how many vertices "point to" or "lead to" the given vertex.

```javascript
type Graph = Map<number, number[]>;

function topologicalSort(graph: Graph): number[] | null {
    const numNodes = graph.size;
    const inDegree: Map<number, number> = new Map();
    const zeroInDegreeQueue: number[] = [];
    const result: number[] = [];

    // Initialize in-degree counts
    for (const [node, neighbors] of graph.entries()) {
        inDegree.set(node, 0);
    }

    for (const [, neighbors] of graph.entries()) {
        for (const neighbor of neighbors) {
            inDegree.set(neighbor, (inDegree.get(neighbor) || 0) + 1);
        }
    }

    // Find all nodes with zero in-degree
    for (const [node, degree] of inDegree.entries()) {
        if (degree === 0) {
            zeroInDegreeQueue.push(node);
        }
    }

    while (zeroInDegreeQueue.length) {
        const current = zeroInDegreeQueue.shift()!;
        result.push(current);

        const neighbors = graph.get(current) || [];
        for (const neighbor of neighbors) {
            inDegree.set(neighbor, inDegree.get(neighbor)! - 1);
            if (inDegree.get(neighbor) === 0) {
                zeroInDegreeQueue.push(neighbor);
            }
        }
    }

    if (result.length !== numNodes) {
        return null;  // Graph has a cycle
    }

    return result;
}

// Test
const graph: Graph = new Map();
graph.set(5, [2]);
graph.set(4, [0, 2]);
graph.set(2, [3]);
graph.set(3, [1]);
graph.set(1, []);
graph.set(0, []);

const sortedOrder = topologicalSort(graph);
console.log(sortedOrder);  // Possible output: [5, 4, 2, 3, 1, 0]
```

## Heap

A heap is a specialized tree-based data structure which is a complete tree that satisfies the heap property.

- Max heap - In a max heap, the value of a node must be greatest among the node values in its entire subtree. The same property must be recursively true for all nodes in the tree.
- Min heap - In a min heap, the value of a node must be smallest among the node values in its entire subtree. The same property must be recursively true for all nodes in the tree.

In the context of algorithm interviews, heaps and priority queues can be treated as the same data structure. A heap is a useful data structure when it is necessary to repeatedly remove the object with the highest (or lowest) priority, or when insertions need to be interspersed with removals of the root node.

### Time complexity
Operation	Big-O<br/>
Find max/min	O(1)<br/>
Insert	O(log(n))<br/>
Remove	O(log(n))<br/>
Heapify (create a heap out of given array of elements)	O(n)<br/>

### Mention of k
If you see a top or lowest k being mentioned in the question, it is usually a signal that a heap can be used to solve the problem, such as in Top K Frequent Elements.

If you require the top k elements use a Min Heap of size k. Iterate through each element, pushing it into the heap (for python heapq, invert the value before pushing to find the max). Whenever the heap size exceeds k, remove the minimum element, that will guarantee that you have the k largest elements.

## Trie

Tries are special trees (prefix trees) that make searching and storing strings more efficient. Tries have many practical applications, such as conducting searches and providing autocomplete. It is helpful to know these common applications so that you can easily identify when a problem can be efficiently solved using a trie.

Be familiar with implementing from scratch, a Trie class and its add, remove and search methods.

Example:
```javascript
class TrieNode {
    children: { [key: string]: TrieNode } = {};
    isEndOfWord: boolean = false;
}

class Trie {
    private root: TrieNode = new TrieNode();

    // Inserts a word into the trie
    insert(word: string): void {
        let currentNode = this.root;
        for (let char of word) {
            if (!currentNode.children[char]) {
                currentNode.children[char] = new TrieNode();
            }
            currentNode = currentNode.children[char];
        }
        currentNode.isEndOfWord = true;
    }

    // Returns if the word is in the trie
    search(word: string): boolean {
        let currentNode = this.root;
        for (let char of word) {
            if (!currentNode.children[char]) {
                return false;
            }
            currentNode = currentNode.children[char];
        }
        return currentNode.isEndOfWord;
    }

    // Returns if there's any word in the trie that starts with the given prefix
    startsWith(prefix: string): boolean {
        let currentNode = this.root;
        for (let char of prefix) {
            if (!currentNode.children[char]) {
                return false;
            }
            currentNode = currentNode.children[char];
        }
        return true;
    }
}

// Test
const trie = new Trie();
trie.insert("apple");
console.log(trie.search("apple"));    // Expected output: true
console.log(trie.search("app"));      // Expected output: false
console.log(trie.startsWith("app"));  // Expected output: true
trie.insert("app");
console.log(trie.search("app"));      // Expected output: true
```

### Time complexity
`m` is the length of the string used in the operation.

Operation	Big-O<br/>
Search	O(m)<br/>
Insert	O(m)<br/>
Remove	O(m)<br/>

### Techniques
Sometimes preprocessing a dictionary of words (given in a list) into a trie, will improve the efficiency of searching for a word of length k, among n words. Searching becomes O(k) instead of O(n).

## Geometry

Distance between two points
```javascript
type Point = {
    x: number,
    y: number
};

function distanceBetweenTwoPoints(point1: Point, point2: Point): number {
    return Math.sqrt(Math.pow(point2.x - point1.x, 2) + Math.pow(point2.y - point1.y, 2));
}
```

Overlapping Circles
```javascript
type Circle = {
    center: Point,
    radius: number
};

function areCirclesOverlapping(circle1: Circle, circle2: Circle): boolean {
    const distance = distanceBetweenTwoPoints(circle1.center, circle2.center);
    return distance <= (circle1.radius + circle2.radius);
}
```

Overlapping Rectanges
```javascript
type Rectangle = {
    topLeft: Point,
    bottomRight: Point
};

function areRectanglesOverlapping(rect1: Rectangle, rect2: Rectangle): boolean {
    // Check if one rectangle is to the left of the other
    if (rect1.topLeft.x > rect2.bottomRight.x || rect2.topLeft.x > rect1.bottomRight.x) {
        return false;
    }

    // Check if one rectangle is above the other
    if (rect1.topLeft.y < rect2.bottomRight.y || rect2.topLeft.y < rect1.bottomRight.y) {
        return false;
    }

    return true; // If none of the above cases occurred, rectangles are overlapping
}
```