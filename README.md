# How to be a CELL miner

The CELL Network test net uses proof-of-activity mining system to generate proofs of workload about time periods for the revenue through Zero-knowledge Proof Techniques

## Download the CELL mining app

You 
Ubuntu 18.04

```sh
wget https://github.com/Cell-chain/wiki/releases/download/v0.4.1/cell
chmod +x ./cell
```
For Ubuntu 20.04 Install first libssl1.0.0

```sh
wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/libssl1.0.0_1.0.2n-1ubuntu5.7_amd64.deb
sudo apt install ./libssl1.0.0_1.0.2n-1ubuntu5.7_amd64.deb
```

Window(PowerShell)

```PowerShell
wget https://github.com/Cell-chain/wiki/releases/download/v0.4.1/cell-win.exe -o cell.exe
```

> ! Note: The directory comes with the parameter files to start the program: download the param.bin and witness.bin files.

> ! Note: check the verson:
```sh
./cell --version
```
Make sure the output is `version 0.4.1-d3b5664`;

## Download the proof parameter file

CELL stores proof parameter files on the decentralized storage network, and access later for free.

Run the following command to download the parameters, confirm the parameters file is in the same directory as the executable.

Ubuntu 18.04

```sh
./cell zkp --params
```

Windows

```PowerShell
./cell.exe zkp --params
```

Or download manually.

Ubuntu example:

```sh
curl https://static.celllab.io/chain/witness.bin > witness.bin
curl https://static.celllab.io/chain/params.bin > params.bin
```

## Create an account to load on chain

Since the mining activity is to obtain by generating Zero-knowledge Proofs and Verifying, then public on the chain. Submit a miner account to the proofs to the chain. Such account use as account to receive the rewards after the campaign ends. Keep such private key security. The gas fee is needed for uploading data to the chain, please to top up the miner account with a small amount of tokens, it is set with a very low amount.

Create the account with the following command:

```sh
./cell key generate
```

The output is as follows.

```txt
Secret phrase `trouble dial maple found milk elite stamp horror cruel tonight immune outdoor` is account:
  Secret seed:      0xd606b3d846eb749fa440365103a5d10a33e099fb7d4adae8091f251d13e15f8e
  Public key (hex): 0xaccdb4918825bb0aee08dfb33d542609e66295f7675130824d4f5a77c2a5b60a
  Account ID:       0xaccdb4918825bb0aee08dfb33d542609e66295f7675130824d4f5a77c2a5b60a
  SS58 Address:     5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd

```

Where Secret seed needed to pass in the node is started.

## Get some test coins

Let's get some test coins with the following command:

```bash
curl 'http://bot.celllab.io/coin/5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd'
```
or visit https://faucet.celllab.io/ to receive your test tokens.

Please replace `5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd` with your address, wait for transaction completed.

Check whether the coin is received:

```bash
curl 'http://bot.celllab.io/balance/5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd'
```

or visit http://wallet.celllab.io/ to check your balance of test tokens

## Start the node

>! Note: If you have ran v0.3.1, delete historical sync data with the following command: 
```sh
./cell purge-chain -y
```

After preparing the parameter file and account, please start the node mining.
The following command starts the mining node.

```sh
./cell --miner 0xd606b3d846eb749fa440365103a5d10a33e099fb7d4adae8091f251d13e15f8e
```

The following output indicates that it is booting normally.

```txt
version 0.4.1-d3b5664-x86_64-linux-gnu
Chain specification: Cell Testnet
Node name: feeble-expansion-6681
Role: FULL
Database: RocksDb at /home/miner/
Native runtime: cell_testnet-101 (cell_testnet-1.tx1.au1)
Local node identity is: 12D3KooWG13Tz3i3aZyggHXHtnotiFUJEcRhGb2oYF4ShujQrzog
Highest known block at #0
Prometheus server started at 127.0.0.1:9615
Listening for new connections on 127.0.0.1:9944.
```

## Start multiple nodes

By setting `--base-path` and creating multiple accounts, you can start multiple nodes on a single machine. you'll need to create several different accounts and get beta coins for each one.

The sample:

```sh
./cell --port=30333 --base-path=/mnt/node1 --miner <seed1>
./cell --port=30334 --base-path=/mnt/node2 --miner <seed2>
./cell --port=30335 --base-path=/mnt/node3 --miner <seed3>
```

## The mining instruction set:

1. *Cell* is the required mining executable program.(windows default is cell-win.exe)
2. *curl*,*wget* are file transfer tools that work under command.
3. *tail* is a text viewer.


* Start synchronous nodes (no mining):
```
cell
```

* Set the storage address of the node:
```
cell --base-path=<path>
```

* Custom bootnode:
```
cell --bootnodes=/ip4/127.0.0.1/tcp/30333/p2p/12D3KooWPJMiEvJ35ads69T4zVAVvihYwqvsA3HwPG47xhFPpUXQ
```

* Set the P2P port:
```
cell --port=30333
```

* Clear the node data:
```
cell purge-chain -y
```

* Create account command:
```
cell key generate
```

* Download mining parameters:
```
cell zkp --params
```

* Start mining:(change to your own address after minner)
```
cell --miner 0x6ad0f5894dfd1d50f0cd5a169bd34c498905709c4efb62085c18b9e0d668f4ac
```

* Get test tokens:
1. visit https://faucet.celllab.io/ to receive your test tokens
2. (change to your own address after /)
```
curl http://bot.celllab.io/coin/5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd
```

* View the balance of test tokens:
1. visit http://wallet.celllab.io/ to check your balance of test tokens
2. (change to your own address after /)
```
curl http://bot.celllab.io/balance/5FyHCb1T4tAMCFci2YhikhtwNBC87usTWmGiGyfdrZtL1Ynd
```

* Background start command:
```
nohup ./cell 2>&1 >> cell.log &
```

* View logs:
```
tail -f cell.log
```

* View cell process PID:
```
ps -e | grep cell
```

* Stop mining:
```
kill -9 [pid]
```
