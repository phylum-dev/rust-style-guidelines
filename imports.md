# Imports

Most import formatting rules should be taken care of by [rustfmt](rustfmt.md).

For functions, their module should be imported, while importing structs and
enums directly.

If the `group_imports` `rustfmt` option is not used to automatically sort
imports, they should be in Std -> External -> Crate order. External crates that
you maintain can be put in separate blocks between External/Crate.

Module definitions should come after the imports, this also applies to imports
referencing that module.

Multiple imports behind the same `#[cfg]` attribute can be grouped together for
legibility, internally they should follow the same order as non-cfg imports.

Glob imports should only be used for `super::*` at the top of test modules and
`prelude` modules.

## Example

Don't do:

```rust,ignore
#[cfg(unix)]
use std::collections::HashMap;
use std::io::Read;
use std::io::Write;

use my_crate::foo::Bar;
use my_crate::bar::Baz;
#[cfg(unix)]
use serde::{Serialize, Deserialize};
use clap::ArgMatches;
use my_crate::extra::Stuff;
use crate::logic::function;

mod util;

use crate::{MyStruct, util::*};
```

Do instead:


```rust,ignore
#[rustfmt::skip]
#[cfg(unix)]
use {
    std::collections::HashMap,

    serde::{Serialize, Deserialize},
};

use std::io::{Read, Write};

use clap::ArgMatches;

use my_crate::bar::Baz;
use my_crate::extra::Stuff;
use my_crate::foo::Bar;

use crate::util::StructINeed;
use crate::{logic, MyStruct};

mod util;
```

The `#[cfg]` groupings in this example are just for demonstration purposes. It
is not recommended to group these imports unless there's a significant amount of
complexity and quantity in `#[cfg]` imports.

## Explanation

Separating imports into relevant blocks makes it easy to audit what imports are
in use and add new imports to the correct place.

Having module-level granularity with nesting only at the last level of the
import allows easily grasping the entire module hierarchy without cognitive
overhead.

Glob imports can easily cause conflicts with other modules, causing potential
friction for future changes. Importing only the necessary APIs will ensure
conflicts are kept to a minimum.
