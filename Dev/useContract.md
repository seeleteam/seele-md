
A contract demo using seeleteam.js

```javascript
'use strict'
const seelejs = require('seeleteam.js')
const zeroAddress = "0x0000000000000000000000000000000000000000"
const fromAddress = "0x987f6215c30f1505e0d42769c5472b410d6bf961"
const fromAddressPrivateKey="0x27ef8d75f918ba1aec7547ee3fd59330488427723fd727232436b4dfb085e739"
const fromShard = 1
const ContractPayload='0x60806040523480156200001157600080fd5b5060405162001e7238038062001e728339810180604052810190808051906020019092919080518201929190602001805190602001909291908051820192919050505083600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550836003819055508260009080519060200190620000b792919062000137565b508060019080519060200190620000d092919062000137565b5081600260006101000a81548160ff021916908360ff16021790555033600460006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555050505050620001e6565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106200017a57805160ff1916838001178555620001ab565b82800160010185558215620001ab579182015b82811115620001aa5782518255916020019190600101906200018d565b5b509050620001ba9190620001be565b5090565b620001e391905b80821115620001df576000816000905550600101620001c5565b5090565b90565b611c7c80620001f66000396000f3006080604052600436106100db576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff16806306fdde03146100dd578063095ea7b31461016d57806318160ddd146101d257806323b872dd146101fd578063313ce567146102825780633bed33ce146102b357806342966c68146102e05780636623fc461461032557806370a082311461036a5780638da5cb5b146103c157806395d89b4114610418578063a9059cbb146104a8578063cd4217c1146104f5578063d7a78db81461054c578063dd62ed3e14610591575b005b3480156100e957600080fd5b506100f2610608565b6040518080602001828103825283818151815260200191508051906020019080838360005b83811015610132578082015181840152602081019050610117565b50505050905090810190601f16801561015f5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561017957600080fd5b506101b8600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506106a6565b604051808215151515815260200191505060405180910390f35b3480156101de57600080fd5b506101e76107aa565b6040518082815260200191505060405180910390f35b34801561020957600080fd5b50610268600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506107b0565b604051808215151515815260200191505060405180910390f35b34801561028e57600080fd5b50610297610dfe565b604051808260ff1660ff16815260200191505060405180910390f35b3480156102bf57600080fd5b506102de60048036038101908080359060200190929190505050610e11565b005b3480156102ec57600080fd5b5061030b60048036038101908080359060200190929190505050610f42565b604051808215151515815260200191505060405180910390f35b34801561033157600080fd5b5061035060048036038101908080359060200190929190505050611168565b604051808215151515815260200191505060405180910390f35b34801561037657600080fd5b506103ab600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050611408565b6040518082815260200191505060405180910390f35b3480156103cd57600080fd5b506103d6611420565b604051808273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200191505060405180910390f35b34801561042457600080fd5b5061042d611446565b6040518080602001828103825283818151815260200191508051906020019080838360005b8381101561046d578082015181840152602081019050610452565b50505050905090810190601f16801561049a5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b3480156104b457600080fd5b506104f3600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506114e4565b005b34801561050157600080fd5b50610536600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050611930565b6040518082815260200191505060405180910390f35b34801561055857600080fd5b5061057760048036038101908080359060200190929190505050611948565b604051808215151515815260200191505060405180910390f35b34801561059d57600080fd5b506105f2600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050611be8565b6040518082815260200191505060405180910390f35b60008054600181600116156101000203166002900480601f01602080910402602001604051908101604052809291908181526020018280546001816001161561010002031660029004801561069e5780601f106106735761010080835404028352916020019161069e565b820191906000526020600020905b81548152906001019060200180831161068157829003601f168201915b505050505081565b6000808211151561071f576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600d8152602001807f76616c756520696e76616c69640000000000000000000000000000000000000081525060200191505060405180910390fd5b81600760003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055506001905092915050565b60035481565b60008073ffffffffffffffffffffffffffffffffffffffff168373ffffffffffffffffffffffffffffffffffffffff1614151515610856576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260158152602001807f302061646472657373206e6f7420616c6c6f776564000000000000000000000081525060200191505060405180910390fd5b6000821115156108ce576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600e8152602001807f76616c756520696e76616c69642000000000000000000000000000000000000081525060200191505060405180910390fd5b81600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410151515610985576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260128152602001807f62616c616e6365206e6f7420656e6f756768000000000000000000000000000081525060200191505060405180910390fd5b600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205482600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205401111515610a7c576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260088152602001807f6f766572666c6f7700000000000000000000000000000000000000000000000081525060200191505060405180910390fd5b600760008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020548211151515610b70576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260148152602001807f616c6c6f77616e6365206e6f7420656e6f75676800000000000000000000000081525060200191505060405180910390fd5b610bb9600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c0d565b600560008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610c45600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c26565b600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550610d0e600760008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c0d565b600760008673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508273ffffffffffffffffffffffffffffffffffffffff168473ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef846040518082815260200191505060405180910390a3600190509392505050565b600260009054906101000a900460ff1681565b600460009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16141515610ed6576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600a8152602001807f6f6e6c79206f776e65720000000000000000000000000000000000000000000081525060200191505060405180910390fd5b600460009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff166108fc829081150290604051600060405180830381858888f19350505050158015610f3e573d6000803e3d6000fd5b5050565b600081600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410151515610ffb576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260128152602001807f62616c616e6365206e6f7420656e6f756768000000000000000000000000000081525060200191505060405180910390fd5b600082111515611073576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600e8152602001807f76616c756520696e76616c69642000000000000000000000000000000000000081525060200191505060405180910390fd5b6110bc600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c0d565b600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000208190555061110b60035483611c0d565b6003819055503373ffffffffffffffffffffffffffffffffffffffff167fcc16f5dbb4873280815c1ee09dbd06736cffcc184412cf7a71a0fdb75d397ca5836040518082815260200191505060405180910390a260019050919050565b600081600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410151515611221576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260128152602001807f62616c616e6365206e6f7420656e6f756768000000000000000000000000000081525060200191505060405180910390fd5b600082111515611299576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600e8152602001807f76616c756520696e76616c69642000000000000000000000000000000000000081525060200191505060405180910390fd5b6112e2600660003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c0d565b600660003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000208190555061136e600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c26565b600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055503373ffffffffffffffffffffffffffffffffffffffff167f2cfce4af01bcb9d6cf6c84ee1b7c491100b8695368264146a94d71e10a63083f836040518082815260200191505060405180910390a260019050919050565b60056020528060005260406000206000915090505481565b600460009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b60018054600181600116156101000203166002900480601f0160208091040260200160405190810160405280929190818152602001828054600181600116156101000203166002900480156114dc5780601f106114b1576101008083540402835291602001916114dc565b820191906000526020600020905b8154815290600101906020018083116114bf57829003601f168201915b505050505081565b600073ffffffffffffffffffffffffffffffffffffffff168273ffffffffffffffffffffffffffffffffffffffff1614151515611589576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260158152602001807f302061646472657373206e6f7420616c6c6f776564000000000000000000000081525060200191505060405180910390fd5b600081111515611601576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600e8152602001807f76616c756520696e76616c69642000000000000000000000000000000000000081525060200191505060405180910390fd5b80600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054101515156116b8576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260128152602001807f62616c616e6365206e6f7420656e6f756768000000000000000000000000000081525060200191505060405180910390fd5b600560008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205481600560008573ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002054011115156117af576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260088152602001807f6f766572666c6f7700000000000000000000000000000000000000000000000081525060200191505060405180910390fd5b6117f8600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205482611c0d565b600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550611884600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205482611c26565b600560008473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055508173ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040518082815260200191505060405180910390a35050565b60066020528060005260406000206000915090505481565b600081600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410151515611a01576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260128152602001807f62616c616e6365206e6f7420656e6f756768000000000000000000000000000081525060200191505060405180910390fd5b600082111515611a79576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600e8152602001807f76616c756520696e76616c69642000000000000000000000000000000000000081525060200191505060405180910390fd5b611ac2600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c0d565b600560003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002081905550611b4e600660003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205483611c26565b600660003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055503373ffffffffffffffffffffffffffffffffffffffff167ff97a274face0b5517365ad396b1fdba6f68bd3135ef603e44272adba3af5a1e0836040518082815260200191505060405180910390a260019050919050565b6007602052816000526040600020602052806000526040600020600091509150505481565b6000828211151515611c1b57fe5b818303905092915050565b6000808284019050838110158015611c3e5750828110155b1515611c4657fe5b80915050929150505600a165627a7a723058200410192b67f26dad697da7c632a49788e566923155a30d733535f99636bf09f10029000000000000000000000000000000000000000000000000000000e8d4a510000000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000000105365656c6553616d706c65436f696e740000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000035353430000000000000000000000000000000000000000000000000000000000'

//与合约交互，必须先确定合约的abi内容和合约地址
//to interact with the contract, you must know the contract's abi and address
const ContractABI ='[{"constant": false,"inputs": [{"name": "_spender","type": "address"},{"name": "_value","type": "uint256"}],"name": "approve","outputs": [{"name": "success","type": "bool"}],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "_value","type": "uint256"}],"name": "burn","outputs": [{"name": "success","type": "bool"}],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "_value","type": "uint256"}],"name": "freeze","outputs": [{"name": "success","type": "bool"}],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "_to","type": "address"},{"name": "_value","type": "uint256"}],"name": "transfer","outputs": [],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "_from","type": "address"},{"name": "_to","type": "address"},{"name": "_value","type": "uint256"}],"name": "transferFrom","outputs": [{"name": "success","type": "bool"}],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "_value","type": "uint256"}],"name": "unfreeze","outputs": [{"name": "success","type": "bool"}],"payable": false,"stateMutability": "nonpayable","type": "function"},{"constant": false,"inputs": [{"name": "amount","type": "uint256"}],"name": "withdrawEther","outputs": [],"payable": false,"stateMutability": "nonpayable","type": "function"},{"inputs": [{"name": "initialSupply","type": "uint256"},{"name": "tokenName","type": "string"},{"name": "decimalUnits","type": "uint8"},{"name": "tokenSymbol","type": "string"}],"payable": false,"stateMutability": "nonpayable","type": "constructor"},{"payable": true,"stateMutability": "payable","type": "fallback"},{"anonymous": false,"inputs": [{"indexed": true,"name": "from","type": "address"},{"indexed": true,"name": "to","type": "address"},{"indexed": false,"name": "value","type": "uint256"}],"name": "Transfer","type": "event"},{"anonymous": false,"inputs": [{"indexed": true,"name": "from","type": "address"},{"indexed": false,"name": "value","type": "uint256"}],"name": "Burn","type": "event"},{"anonymous": false,"inputs": [{"indexed": true,"name": "from","type": "address"},{"indexed": false,"name": "value","type": "uint256"}],"name": "Freeze","type": "event"},{"anonymous": false,"inputs": [{"indexed": true,"name": "from","type": "address"},{"indexed": false,"name": "value","type": "uint256"}],"name": "Unfreeze","type": "event"},{"constant": true,"inputs": [{"name": "","type": "address"},{"name": "","type": "address"}],"name": "allowance","outputs": [{"name": "","type": "uint256"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [{"name": "","type": "address"}],"name": "balanceOf","outputs": [{"name": "","type": "uint256"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [],"name": "decimals","outputs": [{"name": "","type": "uint8"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [{"name": "","type": "address"}],"name": "freezeOf","outputs": [{"name": "","type": "uint256"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [],"name": "name","outputs": [{"name": "","type": "string"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [],"name": "owner","outputs": [{"name": "","type": "address"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [],"name": "symbol","outputs": [{"name": "","type": "string"}],"payable": false,"stateMutability": "view","type": "function"},{"constant": true,"inputs": [],"name": "totalSupply","outputs": [{"name": "","type": "uint256"}],"payable": false,"stateMutability": "view","type": "function"}]'
const ConstractShardNum = 1

//========自定义与合约交互接口方法=============
/*
下述方法列出了本示例中使用到的接口，如需使用更多接口，请参考seele json-rpc 文档，了解接口详细信息
https://seele-seeletech.gitbook.io/wiki/introduction/rpc-content
对于json-rpc接口的调用，seeleteam.js提供了同步和异步两种调用方式：
同步调用使用client.sendSync("methodName",params)的形式；
异步调用使用client.methodName(params)的形式，如client.addTx(params)。
*/
//获得合约某个方法的payload
var generatePayloadTask = function(methodName,data){
    try{
        var payload = client.sendSync("generatePayload", ContractABI, methodName, data)
        return payload;
    }catch(e) {
        console.error(e.message);
        return "";
    }
}
//获得某个账户所属分片
var getShardNum = function (account) {
    try{
        var shardNum = client.sendSync("getShardNum", account)
        return shardNum;
    }catch(e) {
        console.error(e.message);
        return "";
    }
};

//使用私钥在本地实现离线交易签名，得到签名后的transaction
var signTx = function (publicKey,privateKey, nonce,to, amount, price, gaslimit,payload) {
    var rawTx = {
        "Type":0,
        "From": publicKey,
        "To": to,
        "Amount": parseInt(amount*Math.pow(10,8)),
        "AccountNonce": nonce,
        "GasPrice": parseInt(price),
        "GasLimit": parseInt(gaslimit),//3000000,
        "Timestamp": 0,
        "Payload": payload
    }
    try{
        var tx = client.generateTx(privateKey, rawTx);
        return tx;
    }catch(e){
        console.error(e);
        return null;
    }
};

//不改变合约状态的方法调用，通过call实现
var call = function(to, payload,height,callBack){
    return client.sendSync("call",to,payload,height)
};

//改变合约状态的方法调用，通过sendTx实现
var sendTxAsync = function(signedTx){
    return client.addTx(signedTx);      
}

//根据交易hash查询receipt信息
var getReceiptByTxHash = function (hash) {
    if (hash != null && hash != "" && hash != undefined) {
        try{
         return client.sendSync("getReceiptByTxHash",hash,"");
        }catch(e){
            console.error(e);
            return "";
        }
    }
}
//根据交易hash查询交易信息
var getTxByHashAsync = function (hash) {
    if (hash != null && hash != "" && hash != undefined) {
        try{
            return client.sendSync("getTransactionByHash",hash)
           }catch(e){
               console.error(e);
               return "";
           }
    }
}

//预估交易的gas使用量
var estimateGas = function(from,to,payload) {
    var txData = {};
    txData.From = from;
    txData.To = to;
    txData.Amount = 0;
    txData.GasPrice = 0;
    txData.GasLimit = 630000000;
    txData.AccountNonce = 9999999999;
    txData.Payload = payload;
    var tx = {};
    tx.Data = txData;    
    try{
        return client.sendSync("estimateGas",tx);
    }catch(e){
        console.error(e.message);
        return -1;
    }
}
//获得某个账户的nonce值
var getCurNonce = function(account){
    try{
        var nonce = client.sendSync("getAccountNonce", account,"",-1)
        return nonce;
    }catch(e) {
        console.error(e.message);
        return -1;
    }
}


//initialize a seele client to interact with seele blockchain through a seele node address
//初始化seele client，用于和blockchain交互，参数为Seele node节点ip和对应的端口
let client = new seelejs('http://117.50.82.193:8037');

//部署合约
/*
step1: 确认部署合约的账户，该账户所属分片1，则部署的合约也将是分片1内的；其它分片的账户不能与该合约交互
from account:
    public key:  0x987f6215c30f1505e0d42769c5472b410d6bf961
    private key: 0x27ef8d75f918ba1aec7547ee3fd59330488427723fd727232436b4dfb085e739
*/
var estimatedGasValue = estimateGas(fromAddress,zeroAddress,ContractPayload)
//step2:get the sender's account nonce
var nonce = getCurNonce(fromAddress)
if (nonce < 0 ){
    console.log("failed to get sender's account nonce")
    return;
}else{
    console.log("account nonce:"+nonce)
}

//step3:generate a raw transaction and sign it
var signedTx = signTx(fromAddress,fromAddressPrivateKey,nonce,zeroAddress,0,10,estimatedGasValue,ContractPayload);
if(signTx !=null){
    console.log(JSON.stringify(signedTx))
}else{
    console.error("failed to get signed tx");
    return;
}
//step4:send a transaction to deploy the contract
sendTxAsync(signedTx).then(function(info,err){
    if (err!=null){
        console.error(err)
    }else{
        console.log(info)
    }
}).then(function(){
    var txInfo ={}
    txInfo.status="pending" 
    while(txInfo.status=="pending"||txInfo=="pool"){
        txInfo= getTxByHashAsync(signedTranferTx.Hash)
        if(txInfo!=""&&txInfo.status=="block"){
           console.log("transaction already in block")
           console.log("txInfo:"+ JSON.stringify(txInfo))
           break;
        }   
    }
}).then(function(){
    var receiptResult = getReceiptByTxHash(signedTx.Hash)
    if (receiptResult.failed == false){
        console.log("contract address"+receiptResult.contract)
    }
}).catch(function(error){
    console.error(error);
})


//===========合约交互示例===============
/*
case 1: use call to interact with methods that will not change contract's state
SSCCoin contract, balanceOf method：
*/

//case1-step1: generate payload for the method
var deployedContractAddress = "0x12f60a74186f3469290480d54854fe169e430032";
var balanceOfPayload = generatePayloadTask("balanceOf",["0x987f6215c30f1505e0d42769c5472b410d6bf961"]); 
console.log("payload for contract method balanceOf:"+balanceOfPayload);

//case1-step2: make a call to the contract method
var callResult = call(deployedContractAddress,balanceOfPayload,-1)
if (callResult!="" && callResult.failed == false){
        console.log("contract method balanceOf returned:"+callResult.result);
    }else{
        console.log("contract method call failed")
}
/*
case2: use sendtx to interact with methods that change contract's state
SSCCoin contract, transfer method：
function transfer(address _to, uint256 _value) public returns (bool);
*/

//case2-step0: 
/*
[!!!!!!!!!!important: validate shard number !!!!!]
 in case the contract method refers to transfer to another address,
 the very first step should be address shard validation, as Seele doesn't support cross-shard 
 contract interaction. 
 If you transfer tokens to other shard's address, the token might be lost, as the target address
 cannot interact with the contract
 */
 /*
to address:
    public key:  0x5f70d9513c9e83dfe46f1881c92398206f78c401
    private key: 0xa943a8f734fba23e793b110519e83c595831d7a727b63e0774f8bd439cd8817a
from account:
    public key:  0x987f6215c30f1505e0d42769c5472b410d6bf961
    private key: 0x27ef8d75f918ba1aec7547ee3fd59330488427723fd727232436b4dfb085e739
*/

if (fromShard!=ConstractShardNum){
    console.error("transaction sender's shard number should be the same as the contract's")
    return
}
var toAddress = "0x5f70d9513c9e83dfe46f1881c92398206f78c401"

// 0xa9059cbb000000000000000000000000ff34b2767eb4df344f4cdb9cf32b58c863b000320000000000000000000000000000000000000000000000000000000000000064
var toShard = getShardNum(toAddress)
if (toShard != ConstractShardNum){
    console.error("be careful! the target account's shard number is different from the contract's shard number ")
}

//case2-step1: generate payload for the method
// the result should be:
//"0xa9059cbb0000000000000000000000005f70d9513c9e83dfe46f1881c92398206f78c4010000000000000000000000000000000000000000000000000000000000000014"
var transferPayload = generatePayloadTask("transfer",[toAddress,"100"])
console.log("payload for contract method transfer:"+transferPayload);

//case2-step2: estimate the gas
var estimatedGasValue = estimateGas(fromAddress,deployedContractAddress,transferPayload)
if (estimatedGasValue <=0 ){
    console.log("failed to get the estimated gas")
    estimatedGasValue = 99999999999
}else{
    console.log("estimated gas:"+estimatedGasValue)
}

//case2-step3:get the sender's account nonce
var nonce = getCurNonce(fromAddress)
if (nonce < 0 ){
    console.log("failed to get sender's account nonce")
    return;
}else{
    console.log("account nonce:"+nonce)
}

//case2-step4:generate a raw transaction and sign it
var signedTranferTx = signTx(fromAddress,fromAddressPrivateKey,nonce,deployedContractAddress,0,10,estimatedGasValue,transferPayload);
if(signTx !=null){
    console.log(JSON.stringify(signedTranferTx))
}else{
    console.error("failed to get signed tx");
    return;
}
//case2-step5:send a transaction to interact with the contract
 sendTxAsync(signedTranferTx).then(function(info,err){
            if (err!=null){
                console.error(err)
            }else{
                console.log("sendTx:"+info+", transaction already sent")
            }
        }).then(function(){
            var txInfo ={}
            txInfo.status="pending" 
            while(txInfo.status=="pending"||txInfo.status=="pool"){
                 txInfo= getTxByHashAsync(signedTranferTx.Hash)
                 if(txInfo!=""&&txInfo.status=="block"){
                    console.log("transaction already in block")
                    console.log("txInfo:"+ JSON.stringify(txInfo))
                    break;
                 }                       
            }
        }).then(function(){
            var receiptResult = getReceiptByTxHash(signedTranferTx.Hash)
            if (receiptResult.failed == false){
                console.log("logs:"+JSON.stringify(receiptResult.logs))
            }
        }).catch(function(error){
            console.error(error);
        })
```