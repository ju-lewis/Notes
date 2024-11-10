
## Warm-up


```prolog
X = a;
X = e;
false.
```

```prolog
% Infinite loop.
% 
% Each call fails because it's impossible to append to a non-empty 
% list and get a resulting list of length 1 - however there are infinitely
% many different lists we can append to search for a solution.
```

