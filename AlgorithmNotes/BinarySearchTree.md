# Binary Search Tree Notes
- **Binary search tree**: left are <= root node (= either right or left, stay consistent), right are > root
  - Each subtree is a BST

## Simpler Data Structures
- Array: #find O(n), #insert O(1) ammortized, #delete O(n+n)
- Sorted array: **#find O(logn)**, #insert O(n), #delete O(logn+n)
- Min/max heap: #find O(n), **#insert O(logn)**, **#delete O(logn)**
We want O(logn) time complexity for 3 core BST methods.

## BST Methods
- ```#find(val)```: recursively traverse down tree
compare val to root -> if <, check for left child -> if left child, recurse with left child as root -> keep going until = current node (return true) or child is nil (return false)
  1. If ```root.nil?```, return false. Else, compare root to val. Return true if equal.
  2. If root > val, ```root.right_subtree.find(val)```
  3. If < val, ```root.left_subtree.find(val)```
  - O(logn): O(depth)
- ```#insert(val)```: recursively traverse down tree
  1. Compare value to root
  2. If value > root, check for root's right child. If root has right child,  ```insert(value, root.right_child)```. Else, make value root's right child.
  3. Do same if value < root with the left subtree.
  - O(logn): O(depth)
- ```#delete(val)```: val's replacement must be 1. > root 2. > left subtree 3. < right subtree
  - **Hibbard Deletion**: replace w max of left subtree(right as deep as possible) -> left child (there is no right child bc we took deepest right as max) + that subtree of that replaces that max after it's moved
  1. ```find(val)```
  2. If ```val``` has no children, erase ```val```.
  3. If ```val``` has one child, let it replace ```val```
  4. If ```val``` has 2 children, find maximum ```r``` of left subtree
  5. Replace ```val``` w ```r```
  6. If ```r```had left child, replace ```r```with it.

## Balanced BST
- **Balanced BST**: diff in depth of left and right is <= 1 && left and right are balanced BSTs
- **Degenerate BST**: not balanced, where times are not nec O(logn)

## In-Order Traversal
- Extract all vals, sorted
1. ```results = []```
2. In-order traversal of left subtree -> IOT of left subtree's left subtree -> etc. until no left subtree, push in current root
3. Go up one, push in new current root
4. IOT of right subtree
5. Repeat 2-4 until up to original root, push that in
6. Do the same with the right subtree of original root

Great resource: [a/A BST reading](https://github.com/appacademy/sf-job-search-curriculum/blob/master/algorithms/binary_search_trees/bst_reading.md)
