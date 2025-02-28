# Mutation

**EVM**

```solidity
contract Counter {
  mapping(address user => uint256 count) public counter;
  
  function increment(address to, uint256 amount) external {
    counter[to] += amount;
  }
}
```

**Solana**

**First time**

The flag `init` or `init_if_needed` is required to initialize the `Counter` account.

Notes on some terminologies:

* seeds - It is used to derive the address (Program Derived Address). It can be static or dynamic and it can contain multiple elements
* seeds::program - It is used to derive the address for other programs
* bump - Bump seed is a provided value that ensures the account's address is off the Ed25519 curve. An address that's off the curve does not have a corresponding private key
* space - Each account occupies some space and it tells Solana how much space is needed. There is always an extra 8 bytes for Anchor Discriminator. This [post](https://solana.stackexchange.com/questions/4948/what-is-anchor-8-bytes-discriminator#4949) explains it well.

```rust
#[account]
pub struct Counter {
  pub user: Pubkey,
  pub count: u64,
}

#[derive(Accounts)]
pub struct Increment {
  #[account(init, seeds = [b"user", user.key()], bump, space = 8 + 32 + 8)
  pub counter: Account<'info, Counter>,
  
  pub user: Signer<'info>,
}

pub fn increment(ctx: Context<Increment>, amount: u64) -> Result<()> {
  ctx.accounts.counter = ctx.accounts.counter.checked_add(amount).unwrap();
  Ok(())
}
```

**Not the first time**

The flag `mut` is required to let Solana know that the account is mutable. The program will [fail silently](https://github.com/coral-xyz/anchor/issues/326) if the flag is not present!

```rust
#[account]
pub struct Counter {
  pub user: Pubkey,
  pub count: u64,
}

#[derive(Accounts)]
pub struct Increment {
  #[account(mut, seeds = [b"user", user.key()])
  pub counter: Account<'info, Counter>,
  
  pub user: Signer<'info>,
}

pub fn increment(ctx: Context<Increment>, amount: u64) -> Result<()> {
  ctx.accounts.counter = ctx.accounts.counter.checked_add(amount).unwrap();
  Ok(())
}
```



