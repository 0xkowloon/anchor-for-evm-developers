# Access Control

**EVM**

```solidity
contract Contract is AccessControl {
  bytes32 public constant OPERATOR_ROLE = keccak256("OPERATOR_ROLE");
  
  function doSomething() onlyRole(OPERATOR_ROLE) {
  }
}
```

**Solana**

```rust
#[account]
pub struct AccessControl {
    #[max_len(100)]
    pub operators: Vec<Pubkey>,
}

#[error_code]
pub enum ErrorCode {
    #[msg("Unauthorized")]
    Unauthorized,
}

#[derive(Accounts)]
pub struct DoSomething<'info> {
    #[account(mut, constraint = access_control.operators.contains(&operator.key()) @ ErrorCode::Unauthorized)]
    pub operator: Signer<'info>,
    
    pub access_control: Account<'info, AccessControl>,
}

pub fn do_something(ctx: Context<DoSomething>) -> Result<()> {
  Ok(())
}
```

