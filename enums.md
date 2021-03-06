# Enums

Consider extracting enum variant fields into a separate struct, rather than
using struct-like enum variants.

## Example

Don't do:

```rust
enum Test {
    Foo {
        field1: usize,
    },
}
```

Do instead:

```rust
enum Test {
    Foo(Foo),
}

struct Foo {
    field1: usize,
}
```

## Explanation

Storing all fields of an enum in a variable is not possible for struct-like enum
variants, since its type is that of the original enum and thus requires matching
again to extract the fields.

By extracting the fields into a separate struct, it is possible to extract the
variant from the enum and still use the struct as a bundled storage medium for
the fields.

This is especially helpful when creating public enums inside a library, where
you have no control over their usage. If there's any uncertainty about the
enum's usage, it's usually best to go for a separate struct.
