# Binary and cryptography functions

Cloud SQL functions in the Binary and Cryptography categories. Binary conversions that also appear in String or Conversion remain listed here because this is their public Binary category.

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| BASE64 | `BASE64(expression VARBINARY) -> VARCHAR`; Base64-encodes a binary string. | Input is binary. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BASE64/) |
| BIN | `BIN(expression INTEGER) -> VARCHAR`; renders an integer in base 2. | Input is an integer expression. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIN/) |
| BIT_LENGTH | `BIT_LENGTH(expression BINARY, VARCHAR) -> INTEGER`; returns bit length. | Input accepts binary or varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIT_LENGTH/) |
| CRC32 | `CRC32(expression VARBINARY) -> VARCHAR`; computes a CRC value. | Input is a binary string. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CRC32/) |
| ENCODE | `ENCODE(expression STRING, charSet_type STRING) -> VARBINARY`; encodes text with a charset. | Charset is one of US-ASCII, ISO-8859-1, UTF-8, UTF-16BE, UTF-16LE, or UTF-16 (case-insensitive). | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ENCODE/) |
| FROM_HEX | `FROM_HEX(in STRING) -> BINARY`; converts hexadecimal text to binary. | `in` is a hexadecimal string. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FROM_HEX/) |
| HEX | `HEX(expression ANY PRIMITIVE) -> VARCHAR`; produces hexadecimal encoding. | Input must be a primitive expression. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/HEX/) |
| TO_HEX | `TO_HEX(in BINARY) -> STRING`; emits a hexadecimal string. | Input is binary. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_HEX/) |
| UNBASE64 | `UNBASE64(expression VARCHAR) -> VARBINARY`; decodes Base64 text. | Input must be Base64-encoded varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/UNBASE64/) |
| UNHEX | `UNHEX(expression VARCHAR) -> VARBINARY`; turns hexadecimal digits into bytes. | Non-hex input returns `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/UNHEX/) |
| DECRYPT | `DECRYPT(data VARBINARY, key VARBINARY, mode VARCHAR [, iv VARBINARY [, aad VARBINARY]]) -> VARBINARY`; AES-decrypts data. | Key length is 16, 24, or 32 bytes; CBC/GCM require an IV/nonce. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/DECRYPT/) |
| ENCRYPT | `ENCRYPT(data VARBINARY, key VARBINARY, mode VARCHAR [, iv VARBINARY [, aad VARBINARY]]) -> VARBINARY`; AES-encrypts data. | Key length is 16, 24, or 32 bytes; do not use AES-ECB for secure encryption. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ENCRYPT/) |
| MD5 | `MD5(expression VARCHAR) -> VARCHAR`; computes an MD5 hash. | Input is varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MD5/) |
| SHA, SHA1 | `SHA(expression VARCHAR) -> VARCHAR` and `SHA1(expression VARCHAR) -> VARCHAR`; compute SHA-1 hashes. | Input is varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SHA__SHA1/) |
| SHA256 | `SHA256(expression VARCHAR) -> VARCHAR`; computes a 256-bit SHA-2 hash. | Input is varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SHA256/) |
| SHA512 | `SHA512(expression VARCHAR) -> VARCHAR`; computes a 512-bit SHA-2 hash. | Input is varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SHA512/) |
