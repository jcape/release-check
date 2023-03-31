# MobileCoin: A trait for constructing an object from an CSPRNG

[![Project Chat][chat-image]][chat-link]<!--
-->![License][license-image]<!--
-->![Architecture: any][arch-image]<!--
-->[![Crates.io][crate-image]][crate-link]<!--
-->[![Docs Status][docs-image]][docs-link]<!--
-->[![Dependency Status][deps-image]][deps-link]<!--
-->[![CodeCov Status][codecov-image]][codecov-link]<!--
-->[![GitHub Workflow Status][gha-image]][gha-link]<!--
-->[![Contributor Covenant][conduct-image]][conduct-link]

A trait for constructing an object from an CSPRNG.

## Example

```rust
use mc_from_random::{CryptoRng, FromRandom, RngCore};
use rand_chacha::{ChaChaRng, rand_core::SeedableRng};

struct MyStruct {
    pub bytes: [u8; 32],
}

impl FromRandom for MyStruct {
    fn from_random<R: CryptoRng + RngCore>(csprng: &mut R) -> Self {
        MyStruct {
            bytes: <[u8; 32]>::from_random(csprng),
        }
    }
}

const SEED: [u8; 32] = [0b0101_0101; 32];

let mut csprng = ChaChaRng::from_seed(SEED);
let myobj = MyStruct::from_random(&mut csprng);
let expected: [u8; 32] = [
    0xb0, 0x23, 0x58, 0xb3, 0x7e, 0x4f, 0x68, 0x68, 0xfb, 0x48, 0xaf, 0x8a, 0xb2, 0x75, 0x0b, 0x06,
    0x2a, 0xa9, 0x5a, 0x83, 0x1b, 0xc2, 0x19, 0x78, 0xa9, 0x8e, 0x94, 0x42, 0x64, 0xfa, 0x0e, 0x75
];
assert_eq!(expected, myobj.bytes);
```

[chat-image]: https://img.shields.io/discord/844353360348971068?style=flat-square
[chat-link]: https://discord.gg/mobilecoin
[license-image]: https://img.shields.io/crates/l/mc-from-random?style=flat-square
[arch-image]: https://img.shields.io/badge/arch-any-brightgreen?style=flat-square
[crate-image]: https://img.shields.io/crates/v/mc-from-random.svg?style=flat-square
[crate-link]: https://crates.io/crates/mc-from-random
[docs-image]: https://img.shields.io/docsrs/mc-from-random?style=flat-square
[docs-link]: https://docs.rs/crate/mc-from-random
[deps-image]: https://deps.rs/crate/mc-from-random/0.0.0/status.svg?style=flat-square
[deps-link]: https://deps.rs/crate/mc-from-random/0.0.0
[codecov-image]: https://img.shields.io/codecov/c/github/mobilecoinfoundation/from-random/main?style=flat-square
[codecov-link]: https://codecov.io/gh/mobilecoinfoundation/from-random
[gha-image]: https://img.shields.io/github/actions/workflow/status/mobilecoinfoundation/from-random/ci.yaml?branch=main&style=flat-square
[gha-link]: https://github.com/mobilecoinfoundation/from-random/actions/workflows/ci.yaml?query=branch%3Amain
[conduct-link]: CODE_OF_CONDUCT.md
[conduct-image]: https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg?style=flat-square
