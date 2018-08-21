# Practical Byzantine Fault Tolerance
PBFT is a consensus algorithm [used by some of the biggest Blockchains](https://blockonomi.com/practical-byzantine-fault-tolerance/).

It's known for being a more secure alternative to the traditional [Proof of Work](https://en.wikipedia.org/wiki/Proof-of-work_system).

## Execution

It is possible to start many nodes in the same machine or in different VMs, the initialization is the same, as follows:

```sh
$ node networkNode.js <type> <address>
```

Example:

```sh
node networkNode.js master http://localhost:3000
```

Node type should be either `master` or `network`. Only `master` nodes are allowed to create blocks in PBFT. Any node will take part in the voting though.

As soon as the node starts, it will ask the user for a master node ip, so it can retrieve network current information.

This should be a reachable `master` node in the format `http://ip:port`.

If it is the first node in the network, just input `this`, the node will then start as the first master node. Don't do this if you intend to connect to an active network, as the node will just start its own network and won't connect to any running nodes.

To test, you can reach `http://ip:port/` in your browser, it will return a `json` containing information on the node you requested, and the active nodes on the network.

To see the current blockchain, reach `http://ip:port/blockchain`.

To add a block to the blockchain, make a `post` request to `http://ip:port/createBlock` with a `json` payload as follows:
```js
{
	"carPlate": "<plate>",
	"block": {
		"data": "any data, can be an array, or json, str..."
	}
}
```

The `response` will contain the whole created block that was broadcast to the network, however, this does not mean the block was accepted. You can request the `/blockchain` to any node to check if the block was accepted.

There are a number of reasons for a block to be rejected, you can check the results of the voting process in any node `log`.

---

This repository is part of the [CarChain project](https://github.com/alissonfpmorais/blockchain-js)
