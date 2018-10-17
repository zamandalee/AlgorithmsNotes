# Sorting Algorithms

## Bubble sort
- Iterates through arr, tracks boolean ```sorted```, swaps el with one behind it if out of order
  - Time: O(n ^ 2), space: O(1)

  ```rb
  def bubble_sort!(arr)
    sorted = false
    until sorted
      sorted = true

      arr.each_index do |i|
        next if i + 1 == arr.length
        j = i + 1
        if arr[i] > arr[j]
          sorted = false
          arr[i], arr[j] = arr[j], arr[i]
        end
      end
    end

    arr
  end
  ```

## Merge sort
- Breaking input into pieces recursively, then merge them back together
  - Time: O(nlogn), space: O(n)

  ```rb
  def mergesort(arr)
    return arr if arr.length <= 1

    middle_idx = arr.length / 2

    left = mergesort( arr[0...middle_idx] )
    right = mergesort( arr[middle_idx..-1] )

    merge(left, right)
  end

  def merge(left, right)
    merged = []

    until left.empty? || right.empty?
      case left[0] <=> right[0]
      when - 1
        merged << left.shift
      when 0
        merged << left.shift
        merged << right.shift
      when 1
        merged << right.shift
      end
    end

    merged.concat(left).concat(right)
  end
  ```

## Quick sort
- Select a pivot, recurse on left and right of pivot

  ```rb
  def quicksort(arr)
    return arr if arr.length <= 1

    pivot = arr[0]
    left = arr[1..-1].select{ |el| el < pivot }
    right = arr[1..-1].select{ |el| el >= pivot }

    quicksort(left) + [pivot] + quicksort(right)
  end
  ```
