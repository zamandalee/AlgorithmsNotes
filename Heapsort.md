# Heapsort Notes

## Priority Queues
- Priority queue ex.: bronze member -> bronze -> silver -> gold -> gold -> platinum
- Can't be implemented w:
  - Linked list: bc insertion O(n)
  - LRU Cache: bc need a hash just as long as the linked list, not space efficient
- Implement w heap

## Heap
- Heap: data structure, a binary tree (root node, at most 2 children/node) w constraints
  - Must be complete: MUST fill top to bottom, left to right
    - Diff from full (which needs to have full row of 2 children/node)
  - The heap property: parent node <= child
  - Used for priority queues, mins/maxs

- #peek: returns min element in heap, O(1)
  - Alw root node
  - sdfa

- #insert(el): inserts according to priority, < O(n)
  - Add to end, swap with parent until heap property obeyed (sift/heapify up) -> O(logn)

- #extract or #pop: returns min element in heap, removes it
  - Swap root with bottom-most right-most node -> remove and return -> heapify down (swap with smallest of children, left if equal) -> O(logn)

- Under the hood
  - Represented by [top to bottom, left to right]
  - Associations
    - Right_child_idx = 2 * parent_idx + 1
    - Left_child_idx = 2 * parent_idx + 2
    - Parent_idx = (child_idx -  1) / 2
  - #peek: @store[0]
  - #insert(el): @store.push(el), check if parent is <=, swap if not, repeat heapify
  - #extract(el): swap @store[0] and @store[-1], pop, check if <= child, swap if not, repeat heapify

## Heap Sort
Naive:
- O(nlogn) time, O(2n) space
  1. Heapify input into proper heap, O(nlogn)
    - Push input[0]
    - Repeat with all of input
  2. Sort, O(nlogn)
    - Continuously extract, and push the return of extract into sorted []

Optimized/In-Place:
- O(nlogn), O(1) space
  1. Heapify into Max-Heap (parents larger)
    - Move 'boundary' from between 0 & 1 indexes to between 1 & 2
    - heapify_up with el on left of 'boundary'
  2. Sort from right to left
    - Until one element left to left of 'boundary'
    - Extract, except move 'boundary' to in front of @store[-1], then heapify_down excluding right of 'boundary'
