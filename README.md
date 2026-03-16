# Hash Generator

Generate MD5, SHA-1, SHA-256, and SHA-512 cryptographic hashes from text input, entirely in the browser.

**Live Demo:** https://file-converter-free.com/en/developer-tools/hash-generator

## How It Works

MD5 is implemented in pure JavaScript: `str2rstr_utf8` converts the input to a UTF-8 byte string, `rstr2binl` packs bytes into 32-bit little-endian words, `binlMD5` runs the four MD5 rounds (ff/gg/hh/ii) using `safeAdd` with 16-bit overflow safety and `bitRotLeft`, and `rstr2hex` converts the result to lowercase hex. SHA-1, SHA-256, and SHA-512 use `crypto.subtle.digest(algo, TextEncoder().encode(text))` from the Web Crypto API, which returns an `ArrayBuffer` converted to hex via `Array.from(new Uint8Array(buf)).map(b => b.toString(16).padStart(2, '0')).join('')`. Hashes are computed live on every `input` event and rendered in individual rows with per-hash copy buttons.

## Features

- MD5 (pure JS implementation)
- SHA-1, SHA-256, SHA-512 (Web Crypto SubtleCrypto)
- Live computation on every keystroke
- Per-algorithm copy to clipboard button

## Browser APIs Used

- Web Crypto API (`crypto.subtle.digest`)
- Clipboard API (`navigator.clipboard.writeText`)

## Code Structure

| File | Description |
|------|-------------|
| `hash-generator.js` | Pure-JS `md5` (ff/gg/hh/ii rounds, `safeAdd`, `bitRotLeft`), async `sha` via `SubtleCrypto.digest`, `renderRow` DOM builder, live `input` event trigger |

## Usage

| Element ID / Selector | Purpose |
|----------------------|---------|
| `#hashInput` | Text input for hashing |
| `#hashGenerate` | Generate button |
| `#hashClear` | Clear input and results |
| `#hashResults` | Container for hash result rows |
| `.hash-copy-btn` | Per-algorithm copy button |

## License

MIT
