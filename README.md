# lc-study
Repo to hold LeetCode solutions and track personal progress easier than sifting through LC UI.

- [Blind 75](https://leetcode.com/discuss/general-discussion/460599/blind-75-leetcode-questions)

## Topics covered so far

- Arrays
- Hashing
- Two Pointers
- Sliding Window
- Binary Search
- Linked List
    - Floyd's Cycle Algorithm (Floyd's Tortoise and Hare Algorithm) 
- Binary Tree
    - Preorder, postorder, inorder traversal
    - DFS, BFS*

## To-Do

- Tries
- Graphs
- DP
- Greedy
- Specific algorithms (Djikstra's, different sorting algorithms, etc.)

## Notes

- Switched to Python to focus on algorithm rather than syntax
- When you see "substring" in a problem, consider `Sliding Window` technique
- Taking midpoint of an array can be `(l + r) // 2` in Python, but should be `l + (r - l) / 2` in other languages to avoid [integer overflow](https://en.wikipedia.org/wiki/Integer_overflow)
- When you see that a problem requires O(log*n) complexity, consider `Binary Search`
- Reversing a linked list (often used in larger problems) is about reversing pointers, not exchanging list values
- When creating an output list for a linked list problem, it can be smart to initialize it with a dummy node, i.e.:
```
dummy = ListNode()
tail = dummy
[...]
return dummy.next # for list excluding dummy node
```
- Vast majority of tree traversal algorithms involve recursion for optimal solution
- Consider the ability to create dummy values to establish a range to search, i.e. dummy values at the beginning of linked lists, or infinity values for the initial bounds when traversing a tree with conditionals