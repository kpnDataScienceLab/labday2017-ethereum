# Notes Labday Ethereum, Sept 29, 2017



## Basic messing about in console

Steps looking around getting something going working on console

* https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2
* npm install ethereumjs-testrpc web3
* create wallet
* check status of wallet contract at https://rinkeby.etherscan.io/address/0x9d6740019dc6f79e2b9a16e3fbe982ebbf4ee999

* http://www.ethdocs.org/en/latest/contracts-and-transactions/contracts.html
Running through this

* switch to https://alanbuxton.wordpress.com/2017/07/19/first-steps-with-ethereum-private-networks-and-smart-contracts-on-ubuntu-16-04/
* simple.sol

The Alan Buxton page shows how to use the compiler and then do some cut and
paste to get something that can be loaded into the geth console.  With geth
can deploy on the chain.

Very useful is to use https://rinkeby.etherscan.io/ to see what is
happening on the rinkeby chain.



## Mist and Remix

Now trying to get a more usable interface, using the combination of
mist and remix ide.


Bart created a voting contract.  He send me the API, and the contract address.  Here
I assign the ABI (copy and paste into console) to ballot, and then use eth.contract to
get the contract.  On this I can call functions, but in this case since I want to change
the state I send a transaction.

ballot = [{"constant":false,"inputs":[{"name":"to","type":"address"}],"name":"delegate","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"winningProposal","outputs":[{"name":"_winningProposal","type":"uint8"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"voter","type":"address"}],"name":"giveRightToVote","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"proposal","type":"uint8"}],"name":"vote","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"inputs":[{"name":"_numProposals","type":"uint8"}],"payable":false,"stateMutability":"nonpayable","type":"constructor"}]
bartSimple = eth.contract(ballot).at("0xa2b0aeb6f152c91b101e3912d61c1dbcfb62922c")
bartSimple.vote.sendTransaction(2, { from: eth.accounts[0], gas: 5000000, to: "0xa2b0aeb6f152c91b101e3912d61c1dbcfb62922c"})


personal.unlockAccount(eth.accounts[0], "JANJAN23A", 100000)



transabi = [{"constant":false,"inputs":[{"name":"id","type":"uint256"}],"name":"cancelTransaction","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"id","type":"uint2
56"}],"name":"closeTransaction","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"id","type":"uint256"},{"name":"from","type":"address"},{"name":"amount","type":"uint25
6"}],"name":"confirmTransaction","outputs":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":false,"inputs":[{"name":"id","type":"uint256"},{"name":"to","type":"address"}],"name":"createTransaction","outputs
":[],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"transactions","outputs":[{"name":"state","type":"uint8"},{"name":"from","type":"address"},{"name":"to"
,"type":"address"},{"name":"amount","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"add","type":"address"}],"name":"getReputation","outputs":[{"name":"","type":"int256
"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"reputation","outputs":[{"name":"score","type":"int256"},{"name":"pendingTransactions","type":"int256"}],"
payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"id","type":"uint256"}],"name":"refundTransaction","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"anonymo
us":false,"inputs":[{"indexed":false,"name":"id","type":"uint256"}],"name":"Created","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"name":"id","type":"uint256"}],"name":"Confirmed","type":"event"},{"anonymous":false,"i
nputs":[{"indexed":false,"name":"id","type":"uint256"}],"name":"Cancelled","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"name":"id","type":"uint256"}],"name":"Closed","type":"event"}]

trans = eth.contract(transabi).at(contract)
trans.createTransaction(2, myaddr, {from: myaddr, gas:100000, to:contract, value:2000000})
trans.confirmTransaction(2, eth.accounts[0], 1000000, { from: eth.accounts[0], gas: 1000000, to:contract, value:2000000})
trans.closeTransaction(2, { from: eth.accounts[0], gas: 1000000, to:contract})