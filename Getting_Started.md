## Hyperledger Besu

## History

 - Started out as Ethereum client software developed by Protocols team with ConsenSys.
 - Launched in 2018 under the name Pantheon, built in Java.
 - Designed for both public and private use cases. 
 - Hyperledger Besu joined Hyperledger in August 2019
 - First blockchain project accepted by Hyperledger that could run on a public blockchain. 
 - March 2020, Hyperledger Besu has graduated from incubation to active status. 

## Use Cases

 - Used to connect to the existing public Ethereum network, referred to as mainnet. 
 - Used to create Ethereum Virtual Machines (EVM) compatible private blockchain network. 
 - Can be used to run a node on Ethereum mainnet as
	 - Full node, that helps sync Ethereum mainnet
	 - Archive node, which contains data of the blockchain but does not participate in adding new blocks.

## Applications

 - Unified loyalty rewards program across multiple brands
	 - Each retailer would run their own node, submitting transactions to the private blockchain when customers makes purchases.
	 - The rewarded points would accrue to a customer address, allowing the customers to use points across brands or vendors
 - Permissioned EVM compatible blockchain for organisations looking to host blockchain infrastructure, but allows other nodes to join the network provided they agree to certain conditions, for example certain regulations or standards that may not be present on Ethereum mainnet. 
	 - LAC Chain, a project of IDB Lab - created to encourage the use of DLT i.e., Distributed Ledger Technology in the countries of Latin America and Carribean with 50 organizations participating in the network, running 82 nodes as of May 2021.

## Installing Besu
```
sudo apt update
``` 
```
sudo -i apt install openjdk-11-jre-headless
```
Download the stable version of Besu 
```
https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/21.7.4/besu-21.7.4.zip 
```
```
sudo -i apt install unzip
```
```
unzip besu-21.7.4.zip 
```
```
cd /home/synergy_hyperledger/besu-21.7.4/bin
./besu
```

Besu will begin syncing with mainnet, and the logs are stored in the besu folder.
Besu can be configured to connect to Ethereum testnets (Ropsten, Rinkeby, or Goerli). 

    besu --network=<network> --data-path=<path>/<networkdata-path>

`<path>/<networkdata-path>` - Location where the Blockchain data is stored. 

    besu --network=ropsten --data-path=<path>/<ropstendata-path>
    besu --network=rinkeby --data-path=<path>/<rinkebydata-path>
    besu --network=goerli --data-path=<path>/<goerlidata-path>

Alternately, options and subcommands can be in a configuration file - Specifications of initial parameters for Besu. 
Config files are in TOML format. 

```rust
# Valid TOML config file
data-path="~/besudata" # Path

# Network
bootnodes=["enode://001@123:4567", "enode://002@123:4567", "enode://003@123:4567"]

p2p-host="1.2.3.4"
p2p-port=1234
max-peers=42

rpc-http-host="5.6.7.8"
rpc-http-port=5678

rpc-ws-host="9.10.11.12"
rpc-ws-port=9101

# Chain
genesis-file="~/genesis.json" # Path to the custom genesis file

# Mining
miner-enabled=true
miner-coinbase="0xfe3b557e8fb62b89f4916b721be55ceb828dbd73"
```
To start a network using the config file, 

    besu --config-file=/home/prabusivakumar/besu/config.toml

## Genesis Block

 - The first block in a blockchain is called the genesis block. 
 - Ethereum mainnet genesis block was mine on July 30, 2015. 
 - In order to join or create any network, data for the genesis block should be included.

## Genesis File

 - Genesis file defines the data in the first block of a blockchain, as well as rules for the blockchain itself.
 - If a new node or a validator node attempts to join the network, it will use genesis file as the starting point in recreating the history of the chain in order to synchronize with the existing network. 
 - The genesis file for Ethereum mainnet, along with other supported testnets, is included in the download of Besu. 
 - When creating a private network, genesis file must be provided. 
 - Genesis file is a JSON formatted file.

## Genesis file for IBFT 2.0

Istanbul Byzantine Fault Tolerant Private Network. 

```javascript
{
  "config": {
    "chainId": 2018,
    "muirglacierblock": 0,
    "ibft2": {
      "blockperiodseconds": 2,
      "epochlength": 30000,
      "requesttimeoutseconds": 4
    }
}
```

### chainId
Controls the transaction signature process. 
Provide unique identifier to allow for the hashing of signed transactions to only work on the network associated with the corresponding chain ID. 
Most chain ID match the network ID of the network.
The chain ID, **2018** refers to the chain ID associated with a **development** chain.

### muirglacierblock 
Milestone Block. Muir Glacier refers to the specific network upgrade that occured at block 9,200,000 on Ethereum mainnet. 
In private networks, name of the latest milestone block can be listed, and set to be the genesis block.

### ibft2 
Consensus protocol for the blockchain is IBFT 2.0
```javascript
"ibft2": {
      "blockperiodseconds": 2,
      "epochlength": 30000,
      "requesttimeoutseconds": 4
    }
  ```
  With the specification, following three fields are provided:

### blockperiodseconds
The minimum block time in seconds. In this case, after two seconds, a new block will be proposed by the network.

### epochlength 
The number of blocks at which to reset all votes. The votes refer to validators voting to add or remove validators to the network. 
In this case, after 30,000 blocks are created, this IBFT 2.0 network will discard all pending votes collected from received blocks. 
Existing proposals remain in effect and validators re-add their vote the next time they create a block.

### requesttimeoutseconds
The time by which the new block should be proposed or else a new validator will be assigned by the network. 
If the validator goes down, the request time out ensures that proposal of a new block passes on to another validator. 
**Note** - The request time out seconds should be set to be double the minimum block time. 

## Genesis Block
```json
"nonce": "0x0",
  "timestamp": "0x58ee40ba",
  "extraData": "0xf83ea00000000000000000000000000000000000000000000000000000000000000000d5949811ebc35d7b06b3fa8dc5809a1f9c52751e1deb808400000000c0",
  "gasLimit": "0x1fffffffffffff",
  "difficulty": "0x1",
  "mixHash": "0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365",
  "coinbase": "0x0000000000000000000000000000000000000000",
  "alloc": {
    "9811ebc35d7b06b3fa8dc5809a1f9c52751e1deb": {
      "balance": "0xad78ebc5ac6200000"
    }
  }
}
```
### nonce 
The number used once aka nonce, that is a part of the blockheader for the first block set to 0x0.

### timestamp
Creation date and time of the block. As long as it has any value in the past, it will work. Often, this can be set to 0x0.

### extraData
recursive length prefix (RLP) encoded string which is space efficient containing the validator address of the IBFT 2.0 private network.

### gasLimit
total gas limit for all transactions included in a block. It represents how large the block size can be for a block, and is represented by a hexadecimal string. The gasLimit with the maximum size is referred to as "**free gas network**". 

### difficulty
The difficulty of creating a new block. The lowest difficulty is indicated as 1 i.e., 0x1.

### mixHash
Unique identifier for a block. 

### coinbase
The coinbase account where all block rewards for this network will be paid. 

### alloc
The alloc field creates an address on our network, externally owned account (not associated with the smart contract). The number starting with "98" is the public key of the address. The balance is always expressed in Wei, or 10^-18 Ether.

Once you have created your genesis file, you will save it within the directory where your blockchain network files will be stored. 
Do not store it within Node or data folders. 

    --genesis-file=../geneis.json

To start your network using the genesis file,

    besu --genesis-file=../genesis.json
