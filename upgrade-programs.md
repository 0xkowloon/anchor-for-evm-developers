# Upgrade Programs

**EVM**

[Example from Cyfrin](https://www.cyfrin.io/glossary/upgradeable-proxy-solidity-code-example)

**Solana**

If the new program's size is greater than the current program's size, the program account's size has to be extended before the upgrade

```
CURRENT_PROGRAM_SIZE=`solana program show $PROGRAM_ADDRESS --output json | jq .dataLen`
NEW_PROGRAM_SIZE=`ls -la target/deploy/program.so | awk '{print $5}'`

DIFFERENCE=$((NEW_PROGRAM_SIZE - CURRENT_PROGRAM_SIZE))
solana program extend $PROGRAM_ADDRESS $DIFFERENCE
anchor upgrade --program-id $PROGRAM_ADDRESS 
```

**Upgrade a program via Squads using buffer accounts**

[**https://docs.squads.so/main/navigating-your-squad/developers-assets/programs#upgrade-a-program**](https://docs.squads.so/main/navigating-your-squad/developers-assets/programs#upgrade-a-program)
