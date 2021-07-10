# Instructions for Znetwork Private BlockChain Network

**Installed Geth**
This is needed to perform every function mentioned below. Visit the link below for a detailed guide on installing Geth. Before you install Geth, create a folder entitled "blockchain-tools." jThis will be the folder that we'll be working out of.

[Guide to install Geth](https://geth.ethereum.org/docs/install-and-build/installing-geth)



## GitBash ##

**When you open GitBash you must run as admin**

Using GitBash(since we are all on Windows machines here) navigate to the BlockChain-Tools folder that we created during the installation of Geth.


## Nodes 

To get started, I created the custom nodes for the Nxcenet network. I did this by using the following functions:

./geth --datadir znode1 account new (password = 222 address = 0xD2F588B209f878Becd0C22e8B36e56d1cF94dba0)
./geth --datadir znode2 account new (password = 333 address = 0x8Adc4F92C0C587AA1C23DB3CaBEda657c17AfC54)

<img src="Screenshots/znode-creation.jpg" alt="Creating Znodes"> 


This created the two nodes that will be used for our custom network.

(Keep note of the node address and node passcode as we will need these for node initialization later.)

## Genesis Block Creation 

Using 'puppeth" I named the network and created  a new genesis block. Commands are below.

1. ./puppeth (initializes Puppeth)
2. named network 'znetwork' (can't have spaces, hyphens or capital letters)
3. entered option '2' to configure new genesis
4. entered option 2 to use a "Clique" or "proof of authority" consensus engine. This means that only one party has the authority to approve/deny transactions.
5. entered addresses from two nodes so that they can be pre-funded.
6. chose no for wei option to keep the block clean.
7. created chain id of "504" to use later in MyCrypto App
8. finally I selected "manage existing genesis" and "export genesis configurations" this creates the json files that are necessary for network initialization.

<img src="Screenshots/znet-creation-1.jpg" alt="Creating Znet1">
<img src="Screenshots/znet-creation-2.jpg" alt="Creating Znet2">


## Initializing the Nodes 

Using the genesis json file, I initialized the nodes with the following code:

./geth --datadir znode1 init znetwork.json
./geth --datadir znode2 init znetwork.json

<img src="Screenshots/znode-initialization.jpg" alt="Initializing Nodes">


## Time to Mine 

After initializing the nodes must be configured for mining. You will need two separate terminals to execute this. I used the node addresses we saved earlier. Also after entering the code you will need to enter the passcode that was created for each node and then hit enter; this unlocks the address of the node so that mining can take place. The code for this is below:

./geth --datadir znode1 --unlock "SEALER_ONE_ADDRESS" --mine --miner.threads=1 --rpc --allow-insecure-unlock  
./geth --datadir znode2 --unlock "SEALER_TWO_ADDRESS" --mine --miner.threads=1 --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

Keep these nodes/terminals running so that we can implement the network into MyCrypto App.

<img src="Screenshots/znode1-running.jpg" alt="Initializing Nodes">
<img src="Screenshots/znode2-running.jpg" alt="Initializing Nodes">



## MyCrypto Integration

While the nodes are still running I opened MyCrypto. I am including instructions that will assist in configuring the custom network on the app.

1. Click 'Change Network' at the bottom left:
2. Click 'Add Custom Node" then add the custom network information
3. Scroll down to choose "Custom" in the "Network" column to reveal more options like 'Chain ID:"
4. Type `ETH` in the Currency box.    
5. In the Chain ID box, type the chain id you generated during genesis creation. (See genesis block creation step 7)
6. In the URL box type: `http://127.0.0.1:8545`.  This points to the default RPC port on your local machine.
7. Finally, click `Save & Use Custom Node`. 

### Setting up Network
<img src="Screenshots/mycrypto.jpg" alt="MyCrypto Setup">

### Network is live in MyCrypto
<img src="Screenshots/Znetwork-MyCrypto.jpg" alt="Live Network">





## Test Transaction(s) In MyCrypto 

After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

1. Select the `View & Send` option from the left menu pane, then click `Keystore file`.

2. On the next screen, click `Select Wallet File`, then navigate to the keystore directory inside your Node1 directory, select the file located there, provide your password when prompted and  then click `Unlock`. This will open your account wallet inside MyCrypto.  

3. In the `To Address` box, type the account address from Node2, then fill in an arbitrary amount of ETH:
  
4. Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.  

5. Click the `Check TX Status` when the green message pops up, confirm the logout:
   
6. You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.

7. You can click the `Check TX Status` button to update the status.

### Wallet Unlock
<img src="Screenshots/Unlock-wallet.jpg" alt="Wallet Unlock 1">
<img src="Screenshots/Unlock-wallet2.jpg" alt="Wallet Unlock 2">

### Sending Eth on Znet
<img src="Screenshots/sending-eth.jpg" alt="Sending Eth">
<img src="Screenshots/ether-decreased.jpg" alt="Sending Eth">
<img src="Screenshots/TX-pending.jpg" alt="Pending Eth">
<img src="Screenshots/Success-TX.jpg" alt="Sent Eth">















