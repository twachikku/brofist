Multiple Masternodes on Single IPv4 VPS config
=====================================

BroFist Core allows controlling multiple remote masternodes from a single wallet, but it needs to have unique IPv4 for each masternode. 
So, if your VPS has only one IPv4 address, you can start multiple masternodes by running multiple wallet. Each wallet needs to have a valid collateral output of 1000 coins for masternode.

For example, if you need to run 10 master nodes. You must run 10 BroFist wallets, and each wallet must has 1000 coins. That each wallet need at least 100MB of RAM for running. In this sutiation, the large RAM VPS is better.  

Requirements
============
* OS : Linux (Tested on Ubuntu 16.04)
* Wallet : https://github.com/modcrypto/brofist/releases/download/1.0/brofist_ubuntu.16.04.tar.gz

In this guide will show a example of setting 2 masternodes with one IPv4 address.

1. Prepare the environment
Please run theses command line by line.
```bash
sudo apt-get update 
sudo apt-get upgrade 
sudo apt-get install git automake build-essential libtool autotools-dev autoconf pkg-config nano software-properties-common
sudo apt-get install libssl-dev libboost-all-dev libevent-dev 
sudo apt-add-repository ppa:bitcoin/bitcoin 
sudo apt-get update 
sudo apt-get install libdb4.8-dev libdb4.8++-dev sudo libminiupnpc-dev libzmq3-dev
```
2. Download the wallet for ubuntu.
```bash
wget https://github.com/modcrypto/brofist/releases/download/1.0/brofist_ubuntu.16.04.tar.gz
tar -xvf brofist_ubuntu.16.04.tar.gz
cd brofist
ls -la
```

You will see these files in folder :brofist
```
-rwxr--r-- 1 root  2288952 Apr  3 09:16 brofist-cli
-rwxr--r-- 1 root 10123768 Apr  3 12:48 brofistd
-rwxr--r-- 1 root  2602016 Apr  3 09:16 brofist-tx
drwxrwxr-x 4 root     4096 Apr  3 09:28 master
-rwxrwxr-x 1 root      102 Apr 13 02:12 start.sh
-rwxrwxr-x 1 root       41 Apr  3 09:27 stop.sh
```

3. Edit start.sh to this code: 
```bash

```

and uses a configuration file named `masternode.conf` which can be found in the following data directory (depending on your operating system):
 * Windows: %APPDATA%\BroFistCore\
 * Mac OS: ~/Library/Application Support/BroFistCore/
 * Unix/Linux: ~/.brofistcore/

`masternode.conf` is a space separated text file. Each line consists of an alias, IP address followed by port, masternode private key, collateral output transaction id and collateral output index.

Example:
```
mn1 127.0.0.2:11113 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566 0
mn2 127.0.0.4:11113 92Da1aYg6sbenP6uwskJgEY2XWB5LwJ7bXRqc3UPeShtHWJDjDv 5d898e78244f3206e0105f421cdb071d95d111a51cd88eb5511fc0dbf4bfd95f 1
```

_Note: IPs like 127.0.0.* are not allowed actually, we are using them here for explanatory purposes only. Make sure you have real reachable remote IPs in you `masternode.conf`._

In the example above:
* the collateral of 1000 PEW for `mn1` is output `0` of transaction [7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566](https://test.explorer.brofist.org/tx/7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566)
* the collateral of 1000 PEW for `mn2` is output `1` of transaction [5d898e78244f3206e0105f421cdb071d95d111a51cd88eb5511fc0dbf4bfd95f](https://test.explorer.brofist.org/tx/5d898e78244f3206e0105f421cdb071d95d111a51cd88eb5511fc0dbf4bfd95f)

The following RPC commands are available (type `help masternode` in Console for more info):
* list-conf
* start-alias \<alias\>
* start-all
* start-missing
* start-disabled
* outputs
