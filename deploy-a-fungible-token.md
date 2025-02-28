# Deploy A Fungible Token

**EVM**

```solidity
new ERC20("name", "symbol");
```

**Solana**

```rust
let seeds = &[
    b"your_seed".as_bytes(),
    &[ctx.bumps.mint],
];
let signer = [&seeds[..]];

let token_data: DataV2 = DataV2 {
    name: "name".to_string(),
    symbol: "symbol".to_string(),
    uri: "https://anchor-for-evm-developers.com".to_string(),
    seller_fee_basis_points: 0,
    creators: None,
    collection: None,
    uses: None,
};

let metadata_ctx = CpiContext::new_with_signer(
    ctx.accounts.token_metadata_program.to_account_info(),
    CreateMetadataAccountsV3 {
        payer: ctx.accounts.payer.to_account_info(),
        update_authority: ctx.accounts.mint.to_account_info(),
        mint: ctx.accounts.mint.to_account_info(),
        metadata: ctx.accounts.metadata.to_account_info(),
        mint_authority: ctx.accounts.mint.to_account_info(),
        system_program: ctx.accounts.system_program.to_account_info(),
        rent: ctx.accounts.rent.to_account_info(),
    },
    &signer,
);

create_metadata_accounts_v3(metadata_ctx, token_data, false, true, None)?;
```

