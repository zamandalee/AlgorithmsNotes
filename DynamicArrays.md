# Static & Dynamic Arrays Notes

- Ruby is wrapper for C -> C is wrapper for assembly language
- [] in C: fixed size (static arr) -> contiguous memory allocated for array storage

## Static Arrays
```rb
class StaticArray
  def initialize(length)
    @length = length
    @store = Array.new(length)
  end
  # ...
end
```

- #find: arithmetic and lookup at a specific memory location are constant time -> O(1)
- #push: arithmetic and the assignment are constant time -> O(1)
- #delete: shifts elements over after deletion -> O(n)
  - O(n/2) average and O(n - 1) worst case

## Dynamic Arrays
