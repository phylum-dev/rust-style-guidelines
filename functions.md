# Functions

Consider extracting intermediates when dealing with long method chains and
iterators.

When possible, method paths should be used instead of closures as method
parameters.

## Example

Don't do:

```rust,ignore
let result = vec
    .iter()
    .map(|number| u8::from(number))
    .filter(|number| number % 2 == 0)
    .map(|number| number * 2);
```

Do instead:

```rust,ignore
let even = vec.iter().map(u8::from).filter(|number| number % 2 == 0);
let result = even.map(|number| number * 2);
```

## Explanation

Not only does extraction of intermediates allow method chains to use less
vertical space, it also makes it possible for readers to understand what the
purpose of different sub-sections of the chain is by assigning it a meaningful
variable name.

Using method paths as function parameters can help significantly shorten some
function calls, though is rarely worth it when the path is longer than the
closure. Using `Option/Result::as_deref` can help transform more function calls
into the path-parameter form.
