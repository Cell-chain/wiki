# How to be a CELL's miner

The CELL Network test net uses proof-of-activity mining system to generate proofs of workload about time periods for the revenue through Zero-knowledge Proof Techniques

## Download the CELL's mining app

Ubuntu 18.04

```sh
wget https://github.com/Cell-chain/wiki/releases/download/v0.4.0/cell
chmod +x ./cell
```

check the verson:
```sh
./cell --version
```
Make sure the output is `version 0.4.0-f8889ab`;

Window(PowerShell)

```PowerShell
wget https://github.com/Cell-chain/wiki/releases/download/v0.4.0/cell-win.exe -o cell.exe
```

> ! Note: The directory comes with the parameter files to start the program: download the param.bin and witness.bin files.

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
version 0.4.0-f8889ab-x86_64-linux-gnu
Chain specification: Cell Testnet
Node name: feeble-expansion-6681
Role: FULL
Database: RocksDb at /home/miner/
Native runtime: cell_testnet-100 (cell_testnet-1.tx1.au1)
Local node identity is: 12D3KooWG13Tz3i3aZyggHXHtnotiFUJEcRhGb2oYF4ShujQrzog
Highest known block at #0
Prometheus server started at 127.0.0.1:9615
Listening for new connections on 127.0.0.1:9944.
```

## Start multiple nodes

By setting `--base-path` and creating multiple accounts, you can start multiple nodes on a single machine. you'll need to create several different accounts and get beta coins for each one.

The sample:

```sh
./cell --base-path=/mnt/node1 --miner <seed1>
./cell --base-path=/mnt/node2 --miner <seed2>
./cell --base-path=/mnt/node3 --miner <seed3>
```
