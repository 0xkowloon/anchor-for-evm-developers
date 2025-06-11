# Reclaiming Rent From A Token Account

**EVM**

Rent does not exist in EVM

**Solana**

Solana requires a wallet to deposit a small amount of SOL when creating an SPL token account for the account to be rent-exempt. When you no longer hold any tokens, you can reclaim the SOL by calling

```
spl-token close $TOKEN_MINT_ADDRESS
```
