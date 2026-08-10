# Binary and cryptography functions

Scope: Dremio Enterprise current [26.x]. These are public SQL-reference entries; encoding and key-management expectations come from the linked pages.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [BASE64](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BASE64/) | `BASE64(expression varbinary) → varchar` | Base64 encoding | Binary input. |
| [UNBASE64](https://docs.dremio.com/current/reference/sql/sql-functions/functions/UNBASE64/) | `UNBASE64(expression varchar) → varbinary` | Base64 decoding | Varchar input. |
| [BIN](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BIN/) | `BIN(expression integer) → varchar` | Binary string representation | Integer input. |
| [BIT_LENGTH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BIT_LENGTH/) | `BIT_LENGTH(expression binary\|varchar) → integer` | Bit count | Binary/varchar input. |
| [CRC32](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CRC32/) | `CRC32(expression varbinary) → varchar` | CRC32 checksum | Not cryptographic. |
| [ENCODE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ENCODE/) | `ENCODE(expression string, charSet_type string) → varbinary` | Encoded value | Charset type required. |
| [FROM_HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/FROM_HEX/) | `FROM_HEX(expression varchar) → varbinary` | Hex decoding | Varchar input. |
| [HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/HEX/) | `HEX(expression varbinary) → varchar` | Hex encoding | Binary input. |
| [TO_HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_HEX/) | `TO_HEX(binary) → string` | Hex encoding | Binary input. |
| [UNHEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/UNHEX/) | `UNHEX(expression varchar) → varbinary` | Hex decoding | Varchar input. |
| [AES_ENCRYPT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/AES_ENCRYPT/) | `AES_ENCRYPT(plaintext varchar, key varchar) → varchar` | AES-encrypted value | Plaintext/key are varchar. |
| [AES_DECRYPT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/AES_DECRYPT/) | `AES_DECRYPT(ciphertext varchar, key varchar) → varchar` | AES-decrypted value | Ciphertext/key are varchar. |
| [ENCRYPT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ENCRYPT/) | `ENCRYPT(data varbinary, key varbinary, mode varchar [, iv varbinary [, aad varbinary]]) → varbinary` | Encrypted binary value | Optional `iv` precedes optional `aad`. |
| [DECRYPT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/DECRYPT/) | `DECRYPT(data varbinary, key varbinary, mode varchar [, iv varbinary [, aad varbinary]]) → varbinary` | Decrypted binary value | Optional `iv` precedes optional `aad`. |
| [MD5](https://docs.dremio.com/current/reference/sql/sql-functions/functions/MD5/) | `MD5(expression varchar) → varchar` | MD5 digest | One-way digest. |
| [SHA, SHA1](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SHA__SHA1/) | `SHA\|SHA1(expression varchar) → varchar` | SHA-1 digest | Aliases share this overload. |
| [SHA256](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SHA256/) | `SHA256(expression varchar) → varchar` | SHA-256 digest | One-way digest. |
| [SHA512](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SHA512/) | `SHA512(expression varchar) → varchar` | SHA-512 digest | One-way digest. |
