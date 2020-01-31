# Anchor (controller)

## Pages:
1. Node Page
  - mainnet nodes : cur & bac
  - subnet nodes : cur & bac 
2. Account Page
  - Main chain Accounts
    - //transaction line
    - //contract methods lines ... 
    - //contract call/events lines
    - //subchain line 
      - Subchain Account 
  - top few transactions
3. Contract Page
  - general contracts
  - subchain contracts
4. Transaction Page
  - Complete, filter by account, sort by time/status
    - pendings
    - fail
    - done
5. Events Page
  - Subscriptions
  - 

## Cell description
  - Node
    - shard: updatable, 
    - ipport: fixed, 
    - version: updatable
    - peers: updatable
    - height: updatable

## Flow:
  - Transact:
    1. Enter password on **[keyfile version]** to unlock.
    0. Enter **[to]**, **[amount]** click **[send]**.
    - ps:
      - In "Transaction Page," Click **[tx status]** to view receipt.
      - Configure more parameters in **[amount]** field.
      - Beginning of line shows the shard nature of transaction.
  - Employ:
    1. Enter password on **[keyfile version]** to unlock.
    0. Contract line: select **[contract]**, **[method]**, and enter **[parameters]**, click **[estimate]**; 
    0. Click **[send]**.
    - ps:
      - Add frequent methods with contract line shardnumber
      - delete methods with the same shardnumber
      - subscribe to events and calls using contract name
      - automate challenge/relay/respond/rollback using contract name
  - Call:
    1. Go to contract page
    0. 


# Keel (chain explorer)

<!-- **[]** -->
<!-- **** -->





