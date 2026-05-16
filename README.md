# @crypto/bitcoin-hashes

Bitcoin hashing primitives for Zeta — SHA256, SHA256d, Hash160, and SHA512.

## Why This Exists

Bitcoin SV (BSV) relies on specific hash primitives throughout the protocol:

- **SHA256** — the workhorse of Bitcoin
- **SHA256d (double-SHA256)** — SHA256 applied twice, used for proof-of-work and transaction IDs
- **Hash160** — RIPEMD160 after SHA256, used for address generation
- **SHA512** — for extended hashing needs

This crate provides clean, auditable implementations for use in nour and other Zeta-based BSV tooling.

## Usage

```zeta
use @crypto/bitcoin-hashes::{Sha256, Sha256d, Hash160, Sha512, Hash};

// SHA256
let hash = Sha256::hash("hello");
let bytes = hash.to_byte_array();

// Double-SHA256 — Bitcoin's PoW
let dhash = Sha256d::hash(tx_bytes);

// Hash160 — Bitcoin addresses
let addr = Hash160::hash(pubkey);
```

## API

### Hash trait

```zeta
pub trait Hash {
    fn hash(data: &[u8]) -> Self;
    fn from_slice(bytes: &[u8]) -> Result<Self>;
    fn to_byte_array(self) -> [u8];
}
```

### Types

| Type | Output Size | Description |
|------|-------------|-------------|
| `Sha256` | 32 bytes | SHA-256 |
| `Sha256d` | 32 bytes | Double-SHA256 |
| `Hash160` | 20 bytes | RIPEMD160(SHA256(x)) |
| `Sha512` | 64 bytes | SHA-512 |

## License

MIT — per the Zeta Foundation and the original Rust Bitcoin project.

For nour. For Dark Factory. For BSV.
