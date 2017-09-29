# labday2017-ethereum
Datascience lab day 2017, Smart contracts on ethereum

## purpose
To understand some of the capabilities of the Ethereum smart contract

## Goals

* run through a shared vote counting tutorial on the `Rinkeby` test chain
* get hands on experience with Solidity ide's.
* come up with a somewhat more advanced contract idea, and execute it.

## Requirements

* [geth and tools](https://geth.ethereum.org/downloads/)
* [mist](https://github.com/ethereum/mist/releases)
* rinkeby light chain data (Neo-Bart provides on usb key).
* [nodejs](https://nodejs.org/en/download/)
* [solc](https://github.com/ethereum/solidity/releases)
* Mac or Linux laptop or vm. Windows should work, but I'm not able to help.

# Getting Started

Install `geth` 1.7, `solc` 0.4.17  and `mist` 0.9. Open a couple of terminals, and of we go:

* `geth --syncmode light --rinkeby --rpc --rpcapi="db,eth,net,web3,personal,web3"`.  
  Wait til this starts showing single count updates. The rinkeby test chain is
  a few 100 MB, so it might take a while.  You can speed this up by asking Bart for his usb key with the Rinkeby test
  chain.
* _Wait_ for the geth terminal to stabilize.    
  `mist --rpc ~/.ethereum/rinkeby/geth.ipc`

Rinkeby is the 4th ethereum test net, so we use play money.

## create your first account

[Online geth account docs][1]. With your local `geth` in your $PATH and `geth` having synced with the rinkeby chain do

    geth --rinkeby account new
    WARN [09-24|11:37:12] No etherbase set and no accounts found as default 
    Your new account is locked with a password. Please give a password. Do not forget this password.
    Passphrase: 
    Repeat passphrase: 
    Address: {11026e8797350c49105a3622f14dbfe28cf6e5ec}

This action has created an account. The account consists of a private key file in ~/.ethereum/rinkeby/keystore

    $> ls ~/.ethereum/rinkeby/keystore  
    UTC--2017-09-24T09-46-12.855207027Z--11026e8797350c49105a3622f14dbfe28cf6e5ec


This private key is locked with the passphrase you entered, and is your _address_ on the chain.  If you had some ethers,
you could now send them to my address (1102...). If this was on the real chain, you'd very carefully backup this file,
and make sure that no-one has installed a key-logger or so onto your computer, because that could cause you to lose a
lot of Ethers (i.e. money).

Since we're on the [rinkeby][2] test chain, this is all play money, so don't worry about it.

### create account with mist
You can also just start mist and create an account that way :-)


## get some Ethers in your account

[rinkeby.io][2] has a so called faucet, were you can get free Ethers :-) Not bad. Lets get some.
Browse there, click the faucet tap, and fill in your address.

_While writing this, this site was down, but I do have some rinkeby Ethers in an account, so I'll make sure they're available on labday._

The _mining_ menu item in Mist is disabled because we're a _light client_. This means we don't have the full chain on our
local machine, just a [merkle tree][3] that can prove blocks

### Mining
If you start geth without the `--syncmode light` you create a full node. This will take a few GB and a lot more time to download the whole chain, but this allows you to do _mining_. Don't do this on the Lab day!

However, if you feel like it, do this at home, and you can start mining via the Mist user interface. I have no idea how fast you'll be getting some ethers, but I'm trying right now.
_I'm not even sure if this works, because Rinkeby is a Proof Of Authority_ network, instead of the old Ropsten _Proof of Work_ system.

## geth attach
In order to get a javascript console into a running geth instance, do:

    geth attach ipc:///home/bvdeenen/.ethereum/rinkeby/geth.ipc
    
[Javascript Console documentation][10]

# The Voting Tutorial

We're going to follow [this tutorial][7]

# What's next
Up to the genii of DatascienceLab :-)

# Links

* [geth accounts][1]
* [rinkeby.io][2]
* [merkle trees][3]
* [myetherwallet online wallet][4]
* [ENS Ethereum naming service][5]
* [Solidity by example][6]
* [Voting tutorial][7]
* [Rinkeby blockchain explorer][8]
* [Ropsten testnet faucet][9]
* [Geth javascript console][10]
* [July 2017 simple contract example][11]

[1]: https://github.com/ethereum/go-ethereum/wiki/Managing-your-accounts
[2]: http://www.rinkeby.io/
[3]: https://en.wikipedia.org/wiki/Merkle_tree
[4]: https://www.myetherwallet.com
[5]: https://github.com/ethereum/ens/blob/master/docs/userguide.rst
[6]: http://solidity.readthedocs.io/en/develop/solidity-by-example.html
[7]: https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2
[8]: https://rinkeby.etherscan.io/
[9]: http://faucet.ropsten.be:3001/
[10]: https://github.com/ethereum/go-ethereum/wiki/Management-APIs
[11]: https://alanbuxton.wordpress.com/2017/07/19/first-steps-with-ethereum-private-networks-and-smart-contracts-on-ubuntu-16-04/
