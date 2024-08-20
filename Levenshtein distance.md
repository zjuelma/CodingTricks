This function calculates the minimum number of single-character edits (insertions, deletions, or substitutions) required to transform one string into another, while respecting a given limit on the number of edits.

```python
def minimum_mewtations(typed, source, limit):
    """A diff function that computes the edit distance from TYPED to SOURCE.
    This function takes in a string TYPED, a string SOURCE, and a number LIMIT.
    Arguments:
        typed: a starting word
        source: a string representing a desired goal word
        limit: a number representing an upper bound on the number of edits
    >>> big_limit = 10
    >>> minimum_mewtations("cats", "scat", big_limit)       # cats -> scats -> scat
    2
    >>> minimum_mewtations("purng", "purring", big_limit)   # purng -> purrng -> purring
    2
    >>> minimum_mewtations("ckiteus", "kittens", big_limit) # ckiteus -> kiteus -> kitteus -> kittens
    3
    """
    def edit(i,j,edits):
        if edits > limit:
            return edits
        if i == len(typed):
            return len(source) - j + edits
        if j == len(source):
            return len(typed) - i + edits
        
        if typed[i] == source[j]:
            return edit(i + 1,j + 1, edits)
        
        insert_cost = edit(i,j + 1,edits + 1)
        delete_cost = edit(i + 1,j,edits + 1)
        substitute_cost = edit(i + 1,j + 1,edits + 1)
        
        return min(insert_cost,delete_cost,substitute_cost)

    return edit(0,0,0)
```

