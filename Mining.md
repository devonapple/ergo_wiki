# Introduction

Mining is the process of adding new blocks into the Ergo blockchain by performing resource-intensive computations. 

Ergo mining is based on [Autolykos](https://docs.ergoplatform.com/ErgoPow.pdf), a Proof-of-Work algorithm designed to be ASIC and pool resistant. Miners have to perform memory-hard computations~(at least 2 GB memory is needed, but the current most efficient implementation utilizes between 4-8 GB of RAM) that makes Ergo friendly for GPU mining. In addition, Autolykos requires access to **private** keys, thereby preventing mining pool formation. As soon as a correct solution is found, the miner broadcasts the block along with the solution and is able to collect the block reward after a delay of 720 blocks using the secret he used during mining. The rest of the network verifies the solution using the miner's **public** key and this verification can be done very efficiently, requiring less than a kilobyte of memory.

# How to mine Ergo

Ergo mining requires one configured and synchronized Ergo node and at least one GPU to perform the actual PoW computations. You may use multiple GPUs if you wish (to multiply your hashing power) but you only need one Ergo node.

## Configuring a full node

To configure a full node check this [manual](https://github.com/ergoplatform/ergo/wiki/Set-up-a-full-node). To support an external miner (which is what we will be using), you should have the following settings in your config file:
```
ergo.mining.mining = true
ergo.mining.useExternalMiner = true
```

If you already have a private/public key pair, you may specify your public key or address in your config:
```
ergo.mining.miningPubKeyHex = "11aa...FF"
```
If this parameter is not present, the node will use the first public key from the built-in wallet to form blocks for the external miner. 

You're ready to start mining once your node is synchronized with the network.

## Configuring miner

**!!!WARNING!!! Since Autolykos utilizes private keys, you should never use untrusted mining software. Check that the software is open-source and validated by the community**

Install your miner software from the list available:
- [CUDA miner](https://github.com/ergoplatform/cuda-miner) (Nvidia GPU only)

Miner configuration file looks like this:
```
{
    "seed": "Achtung!!! Replace this to any big enough string and keep it in secret or you will get robbed", 
    "node": "http://188.166.89.71:9052",
    "keepPrehash": false
}
```
where:
- **seed** is the mnemonic sentence from your node configuration or a mnemonic sentence that allows calculating the private key for `miningPubKeyHex` specified in the config.
- **node** is the URL of your node API.
- **keepPrehash** is an optimization parameter. If set to `true`, the miner will consume at most 8GB of memory. If set to `false` the miner will consume at most 4GB of memory, but its performance will be for about 25% lower.

Run your miner using the command `./auto.out config.json` (for Linux) and enjoy receiving block rewards!
