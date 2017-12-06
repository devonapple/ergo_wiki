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

  # Wallet settings
  wallet {
    # By default, the node will attempt to generate a new seed. To use a specific seed, uncomment the following line and
    # specify your base58-encoded seed.
    seed = "S"
    # Password to protect wallet file
    password = "scorex"
    # Path to wallet folder
    walletDir = ${user.home}"/wallet"
  }

  # Node data directory
  dataDir = ${user.home}"/scorex"
  # Node logs directory
  logDir = ${scorex.dataDir}"/log"

  # Node's REST API settings
  restApi {
    # Network address to bind to
    bindAddress = "127.0.0.1"

    # Port to listen to REST API requests
    port = 6886

    # Hash of API key string
    apiKeyHash = ""

    # Enable/disable CORS support
    corsAllowed = false

    # request processing timeout
    timeout = 5s

    # Project info to show in swagger
    swaggerInfo {
      description = "The Web Interface to the Scorex API",
      version = "",
      title = "Scorex API",
      termsOfService = "License: Creative Commons CC0",
      contact {
        name = "Alex"
        url = "https://scorex-dev.groups.io/g/main"
        email = "alex.chepurnoy@iohk.io"
      }
      license {
        name = "License: Creative Commons CC0"
        url = "https://github.com/ScorexProject/Scorex/blob/master/COPYING"
      }
    }
  }

  # P2P Network settings
  network {
    # Node name to send during handshake
    nodeName = "My node"

    # Network address
    bindAddress = "0.0.0.0"

    # String with IP address and port to send as external address during handshake. Could be set automatically if UPnP
    # is enabled.
    #
    # If `declared-address` is set, which is the common scenario for nodes running in the cloud, the node will just
    # listen to incoming connections on `bindAddress:port` and broadcast its `declaredAddress` to its peers. UPnP
    # is supposed to be disabled in this scenario.
    #
    # If declared address is not set and UPnP is not enabled, the node will not listen to incoming connections at all.
    #
    # If declared address is not set and UPnP is enabled, the node will attempt to connect to an IGD, retrieve its
    # external IP address and configure the gateway to allow traffic through. If the node succeeds, the IGD's external
    # IP address becomes the node's declared address.
    #
    # In some cases, you may both set `decalredAddress` and enable UPnP (e.g. when IGD can't reliably determine its
    # external IP address). In such cases the node will attempt to configure an IGD to pass traffic from external port
    # to `bind-address:port`. Please note, however, that this setup is not recommended.
    # declaredAddress = ""

    # Port number
    port = 9068

    # Node nonce to send during handshake. Should be different if few nodes runs on the same external IP address. Comment this out to set random nonce.
    # nodeNonce = 12345

    # Add delay for sending message
    # addedMaxDelay = 0ms

    networkChunkSize = 10

    # Accept only local connections
    localOnly = false

    # List of IP addresses of well known nodes.
    knownPeers = []

    # Number of network connections
    maxConnections = 20

    # Network connection timeout
    connectionTimeout = 1s

    # Enable UPnP tunnel creation only if you router/gateway supports it. Useful if your node is runnin in home
    # network. Completely useless if you node is in cloud.
    upnpEnabled = no

    # UPnP timeouts
    # upnp-gateway-timeout = 7s
    # upnp-discover-timeout = 3s

    # Network handshake timeout
    handshakeTimeout = 2s

    # Network delivery timeout
    deliveryTimeout = 2s

    maxDeliveryChecks = 1

    # Network version send in handshake
    appVersion = 0.0.1

    # Network agent name
    agentName = "scorex"

    # Maximum income package size
    maxPacketLen = 1048576

    # Accept maximum inv objects
    maxInvObjects = 500

    # Synchronization interval
    syncInterval = 15s

    # Synchronization status update interval
    syncStatusRefresh = 2m
  }

}
```

## Ergo configuration section

Root configuration section `ergo` holds essential application parameters and other configuration subsections. There are also another one root section `scorex`, it holds the parameters inherited from the [Scorex project](https://github.com/ScorexFoundation/Scorex).

Using parameter `directory` it is possible to set a path to the base application directory. Also it is possible to use environment variables to set configuration parameters. For example, by default, the base directory constructed relative to the user's `HOME` environment variable. Please, do not enclose environment variables references in quotes, in this case, they will be handled as strings and won't be resolved. 

***

Note for Windows users. 

Often on Windows, the HOME environment variable is not set. Please, replace `${HOME}` with `${HOMEPATH}` or `${APPDATA}` in your additional configuration file.
Also, you should remember that Windows' environment variables names are case sensitive. 

### Network settings

In `scorex.network` section P2P network related settings could be set. 

Using `declaredAddress` parameter you can set the external IP address and port number of the node. It's necessary to work behind NAT in most cloud hosting, where the machine does not interface directly with the external address. If you do not specify it, then your node connects to the P2P network, but it won't listen to incoming connections so other nodes will not be able to connect. Other nodes are connected to your node using these data. The format of this parameter is "[ip-address]:[port]".

Using parameter `bindAddress` you can set the IP address of local network interface on which Waves Node will accept incoming connections. By default, node binds to "0.0.0.0" that means that it will listen on all available network adapters. 

Use `port` parameter to set the network port number to which other Waves nodes will connect. Check that the port is reachable from outside otherwise, your node will connect to P2P network only using outgoing connections. If this the port is taken by other application, your node won't start. 

Parameter `nodeName` could be used to set the name of your node visible to other participants of the P2P network. The name transmitted during initial handshake. In the default configuration, this parameter is commented out, which leads to random name generation. 

Parameter `nodeNonce` is sent during a handshake. By default, it's not set and nonce will be generated randomly. This value is used to distinguish nodes connected from one IP address. 

The `knownPeers` parameter stores the list of bootstrap nodes to which your node will establish outgoing connections while initializing. 

***

Note about time parameter values.

All time span parameters are set in milliseconds. But duration units can be used to shorten the value. Supported units are:
* s, second, seconds
* m, minute, minutes
* h, hour, hours
* d, day, days

For usage examples see the default configuration file above. 

***

Use `maxConnections` parameter to set the maximum number of simultaneous connections handled by the node.

Parameter `connectionTimeout` could be used to change the network communication timeout. 

Using `handshakeTimeout` parameter it is possible to set time period to wait for reply during handshake. In case of no reply the peer will be blacklisted.

Using parameters starts with `upnp` you can set the UPnP settings. Actually, those settings are useful only if you ran your Waves node on the home network where the node could ask your router to establish a tunnel. By default, this functionality is disabled. Use `upnpEnabled` parameter to enable this functionality.

### Wallet settings

In `wallet` section you can configure wallet built in Waves node.

Use `walletDir` parameter to set the path to the wallet folder. By default, the path to the file is calculated relatively to the base user directory. 

Parameter `password` could be used to set the password string to protect the wallet file.

Using `seed` parameter you could recreate an existing walled on a new node. Provide the BASE58 string of your seed here. If you don't have any existing wallet comment out this parameter and start the node. During the first run, the application will create a new wallet with a random seed for you. In this case, the seed will be displayed in the application log. If you miss it or if you don't want to check the log files.

***
Attention!

The wallet is a critical part of your node. Better to create its file in a safe and protected location. Don't forget to backup your wallet's file. 

It's recommended to remove the seed from the configuration file immediately after the start of the node. If an attacker gains access to this seed string, he has access to all your funds on all your addresses!

***

### Blockchain settings

At `ergo.chain` you can select or custom the blockchain parameters.

Use `blockInterval` parameter to set desired time interval between blocks.

Parameter `epochLength` used to set the length of an epoch in difficulty recalculation. 1 means difficulty recalculation every block

In `useLastEpochs` parameter stored a number of last epochs that will be used for difficulty recalculation.

You can change the PoW algo or related parameters using `poWScheme` section.

### Node settings

In section `ergo.node` it is possible to configure parameters of the node regime.

Use `enable` parameter to enable or disable block generation on the node. By default, it's disable.

Disabled `offlineGeneration` parameter will start mining as soon as it connects to the first peer in the P2P network. Setting this parameter to `true` will enable off-line generation.

Using `miningDelay` parameter you tune your node's mining delay after finding a new block. 

### TODO other parameters

### REST API settings

In section `scorex.rest-api` you can set the node's REST API parameters.

Parameter `bindAddress` could be used to select network interface on which REST API will accept incoming connections. 

Parameter `port` could be used to change the port number on which REST API will await connections.

***

Attention!

For better security, do not change `bindAddress` from "127.0.0.1" if you do not know what you're doing! For external access, you should use instead [Nginx's proxy_pass module](http://nginx.org/ru/docs/http/ngx_http_proxy_module.html) or [SSH port-forwarding](http://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html).

***

Use `api-key-hash` parameter to set the hash of your API key. The API key is used to protect calls of critical API methods. Remember, that in this parameter you should provide the hash of API key, but during REST calls you should provide API key itself. You can use blake2b to produce the hash of your API key.

***

Attention!

API key is transmitted in the HTTP header as unprotected plain text! An attacker could intercept it in network transit and use it to transfer your money to any address! So you have to protect the transmission using HTTPS or use SSH port forwarding.

***

Parameter `cors` could be used to enable or disable CORS support in REST API. CORS allows to safely resolve queries to other domains outside the one running the node. It's necessary for Swagger and Lite client. You can read about it [here](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).
