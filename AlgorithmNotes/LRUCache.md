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

```rb
  def resize!
    new_set = ResizingIntSet.new(num_buckets * 2)

    @store.each do |bucket|
      bucket.each do |el|
        new_set.insert(el)
      end
    end

    @store = new_set.store
  end
```

## Hashing
- Good hashing function:
  - Applicable to anything
  - Deterministic: always produce same output for same input
  - One-way

## Linked List
- Linked list: data structure containing nodes
  - Head and tail: sentinel nodes (dummy node w/o val), never reassigned
  - Node: val, pointer to next node
- Doubly linked list: nodes have pointer to prev and next
- #first, #empty?, #include?(key), #get(key), #append(key, val), #update(key, val), #remove(key), #each(&prc)

## HashMap
- To get bucket: hash the key before %ing by num_buckets

```rb
def set(key, val)
  unless include?(key)
    @count += 1
    resize! if @count == num_buckets
    bucket(key.hash).append(key, val)
  else
    bucket(key.hash).update(key, val)
  end
end

def bucket(key)
  @store[key.hash % num_buckets]
end
```

### HashMap Example
```rb
# if string can be permuted into a palindrome
def can_string_be_palindrome?(string)
  pal_hash = HashMap.new

  string.downcase.split("").each do |letter|
    val = pal_hash.get(letter)
    pal_hash.include?(letter) ? pal_hash.set(letter, val += 1) : pal_hash.set(letter, 1)
  end

  num_odd_vals = 0
  pal_hash.each do |key, val|
    num_odd_vals += 1 if val.odd?
  end

  num_odd_vals < 2
end
```

## LRU Cache
- Least Recently Used Cache: cache of top `max` most recently used
- Each time append:
  - If key alr in cache: move node to end of list (now it is the most recently used)
  - If not in cache:
    1. Call proc on key -> output is val
    2. Append so it's the most recently used
    3. If cache exceeded `max`, call #eject! to delete least recently used (the #first)
