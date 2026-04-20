# lateralus-stdlib

The Lateralus standard library. Zero dependencies outside the compiler itself.

## Layout

```
collections/     # List, Map, Set, Deque, Heap, Trie, Rope, Graph, IntervalTree
io/              # File, Buf, Pipe, Stdio
net/             # TCP, UDP, TLS, HTTP, SMTP, DNS
crypto/          # SHA2, SHA3, HMAC, AES, ChaCha20, Ed25519, X25519
encoding/        # Base64, Hex, JSON, TOML, YAML, CBOR
bin/             # Big-/little-endian reads, varint, LEB128
time/            # UnixTime, Duration, Tz (IANA), Clock
fs/              # Path, Dir, Metadata, Watcher
os/              # Env, Process, Signal, Pipe
sync/            # Mutex, RWLock, Channel, Pool, Once
thread/          # spawn, Scope, Join, parker
rand/            # Rng (xoshiro256++), CSPRNG, distributions
test/            # Arbitrary, shrinker (used by compiler #[property] pass)
compress/        # Deflate, Gzip, Zstd-read, LZ4-read
math/            # prime, gcd, matrix, statistics, linalg
ast/             # AST types shared by compiler passes
compiler/        # Pass trait, Module, Diagnostic
```

## Installing

Shipped with the Lateralus compiler — no separate install. Every module
is in scope as `std::<module>` from any Lateralus source file.

```
import std::net::tcp
import std::crypto::{hmac, sha256}
import std::time::{tz, Duration}
```

## This repo

This is the authoritative source tree for the standard library.
Changes here are mirrored into the `lateralus-lang` monorepo under
`stdlib/` on every release.

## Policy

- **Zero runtime dependencies.** Only what ships with the compiler.
- **Pipeline-first.** Every module that processes data exposes functions
  that compose via `|>`.
- **Exhaustive errors.** Every fallible function returns `Result<T, E>`
  where `E` is a closed enum — no open exception hierarchies.
- **No hidden allocation.** Iterators are lazy. Collections are explicit.
- **Deterministic.** Iteration order is specified for every container.

## Status

- **Stable:** `collections`, `io`, `net::tcp`, `net::http`, `crypto`,
  `encoding::json`, `encoding::base64`, `bin`, `time` (UTC).
- **Beta:** `time::tz`, `net::tls`, `net::dns`, `compress`, `sync`.
- **Experimental:** `test::arbitrary`, `compiler::*`, `ast::*`.

## Contributing

See [lateralus-lang/CONTRIBUTING.md](https://github.com/bad-antics/lateralus-lang/blob/main/CONTRIBUTING.md).

License: same as `lateralus-lang`.
