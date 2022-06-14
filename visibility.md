# Visibility

Avoid overly-specific visibility modifiers like `pub(super)`.

## Example (where applicable)

```rust
pub(super) struct Test;
```

Use instead:

```rust
pub(crate) struct Test;
```

## Explanation

Visibility modifiers are helpful to prevent modification outside of the module
context and reduce the noise in APIs. Having overly-specific visibility
modifiers creates confusing module relationships without providing significant
additional benefit.
