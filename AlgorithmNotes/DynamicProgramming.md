# Dynamic Programming

- Improving performance of solutions using methods that reuse work that's already done


- 2 paradigms:
1. ***Top-down***: AKA ***memoization***, often in recursion, build stacks and save work to a cache when bubbling up
- globally scoped ```@cache```


2. ***Bottom-up***: typical of iterative, use smaller solutions as basis of larger one
- def build_cache(arg) to first build out cache, then helper method called within function
