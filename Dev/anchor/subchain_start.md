

# Seele subchain (STEM) start guideline
###(only verifier has the right to vote)

### Download

Download the newest[executables and configuration templates](https://github.com/seeleteam/go-seele-sub/releases/latest). The extracted directory has the following structure:

```
mac/linux/win32_v#.#.#
├── node1.json //shard1 config template
├── node2.json //shard2 config template
├── node3.json //shard3 config template
├── node4.json //shard4 config template
└── build 
    ├── client //client executable: for using node services
    ├── discovery
    ├── light
    ├── node //node executable: for runnig a node
    ├── tool
    └── vm
```

Use the following commands in the `build` directory.

### Accounts

Generate: generate keypairs using shard numbers.

```bash
$ ./client key --shard 1
public key:  0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
private key: 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
```

Validate: check privatekey or pulickey validity and key shard number.

```bash
$ ./client getshardnum --account 0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
shard number: 1
$ ./client getshardnum --privatekey 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
shard number: 1
```

Save: Create keyfile using privatekey, filename, password.

```bash
$ ./client savekey --privatekey 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a --file shard1account
Password:
Repeat password:
store key successfully, the key file path is shard1account
```

Restore: restore privateKey with keyfile and password.

```bash
$ ./client deckeyfile --file shard1account
Please input your key file password:
public key:  0x43ff8ee89e56de149fd29bedbf8f3f4094cfe451
private key: 0x85c7d55a434037336a094575506229d82f771d14e9ba6e8c8ffc6e5c1f21de8a
```

### Configure node.json
(there are two roles in STEM: 1) operator: can process a block and vote for verification. 2) normal user: can only send tx and challenge)

1. Change coinbase account:
  - To run in shard 1, generate a shard 1 keypaire, then place the publickey in node1.json template.
  - To run in shard 2, generate a shard 2 keypaire, then place the publickey in node2.json template.
  - Similarly for 3 and 4.

2. Change node id:
  - Generate a keypair whose shard matters not, and fill the template with the privatekey.

3. Change PrivateKey:
   - operator: change privateKey using the one from keypair in step 1
   - normal user: generate a keypair whose shard matters not, and fill the template with the privatekey.

4. Configure genesis informations:
   - rootaccounts: [mintAccount, meltAccount, challengeAccount].
   - supply: total initiated supply of the subchain will join.
   - validators: operators. 

Example with configuring shard1 template.
```
{
  "basic":{
    ...
    "coinbase": "0xcee66ad4a1909f6b5170dec230c1a69bfc2b21d1", ← publickey
    "privateKey": "0x3ab5c40093aa68031c9b45ce7d0e1cb9f916db18561f1c740b5675575e6e81c9", ← privatekey
    ...
  },
  "p2p": {
    "privateKey": "0xf65e40c6809643b25ce4df33153da2f3338876f181f83d2281c6ac4a987b1479", ← node id
    ...
  },
  ...
   "genesis": {
    ...
    "rootaccounts": ["0xdbf307e58046933e0062d6d4397aaf0c67acffa1","0xdbf307e58046933e0062d6d4397aaf0c67acffa1","0xdbf307e58046933e0062d6d4397aaf0c67acffa1"],
    "supply": 1000000, 
    "validators":["0x5cb277c269f789aefcfbf28902aa1f517a3c15e1","0x7460dde5d3da978dd719aa5c6e35b7b8564682d1"]
  }
}
```


### Run node 

Operator:
Run voting node: using node1.json as configuration file.
```bash
./node substart -s your_configuration_file_location/node1.json -v start
```
Normal User:
Run node without voting: 
```bash
./node substart -s your_configuration_file_location/node1.json -v stop
```



# Practical-Byzantine-Fault-Tolerance-In-Details
Practical-Byzantine-Fault-Tolerance-In-Details

<h1>Basic Concepts:</h1>

* Verifier: A participant to verify a block .<br/>
* Proposer: A verifier that is chosen to propose block in a consensus round.<br/>
* Proposal: A new block creation proposal which is undergoing consensus processing.<br/>
* Sequence: Sequence number of a proposal. A sequence number should be greater than all previous sequence numbers. Currently each proposed block height is its associated sequence number.<br/>
* Round: consensus cycle. A round starts with a proposer creating a block proposal and ends with a block commitment or round change.<br/>
*	Round state: Consensus messages of a specific sequence and round, including pre-prepare message, prepare message, and commit message.<br/>
*	Consensus proof: The commitment signatures of a block that can prove the block has gone through the consensus process.
*	Snapshot: The verifier voting state from last epoch.<br/>


<h1>Core (consensus)</h1>

<h2>Fault Tolerance</h2>
Seele BFT inherits from the original PBFT by using 3-phase consensus, PRE-PREPARE, PREPARE, and COMMIT. The system can tolerate at most of F faulty nodes in a N verifier nodes network, where N = 3F + 1. We only need at least 2F + 1 honest commits because (2F + 1)/ (3F + 1) > 2F / 3F = 2/3. <br/>

<h2>Process</h2>
Before each round, the verifiers will pick one of them as the proposer, by default, in a round robin fashion. <br/>

* The proposer will then propose a new block proposal and broadcast it along with the PRE-PREPARE message.<br/>
* Upon receiving the PRE-PREPARE message from the proposer, verifiers enter the state of PRE-PREPARED and then broadcast PREPARE message. This step is to make sure all verifiers are working on the same sequence and the same round.<br/>
* While receiving 2F + 1 of PREPARE messages, the verifier enters the state of PREPARED and then broadcasts COMMIT message. This step is to inform its peers that it accepts the proposed block and is going to insert the block to the chain.<br/>
* Lastly, verifiers wait for 2F + 1 of COMMIT messages to enter COMMITTED state and then insert the block to the chain.<br/>

