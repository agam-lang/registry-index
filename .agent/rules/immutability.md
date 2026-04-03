# Registry Immutability Rules

- Published package versions are immutable. Never allow overwrites.
- Every release must include cryptographic checksums and provenance data.
- Yanked packages remain in the index with a yank marker, they are not deleted.
