# LRU Cache Notes

## Set
- Abstract Data Type (ADT): high-level description of a structure and an API (specific set of methods)
  - Ex.: set, map, queue
  - Data structure: implementation of data type or API


- Set: abstract data type of unordered, unique elements
  - Fast retrieval time

### IntSet
- IntSet: integer [], values at indices corr to presence
  - Ex.: ```@store = [F, T, F, T, F]```
- Fast, but only ints and limited range
- #include?(num), #insert(num), #remove(num)

### ResizingIntSet
- @store, @count
- #insert(num): O(n) amortized -> O(1) avg

# Hashing
- Good hashing function:
  - Applicable to anything
  - Deterministic: always produce same output for same input
  - One-way

# Linked List
- Linked list: data structure containing nodes
  - Head and tail: sentinel nodes (dummy node w/o val), never reassigned
  - Node: val, pointer to next node
- Doubly linked list: nodes have pointer to prev and next
- #first, #empty?, #include?(key), #get(key), #append(key, val), #update(key, val), #remove(key), #each(&prc)

# HashMap
- 
