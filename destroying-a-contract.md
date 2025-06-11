# Destroying A Contract

**EVM**

Deployed contracts cannot be destroyed unless it contains a function that calls `selfdestruct`. However, since the Cancun hard fork, a contract can only be destroyed if `selfdestruct` is called in the same transaction that deploys the contract.

**Solana**

```
solana program close $PROGRAM_ID
```

Use this with caution as you can accidentally lock users out of their funds!

{% embed url="https://medium.com/%40OptiFi/optifi-program-incident-report-08-29-22-d8fe6d229bad" %}
