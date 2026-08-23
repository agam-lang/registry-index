# 📦 Agam Central Package Registry Index

> Part of the [agam-lang](https://github.com/agam-lang) organization.  
> The official decentralized Git-based metadata registry index for the **Agam** package ecosystem (`agam_pkg`), enabling rapid dependency resolution, cryptographically verified publication, and semantic versioning.

---

## 🏛️ Architecture & Index Structure

The registry index follows a sharded prefix directory structure optimized for high-speed shallow Git clones and cache locality:

```text
registry-index/
├── 1/
│   └── a                   # Single-letter package names
├── 2/
│   └── ai                  # Two-letter package names
├── 3/
│   └── n/
│       └── nlp             # Three-letter package names (sharded by first char)
├── to/
│   └── rc/
│       └── torch           # 4+ letter package names (2-char / 2-char shard)
└── config.json             # Registry download API and upload endpoint configuration
```

Each package file contains newline-delimited JSON (`ndjson`) entries for every released version:

```json
{
  "name": "torch",
  "vers": "0.1.0",
  "deps": [{"name": "tensor_core", "req": "^0.2.0"}],
  "cksum": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
  "yanked": false
}
```

---

## ⚡ Dependency Resolution & Publication

- **PubGrub SAT Solver**: `agam_pkg` resolves version constraints in linear time with clear conflict diagnostics.
- **SHA-256 Cryptographic Checksums**: Every package archive is hashed and verified before compilation.
- **Publication via CLI**:
  ```bash
  # Publish a verified package to the registry
  agamc publish
  
  # Search packages in the index
  agamc registry search tensor
  ```

---

## 📜 License

Dual-licensed under [MIT](LICENSE-MIT) and [Apache 2.0](LICENSE-APACHE).
