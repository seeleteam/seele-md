# Seele Stem subchain

Seele Stem subchain protocol is a layer-2 solution to improve the scalability of Seele mainnet. A general introduction of the protocol can be found [here](https://medium.com/@SeeleTech/seele-stem-subchain-protocol-b5eceb02aaa3). 



## Deploy a new Stem contract
To create your own Stem subchain, you need to deploy a Stem contract on Seele mainnet. Stem contract serves as an important interface between Seele mainnet and subchains. It ensures the ultimate safety of your assets in the subchains. Each Stem subchain should have its own Stem contract.

### 1. Customize parameters
Before deploying Stem contract, you should customize the parameters in function **init** in **StemCreation.sol**.

|Parameter| Description|
|---------|------------|
|MIN\_LENGTH\_OPERATOR | minimum number of operators |
|MAX\_LENGTH\_OPERATOR | maximum number of operators |
|CHILD\_BLOCK\_INTERVAL | relay frequency, i.e. relay information should be submitted with this frequency|
|IS\_NEW\_OPERATOR\_ALLOWED| true if new operators are allowed to join; otherwise false|
|creatorMinDeposit | minimum deposit of the creator|
|childBlockChallengePeriod | response to block challenges are allowed within [submission time of last relay block, submission time of last relay block + childBlockChallengePeriod]|
|childBlockChallengeSubmissionPeriod | block challenges are allowed within [submission time of last relay block, submission time of last relay block + childBlockChallengeSubmissionPeriod]|
|relayTimeout | the contract will be discarded if the last relay block is not confirmed within [submission time of last relay block, submission time of last relay block + relayTimeout]|
|isBlockSubmissionBondReleased | should be true initially|
|blockSubmissionBond | the bond a block submitter pays |
|blockChallengeBond | the bond a block challenger pays|
|operatorMinDeposit | the minimum value for each operator deposit|
|userMinDeposit | the minimum value for each user deposit| 
|userExitBond| the bond a user pays to exit|
|isFrozen | true if the contract is discarded; otherwise false; should be false initially |

You can use **MIN\_LENGTH\_OPERATOR** and **MAX\_LENGTH\_OPERATOR** to specify how many operators are allowed in your subchain.

After a constant number of blocks are produced in the subchain, some relay information needs to be submitted to Stem contract. This constant number is specified by **CHILD\_BLOCK\_INTERVAL**.

**IS\_NEW\_OPERATOR\_ALLOWED** is used to specify whether new operators are allowed to join after the creation of the subchain. If it is set as false, then operators can only be set up at the creation of the subchain.

**creatorMinDeposit**, **operatorMinDeposit** and **userMinDeposit** are the minimum amount of deposits for each deposit operation. Creator deposit is only needed when the creator creates the Stem contract. Operator deposit is needed when a new operator wants to join the subchain. A minimum user deposit is required when a user wants to deposit more funds into its subchain account.

After the information of a relay block is submitted, it could be challenged if someone finds the information incorrect. There is a time window for submitting challenges. The length of this time window is specified by **childBlockChallengeSubmissionPeriod**. There is a longer time window, of which the length is **childBlockChallengePeriod**, for submitting responses to the challenges. After **childBlockChallengePeriod** if there is no unresolved challenge, the relay block is confirmed. 

To prevent the case that a relay block is not confirmed for a long time, **relayTimeout** is used as the timeout limit. When relayTimeout is exceeded, the Stem contract will be discarded, which means it can not be used anymore and reasonable mainnet funds will be returned to subchain participants. **isFrozen** is an indicator of whether the Stem contract is discarded. Note that once the Stem contract is discarded, it is permanent.

Bonds are used to penalize possible malicious behaviors. **blockSubmissionBond** is required when an operator or owner submits the information of a new relay block. If the new relay block is successfully challenged, then the **blockSubmissionBond** is rewarded to the challenger. The **blockSubmissionBond** will be returned to the submitter upon the confirmation of the relay block.

Similarly, **blockChallengeBond** is required when someone wants to challenge a relay block. If the challenge is successful, the challenger gets **blockChallengeBond** back plus the **blockSubmissionBond**. Otherwise, the **blockChallengeBond** is forfeited.

**userExitBond** is required when a user wants to exit part of its fund from the subchain. If the exit is completed successfully, **userExitBond** will be returned to the user.

### 2. Use controller to deploy Stem contract
You will need to deploy a series of contracts on Seele mainnet. The best way is to use controller to do it.


The input of the constructor

|type| name | note |
|---------|------------|-----------|
|bytes32 | subchainName | name of the subchain (optional)|
| bytes32[] | genesisInfo| [root hash of balance merkle tree, root hash of recent transaction merkle tree] 
| bytes32[] | staticNodes| array of static nodes (optional) |
| uint256 | creatorDeposit| creator deposit|
| address[] | ops | array of operator account (subchain account); the first account is the mint account in the subchain; the second account is the melt account in the subchain; operator accounts start from the third account|
| uint256[] | opsDeposits | array of initial operator deposit; the fist two elements are not used; starting from the third element, opsDeposits[i] is the amount of deposit of ops[i]|
| address[] | refundAccounts | array of refund accounts (Seele mainnet accounts); the first two elements are not used; starting from the third element, refundAccounts[i] is the Seele mainnet account of ops[i] |

Note that the contract deployment itself is a mainnet transaction. The sender of the transaction will be the **owner** of the Stem contract. The amount of the transaction must be greater than or equal to the sum of creator deposit and all operator deposits. The length of array **ops**, **opsDeposits** and **refundAccounts** must be the same. The length of **ops** should be at least 3; in this case, the subchain has one mint account, one melt account and an operator account. The mint account is the subchain account which issues token to subchain participants. The melt account is 

After the deployment of **StemRootchain.sol**, you've created a Seele stem contract successfully. Congratulations!
### 
 
## Owner 
### Discard contract 
The contract owner is able to discard the Stem contract. All the funds in the Stem contract will be returned to participants based on the information of the most recent confirmed relay block.



## Operator

### Register a new operator 
To register a new operator, you need to provide the operator's subchain account and mainnet account (for the use of refund). The subchain account should not be used before by other operators or users in the same subchain. The deposit amount should be greater than **operatorMinDeposit**.

### Operator exit
The operator can exit from the subchain by submitting an exit request.  

### Fee exit
The operator can withdraw his reward (users' transaction fee in the subchain) by submitting a fee exit request. 

### Submit relay block
The operators or owner need to submit information of relay blocks. The information is shown in the following table.

|type| name | note |
|---------|------------|-----------|
| uint256 | the height of relay block | should be a multiple of **CHILD\_BLOCK\_INTERVAL**| 
| bytes32 | root hash of balance merkle tree of the relay block| | 
|bytes32 | root hash of recent transaction merkle tree of the relay block| |
| address[] | updated accounts | the accounts which have a balance change since last relay block | 
| uint256[] | updated balances | | 
| uint256  | fee | fee income for each operator (same for each operator) since last relay block|

### Respond to block challenge
Operators need to respond to every valid block challenge during **childBlockChallengePeriod**. Otherwise, the new relay block will not be confirmed. Operators needs to provide transaction history to prove the challenged accounts have claimed updated balances. 
 

## User

### User deposit
To deposit more fund to a (new or existing) user account, you need to provide the user's subchain account and mainnet account (for the use of refund). The subchain account should not be used before by other operators in the same subchain. The deposit amount should be greater than **userMinDeposit**.

### User exit
The user can exit part (or all) of his fund from the subchain by submitting an exit request. 

### Challenge submitted block
Users can check the updated balances in the Stem contract. If they believe the balances are incorrect, they can submit challenges during **childBlockChallengeSubmissionPeriod**. 

The challenger needs to provide the subchain account to challenge. Additionally, the challenger can provide evidence that a transaction is included in a valid block since last confirmed relay block.
 


