# Feature Dependencies

**Solana**

**Cargo.toml**

```
[features]
default = ["feature-you-want-to-enable"]
feature-you-want-to-enable = ["dependency-1/feature-name", "dependency-2/feature-name"]

[dependencies]
dependency-1 = { version = "x.x.x" }
dependency-2 = { version = "x.x.x" }
```

