# neat-stuff

A curated list of tools and libraries that I personally find useful or interesting. This list is not meant to be comprehensive - when you need to reach for a tool or library that solves X problem, look at traditional awesome lists (and other resources, because they're often not complete or up to date) for domain-specific suggestions. This list is instead a filtered list of tools that apply in many situations that you may not be aware of or naturally think to reach for, and will probably skew toward CLI editors, debugging tools, and Rust crates/macros that {ab,}use the type system.

This isn't really meant as anything other than a reminder for me to reference occasionally, or when starting new projects, updating older ones, etc.

- [Awesome Stuff](#awesome-stuff)
  - [Stuff](#stuff)
- [That's pretty neat](#thats-pretty-neat)
  - [Debugging](#debugging)
  - [Files and Code](#files-and-code)
  - [Editors](#editors)
  - [Rust](#rust)
    - [Build and supporting tools](#build-and-supporting-tools)
    - [Compile-time or constant guarantees and helpers](#compile-time-or-constant-guarantees-and-helpers)
    - [Derive macros and type generators](#derive-macros-and-type-generators)
      - [Serde utilities](#serde-utilities)
    - [Macro helpers](#macro-helpers)
    - [Debugging and diagnostics](#debugging-and-diagnostics)
    - [Miscellaneous](#miscellaneous)
- [Might be neat?](#might-be-neat)
  - [Rust](#rust-1)
    - [Unstable Features](#unstable-features)
- [Would be neat](#would-be-neat)


## Awesome Stuff

Actual "awesome" lists that are useful to check up on occasionally or for more domain-specific suggestions.

- [awesome-shell](https://github.com/alebcay/awesome-shell)
  - see also: [awesome-zsh](https://github.com/unixorn/awesome-zsh-plugins), [awesome-bash](https://github.com/awesome-lists/awesome-bash), [awesome-fish](https://github.com/jorgebucaran/awesome-fish), [Awesome Linux Software](https://github.com/luong-komorebi/Awesome-Linux-Software)
- [awesome-rust](https://github.com/rust-unofficial/awesome-rust)
  - [awesome-embedded-rust](https://github.com/rust-embedded/awesome-embedded-rust)

### Stuff

Lists to look through that are not necessarily curated or up to date.

- [cargo subcommands](https://github.com/rust-lang/cargo/wiki/Third-party-cargo-subcommands)


## That's pretty neat

### Debugging

Why can't rustc just catch all the bugs for me?

- [rr](https://rr-project.org/) — gdb + backwards stepping
  - [unreliable on Ryzen though](https://github.com/mozilla/rr/issues/2034) :(
- [radare2](https://rada.re/r/) — an interactive CLI disassembler and hex editor
  - Note the steep learning curve
- [hexyl](https://github.com/sharkdp/hexyl) — pretty colourful hexdump
  - alternatively: [hex](https://github.com/sitkevij/hex)
- [hyperfine](https://github.com/sharkdp/hyperfine) — better `time`
- [performance co-pilot](https://pcp.io/index.html) — system monitoring and analytics
- [FlameGraph](https://github.com/brendangregg/FlameGraph) — profile and visualize stack traces
- [grcov](https://github.com/mozilla/grcov) — test/code coverage collection and aggregation
  - [codecov.io](https://codecov.io/) — code coverage reporting service like [coveralls.io](coveralls.io).

### Files and Code

- [ripgrep](https://github.com/BurntSushi/ripgrep) — better recursive grep
- [fd](https://github.com/sharkdp/fd) — faster `find`
- [tokei](https://github.com/XAMPPRocky/tokei) — SLoC counting
- [Conventional Changelog](https://github.com/conventional-changelog/conventional-changelog) — Generate changelogs from version history.
  - [clog](https://github.com/clog-tool/clog-cli) — no longer maintained?
  - [conventional-changelog-cli](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-cli)

### Editors

- [kakoune](http://kakoune.org/) — experimental modal editor, maybe better than vim
  - [kakoune/kak-lsp](https://github.com/ul/kak-lsp/) for language server code completion
- [neovim](https://neovim.io/) — still trying to find a reason to switch from vim
  - better plugin framework: likely a reason to switch whenever I get around to writing vim plugins
  - [oni](https://github.com/onivim/oni2) — pretty GUI backed by neovim
    - unfortunately semi-commercial..?
    - and who needs a GUI anyway
- [vim](https://www.vim.org/) — needs no introduction?
  - [vim/lsp](https://github.com/prabirshrestha/vim-lsp) or [vim/LanguageClient](https://github.com/autozimu/LanguageClient-neovim) or [vim/lsc?](https://github.com/natebosch/vim-lsc) or [vim/ALE](https://github.com/w0rp/ale) for language server protocol code completion
    - with [deoplete](https://github.com/Shougo/deoplete.nvim) or [asyncomplete](https://github.com/prabirshrestha/asyncomplete.vim)
  - [coc](https://github.com/neoclide/coc.nvim) — heaver but combines LSP client, autocompletion, and plugins all in one

### Rust

#### Build and supporting tools

- [clippy](https://github.com/rust-lang/rust-clippy) — remind me to use it more
- [rustfmt](https://github.com/rust-lang/rustfmt) — remind me to use it
- [rust-analyzer](https://github.com/rust-analyzer/rust-analyzer) — Rust Language Server 2.0 (experimental)
- [cargo-outdated](https://github.com/kbknapp/cargo-outdated) — check for dependency updates
- [cargo-expand](https://github.com/dtolnay/cargo-expand) — show macro expansions
- [cargo-llvm-lines](https://github.com/dtolnay/cargo-llvm-lines) — for a rough idea of generic code size overhead
- [cargo-bloat](https://github.com/RazrFalcon/cargo-bloat) — rough idea of binary size bloat
- [cargo-deps](https://github.com/m-cat/cargo-deps) — dependency graphs!
- [cargo-with](https://github.com/cbourjau/cargo-with) — run cargo generated binaries with a debugger
- [cargo-readme](https://github.com/livioribeiro/cargo-readme) — README generated from crate docs
- [cargo-release](https://github.com/sunng87/cargo-release) — automated crates.io publishing
  - alternatively [semantic-rs](https://github.com/semantic-rs/semantic-rs) — unmaintained?
- [cargo-make](https://sagiegurari.github.io/cargo-make/), [cargo-script](https://github.com/DanielKeep/cargo-script), [tinyrick](https://github.com/mcandre/tinyrick), [just](https://github.com/casey/just) — not-makefile build task tools (questionable but)
  - `.cargo/config` [`[alias]`](https://doc.rust-lang.org/cargo/reference/config.html#configuration-keys) section covers this as well
- [afl.rs](https://github.com/rust-fuzz/afl.rs), [proptest](https://github.com/altsysrq/proptest), [quickcheck](https://github.com/BurntSushi/quickcheck) — fuzzing and property testing

#### Compile-time or constant guarantees and helpers

- [no-panic](https://github.com/dtolnay/no-panic) — assert at link-time that a function cannot panic
- [select-rustc](https://github.com/dtolnay/select-rustc) — `#[cfg(..)]` for rustc versions
- [static-assertions](https://github.com/nvzqz/static-assertions-rs) — nice for asserting type impls.
- [linkme](https://github.com/dtolnay/linkme) — compile-time distributed slice/list initialization
  - [unfortunately no windows support yet](https://github.com/dtolnay/linkme/issues/2)
- [inventory](https://github.com/dtolnay/inventory) — compile-time plugins distributed throughout crates and source files

#### Derive macros and type generators

- [snafu](https://github.com/shepmaster/snafu) — still immature, but an improvement over [failure](https://github.com/rust-lang-nursery/failure), [error-chain](https://github.com/rust-lang-nursery/error-chain), and other approaches to creating error types and enums.
- [clap](https://github.com/clap-rs/clap) and [StructOpt](https://github.com/TeXitoi/structopt) — CLI option parsing
- [auto_enums](https://github.com/taiki-e/auto_enums) — unify disjoint return types with an anonymous enum
- [enumflags2](https://github.com/NieDzejkob/enumflags2) — alternative to [bitflags](https://github.com/bitflags/bitflags) that uses strongly-typed enums instead
- [ref-cast](https://github.com/dtolnay/ref-cast) — safe reference conversion for newtypes
- [derive_more](https://github.com/JelteF/derive_more) — collection of newtype and other helper derive macros
- [enum-kinds](https://bitbucket.org/Soft/enum-kinds/src/master/enum-kinds/) — generate a C-like enum for the variants of an enum type
- [from-primitive](https://github.com/mauricekayser/rs-from-primitive) or [enum-tryfrom-derive](https://github.com/kwohlfahrt/enum-tryfrom) — derive TryFrom for enum discriminators

##### Serde utilities

- [serde_with](https://github.com/jonasbb/serde_with) — serde field utility library
- [serde-repr](https://github.com/dtolnay/serde-repr) — enum {de,}serialize from discriminator
- [typetag](https://github.com/dtolnay/typetag) — serde for trait objects
- [unstructured](https://github.com/proctorlabs/unstructured-rs) — alternative to [serde-value](https://github.com/arcnmx/serde-value) and `serde_json::Value`
  - Emphasis on manipulation and element access rather than as an interim data container. Maybe worth it over `Deserialize` structs for quick hacks and scripts?

#### Macro helpers

- [paste](https://github.com/dtolnay/paste) — stable `concat_idents!`

#### Debugging and diagnostics

- [color-backtrace](https://github.com/athre0z/color-backtrace) — pretty panics and useful backtrace source-code snippets
- [log](https://github.com/rust-lang-nursery/log) — debug logging
  - env-logger is boring, [remember that there are nicer options](https://github.com/rust-lang-nursery/log#in-executables)
  - [structured logging](https://github.com/rust-lang-nursery/log/issues/328) is being worked on, supplants slog

#### Miscellaneous

- [combine](https://github.com/Marwes/combine) vs [nom](https://github.com/Geal/nom) seems to be an age-old struggle without a clear answer
- [itertools](https://github.com/bluss/rust-itertools) — fancier `Iterator` trait adaptors
- [rayon](https://github.com/rayon-rs/rayon) — parallel data processing
- [crossbeam](https://github.com/crossbeam-rs/crossbeam) — parallel data structures and primitives
  - a good alternative to `std::sync` and other primitives?
- [threadbound](https://github.com/dtolnay/threadbound) — runtime `Send`/`Sync` checking
  - wrapper that ensures contents can only be accessed on origin thread
- [downcast](https://github.com/marcianx/downcast-rs) — recover concrete type from a trait object
- [objekt](https://github.com/dtolnay/objekt) — object-safe clone for trait objects


## Might be neat?

Unstable or incomplete projects to keep an eye on that may be neat in the
future.

- [deorise](https://github.com/Shougo/deorise.nvim) — neovim hex editor plugin
  - A successor to [vinarise](https://github.com/Shougo/vinarise.vim)
  - Currently just an empty repo
- [pijul](https://pijul.org/) — better than git probably eventually
- [artifact](https://github.com/vitiral/artifact) — would I find explicit project design documents useful?
- [dhall](https://github.com/dhall-lang/dhall-lang) — a better yaml
  - maybe something to avoid until it gets more implementations though?

### Rust

- [tarpaulin](https://github.com/xd009642/tarpaulin) — potential grcov alternative?
- [clap-derive](https://github.com/clap-rs/clap_derive) — will replace `StructOpt` eventually?
- [cargo-panic](https://github.com/arcnmx/cargo-panic) — effortless `color-backtrace`
- [enum_traits](https://github.com/Lolirofle/enum_traits) — comprehensive set of traits and derives for enums
  - unfortunately unmaintained, are there any good alternatives?
- [num_enum](https://github.com/illicitonion/num_enum) — might be a nice enum derive crate?
- [enumn](https://github.com/dtolnay/enumn) — enum derive from primitive, but why isn't this `TryFrom`?

#### Unstable Features

Nightly rust has lots of goodies that aren't quite ready for stable use yet:

- [async/await](https://github.com/rust-lang/rust/issues/50547) — whee futures
- [generic associated types](https://github.com/rust-lang/rust/issues/44265) — type constructors and a step toward higher-kinded types
- [existential types](https://github.com/rust-lang/rust/issues/34511) — improved `impl Trait`
- [specialization](https://github.com/rust-lang/rust/issues/31844) — has been in limbo for years so um
- [const generics](https://github.com/rust-lang/rust/issues/44580) — partial/initial implementation


## Would be neat

A wishlist of ideas that probably aren't close to existing yet, or I haven't looked hard enough.

- Are there no decently maintained CLI/curses hex editors?
  - [hexcurse](https://github.com/arm0th/hexcurse) seems inactive
  - vim options don't seem that great
  - Properly get used to radare2!
- Figure out a good notmuch mail CLI client, notmuch-vim is pretty dead
- A Rust testing framework might be nice; there [seems to be an aversion](https://github.com/rust-lang/rust/issues/46488#issuecomment-358783310) to expanding the built-in test functionality
