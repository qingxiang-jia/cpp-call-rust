# cpp-call-rust

Demonstrates calling Rust functions from C++. Roughly following: http://bitboom.github.io/calling-rust-from-cpp

## Why Not Just a Gist?

That's my initial plan since I really don't want to make things more complicated than they should be. But I did because a project I am working on requires C++ code to call Rust code and the C++ side is using Meson. I am new to both Meson and C++ so the gist would focus a lot on those. If I had to do so much documentation, may be it would be easier to just include the entire Rust and C++ code.

## Rust Side

1. Each function that you want to expose to C++ will need `#[no_mangle]` attribute.
2. The same function also need `extern "C"`.
3. The `Cargo.toml` needs to specify that you are building a C styled shared library: `crate-type = ["cdylib"]`
4. You also need a header file that includes all signatures of the functions to be exposed to C++. They also need `extern "C"` so when the C++ code calls, it knows to use C calling convention instead of the C++ one.

## C++ Side

1. You need to include the header file for Rust functions wherever you use them.
2. For your `meson.build` file, there's many ways to let the build system know that you are doing. I used `find_library` approach. See code for details.

## Build Order
I keep it simple:
1. Build Rust side first, producing a `.so` file (in my case, Linux).
2. Build C++ side (meson.build has information about the `.so` file and header).
