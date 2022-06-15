# Naming

When naming fields, functions, or variables, abbreviations should be avoided
unless they're the standard way to refer to something or extraordinary space
constraints are present.

Trait names must avoid the `-able` suffix and try to use the imperative instead
(see `Debug`/`Display`/`Hash`).

Function names returning a field should omit the `get_` prefix.

## Example

Don't do:

```rust
trait Explodable {
    fn get_f(&self) -> u8;
}
```

Do instead:

```rust
trait Explode {
    fn fuel(&self) -> u8;
}
```

## Explanation

Abbreviating names usually doesn't save much space, while ultimately only making
the code more difficult to read. Avoiding them makes their purpose clear and
prevents potential confusion.

While there are numerous examples for naming traits, the `-able` suffix is
almost universally avoided. While the imperative is less frequently enforced as
a rule, having a unified guideline hopefully makes the naming process simpler
with less potential for confusion and bikeshedding.
