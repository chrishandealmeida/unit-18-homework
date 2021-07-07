# Unit 18 - Proof of Authority Development Chain

## Objective
To set up testnet blockchain for ZBank through the following four deliverables:
- Set up custom testnet blockchain
- Send a test transaction
- Create a repository
- Write instructions on how to use the chain for the rest of my team

---

## Preliminary Setup

1) Download Go Ethereum Tools - Navigate to https://geth.ethereum.org/downloads/ and download the most recent stable version of 'Geth & Tools' for your operating system:
![](Screenshots/1-download-geth.png)

---

2) Unzip geth folder:
![](Screenshots/2-unzip-geth.png)

---

3) Download MyCrypto - Navigate to https://app.mycrypto.com/download-desktop-app and download for your operating system.
![](Screenshots/3b-mycrypto.png)

---

## Setup custom out-of-the-box blockchain

1) Open Terminal and navigate into the unzipped geth & tools folder:
![](Screenshots/3-navigate-to-geth.png)

---

2) Create First Node - We will need at least 2 nodes to create a blockchain.  To create node 1, execute command: 
    <pre>./geth --datadir node1 account new</pre>
![](Screenshots/4-command-node1.png)

---

3) Node 1 Password - Nodes require password to access them in order to transact. You will be prompted to enter a password.  Select any password you'd like and make note of it.
![](Screenshots/5-node1-password.png)

---

4) Node 1 Public Address - After setting your password, node 1 will have been created and its public address of the key will be displayed.  Copy this.
![](Screenshots/6-node1-address.png)
    Paste the public address in a text file for future reference.
![](Screenshots/7-node1-copy-address.png)

---

5) Create Second Node - To create the second node, execute command:
<pre> ./geth --datadir node2 account new</pre>
![](Screenshots/8-command-node2.png)

---

6) Node 2 Password - You will be prompted again to create a password, this time for node 2.  Enter and reenter it in.
![](Screenshots/9-node2-password.png)

---

7) Node 2 Public Address - Node 2's public address will be displayed.  Copy this.
![](Screenshots/10-node2-address.png)
    Paste Node 2's public address in the text file you have created for future reference.
![](Screenshots/11-node2-copy-address.png)

---

8) Ethereum Private Network Manager - In order to create your blockchain, you must launch puppeth, which is your network manager.  Execute command:
<pre>./puppeth</pre>
![](Screenshots/12-puppeth.png)

---

9) Name Your Network - Give the network a name.  In this case, I've named it 'fintech':
![](Screenshots/13-network-name.png)

---

10) Configure New Genesis - Enter in option 2:
![](Screenshots/14-configure-new-genesis.png)

---

11) Create New Genesis from Scratch - Enter in option 1:
![](Screenshots/15-create-genesis-scratch.png)

---

12) Select Consensus Engine - We are using 'Clique - proof-of-authority'. Enter in option 2:
![](Screenshots/16-clique-poa.png)

---

13) Block Time - The block time is the time required to create the next block in a chain.  We can specify it for the genesis block.  It cannot be changed after. I chose to use the default time of 15 seconds by just hitting enter:
![](Screenshots/17-block-seconds.png)

---

14) Allow Accounts to Seal - Paste in the public addresses of nodes 1 and 2 that we recorded in our text file:
![](Screenshots/19-address-seal-node1and2.png)

---

15) Prefunding - Paste the public addresses of nodes 1 and 2 to be prefunded.
![](Screenshots/20-prefunded-node1and2.png)

    Say no to wei:
![](Screenshots/21-no-wei-jose.png)

---

16) Chain ID - A chain ID is used to prevent replay attacks between the main ETH and other chains.  It is an additional way of telling chains apart. At this stage, you will now be prompted to enter in a chain ID.  You may choose anything you'd like.  I have used '888':
![](Screenshots/22-chain-id.png)

---

17) Manage Existing Genesis - You must now enter in option 2:
![](Screenshots/23-existing-genesis.png)

---

18) Export Genesis Configuration - Enter in option 2:
![](Screenshots/24-export-genesis.png)

---

19) Choose Folder for Genesis Specs - Select the default (current) folder by hitting enter:
![](Screenshots/25-specs-folder.png)

---

20) Puppeth Configuration - Here we can see the json files that have been saved. 'fintech.json' and 'fintech-harmony.json':
![](Screenshots/26-config-files.png)

---

21) Delete Fintech-Harmony.json - We only need the 'fintech.json' file, so we can go into Finder and delete 'fintech-harmony.json':
![](Screenshots/27-delete-harmony.png)

---

