# Unwrap To Native Token

**EVM**

```solidity
IWETH(WETH).withdraw(amount);
```

**Solana**

wSOL can be unwrapped to SOL by closing the wSOL token account with `destination` set to the owner of the ATA.

{% embed url="https://www.quicknode.com/guides/solana-development/getting-started/a-complete-guide-to-wrapped-sol#4-unwrap-sol" %}
