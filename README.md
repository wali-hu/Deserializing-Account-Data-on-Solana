# Deserializing-Account-Data-on-Solana
A Rust script that fetches a raw account buffer (e.g., a specific Token Account) via RPC and deserialize it using borsh to read the balance and owner without using the spl-token crate's helper functions.
