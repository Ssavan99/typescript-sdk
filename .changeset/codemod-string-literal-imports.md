---
'@modelcontextprotocol/codemod': patch
---

Project-type inference no longer counts SDK paths that appear only in ordinary string literals. The v1→v2 codemod's source scanner matched any quoted `@modelcontextprotocol/sdk/client|server` subpath anywhere in a file, so a server path stored as data (example text, a log message, a config value) misclassified a client-only project as `both` — rewriting shared type imports to `@modelcontextprotocol/server` and adding a server dependency the project never uses. The scanner now only counts genuine module specifiers: static imports and re-exports (`from '...'`), side-effect imports, dynamic `import('...')`, and `require('...')`.
