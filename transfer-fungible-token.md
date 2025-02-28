# Transfer Fungible Token

**EVM**

```solidity
IERC20(token).transfer(receiver, amount);
IERC20(token).safeTransfer(receiver, amount);
```

```solidity
// owner
IERC20(token).approve(spender, amount);

// spender
IERC20(token).transferFrom(owner, receiver, amount);
IERC20(token).safeTransferFrom(owner, receiver, amount);
```

**Solana**

1. From regular accounts

```rust
let transfer_accounts = TransferChecked {
    from: ctx.accounts.from_token_account.to_account_info(),
    mint: ctx.accounts.mint.to_account_info(),
    to: ctx.accounts.to_token_account.to_account_info(),
    authority: ctx.accounts.from.to_account_info(),
};

let cpi_ctx = CpiContext::new(
    ctx.accounts.token_program.to_account_info(),
    transfer_accounts,
);

transfer_checked(cpi_ctx, amount, ctx.accounts.mint.decimals)?;
```

2. From PDAs

```rust
let seeds = &[
    b"from".as_bytes(),
    &[ctx.bumps.from],
];
let signer = &[&seeds[..]];

let transfer_accounts = TransferChecked {
    from: ctx.accounts.from_token_account.to_account_info(),
    mint: ctx.accounts.mint.to_account_info(),
    to: ctx.accounts.to_token_account.to_account_info(),
    authority: ctx.accounts.from.to_account_info(),
};

let cpi_ctx = CpiContext::new_with_signer(
    ctx.accounts.token_program.to_account_info(),
    transfer_accounts,
    vault_authority_signer,
);

transfer_checked(cpi_ctx, amount, ctx.accounts.mint.decimals)?;
```
