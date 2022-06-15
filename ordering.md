# Ordering

Use the following rules when writing comments:

 - Constructors like `new`/`from_` must always be the first impl methods
 - Pub fields, methods and constants should be above their non-pub counterparts
 - Structs depending on each other can be grouped together, but must not
     interrupt the struct definition/impl block grouping
 - Trait impls should be below their struct, unless the struct is foreign
 - Struct initialization fields should have the following order:
    - Shorthand fields with identical variable/field name 
    - Fields with custom assignment inline
    - Fields with Default::default() assignment
 - Impl blocks should have the following order:
    - Constructor trait impls like Default/From
    - Struct impl
    - Other trait impls

## Example

Don't do:

```rust
impl Default for Example {
    fn default() -> Self {
        let field1 = 13;

        Self {
            field3: Default::default(),
            field1,
            field2: 99,
        }
    }
}

struct Example {
    field1: usize,
    pub field2: usize,
    field3: usize,
}

impl Example {
    fn field1(&self) -> usize {
        self.field1
    }

    fn new() -> Self {
        Self::default()
    }
}

trait Print {
    fn print(&self);
}

impl Print for Example {
    fn print(&self) {
        println!("{} - {} - {}", self.field1, self.field2, self.field3);
    }
}
```

Do instead:

```rust
trait Print {
    fn print(&self);
}

struct Example {
    pub field2: usize,

    field1: usize,
    field3: usize,
}

impl Default for Example {
    fn default() -> Self {
        let field1 = 13;

        Self {
            field1,
            field2: 99,
            field3: Default::default(),
        }
    }
}

impl Example {
    fn new() -> Self {
        Self::default()
    }

    fn field1(&self) -> usize {
        self.field1
    }
}

impl Print for Example {
    fn print(&self) {
        println!("{} - {} - {}", self.field1, self.field2, self.field3);
    }
}
```

## Explanation

Putting constructors and constructor types at the top makes it easier for
consumers to determine how a struct can be created. Combining this with putting
`pub` elements at the top allows easy identification of the intended API
interface process.

Having structs and all their impl blocks grouped together prevents guesswork
when trying to add new functionality. It also ensures that the local context
used by these methods is easily discoverable.

Ordering struct initialization fields makes it possible to clearly distinguish
between fields explicitly set and fields set to default for the sake of
convenience. In `Default` implementations this also allows clear identification
which fields prevent the derivation of the `Default` trait.
