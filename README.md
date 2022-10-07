[![API reference](https://docs.rs/once_cell/badge.svg)](https://docs.rs/xflags/)

# xflags

Moderately simple command line arguments parsing:

```rust
mod flags {
    use std::path::PathBuf;

    xflags::xflags! {
        src "./examples/basic.rs"

        cmd my-command {
            required path: PathBuf
            optional -v, --verbose
        }
    }

    // generated start
    // The following code is generated by `xflags` macro.
    // Run `env UPDATE_XFLAGS=1 cargo build` to regenerate.
    #[derive(Debug)]
    pub struct MyCommand {
        pub path: PathBuf,

        pub verbose: bool,
    }

    impl MyCommand {
        pub const HELP: &'static str = Self::HELP_;

        pub fn from_env() -> xflags::Result<Self> {
            Self::from_env_()
        }

        pub fn from_vec(args: Vec<std::ffi::OsString>) -> xflags::Result<Self> {
            Self::from_vec_(args)
        }
    }
    // generated end
}

fn main() {
    let flags = flags::MyCommand::from_env();
    println!("{:#?}", flags);
}
```
