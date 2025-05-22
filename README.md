# Vaulta EVM NODE

## Overview

The Vaulta EVM Node consumes Antelope (Vaulta) blocks from a Leap node via state history (SHiP) endpoint and builds the virtual EVM blockchain in a deterministic way.
The Vaulta EVM RPC will talk with the Vaulta EVM node, and provide read-only Ethereum compatible RPC services for clients (such as MetaMask).

Clients can also push Ethereum compatible transactions (aka EVM transactions) to the Vaulta blockchain, via proxy and Transaction Wrapper (TX-Wrapper), which encapsulates EVM transactions into Antelope transactions. All EVM transactions will be validated and executed by the Vaulta EVM Contract deployed on the Vaulta blockchain.

```
         |                                                 
         |                     WRITE              +-----------------+
         |             +------------------------->|    EVM MINER    |
         |             |                          +-------v---------+
         |             |                          |    Leap node    | ---> connect to the other nodes in the blockchain network
 client  |             |                          +-------+---------+
 request |       +-----+-----+                            |
---------+------>|   Proxy   |                            |
         |       +-----------+                            v       
         |             |                          +-----------------+
         |        READ |     +--------------+     |                 |
         |             +---->|    EVM RPC   |---->|   EVM Node      +
         |                   +--------------+     |                 |
         |                                        +-----------------+
```
         
## Compilation

### checkout the source code:
```
git clone https://github.com/VaultaFoundation/evm-node.git
cd eos-evm-node
git submodule update --init --recursive
```

### compile eos-evm-node, eos-evm-rpc

Prerequisites:
- Ubuntu 22 or later or other compatible Linux
- gcc 11 or later
- cmake
- conan

Conan install
```shell
pip3 install --user conan==1.58.0 chardet
```

Easy Steps:
```
mkdir build
cd build
cmake ..
make -j8
```
You'll get the list of binaries with other tools:
```
bin/eos-evm-node
bin/eos-evm-rpc
```

Alternatively, to build with specific compiler:
```
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ ..
make -j8
```

## Deployments

For local testnet deployment and testings, please refer to 
https://github.com/VaultaFoundation/evm-contract/blob/main/docs/local_testnet_deployment_plan.md

For public testnet deployment, please refer to 
https://github.com/VaultaFoundation/evm-contract/blob/main/docs/public_testnet_deployment_plan.md

## CI
This repo contains the following GitHub Actions workflows for CI:
- Vaulta EVM Node CI - build the Vaulta EVM node
    - [Pipeline](https://github.com/VaultaFoundation/evm-node/actions/workflows/node.yml)
    - [Documentation](./.github/workflows/node.md)

See the pipeline documentation for more information.

