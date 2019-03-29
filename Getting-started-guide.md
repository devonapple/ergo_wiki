# How to set up and configure full Ergo node

This tutorial explains how to install and configure Ergo node.

## Node security

There are few important aspects of node usage your wallet and money safety depends on:
* Ergo node requires storing of security-critical parameters in the configuration file. You should never make the file public.
* Ergo node provides interface for interacting with built-in wallet through REST API. Sensitive API methods require a security token, that should not be sent by untrusted channels.

## Setting up the environment

To run Ergo node you need the JRE version >= 8 to be installed. One way to install it is to use [Oracle implementation of Java](https://www.oracle.com/technetwork/java/javase/downloads/index.html).

## Setting up an Ergo node


When the environment is ready itʼs time to download latest Ergo node [release](https://github.com/ergoplatform/ergo/releases/) and create a configuration file.
All set of parameters is described in default configuration [file](https://github.com/ergoplatform/ergo/blob/master/src/main/resources/application.conf), in your configuration file you only need to rewrite parameters that you want to change from the default ones. For example, you can check the example configuration [file](https://github.com/ergoplatform/ergo/blob/master/src/main/resources/nodeTestnet/application.conf) for latest testnet.

Letʼs now take a look at few important parameters:

**1)**
One of the most important parameter is wallet seed:
```
# Seed the wallet private keys are derived from
ergo.wallet.seed = "Achtung!!! Replace this to any big enough string and keep it in secret or you will get robbed"
```
To generate new seed it is strongly recommended to use a secure random generator like one that is used in this [script](https://gist.github.com/oskin1/7390048db61dc6c31b5343f51d5ffde1/). Run the script and paste the output hex-string into your config file.
(Since Ergo does not yet support configs encryption it is recommended not to store it on your machine, so youʼd better deleting it when the node is running. Donʼt forget to save your seed in some secure place before deleting config).

**2)**
If you plan to use built-in wallet API then you should configure apiKeyHash parameter
```
scorex.restApi.apiKeyHash = "1111"
```
It is a Blake2b hash from your secret phrase that will be used to authenticate your API requests. You can use this [script](https://gist.github.com/oskin1/704ef3fba8d40bb1e7691919bf1e9cf9/) or any other script to calculate blake2b hash for that purpose (but please ensure that your secret phrase remains secret and is not sent to any untrasted services).

## Running Ergo node

To run a node from `ergo-assembly-<version>.jar` binaries and `ergo.conf` conficuration file execute:
```
$ java -jar ergo-assembly-<version>.jar ergo.conf
```

To make sure node is running open `127.0.0.1:9052/info` in your browser, that will contain a general information about your node. You can use swagger `127.0.0.1:9052/swagger` to perform API requests and check full API [specification](https://github.com/ergoplatform/ergo/blob/master/src/main/resources/api/openapi.yaml) in openapi format. To access protected API routes, provide your secret in the request headers `[api_key, Content-Type]`, or click `Authorize` button in swagger and write down your secret there.

