# Verifying A Contract

**EVM**

**Foundry**

{% embed url="https://getfoundry.sh/forge/deploying/#verifying-a-pre-existing-contract" %}
Verify a pre-existing contract
{% endembed %}

**Hardhat**

{% embed url="https://hardhat.org/hardhat-runner/docs/guides/verifying" %}

**Solana**

In Anchor you need to build a verifiable build using Docker to produce a consistent executable.

{% embed url="https://www.anchor-lang.com/docs/references/verifiable-builds" %}

IDL (Interface Definition Language) is Solana's lingo for ABI. An IDL is uploaded to an account on-chain and block explorers are able to pick it up automatically.

```sh
anchor idl init --filepath target/idl/your_program.json $PROGRAM_ID --provider.cluster mainnet
```

To verify that it is stored correctly, run

```
anchor idl fetch $PROGRAM_ID --provider.cluster mainnet
```

Solana programs are upgradeable by default, so you can also upgrade the IDL:

```
anchor idl upgrade --filepath target/idl/your_program.json $PROGRAM_ID --provider.cluster mainnet
```
