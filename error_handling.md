# Error Handling

When handling errors, `unwrap` should only be used when failure is not possible,
otherwise `expect` should be preferred.

Inside of libraries, panics must be avoided unless recovery is impossible.

## Example

Don't do:

```rust
let text = std::fs::read_to_string("test").unwrap();
```

Do instead:

```rust
let text = std::fs::read_to_string("test").expect("failed to read 'test'");
```

## Explanation

See this excerpt from the latest version of the [Rust book]:

> In production-quality code, most Rustaceans choose `expect` rather than
> `unwrap` and give more context about why the operation is expected to always
> succeed. That way, if your assumptions are ever proven wrong, you have more
> information to use in debugging.

[Rust book]: https://doc.rust-lang.org/stable/book
