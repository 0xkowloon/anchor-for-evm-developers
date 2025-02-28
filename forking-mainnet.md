# Forking Mainnet

**EVM**

**Foundry for testing**

```solidity
vm.createSelectFork(MAINNET_RPC_URL);

// or

vm.createSelectFork(MAINNET_RPC_URL, blockNumber);
```

**Running a local node**

```bash
anvil --fork-url https://eth.llamarpc.com
```

**Solana**

In Solana you have to download program binaries and accounts you need

```bash
solana program dump -u m metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s tests/fixtures/mpl_token_metadata.so

solana account XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX --output json > tests/fixtures/your_account.json
```

**Anchor.toml for testing**

```rust
[[test.genesis]]
address = "metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s"
program = "tests/fixtures/mpl_token_metadata.so"

[[test.validator.account]]
address = "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
filename = "tests/fixtures/your_account.json"
```

**Running a local node**

```bash
solana-test-validator \
  --bpf-program metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s tests/fixtures/your_account.json \
  --account XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX tests/fixtures/your_account.json
```



