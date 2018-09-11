# Quicksort
- Recursive, O(nlogn) time complexity

1. Base case: return if length <= 1
2. Select pivot element: ~~arr[0]~~ random index
3. Partition [] around pivot (> are to right, <= left of pivot)
4. Quicksort(left) + [pivot] + Quicksort(right)

## Not In-Place
- Creates new [] for each step
- Step 3: left = [], left << smaller el's than pivot, same w right

## In-Place
- Step 3: no new arrays, just swapping to right of 'barrier'
  1. First round: only pivot, 'barrier', and unchecked els
  2. Iterate through unchecked:
    - If <= pivot, swap with first el to right of 'barrier' idx, increment 'barrier' idx
    - If > pivot, nothing
    - Unchecked length shrinks by 1 naturally
  3. Swap pivot with el direct to left of 'barrier', change pivot_idx
- Step 4: quicksort(arr, start_idx = 0, end_idx = arr.length)
  - Left []: quicksort(arr, 0, barrier_idx not inclusive])
  - Right []: quicksort(arr, barrier_idx, arr.length not inclusive])

## Analysis
Time Complexity
- O(nlogn) bc division of array 'split' each recursive call for n calls
- O(n**2): qs(already_sorted_arr)
  - Fix: pivot is randomly generated -> almost always O(nlogn) again

Space Complexity
- O(logn): number of recursive calls, another reason for random pivot