22) Kill Process - We are now getting ready to initialize our nodes.  But first we must kill the current process using ctrl + c:
![](Screenshots/28-ctrl-c.png)

---

23) Initialize Node 1 - In order to initialize node 1, execute command:
<pre>./geth init fintech.json --datadir node1</pre>:
![](Screenshots/29-initialize-node1.png)

---

24) Initialize Node 2 - Now initialize node 2 by executing command:
<pre>./geth init fintech.json --datadir node2</pre>
![](Screenshots/30-initialize-node2.png)

---

25) Launch Node 1 - Now that the two nodes have been initialized, we are ready to launch node 1. There are several flags we will include in the code:
- The '--unlock' flag allows us to send transactions from node 1, otherwise by default it is locked.  
- The '--mine' flag tells the node to mine new blocks. 
- The '--rpc' flag enables us to talk to our second node, which will allow us to later use MyCrypto to transact on our chain.
- The '--syncmode=full' flag makes your machine initialize a local copy of the Ethereum Virtual Machine in its original clean state, downloads every block since the beginning of the blockchain, and executes every transaction in every block which updates the EVM to its present-day state.
- The '--snapshot=false' flag are to turn off snapshots.  Snapshots are an acceleration data structure on top of the Ethereum state that allows reading accounts and contract storage to be done faster. Disabling it prevents instability that could be caused by this feature. 
- The 'allow-insecure-unlock' flag fixes the error that you receive when you try to access the node with geth via HTTP protocol

To launch node 1, execute command:
<pre>./geth --datadir node1 --unlock "Node 1 public address" --mine --rpc --syncmode "full" --snapshot=false --allow-insecure-unlock</pre>
![](Screenshots/31-launch-node1.png)

---

26) Copy Enode Address of Node 1 - After launching node 1, scroll up in the executed code to find the enode address.  Copy the entire thing:
![](Screenshots/32-copy-enode1.png)
Paste the enode address in your text file:
![](Screenshots/33-paste-enode1.png)

---

27) Launch Node 2 - First, open a new Terminal window, but don't close the first one:
![](Screenshots/34-new-terminal.png)
To launch node 2, execute command:
<pre>./geth --datadir node2 --port 30304 --bootnodes "enode://enter enode address"</pre>
![](Screenshots/35-launch-node2.png)

Our blockchain is now live!

---


## Send a Transaction

1) Create Custom Node - Open MyCrypto and click on 'Add Custom Node' on bottom right corner of window:
![](Screenshots/36-custom-node.png)

---

2) Custom Node Settings - Enter in a name for both Node Name and Network Name.  I have used 'fintech'. 

Enter 'ETH' for the Currency. 

Select 'Custom' for Network. 

Enter in the Chain ID you used earlier.  I used '888'.

Enter in 'http://127.0.0.1:8545' for URL.

Click 'Save & Use Custom Node'
![](Screenshots/37-custom-node-settings.png)

---

3) Access Wallet - Click 'Keystore File' to access our wallet:
![](Screenshots/38-keystore.png)

---

4) Unlock Keystore - Click 'Select Wallet File':
![](Screenshots/39-wallet-file.png)

---

5) Select Node 1 Keystore File - In the file browser, navigate to the node 1 folder within the geth folder you downloaded.  Within the node 1 folder, navigate into the keystore folder and select the keystore file in there:
![](Screenshots/40-select-keystore.png)

---

6) Enter in Password - Enter in the password you initially set for node 1.  Click 'Unlock':
![](Screenshots/41-wallet-login.png)

---

7) Send ETH - After unlocking your wallet, you will see inputs to send ETH.  Enter in node 2's public address into 'To Address' field.  Enter in the amount.  I have used '888'.  Select 'ETH' as the currency.  Click 'Send Transaction':
![](Screenshots/42-sending-eth.png)

---

8) Confirm Transaction - Verify the transaction details, and if correct, click 'Send':
![](Screenshots/43-confirm-transaction.png)

---

9) Check Transaction Status - After sending your transaction, a green banner will appear at the bottom of the window informing you of the transaction you have sent.  It contains a button called 'Check TX Status'.  Click that to view your recently made transaction:
![](Screenshots/44-transaction-broadcast.png)
It will warn you that you are about to logout, click 'logout':
![](Screenshots/45-logout-warning.png)

---

10) Transaction Status - On this page you will see the transaction status of the transaction you have just completed.  As you can see here, it is still pending.  Once the transaction has been verified and added to the blockchain, the status will show it as completed:
![](Screenshots/46-transaction-pending.png)

# Successs! Transaction complete!