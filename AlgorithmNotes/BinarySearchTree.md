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
