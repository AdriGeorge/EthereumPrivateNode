# Ethereum node on Raspberry

* **[Pre-requisites](#pre-requisites)**
* **[Setup](#setup)**

## Getting Started

These instructions will allow you to connect to an ethereum private network. 

## Pre-requisites

* You need the original genesis.json file from the private network and the enode from the bootnode

* Install go-ethereum


```sh
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```

Check version
```sh
geth version
```

Other Operating systems: <https://github.com/ethereum/go-ethereum/wiki/Building-Ethereum>

## Setup
###  1]  Enviroment

Clone the repository
```sh
git clone https://github.com/AdriGeorge/EthereumPrivateNode.git
cd EthereumPrivateNode
```
Init the genesis file
```sh
geth --datadir node/ init genesis.json
```
Create a new account
```sh
geth --datadir node/ account new
```
[OPTIONAL]
Save the data (password and address)
```sh
echo 'password' >> node/password.txt
echo 'address' >> accounts.txt
```
Add the following flags to startnode.sh (you can skip this step, but after you have to unlock your account from console with command: personal.unlockAccounts("account", "password"))

--allow-insecure-unlock

-unlock 'YOUR ACCOUNT'

--password node/password.txt

### 2] Add your configuration

Open startnode.sh and change the following parmeters with yours: port, rpcaddr, rpcport

Make your sh file executable
```sh
chmod +x ./startnode.sh
```

###  3]  Start the node and connect

```sh
./startnode.sh
```
If you have this error: "/bin/bash^M: bad interpreter: No such file or directory",
just cancel the empty line (second) in startnode.sh

Open a new terminal

```sh
cd node
node$: geth attach geth.ipc
```


###  4]  Wait until 50%+1 of signers give you the autorization (clique.propose("address", true))

Now you can interact with the blockchain from console.

For the full list of geth command check: 
https://ethereum.stackexchange.com/questions/28703/full-list-of-geth-terminal-commands

For the full command line options check:
https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options
