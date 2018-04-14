![Brofist Logo](/src/qt/res/icons/bitcoin.png)

BROFIST COIN - A COMMUNITY RE-DESIGNED COIN 

What is BroFist?
----------------

This is just another one coin that the developer had gone away, and left it to be a shit coin.
Therefore, I make this fork to look after it, and make it to be the community stable and reliable coin.

- Maximum Supply: 31,000,000 coins
- Algorithm: NeoScrypt
- Type: PoW + MasterNode
- Coin name: BroFist Coin
- Coin abbreviation: PEW
- Block Time Average: 120 sec
- Block Reward: 0-150 - 1 PEW, 150-250 - 3 PEW, 250+ - 12 PEW. 
- Block Reward Distribution: 6 PEW to Masternodes, 6 PEW to Miners
- Premine: 1% (300,000 PEW with Old Dev)

* Block Explorer : https://pew.overemo.com/
* Bitcointalk ANN : https://bitcointalk.org/index.php?topic=3025770.80 
* Website: http://brofist-coin.firebaseapp.com  (coming soon)
* Exchange: https://graviex.net/markets/pewbtc
* Discord: https://discord.gg/p2rsNEb

Downloads
----------------
* [Windows 32 Wallet](https://github.com/modcrypto/brofist/releases/download/1.1/brofist32-qt.zip) (Stable)
* [Linux Wallet](https://github.com/modcrypto/brofist/releases/download/1.1/brofishd_ubuntu.1.1.tar.gz)
* MacOS Wallet
* [Blockchain](https://github.com/modcrypto/brofist/releases/download/1.0/brofist_blockchain_24176.zip) 1 - 24176 blocks

How to Repair Your Masternode
------------------------
1. Close your BroFist wallet.
2. Delete everything from the folder <USER_FOLDER>\AppData\Roaming\BroFistCore (for windows), 
   EXCEPT wallet.dat, brofist.conf, masternode.conf and backup folder.

![Sample Screen](/doc/brofist_doc/step1.png)

Be extremely careful not to delete wallet.dat, or you may loose all your coins.

3. Then you need to add nodes that are 100% sure on the right chain to your brofist.conf file :
Code: Last update 13-04-2018 
```ini
maxconnections=30
addnode=pew.overemo.com
addnode=159.203.186.24
addnode=212.237.25.226
addnode=51.15.61.35
addnode=13.59.190.151
addnode=104.168.87.183
addnode=35.203.57.179
addnode=104.197.130.51
addnode=45.77.227.85
addnode=213.110.122.225
addnode=144.202.84.33
addnode=94.181.94.119
addnode=185.148.39.82
addnode=90.189.149.194
addnode=87.224.202.66
addnode=216.187.82.74
addnode=80.64.131.234
addnode=45.63.115.225
addnode=45.32.186.12
addnode=45.58.16.26
addnode=185.160.60.164
addnode=83.220.170.213
addnode=212.12.20.198
addnode=45.32.24.168
addnode=198.13.62.66
addnode=185.5.251.7
addnode=185.117.153.77
addnode=134.196.70.186
addnode=35.197.95.164
addnode=35.199.63.148
addnode=35.227.57.57
addnode=176.62.66.106
addnode=173.179.231.182
addnode=45.77.198.234
addnode=92.242.3.82
addnode=104.156.247.243
addnode=142.44.247.32
addnode=81.5.117.163
addnode=207.148.119.112
addnode=195.211.160.86
addnode=184.145.218.70
addnode=173.249.23.236
addnode=2.225.249.244
addnode=173.212.201.123
addnode=51.15.86.239
addnode=51.15.81.233
addnode=45.32.112.230
addnode=184.145.218.78
addnode=173.249.41.184


```
Please don't make maxconnections number higher than 30, or you might desync again.

4. Open your BroFist wallet again.

Master Node Guide
----------------
* [Setting Multiple Masternodes on Ubuntu VPS](https://github.com/modcrypto/brofist/blob/master/doc/masternode_multi.md)


License
-------

BroFist Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is meant to be stable. Development is normally done in separate branches.
[Tags](https://github.com/brofistcoin/brofist/tags) are created to indicate new official,
stable release versions of BroFist Core.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md).

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](/doc/unit-tests.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

The Travis CI system makes sure that every pull request is built for Windows
and Linux, OS X, and that unit and sanity tests are automatically run.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.
