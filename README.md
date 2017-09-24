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
* Mac or Linux laptop or vm. Windows should work, but I'm not able to help.

# Getting Started

Install `geth` 1.7 and `mist` 0.9. Open a couple of terminals, and of we go:

* `geth --syncmode light --rinkeby --rpc`. Wait til this starts showing single count updates. The rinkeby test chain is
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

This action has created an account. The account consists of a private key file in ~/.ethereum/keystore

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

[1]: https://github.com/ethereum/go-ethereum/wiki/Managing-your-accounts
[2]: http://www.rinkeby.io/
