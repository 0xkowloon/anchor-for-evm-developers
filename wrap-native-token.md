# Wrap Native Token

**EVM**

```solidity
IWETH(WETH).deposit{value: msg.value}();
```

```solidity
payable(WETH).call{value: msg.value}("");
```

**Solana**

1. Send native SOL to your token account
2. Call `sync_native`

```rust
#[derive(Accounts)]
pub struct SyncNative<'info> {
    #[account(mut)]
    pub my_token_account: Account<'info, TokenAccount>,
    pub token_program: Program<'info, Token>,
}

pub fn sync_native(ctx: Context<SyncNative>) -> Result<()> {
    sync_native(CpiContext::new(
        ctx.accounts.token_program.to_account_info(),
        SyncNative {
            account: ctx.accounts.my_token_account.to_account_info(),
        },
    ))?;
}
```

