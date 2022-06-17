# Control Flow

Avoid excessive nesting by using an early `return` when matching options.

When branching at the end of a function and returning a value, consider using an
`else` block instead of an early return.

## Example

Don't do:

```rust,ignore
if let Some(test) = option {
    if check {
        return 15;
    }
    0
}
```

Do instead:

```rust,ignore
let test = match option {
    Some(test) => test,
    None => return,
};

if check {
    15
} else {
    0
}
```

## Explanation

Rust code can easily fall victim to excessive nesting when combining impl
blocks, loops and option matching. One of the best ways to avoid this is to
extract options and results in `match` statements and `return`/`break` in the
`None`/`Err` case.

Putting an early return at the end of a function produces inconsistent code
which makes it more difficult to follow its control flow. By introducing an
`else` branch, the early return is removed and the branches are unified. However
this does introduce another layer of nesting, so the `else` branch should be
simple.
