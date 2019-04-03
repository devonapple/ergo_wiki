# Introduction

Mining is the process of adding new blocks into the Ergo blockchain, by performing resource-intensive computations. 

Ergo mining is based on [Autolykos](https://docs.ergoplatform.com/ErgoPow.pdf) Proof-of-Wok algorithm, that is designed to be ASIC and pool resistant. Miners should perform memory-hard computations~(at least 2 Gb of memory, but current most efficient implementation utilizes 4-8 Gb of RAM) that makes Ergo friendly for GPU mining. In addition, Autolykos require access to **private** keys, preventing mining pool formation. As soon as a correct solution is found, miner broadcasts a block with the correct solution and will be able to collect the block reward after 720 blocks delay using secret he used during mining. The rest of the network verifies the solution using miners **public** key and this verification may be done very efficient and requires less than a kilobyte of memory.

# How to mine Ergo

Ergo mining requires configured and synchronized Ergo node, as well as at least one (but potentially as many as you wish) GPU to perform actual PoW computations.

## Configuring a full node

To configure a full node check this [manual](https://github.com/ergoplatform/ergo/wiki/Set-up-a-full-node). To support external miner, you should set the following settings in your config file:
```
ergo.mining.mining = true
ergo.mining.useExternalMiner = true
```

If you already have a private/public key pair, you may specify your public key or address in your config:
```
ergo.mining.miningPubKeyHex = "11aa...FF"
```
otherwise, the node will use the first public from build-in wallet to form blocks for an external miner, in such a case don't forget to replace you seed phrase in the config:
```
ergo.wallet.seed = "Achtung!!! Replace this to any big enough string and keep it in secret or you will get robbed"
```
When your node will be synchronized with the network, you're ready to start mining.

## Configuring miner
**!!!Attention!!! As far as Autolykos utilizes private keys never use untrusted mining software. Check that software is open-source and is validated by the community**


