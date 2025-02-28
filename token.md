# Token

**EVM**

```solidity
contract Token {
  mapping(address user => uint256 balance) public balances;
}
```

**Solana**

In Solana, the equivalent of an **ERC-20 token** is **SPL token**. For a wallet to receive SPL tokens, a token account for the SPL token has to be created.

```rust
#[derive(Accounts)]
pub struct Swap<'info> {
  pub token: Account<'info, Mint>,
  
  #[account(
    init_if_needed,
    payer = buyer,
    associated_token::mint = mint,
    associated_token::authority = buyer
  )]
  pub buyer_token_account: Account<'info, TokenAccount>,
  
  pub buyer: Signer<'info>
}
```

Here we are using the `associated_token_program` to initialize the account. `mint`is the token's address and `authority`is the address that controls the token account.
