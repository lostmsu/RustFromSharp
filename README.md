This repository is here to help .NET developers get started with Rust quickly

# LINQ in Rust
General syntax in Rust: `collection.iter().filter(|i| i > 0).count()` for single value queries, and `collection.iter().filter(...).collect()` for queries, that need to be converted back to a collection (e.g. `.ToList`) 

Before applying any querying on Rust collections, often one must manually call `.iter()`, as Rust's LINQ-like methods are defined on [`Iterator` trait](https://doc.rust-lang.org/std/iter/trait.Iterator.html), which is a direct counterpart of [`IEnumerator<T>`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerator-1). In .NET world LINQ methods are defined on [`IEnumerable<T>`](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1).

Another rule of thumb is that some .NET operators, that have overloads with or without embedded filter might not have this filter in Rust counterpart, or vice versa. For example, `.All` in LINQ has both, while `.all` in Rust requires filter argument. `.Count` has both, but in Rust `.count` does not take filter.

|.NET|Rust|
|---|---|
|Aggregate|fold|
|All|all|
|Any|any|
|Concat|chain|
|Count|count/filter+count|
|First/FirstOrDefault|find|
|Last|last|
|Max|max|
|Min|min|
|Select|map|
|SelectMany|flat_map|
|Skip|skip|
|SkipWhile|skip_while|
|Take|take|
|TakeWhile|take_while|
|ToList/To*|[collect](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.collect)|
|Where|filter|
|Where+Select|filter_map|
|Zip|[zip (!)](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.zip "Semantics might differ")|

Rust also has the following additional methods:
* `cloned` - behaves like `.Select(i => i.Clone())`
* `flatten` - behaves like `.Select(i => i)`
* [`inspect`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.inspect) - useful for debugging (e.g. print every element). Behaves like `.Select(i => { UserAction(i); return i; })`
* `nth`
* `position` and `rposition` - find the index of an element matching criteria. Generally similar to `.IndexOf` and `.LastIndexOf` respectively
* [`step_by`](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.step_by)