<h2>Forks</h2>

Blocks in Seele BFT protocol are final, which means that there are no forks and any valid block must be somewhere in the main chain. To prevent a faulty node from generating a totally different chain from the main chain, each verifier appends 2F + 1 received COMMIT signatures to extraData field in the header before inserting it into the chain. Thus blocks are self-verifiable and light client can be supported as well.

However, the dynamic extraData would cause an issue on block hash calculation. Since the same block from different verifiers can have different set of COMMIT signatures, the same block can have different block hashes as well. To solve this, we calculate the block hash by excluding the COMMIT signatures part. Therefore, we can still keep the block/block hash consistency as well as put the consensus proof in the block header.<br/>

<h2>Proposer Selection</h2>

Since each proposal is similar and each verifier will have equal oppotunity to propose. We use two policies for Proposer Selection: Round Robin and Sticky property.
   
   ![RoundRobin](https://user-images.githubusercontent.com/29580346/65648417-0bb60c00-dfb7-11e9-8bf8-5d9f75243db0.png)
   * Round Robin: Proposer will be changed for a new block or Round Change request.
   * Sticky: Only when a round change the proposer will change. (Proposer will keep same for one round).

<h2>States Transition (One Round)</h2>

Because of orders of blocks and multiply consensus processing steps of one block, Seele BFT implements a state to maintain right order of steps to prevent messing up which may bring up security issues.

Here are what a state and how it works in details:</br>

*	NEW ROUND: Proposer (selection rules will be discussed later) to send new block proposal. Verifiers wait for PRE-PREPARE message.</br>
*	PRE-PREPARED: A verfier has received PRE-PREPARE message and broadcasts PREPARE message. Then it waits for 2F + 1 of PREPARE or COMMIT messages.</br>
*	PREPARED: A verifier has received 2F + 1 of PREPARE messages and broadcasts COMMIT messages. Then it waits for 2F + 1 of COMMIT messages.</br>
*	COMMITTED: A verifier has received 2F + 1 of COMMIT messages and is able to insert the proposed block into the blockchain.</br>
*	SEAL COMMITTED: A new block is successfully inserted into the blockchain and the verifier is ready for the next round.</br>
*	ROUND CHANGE: A verifier is waiting for 2F + 1 of ROUND CHANGE messages on the same proposed round number.</br>

![pbft](https://user-images.githubusercontent.com/29580346/65644928-7f055100-dfaa-11e9-9546-856b8e6df8fe.png)

1. NEW ROUND --> PRE-PREPARED (PROPOSAL/PRE-PREPARE phase)
    * Proposer collects transitions from txpool.
    * Proposer generates a block proposal and broadcasts it to verifiers. It then enters the PRE-PREPARED state.<br/>
      Each verifier enters PRE-PREPARED upon receiving the PRE-PREPARE message with the following conditions:
         *	Block proposal is from the valid proposer.
         *	Block header is valid.
         *	Block proposal's sequence and round match the verifier's state.
    
2. PRE-PREPARED --> PREPARED: (PREPARE phase)
   * Verifier broadcasts PREPARE message to other verifiers.
   * Verifier received 2F + 1 of valid PREPARE messages to enter PREPARED state.<br/>
     Valid messages conform to following condidtions:
      * Messages are from valid Verifiers.
      * Sequence and Round matched.
      * BlockHash matched.

3. PREPARED --> COMMITTED: (COMMIT phase)
   * Verifier broadcasts COMMIT message to other verifiers.
   * Verifier received 2F + 1 of valid COMMIT message to enter COMMITTED state.<br/>
      * Messages are from valid Verifiers.
      * Sequence and Round matched.
      * BlockHash matched.
 
 4. COMMITTED --> SEAL COMMITTED: (SEAL phase)
      * Verifier received 2F + + 1 commitments signatures to <strong>extraData</strong> and insert the block into blockchain.
      * Verifier enter SEAL COMMITTED state when insertion succeeds.
   
 5. SEAL COMMITTED --> NEW ROUND: (NEXT ROUND phase)
      * Verifiers calculate/pick a new proposer and start a new round
         

<h2>Round Change (Round Management)</h2>

Conditions will trigger round change:
   * Round Change Timer Expires
   * Invalid PREPARE Message
   * Block Insertion Fails
   * Catchup (not shown in the picture above): jumps out of round change loop when it receives verified block(s) through peer synchronization.
   
How Round Change works:</br>
  1. When a verifier notices that one of the above conditions applies, it broadcasts a ROUND CHANGE message along with the proposed round number and waits for ROUND CHANGE messages from other validators. The proposed round number is selected based on following condition:
      * If the verifier has received ROUND CHANGE messages from its peers, it picks the largest round number which has F + 1 of ROUND CHANGE messages.
      * Otherwise, it picks 1 + current round number as the proposed round number.
   
 2. Whenever a verifier receives F + 1 of ROUND CHANGE messages on the same proposed round number, it compares the received one with its own. If the received is larger, the verifier broadcasts ROUND CHANGE message again with the received number.
 3. Upon receiving 2F + 1 of ROUND CHANGE messages on the same proposed round number, the verifier exits the round change loop, calculates the new proposer, and then enters NEW ROUND state.

<h2>Voting</h2>

   * Verifier can cast one vote to propose a change to the verifier list. (verifier list voting)
   * Verifiers vote on one block with "for" or "against", once a proposal meets the majority votes will come into effect immediately.
   * A effective proposal will entails discarding all pending votes, and reset state to start a new round.
   * Concurrent proposals are allowed and votes are tallied live as chain proceedes.
   
