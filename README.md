# vcpkg-rs [![Windows](https://github.com/mcgoo/cargo-vcpkg/workflows/Windows/badge.svg?branch=master)](https://github.com/mcgoo/cargo-vcpkg/actions?query=workflow%3AWindows) [![macOS](https://github.com/mcgoo/cargo-vcpkg/workflows/macOS/badge.svg?branch=master)](https://github.com/mcgoo/cargo-vcpkg/actions?query=workflow%3AmacOS) [![Linux](https://github.com/mcgoo/cargo-vcpkg/workflows/Linux/badge.svg?branch=master)](https://github.com/mcgoo/cargo-vcpkg/actions?query=workflow%3ALinux)

** This is to be the repository for the next release for cargo-vcpkg. The existing release is from mcgoo/vcpkg-rs. **

[Documentation](https://docs.rs/cargo-vcpkg) [Changelog](CHANGELOG.md)

This is a helper for finding libraries in a [Vcpkg](https://github.com/Microsoft/vcpkg) installation from cargo build scripts. It works similarly to [pkg-config](https://github.com/alexcrichton/pkg-config-rs). It works on Windows (MSVC ABI), Linux and MacOS.

## Example

Find the library named `foo` in a [Vcpkg](https://github.com/Microsoft/vcpkg) installation and emit cargo metadata to link it:

```rust
// build.rs
fn main() {
    vcpkg::find_package("foo").unwrap();
}
```

See the crate [documentation](https://docs.rs/vcpkg) for more information. See [cargo-vcpkg](https://crates.io/crates/cargo-vcpkg) for a convenient way of creating a vcpkg installation.

## License

See LICENSE-APACHE, and LICENSE-MIT for details.
