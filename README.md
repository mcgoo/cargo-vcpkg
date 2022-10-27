# cargo-vcpkg [![Windows](https://github.com/mcgoo/vcpkg-rs/workflows/Windows/badge.svg?branch=master)](https://github.com/mcgoo/vcpkg-rs/actions?query=workflow%3AWindows) [![macOS](https://github.com/mcgoo/vcpkg-rs/workflows/macOS/badge.svg?branch=master)](https://github.com/mcgoo/vcpkg-rs/actions?query=workflow%3AmacOS) [![Linux](https://github.com/mcgoo/vcpkg-rs/workflows/Linux/badge.svg?branch=master)](https://github.com/mcgoo/vcpkg-rs/actions?query=workflow%3ALinux)

### This is the version that cargo-vcpkg has been released from since 0.1.6. Previous versions were homed at mcgoo/vcpkg-rs. crates.io/vcpkg needs older Rust for compatibility with older projects, while cargo-vcpkg would like to track new versions for the latest features in Cargo.toml, hense the split of repos between components.

[Changelog](https://github.com/mcgoo/vcpkg-rs/blob/master/cargo-vcpkg/CHANGELOG.md)

This command `cargo vcpkg` will create a [vcpkg](https://github.com/microsoft/vcpkg) tree and install the packages specified in `Cargo.toml` files in the crate being built and crates it depends on. Crates that use the [vcpkg crate](https://crates.io/crates/vcpkg) will be able to find libraries automatically.

## Example

```toml
[package.metadata.vcpkg]
git = "https://github.com/microsoft/vcpkg"
rev = "4c1db68"
dependencies = ["pkg1", "pkg2"]
```

```
$ cargo install cargo-vcpkg
$ cargo vcpkg build
    Fetching vcpkg
    Checkout rev/tag/branch 4c1db68
   Compiling pkg1, pkg2
    Finished in 1.93s
$ cargo build
[...]
```

## Per target configuration

It is also possible to install different sets of packages per target, and override the vcpkg triplet to install.

```toml
[package.metadata.vcpkg]
git = "https://github.com/microsoft/vcpkg"
rev = "4c1db68"
dependencies = ["sdl2"]

[package.metadata.vcpkg.target]
x86_64-apple-darwin = { dependencies = ["sdl2", "sdl2-gfx" ] }
x86_64-unknown-linux-gnu = { dependencies = ["sdl2", "opencv"] }
x86_64-pc-windows-msvc = { triplet = "x64-windows-static", dependencies = ["sdl2", "zeromq"] }
```

## Development dependencies

Setting the `dev-dependencies` key allows building libraries that are required by binaries in this crate. Only the packages in the `dependencies` key will be installed if `cargo vcpkg` is run on a crate that depends on this crate.

```toml
[package.metadata.vcpkg]
git = "https://github.com/microsoft/vcpkg"
rev = "4c1db68"
dependencies = ["sdl2"]
dev-dependencies = ["sdl2-image"]

[package.metadata.vcpkg.target]
x86_64-apple-darwin = { dev-dependencies = ["sdl2-gfx" ] }
```

## Overlay triplets

Setting the `overlay-triplets-path` key allows you use custom [triplet files] in
your build. The value of this key should be the path to a directory containing
triplet files. These files will be made available during the vcpkg build through
its `--overlay-triplets` argument.

[triplet files]: https://vcpkg.readthedocs.io/en/latest/users/triplets/

```toml
[package.metadata.vcpkg]
git = "https://github.com/microsoft/vcpkg"
rev = "4c1db68"
dependencies = ["sdl2"]
overlay-triplets-path = "support/custom-triplets"

[package.metadata.vcpkg.target]
x86_64-pc-windows-msvc = { triplet = "x64-windows-static-release" }
```

Here, the repository should contain a file named
`support/custom-triplets/x64-windows-static-release.cmake`.

## Installation

Install by running

```
cargo install cargo-vcpkg
```

## License

See LICENSE-APACHE, and LICENSE-MIT for details.
