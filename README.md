![Build Status](https://travis-ci.org/cryptape/appchain-plugin.svg?branch=master)
![npm (scoped)](https://img.shields.io/npm/v/@appchain/plugin.svg)
[![MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/cryptape/appchain-plugin)
[![AppChain](https://img.shields.io/badge/made%20for-Nervos%20AppChain-blue.svg)](https://appchain.appchain.org/)

# AppChain-Plugin

Promise based [CITA RPC](https://docs.nervos.org/cita/#/rpc_guide/rpc) toolkit.

# Features

- Supports the Promise API

# Installing

```bash
$ yarn add @appchain/plugin
```

# Example

```javascript
import appchainPlugin from '@appchain/plugin'

const SERVER = 'localhost:1337'

const { appchain } = appchainPlugin({ server: SERVER })

/**
 * @function metadata
 * @description request metadata of specified chain
 * @param {{blockNumber}}
 * @return {Metadata}
 */
appchain.metadata({ blockNumer: '0x0' }).then(metadata => console.log(metadata))

/**
 * @function netPeerCount
 * @description request net peer count
 * @param null
 * @returns {string} peerCount
 */
appchain.netPeerCount().then(count => console.log(count))

/**
 * @function getBlockByNumber
 * @description request block by block number
 * @param {string} quantity - quantity is the current block height of CITA
 * @param {boolean} detialed - return transaction list if true, otherwise return hash of transaction
 * @returns {object} block
 */
appchain
  .getBlockByNumber({
    quantity: blockNumber,
    detailed: true,
  })
  .then(block => console.log(block))

/**
 * @function getBlockByHash
 * @description request block by block hash
 * @param {string} hash - block hash
 * @param {boolean} detailed - return transaction list if true, otherwise return hash of transaction
 * @returns {object} block
 */
appchain
  .getBlockByHash({
    hash: blockHash,
    detailed: true,
  })
  .then(block => console.log(block))

/**
 * @function getBlockHistory
 * @description retrieve blocks of height from (by - count + 1) to by
 * @param {by: string, count: number} - by: the startpoint of history, count: the count of records to retrieve
 * @return {array} list of block
 */
appchain
  .getBlockHistory({
    by: '0x4bb99',
    count: 5,
  })
  .then(blocks => console.log(blocks))

/**
 * @function getTransaction
 * @description request transaction detail
 * @param {string} transactionHash
 * @return {object} Transaction
 */
appchain.getTransaction('0x...').then(transaction => console.log(transaction))

/**
 * @function getLogs
 * @description requestion log on specified block
 * @param {{topics: Topic[]}}
 * @return {object} Logs
 */
appchain.getLogs({ topics: [] }).then(logs => console.log(logs))

/**
 * @function getBalance
 * @description get balance of specified address
 * @param {{addr}} - addr: specified address
 * @return {Balance}
 */
appchain.getBalance({ addr: '0x...' }).then(balance => console.log(balance))

/**
 * @function getTransactionCount
 * @description get transaction count of specified addr
 * @param {{addr, blockNumber}}
 * @return {TransactionCount}
 */
appchain.getTransactionCount({ addr: '0x..', blockNumber: 'latest' }).then(count => console.log(count))

/**
 * @function getTransactionProof
 * @description get transaction proof of specified transaction hash
 * @param {string} trasnactionHash
 * @return {string} transaction proof
 */

appchain.getTransactionProof('0x...').then(proof => console.log(proof))

/**
 * @function newFilter
 * @desc create new filter
 * @param {Array<topic>} topics
 * @return {string} filterId
 */
appchain.newFilter([])

/**
 * @function newBlockFilter
 * @desc create new block filter
 * @param None
 * @return {string} filterId
 */
appchain.newBlockFilter()

/**
 * @function uninstallFilter
 * @desc uninstall filter
 * @param {string} filterId
 * @return {boolean} success
 */

appchain.uninstallFilter(id)

/**
 * @function getFilterChanges
 * @desc get filter changes
 * @param {string} filterId
 * @return {Array<Result>} logArray
 */
appchain.getFilterChanges(id)

/**
 * @function sendSignedTransaction
 * @desc send signed transaction
 * @param {string} signedTransaction
 * @return {object}
 */
appchain.sendSignedTransaction(signedTransaction)

/**
 * @function setServer
 * @description set server
 * @param {string} server
 * @return undefined
 */

appchain.setServer('http://localhost:1301')
```
