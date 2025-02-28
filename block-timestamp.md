# Block timestamp

**EVM**

```solidity
block.timestamp
```

**Solana**

```rust
clock::Clock::get()
    .unwrap()
    .unix_timestamp
    .try_into()
    .unwrap();
```

