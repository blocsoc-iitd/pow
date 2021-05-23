# Blockchain Full Node from scratch

**What i covered in this demo:**

* Blockchain based on Proof Of Work algorithm
* Transaction spent control. Each Tx Input pointed to the previous Tx Output
* Signed Inputs by wallet private key
* Using Merkel Tree for faster Block hash computation during mining
* Mining process
* Sync process between nodes
* Transaction and Block verifiers
* Same configuration on reward and difficulty for all blocks. Thus no supply limits.
* Nodes blocks, txs, nodes addresses gossip broadcast
* Covering Blockchain split brain situation but only for 2 blocks ahead.
* Openapi schema + UI (generated by FastAPI)
* Some tests for blockchain. Cause it very simple to mess things up with all this hashes

**What i didn't covered in this demo:**
* Hard split brain with any levels of new blocks ahead 
* Automtic node discovery in a subnets through service discovery protocol and ping
* Integration testing
* Byzantine testing
* Many things that real blockchain solution has. If you interesting in such, you can open Bitcoin or Ethereum after reading this.
* Multiprocessing for mining
* Light client
* No limitation on block sizes or number of Txs. Block mining starts after previous mininig ends.

## Running thins up

`pip install -r requirements.txt`

Open 3 terminals. In first run:

`python3 full_node.py --port=8000 -mine=1`

After you see that server up and sync process finished, in two next terminals run:

`python3 full_node.py --port=8001 --node=127.0.0.1:8000 --mine=1`

`python3 full_node.py --port=8002 --node=127.0.0.1:8000 --mine=1`

Open 4th terminal and run:

`python3 testrun.py`

This will show you info about last block on the chain on each node. They should be same.

If you open in browser any node, like [http://127.0.0.1:8001/docs](http://127.0.0.1:8001/docs) you can see API UI, and can interact with it.
It not so powerfull API, but still enough to see how things work and get basic understaning.

## Tests
Run `pytest`

### Problems
If set difficulty to low and mininig will end to fast, nodes can get hard split brain situation which is not covered by this code.
So if this happens, just increase difficulty of the each node from 22 (default) to something bigger, 25 for example. 
Or if you have not powerfull cpu you can decrease difficulty as well.




