# Tests

Tests should be in a `tests` module, in the same file they're testing. They can
be moved to a separate submodule file if necessary.

Parent module members should be imported with `use super::*` at the top of the
submodule.

## Example

Don't do:

```rust
fn to_test(param: u8) {
    param
}

#[test]
fn testing() {
    assert_eq!(to_test(3), 3);
}
```

Do instead:

```rust
fn to_test(param: u8) {
    param
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn testing() {
        assert_eq!(to_test(3), 3);
    }
}
```

## Explanation

Having a submodule for tests ensures no unused code warnings are emitted when
building the project. The shorthand of `use super::*` as the first line of the
tests module makes it possible to write tests without worrying about being in a
separate module.
