# Calling Other Contract

**EVM**

```solidity
contract A {
  address private _hello = 0x6e110......011e6;
  
  function hello() external {
    IHello(_hello).hello(10);
  }
}

interface IHello {
  function hello(uint256 times) external;
}

contract Hello {
  mapping(address caller => uint256 times) public contacted;
  
  function hello(uint256 times) external {
    contacted[msg.sender] += times;  
  }
}
```

**Solana**

In Solana it is called cross-program invocation (CPI). To make a CPI you need to provide the program address, accounts and arguments.

```rust
#[account]
pub struct Caller {
  pub caller: Pubkey,
  pub times: u64,
}

let cpi_accounts = cpi::accounts::Hello {
    caller: ctx.accounts.caller.to_account_info(),
};

let cpi_context = CpiContext::new(
    ctx.accounts.hello_program.to_account_info(),
    cpi_accounts,
);

let times = 10;
cpi::hello(cpi_context, times)?;
```

A signature is sometimes required (e.g. the destination program pulls funds from source program accounts) and you can use `new_with_signer` to create the context

```rust
let cpi_accounts = cpi::accounts::Hello {
    authority: ctx.accounts.caller.to_account_info(),
};

let authority_seeds = &[
    b"authority".as_ref(),
    &[ctx.bumps.authority],
];
let authority_signer = &[&authority_seeds[..]];

let cpi_context = CpiContext::new_with_signer(
    ctx.accounts.hello_program.to_account_info(),
    cpi_accounts,
    authority_signer,
);

let times = 10;
cpi::hello(cpi_context, times)?;
```

