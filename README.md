This crate provides convenience methods for encoding and decoding numbers in
either big-endian or little-endian order. This is meant to replace the old
methods defined on the standard library `Reader` and `Writer` traits.

[![Build status](https://api.travis-ci.org/BurntSushi/byteorder.png)](https://travis-ci.org/BurntSushi/byteorder)
[![](http://meritbadge.herokuapp.com/byteorder)](https://crates.io/crates/byteorder)

Dual-licensed under MIT or the [UNLICENSE](http://unlicense.org).

### This fork

This fork uses core_io instead std::io, and is maintained by the Robigalia
project (https://robigalia.org/).

### Documentation

[http://burntsushi.net/rustdoc/byteorder/](http://burntsushi.net/rustdoc/byteorder/).

The documentation includes examples.


### Installation

This crate works with Cargo and is on
[crates.io](https://crates.io/crates/byteorder). The package is regularly
updated.  Add it to your `Cargo.toml` like so:

```toml
[dependencies]
byteorder = "0.5"
```

If you want to augment existing `Read` and `Write` traits, then import the
extension methods like so:

```rust
extern crate byteorder;

use byteorder::{ReadBytesExt, WriteBytesExt, BigEndian, LittleEndian};
```

For example:

```rust
use std::io::Cursor;
use byteorder::{BigEndian, ReadBytesExt};

let mut rdr = Cursor::new(vec![2, 5, 3, 0]);
// Note that we use type parameters to indicate which kind of byte order
// we want!
assert_eq!(517, rdr.read_u16::<BigEndian>().unwrap());
assert_eq!(768, rdr.read_u16::<BigEndian>().unwrap());
```

### `no_std` crates

This crate has a feature, `std`, that is enabled by default. To use this crate
in a `no_std` context, add the following to your `Cargo.toml`:

```toml
[dependencies]
byteorder = { version = "0.5", default-features = false }
```
