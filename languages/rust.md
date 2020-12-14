# Rust

## Resources

- [Learn Rust](https://www.rust-lang.org/learn)
  - [The Rust Programming Language aka "The Book"](https://doc.rust-lang.org/book)
  - [Easy Rust](https://github.com/Dhghomon/easy_rust) tutorial on a single
    GitHub page, can be done mostly in the playground

## Tooling

- [Rust Playground](https://play.rust-lang.org) code in the browser
- *VS Code extensions*
  - [Rust](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust)
  - [crates](https://marketplace.visualstudio.com/items?itemName=serayuzgur.crates)
    (version management of deps in `Cargo.toml`)
  - [Better TOML](https://marketplace.visualstudio.com/items?itemName=bungcip.better-toml)
    syntax highlighting for `*.toml`

## Installation

Quick & dirty (works well, though):

```sh
curl https://sh.rustup.rs -sSf | sh  # modifies PATH in .profile / .bashrc
add_path ~/.caro/bin                 # fish only, with `add_path` func defined
rustc --version ; cargo --version
```

## Cargo

- The `npm` of Rust
- Packages are called *crates*
- Documentation: [The Cargo Book](https://doc.rust-lang.org/cargo)

### [Create a Project](https://doc.rust-lang.org/cargo/guide/creating-a-new-project.html)

```sh
cargo new my_cool_app --bin
```

Creates a hello world package. Even initialized a Git repo, `.gitignore`
included.

Build and run compiled binary:

```sh
cargo build
./target/debug/my_cool_app
```

Run directly:

```sh
cargo run
```

## Tests

```sh
cargo test                 # run all tests

cargo test sum             # run all tests with "sum" in name
cargo test my_module       # works for modules as well, because test names
                           # look like my_module::test::sum_returns_42

cargo test -- --nocapture  # show stdout (captured and hidden by default)
```

