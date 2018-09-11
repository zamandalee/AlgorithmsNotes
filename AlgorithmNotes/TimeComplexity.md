# Algorithm Time Complexities

|     Name     | Big O    | Example                    |
|:------------:|----------|----------------------------|
| constant     | O(1)     | hash map                   |
| logarithmic  | O(log n) | binary search              |
| linear       | O(n)     | iteration                  |
| linearithmic | O(nlogn) | merge sort                 |
| quadratic    | O(n**2)  | doubly nested loops        |
| exponential  | O(2**n)  | subsets                    |
| factorial    | O(n!)    | permutations, subsequences |

- (n+1) / 2: partial sum for divergent series expression
  - ex.: n( (n + 1) / 2 )
  ```rb
  arr.each do |el|
    # as el++, search does 1 more iteration
    results << search(arr, el)
  end
  ```
  ```js
  for(let i = 0; i < n; i++) { // O(n)
    for( let j = i; j >= 0; j--) { // O((n + 1) / 2)
      ...
    }
  }
  ```
- logn: whenever dividing each time, divisor = base
  - ex.: recursive( n / 5) -> log base5 n
