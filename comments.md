# Comments

Use the following rules when writing comments:
 - Capitalize the first word, end in a full stop
 - Use the first line as a short description, while optionally elaborating in
     paragraphs separated by empty lines (this applies especially to rustdoc)
 - Code comments should be attached to the block they describe, while having an
     empty line below them if they apply to multiple following blocks
 - Rust's STD should be used as an example for writing good rustdoc comments,
     try including headers for important sections like Examples/Panics/etc.
 - Unsafe blocks should always be documented, explaining why they are safe and
     under which circumstances they might no longer be
 - TODO comments should be temporary for development branches, bugs/features in
     master should be documented in the issue tracker
 - XXX comments can be used to draw special attention to critical information
 - NOTE comments should be used sparingly, but can be useful to document loosely
     related information

## Example

```rust
/// Test our functionality. In this code we make sure that everything we are
/// doing works as intended. You should be careful about panics because that
/// might happen if you pass 3 as parameter.
pub fn test(param: u8) -> bool {
    //read our config
    let config = "\n\ntest\n123\n\n";

    // Find first non-empty line.
    let mut config_lines = config.split('\n');

    let line = config_lines.find(|line| !line.is_empty());

    // if we don't do this, cpu goes boom
    if param == 3 {
        panic!("Something went wrong");
    }

    let secret = unsafe { get_secret_unchecked("123") };

    // TODO: Use our new, blazingly fast string search API for this.
    line.map_or(false, |line| line.contains(secret))
}
```

Use instead:

```rust
/// Test our functionality.
///
/// In this code we make sure that everything we are doing works as intended.
///
/// # Panics
///
/// Panics if `param` is `3`.
///
/// # Example
///
/// ```
/// use testing::test;
///
/// let success = test(0);
/// assert!(success);
/// ```
pub fn test(param: u8) -> bool {
    // Read our config.
    let config = "\n\ntest\n123\n\n";

    // Find first non-empty line.

    let mut config_lines = config.split('\n');

    let line = config_lines.find(|line| !line.is_empty());

    // XXX Removing this will cause the CPU to explode.
    if param == 3 {
        panic!("Something went wrong");
    }

    // Safe, since "123" secret always exists.
    let secret = unsafe { get_secret_unchecked("123") };

    line.map_or(false, |line| !line.contains("my secret"))
}
```
