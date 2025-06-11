# Events

**EVM**

```solidity
event TokenDeployed(address indexed addy);

emit TokenDeployed(addy);
```

**Solana**

**Regular Emit (Can be dropped from log truncation)**

```rust
#[event]
pub struct TokenDeployed {
  mint: Pubkey,
}

emit!(TokenDeployed {
  mint: ctx.accounts.mint.key(),
})
```

**CPI Emit (Event logged as a self CPI instruction, does not get dropped)**

You first need to turn on the `event-cpi` feature in `Cargo.toml` ,

```rust
[dependencies]
anchor-lang = { version = "0.31.1", features = ["event-cpi"] }
```

then

```rust
#[event_cpi]
pub struct TokenDeployed {
  mint: Pubkey,
}

emit_cpi!(TokenDeployed {
  mint: ctx.accounts.mint.key(),
})
```
