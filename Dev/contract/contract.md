# Contract

### Compile

Compile from solidity source code to obtain **source bytecode** and **abi**.

### Generate

Using arguments and abi to generate **function bytecode** of all sorts.

### Deploy

Send transaction with source bytecode as payload to obtain **contract address**.

### Employ

Send transaction with function bytecode as payload, with contract address as receiver to obtain **results** and **logs** (results contain function outputs, logs contain emitted events).

### Call

Send json-rpc call request with function bytecode and contract address to obtain **results** (contains function outputs).
