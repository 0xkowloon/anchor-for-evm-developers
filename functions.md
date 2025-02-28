# Functions

**EVM**

Functions that can be called are marked as `external` or `public`

```solidity
contract Dex {
  function swap(uint256 amountIn, address token) external payable {
    // Buy token
  }
  
  function swap2(uint256 amountIn, address token) public payable {
    // Buy token
  }
}

contract Token {
  mapping(address user => uint256 balance) public balances;
}
```

**Solana**

1. **The `program` macro specifies the module containing the program's instruction logic, it is equivalent to an EVM `contract`.**
2. An `instruction` is the equivalent of an EVM function.
3. Each instruction comes with a context. A context contains all the accounts an instruction needs to access. In Solana, data is stored in accounts, it is similar to an EVM mapping, but they are not the same because in EVM, data is stored within a contract while Solana programs are stateless. Data is stored separately and their storage addresses are derived.
4. In this example, we have to specify the buyer's token account because a successful swap increments the buyer's token account's balance (more on token accounts in another section). The `buyer_token_account` is the equivalent of the EVM Token's `balances` mapping.

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

#[program]
pub mod dex {
  pub fn swap(Context<Swap>, amount_in: u64, token: Pubkey) {
    // Buy token
  }
}
```

