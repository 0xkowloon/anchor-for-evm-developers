# Validation

**EVM**

```solidity
contract Dex {
  bool private _paused;
  
  function setPaused(bool paused) external {
    if (msg.sender != owner) {
      revert NotOwner();
    }
    
    _paused = paused;
  }
}
```

**Solana**

1. Using **constraint**

```rust
#[account]
pub struct Config {
  pub authority: Pubkey,
  pub paused: bool,
}

#[derive(Accounts)]
pub struct SetPaused<'info> {
  pub signer: Signer<'info>,
  
  #[account(mut, constraint = config.authority == signer.key() @ ErrorCode::Unauthorized)]
  pub config: Account<'info, Config>
}


pub fn set_paused(Context<SetPaused, bool paused) -> Result<()> {
  ctx.accounts.config.paused = paused;
}
```

2. Using **require!**

```rust
#[account]
pub struct Config {
  pub authority: Pubkey,
  pub paused: bool,
}

#[derive(Accounts)]
pub struct SetPaused<'info> {
  pub signer: Signer<'info>,
  
  #[account(mut, constraint = config.authority == signer.key() @ ErrorCode::Unauthorized)]
  pub config: Account<'info, Config>
}


pub fn set_paused(Context<SetPaused, bool paused) -> Result<()> {
  require!(ctx.accounts.config.authority == ctx.accounts.signer.key(), ErrorCode::Unauthorized);
  ctx.accounts.config.paused = paused;
}
```

3. Using **has\_one**

Notice how I've changed the caller's field name from `signer` to `authority. has_one` is looking for an account called `authority` that matches the account `config`'s `authority`.

```rust
#[account]
pub struct Config {
  pub authority: Pubkey,
  pub paused: bool,
}

#[derive(Accounts)]
pub struct SetPaused<'info> {
  pub authority: Signer<'info>,
  
  #[account(mut, has_one = authority) @ ErrorCode::Unauthorized)]
  pub config: Account<'info, Config>
}


pub fn set_paused(Context<SetPaused, bool paused) -> Result<()> {
  ctx.accounts.config.paused = paused;
}
```

