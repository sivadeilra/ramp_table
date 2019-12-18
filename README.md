# RampTable

This crate formalizes a data structure that I've encountered many times. I've never seen this
data structure treated in its own right. Instead, I've only seen it used in many code bases,
implicitly, and never given a name. Perhaps it _does_ have a name and is well-known, but I
have not yet been able to find any discussion of it. (If you know of it, please let me know.)

A _ramp table_ is a specific representation for storing a set of lists. The sets are numbered,
and the (non-negative) numbers cluster near zero. Ideally, the set numbers are contiguous,
or close to it. Each set maps to a list of items.

The representation uses two vectors: `index` and `values`. Each entry in the `index` array
corresponds to a set number (also called a _key_). The `index` array also contains one
additional entry, at the end, which is not associated with any set but which terminates
the `index` vector.

`index[key]` gives the index within `values` of the beginning of the values for that key.
`index[key + 1]` gives the index within `values` of the end (exclusive upper bound) of
the values for that key. Thus, `&values[index[key]..index[key + 1]]` gives the slice of
values for a `key`.

At this point you're about to say, "Oh, _that_ data structure? Everyone knows about that."
Precisely! It's so common that it's used all over the place. However, usually I see this
data structure "open-coded" into its applications, so it's a little hard to identify it
at first. It's also useful to formalize a data structure and give it a name. It also
improves readability.

I've seen this data structure used in:

    * graphviz (SparseMatrix, lots of other things)
    * Berkeley YACC (storing all kinds of things)
    * and many more

