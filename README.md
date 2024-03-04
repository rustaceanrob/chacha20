## ChaCha20

A Rust implementation of the ChaCha20 stream cipher. Complete with simple, auditable code.

#### Features

- [x] Stack-allocated
- [x] No unsafe code blocks
- [x] Zero dependencies
- [x] Seek an index in the keystream or a block in the keystream.

#### Usage

```rust
use chacha20::ChaCha20;
let key = hex::decode("000102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f").unwrap();
let key: [u8; 32] = key.try_into().unwrap();
let nonce = hex::decode("000000000000004a00000000").unwrap();
let nonce: [u8; 12] = nonce.try_into().unwrap();
let seek = 42; // start the cipher at the 42nd index
let mut chacha = ChaCha20::new(key, nonce, seek);
let mut binding = *b"Ladies and Gentlemen of the class of '99: If I could offer you only one tip for the future, sunscreen would be it.";
let to = binding.as_mut_slice();
chacha.apply_keystream(to);
chacha.seek(seek); // move the keystream index back to 42
```