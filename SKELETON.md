# (Rule Name)

(Please describe the rule's core and its purpose in a short sentence)

## Example (where applicable)

Don't do:

```rust
can_fail.unwrap();
```

Do instead:

```rust
can_fail.expect("failure reason");
```

## Explanation

(Optional: Detailed explanation)
