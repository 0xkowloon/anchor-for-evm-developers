# Feature Flags

**EVM**

**Solana**

```rust
#[cfg(feature = "devnet")]
pub const RANDOM_CONSTANT: u64 = 1;
#[cfg(not(feature = "devnet"))]
pub const RANDOM_CONSTANT: u64 = 2;

#[cfg(feature = "devnet")]
msg!("This should only be logged when devnet is enabled!")
```

Then run

`anchor build — --features devnet`
