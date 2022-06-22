# Macros

Macros must be surrounded by double brackets. Optional trailing commas should be
added when possible.

## Example

Don't do:

```rust
macro_rules! print_user_success {
    ($($tts:tt)*) => {
        eprint!("✅ ");
        eprintln!($($tts)*);
    }
}
```

Do instead:

```rust
macro_rules! print_user_success {
    ($($tts:tt)* $(,)?) => {{
        eprint!("✅ ");
        eprintln!($($tts)*);
    }}
}
```

## Explanation

When trying to use macros as values, it can cause errors when the macros don't
include their own block in the macro itself. Using two brackets ensures the
macro can be used in match arms without extra brackets.

Having an optional trailing comma makes it possible to use and format macros
like any other Rust function. This is especially important when multiple
arguments are taken and a linebreak is not unlikely.
