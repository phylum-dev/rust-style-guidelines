# Rustfmt

All code should be formatted with `rustfmt`, this should also be enforced by CI.
Since most rules are only available on Rust nightly `cargo +nightly fmt` should
be used.

The following `rustfmt.toml` configuration options are recommended:

```
format_code_in_doc_comments = true
group_imports = "StdExternalCrate"
match_block_trailing_comma = true
condense_wildcard_suffixes = true
use_field_init_shorthand = true
normalize_doc_attributes = true
overflow_delimited_expr = true
imports_granularity = "Module"
use_small_heuristics = "Max"
normalize_comments = true
reorder_impl_items = true
use_try_shorthand = true
newline_style = "Unix"
format_strings = true
wrap_comments = true
```

## Configuration options

Some configuration options significantly help with the code formatting of
`rustfmt`, the following describes why these options are recommended.

A full description of every rule can be found in rustfmt's documentation:
https://rust-lang.github.io/rustfmt

### Comment formatting

These options ensure that rustfmt's rules are also applied to comments and that
comment formatting is consistent.

```
format_code_in_doc_comments = true
normalize_doc_attributes = true
normalize_comments = true
wrap_comments = true
```

### Trailing commas

Trailing commas are generally recommend whenever possible, since this can reduce
the noise when making new additions to existing code. By default this is already
done for functions, but an option is necessary to also apply it to match blocks.

```
match_block_trailing_comma = true
```

### Avoid verbose variants

The following rules all apply normalization to certain patterns to ensure the
recommended and shortest variant is used. Their behavior should not change.

```
condense_wildcard_suffixes = true
use_field_init_shorthand = true
use_try_shorthand = true
```

### Reduce vertical space usage

Delimited expressions like closures or slices at the end of a function can often
take up a significant amount of vertical space. This rule effectively reduces
that vertical space usage while improving comprehensibility.

```
overflow_delimited_expr = true
```

### Consistent line length limitations

By default, `rustfmt` will introduce arbitrary percentage-based limits for
formatting several different Rust structures. Using `"Max"` small heuristics
will consistently use the full line length available regardless of content. This
keeps line length predictable while still ensuring every line is within the
limit.

```
use_small_heuristics = "Max"
```

### Item order

The recommended order of items like `type` or `fn` in trait implementations is
clearly defined, this rule allows `rustfmt` to automatically take care of it.

```
reorder_impl_items = true
```

### String formatting

By default, strings are not confined to the maximum line length set in
`rustfmt`. Instead of manually formatting strings, using `rustfmt` allows
automating this procedure without affecting string content.

```
format_strings = true
```

### Consistent newlines

Unix newlines are the standard in most software projects, this way `rustfmt`
will automatically transform all newlines to the correct format even for new
files.

It's also a good idea to make sure your git configuration does not transform
newlines to crlf automatically.

```
newline_style = "Unix"
```

### Imports

Setting import granularity to the module level makes it possible to change
imports while generating only minimal diffs. At the same time vertical space is
kept in check for files with many different imports.

Setting the `group_imports` option to `StdExternalCrate` is a helpful way to
automatically order imports. However this should be applied with caution since
it will not allow for any other import blocks to be used. Separate blocks can be
desirable for example, when grouping crates which are maintained by the same
organization, in this case the `group_imports` option should be removed.

```
group_imports = "StdExternalCrate"
imports_granularity = "Module"
```
