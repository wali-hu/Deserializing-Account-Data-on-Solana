# Deserializing Account Data on Solana

**Description**
This repo shows how to fetch and deserialize raw account buffers from Solana RPC and deserialize them into meaningful fields. It is intended as a learning reference for developers who want to understand how on-chain data is laid out and how to decode it locally.

## Prerequisites

* Node.js
* npm (or yarn)
* `ts-node` installed
* A working Solana RPC endpoint (Helius or other provider)

## Installation

```bash
# Clone the repo
git clone https://github.com/wali-hu/Deserializing-Account-Data-on-Solana.git
cd Deserializing-Account-Data-on-Solana

# Install dependencies
npm install
```

## Configuration

Open the source file (e.g. the main script inside `src/`) and locate the RPC URL placeholder. If the project uses a Helius RPC URL, replace the placeholder with your Helius API key, for example:

```ts
const rpc = 'https://rpc.helius.xyz/?api-key=YOUR_HELIUS_KEY';
```

Also modify the `mint` or `account` `PublicKey` variable in the script to point at the account you want to deserialize.

## Usage

```bash
npx ts-node src/deserialize.ts

npm run dev
# or
npm run deserialize
```

You should see the raw account buffer printed to the console followed by parsed fields after deserialization.

## How deserialization works (high level)

1. Use `Connection.getAccountInfo(pubkey)` to fetch the raw `AccountInfo` object from RPC.
2. Inspect `accountInfo.data` — it is a `Buffer` containing tightly-packed bytes according to the on-chain program's data layout.
3. For common Solana programs (like the Token Program), the byte layout is well-known and you can decode fields by reading bytes at fixed offsets and converting using integer/UTF8 parsers or Borsh where appropriate.
4. For Anchor programs or custom programs, examine the program's Rust source or IDL to learn the struct layout. Tools like Borsh schemas and buffer readers help convert raw bytes to typed objects.

> Solana often uses Borsh serialization for structured data. Borsh is deterministic and compact; if the on-chain program used Borsh, use the same schema to deserialize.

## License
MIT


