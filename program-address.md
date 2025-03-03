# Program Address

**EVM**

1. **Contract address is determined by the deployer's address and nonce (CREATE)**
2. **Contract address is determined by the contract's bytecode's hash, deployer's address and a random salt (CREATE2)**

```solidity
function determineAddress(bytes memory bytecode, uint256 salt)
    public
    view
    returns (address)
{
    bytes32 hash = keccak256(
        abi.encodePacked(
            bytes1(0xff), address(deployer), salt, keccak256(bytecode)
        )
    );

    return address(uint160(uint256(hash)));
}
```

Solana

Program address is determined by a generated private key. It has nothing to do with the deployer address nor the bytecode. The private key for the program is located at \`target/deploy/$PROGRAM\_NAME-keypair.json\`.
