# Transfer Native Token

**EVM**

```solidity
payable(recipient){value: amount}("");
```

**Solana**

1. From regular accounts

```rust
let ix = transfer(&from.key(), &to.key(), amount);

invoke(
    &ix,
    &[
        from.to_account_info(),
        to.to_account_info(),
        system_program.to_account_info(),
    ],
)?;
```

2. From PDAs

```rust
let ix = transfer(&from.key(), &to.key(), amount);

invoke_signed(
    &ix,
    &[
        from.to_account_info(),
        to.to_account_info(),
        system_program.to_account_info(),
    ],
    &[signer_seeds],
)?;
```



