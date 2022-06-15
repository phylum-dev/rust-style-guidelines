# Visibility

Avoid overly-specific visibility modifiers like `pub(super)`.

## Example

Don't do:

```rust
pub(super) struct Test;
```

Do instead:

```rust
pub(crate) struct Test;
```

## Explanation

Visibility modifiers are helpful to prevent modification outside of the module
context and reduce the noise in APIs. If you're unsure about the optimal
visbility, it's usually best to stick with `pub` or omitting the modifier. You
can use `pub(crate)` if you explicitly want to deny consumers from interacting
with an internal API.
