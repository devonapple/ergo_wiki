## Actual for version 0.1.0

Below you can find a complete Ergo Node configuration file. This is the default configuration shipped with the application. It is possible to overwrite any parameters by providing an additional configuration file. You can pass an additional configuration file by providing the path to it as the first command line parameter then starting Ergo Node application.

```
ergo {
  # Directory to keep data
  directory = ${user.dir}"/ergo/data"

  # Settings for node view holder regime. See papers.yellow.ModifiersProcessing.md
  node {
    # Keep state root hash only and validate transactions via ADProofs
    ADState = false

    # Download block transactions and verify them (requires BlocksToKeep == 0 if disabled)
    verifyTransactions = true

    # Number of last blocks to keep with transactions and ADproofs, for all other blocks only header will be stored.
    # Keep all blocks from genesis if negative
    blocksToKeep = -1

    # Download PoPoW proof on node bootstrap
    PoPoWBootstrap = false

    # Minimal suffix size for PoPoW proof (may be pre-defined constant or settings parameter)
    minimalSuffix = 10

    # Is the node is doing mining
    mining = false

    # If true, a node generates blocks being offline. The only really useful case for it probably is to start a new
    # blockchain
    offlineGeneration = false

    # Delay for miner after succesful block creation
    miningDelay = 1s
  }

  testing {
    # Turn on transaction generator
    transactionGeneration = false

    # If generator is enabled, it generates transactions when mempool size is smaller than keepPoolSize
    keepPoolSize = 1
  }

  #Chain-specific settings. Change only if you are going to launch a new chain!
  chain {

    # Desired time interval between blocks
    blockInterval = 1m

    # length of an epoch in difficulty recalculation. 1 means difficulty recalculation every block
    epochLength = 1

    # Number of last epochs that will  be used for difficulty recalculation
    useLastEpochs = 100

    //Proof-of-Work algorithm and its parameters. Possible options are "fake" and "equihash".
    poWScheme {
      powType = "equihash"
      n = 96 //used by Equihash
      k = 5  //used by Equihash
    }
  }
}
scorex {
  wallet {
    seed = "S"
    password = "scorex"
    walletDir = ${user.home}"/wallet"
  }
  dataDir = ${user.home}"/waves"
  logDir = ${scorex.dataDir}"/log"
  restApi {
    bindAddress = "0.0.0.0"
    port = 9051
    # apiKeyHash = ""
    corsAllowed = false
    timeout = 5s
    swaggerInfo {
      description = "The Web Interface to the Ergo API",
      title = "Ergo API",
      termsOfService = "License: Creative Commons CC0",
      contact {
        name = "kushti"
        url = "https://ergoplatform.org/"
        email = "kushti@protonmail.ch"
      }
      license {
        name = "License: Creative Commons CC0"
        url = "https://raw.githubusercontent.com/ergoplatform/ergo/master/LICENSE"
      }
    }
  }

  network {
    nodeName = "ergo-testnet"
    bindAddress = "127.0.0.1"
    # declaredAddress = ""
    port = 9001
    # nodeNonce = 12345
    # addedMaxDelay = 0ms
    networkChunkSize = 400
    localOnly = false
    knownPeers = ["88.198.13.202:9001", "139.59.165.103:9003", "159.203.94.149:9003"]
    maxConnections = 20
    connectionTimeout = 1s
    upnpEnabled = no
    # upnp-gateway-timeout = 7s
    # upnp-discover-timeout = 3s
    handshakeTimeout = 2s
    deliveryTimeout = 2s
    maxDeliveryChecks = 1
    appVersion = 0.0.1
    agentName = "scorex"
    maxPacketLen = 1048576
    maxInvObjects = 500
  }

}
```

## Ergo configuration section

Root configuration section `ergo` holds essential application parameters and other configuration subsections.

Using parameter `directory` it is possible to set a path to the base application directory. Also it is possible to use environment variables to set configuration parameters. For example, by default, the base directory constructed relative to the user's `HOME` environment variable. Please, do not enclose environment variables references in quotes, in this case, they will be handled as strings and won't be resolved. 

***

Note for Windows users. 

Often on Windows, the HOME environment variable is not set. Please, replace `${HOME}` with `${HOMEPATH}` or `${APPDATA}` in your additional configuration file.
Also, you should remember that Windows' environment variables names are case sensitive. 

