# (Rule Name)

(Please describe the rule's core and its purpose in a short sentence)

## Example (where applicable)

Don't do:

```rust,ignore
can_fail.unwrap();
```

Do instead:

```rust,ignore
can_fail.expect("failure reason");
```

## Explanation

(Optional: Detailed explanation)
