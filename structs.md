# Structs

Use `Default::default` for initializing struct fields without a specific value.

Use `..struct` notation to shorten struct initialization, especially when
initializing most fields of a struct to its default implementation.

## Example

Don't do:

```rust
struct Test {
    field1: usize,
    field2: usize,
    field3: usize,
}

impl Default for Test {
    fn default() -> Self {
        Self {
            field1: 0,
            field2: 13,
            field3: 0,
        }
    }
}

impl Test {
    fn new(field1: usize) -> Self {
        Self {
            field1,
            field2: 13,
            field3: 0,
        }
    }
}
```

Do instead:

```rust
struct Test {
    field1: usize,
    field2: usize,
    field3: usize,
}

impl Default for Test {
    fn default() -> Self {
        Self {
            field2: 13,
            field1: Default::default(),
            field3: Default::default(),
        }
    }
}

impl Test {
    fn new(field1: usize) -> Self {
        Self {
            field1,
            ..Default::default()
        }
    }
}
```

## Explanation

Initializing struct fields with `Default::default` can make it more clear to a
reader that the chosen value is of no special significance. Additionally for
`Default` implementations it makes it obvious which values prevent the
derivation of the `Default` trait.

Using the `..struct` shorthand not only makes it clear that only part of a
struct is explicitly overridden, it also automatically applies future changes to
the parts that are copied from the other struct.
