# Binary Search Tree Notes

## Previous, Simpler Data Structures
- Array: #find O(n), #insert O(1) ammortized, #delete O(n+n)
- Sorted array: **#find O(logn)**, #insert O(n), #delete O(logn+n)
- Min/max heap: #find O(n), **#insert O(logn)**, **#delete O(logn)**

## BST
- Binary search tree: left are <= root node (= either right or left, stay consistent), right are > root
  - Each subtree is a BST (recursion)
- ```#find(val)```: compare val to root -> if <, check for left child -> if left child, recurse with left child as root -> keep going until = current node (return true) or child is nil (return false)
  - O(logn): O(depth)
- ```#insert(val)```: traverse down tree to find simplest spot for insertion
  - O(logn): O(depth)
- ```#delete(val)```: val's replacement must be 1. > root 2. > left subtree 3. < right subtree
  - Hibbard Deletion: replace w max (right as far as possible) of left subtree -> left children + that subtree of max replaces that max after it's moved

## Balanced BST
- Balanced BST: diff in depth of left and right is <= 1 && left and right are balanced BSTs
-


Great resource: [a/A BST reading](https://github.com/appacademy/sf-job-search-curriculum/blob/master/algorithms/binary_search_trees/bst_reading.md)
