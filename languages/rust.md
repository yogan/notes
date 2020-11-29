# Rust

## Resources

- [Learn Rust](https://www.rust-lang.org/learn)
  - [The Rust Programming Language aka "The Book"](https://doc.rust-lang.org/book)
  - [Easy Rust](https://github.com/Dhghomon/easy_rust) tutorial on a single
    GitHub page, can be done mostly in the playground

## Tooling

- [Rust Playground](https://play.rust-lang.org) code in the browser

## Installation

Quick & dirty (works well, though):

```sh
curl https://sh.rustup.rs -sSf | sh  # modifies PATH in .profile / .bashrc
add_path ~/.caro/bin                 # fish only, with `add_path` func defined
rustc --version ; cargo --version
```