# Function Selector

**EVM**

```bash
cast keccak 'safeTransferFrom(address,address,uint256)' | cut -c 1-10
```

**Solana**

```typescript
const crypto = require("crypto");
const hash = crypto.createHash("sha256").update("global:your_function_name").digest();
const discriminator = hash.slice(0, 8);
Array.from(discriminator) // [114, 204, 207, 109, 109, 135, 17, 164]
```

