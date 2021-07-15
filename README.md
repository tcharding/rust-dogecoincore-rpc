# Rust RPC client for Dogecoin Core JSON-RPC

**Work In Progress**

This repository was forked from [rust-bitcoincore-rpc](https://github.com/rust-bitcoin/rust-bitcoincore-rpc) in
an effort to get [doge-bdk](https://github.com/tcharding/doge-bdk) working with `dogecoind`.

Only tested on testnet, use at your own risk.

# ----- Original rust-miniscript README ------


[![Status](https://travis-ci.org/rust-bitcoin/rust-bitcoincore-rpc.png?branch=master)](https://travis-ci.org/rust-bitcoin/rust-bitcoincore-rpc)

# Rust RPC client for Bitcoin Core JSON-RPC 

This is a Rust RPC client library for calling the Bitcoin Core JSON-RPC API. It provides a layer of abstraction over 
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Bitcoin JSON-RPC interface 

This git package compiles into two crates.
1. [bitcoincore-rpc](https://crates.io/crates/bitcoincore-rpc) - contains an implementation of an rpc client that exposes 
the Bitcoin Core JSON-RPC APIs as rust functions.

2. [bitcoincore-rpc-json](https://crates.io/crates/bitcoincore-rpc-json) -  contains rust data structures that represent 
the json responses from the Bitcoin Core JSON-RPC APIs. bitcoincore-rpc depends on this.

# Usage
Given below is an example of how to connect to the Bitcoin Core JSON-RPC for a Bitcoin Core node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `8332` and the node
is set up to accept RPC connections. 

```rust
extern crate bitcoincore_rpc;

use bitcoincore_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:8332".to_string(),
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples. 

# Supported Bitcoin Core Versions
The following versions are officially supported and automatically tested:
* 0.18.0
* 0.18.1
* 0.19.0.1
* 0.19.1
* 0.20.0
* 0.20.1
* 0.21.0

# Minimum Supported Rust Version (MSRV)
This library should always compile with any combination of features on **Rust 1.29**.

Because some dependencies have broken the build in minor/patch releases, to
compile with 1.29.0 you will need to run the following version-pinning command:
```
cargo update --package "cc" --precise "1.0.41"
cargo update --package "log:0.4.x" --precise "0.4.13" # x being the highest patch version
cargo update --package "cfg-if" --precise "0.1.9"
cargo update --package "unicode-normalization" --precise "0.1.9"
cargo update --package "serde_json" --precise "1.0.39"
cargo update --package "serde" --precise "1.0.98"
cargo update --package "serde_derive" --precise "1.0.98"
cargo update --package "byteorder" --precise "1.3.4"
```
