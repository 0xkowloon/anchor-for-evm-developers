# Events

**EVM**

```solidity
event TokenDeployed(address indexed addy);

emit TokenDeployed(addy);
```

**Solana**

```rust
#[event]
pub struct TokenDeployed {
  mint: Pubkey,
}

emit!(TokenDeployed {
  mint: ctx.accounts.mint.key(),
})
```

