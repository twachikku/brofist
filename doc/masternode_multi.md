Multiple Masternodes on Single IPv4 VPS config
=====================================

BroFist Core allows controlling multiple remote masternodes from a single wallet, but it needs to have unique IPv4 for each masternode. 
So, if your VPS has only one IPv4 address, you can start multiple masternodes by running multiple wallet. Each wallet needs to have a valid collateral output of 1000 coins for masternode.

For example, if you need to run 10 master nodes. You must run 10 BroFist wallets, and each wallet must has 1000 coins. That each wallet need at least 100MB of RAM for running. In this sutiation, the large RAM VPS is better.  

Requirements
============
* OS : Linux (Tested on Ubuntu 16.04)
* Wallet : https://github.com/modcrypto/brofist/releases/download/1.1/brofistmaster_ubuntu.1.1.tar.gz

### 1. Steps to Create a New Sudo User
1. Log in to your VPS server as the root user.
2. Use the adduser command to add a new user to your system.
3. Use the usermod command to add the user to the sudo group.
4. Close the terminal and re-login with your new username.
(You can replace ***brofist*** with the username that you want to create.)
```bash 
adduser brofist
usermod -aG sudo brofist
```

### 2. Prepare the environment for runnning the Brofist wallet
Login with your brofist username.
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
### 3. Download and Setup the Brofist Core Masternode.
1. Download the latest file "brofistmaster_ubuntu.x.x.tar.gz"
```bash
wget https://github.com/modcrypto/brofist/releases/download/1.1/brofistmaster_ubuntu.1.1.tar.gz
tar -xvf brofistmaster_ubuntu.1.1.tar.gz
cd brofist
ls -la
```

You will see these files in folder :brofist
```
-rwxr--r-- 1 brofist brofist    1294 Apr 13 11:33 addnodes.txt
-rwxr--r-- 1 brofist brofist  485776 Apr 12 21:43 brofist-cli
-rwxrwxr-x 1 brofist brofist 6522208 Apr 13 14:26 brofistd
-rwxr--r-- 1 brofist brofist 1004104 Apr 13 04:16 brofist-tx
-rwxrwxr-x 1 brofist brofist      51 Apr 13 14:28 cli.sh
-rwxrwxr-x 1 brofist brofist     583 Apr 13 15:24 start.sh
-rwxrwxr-x 1 brofist brofist      55 Apr 12 21:57 stop.sh
```
* **brofistd** is the Brofist daemon. 
* **brofist-cli** is the Brofist command-line interface. 
* **cli.sh** is the bash script file wrapper for calling brofist-cli.
* **start.sh** is the bash script file wrapper for starting brofist daemon.
* **stop.sh** is the bash script file wrapper for stopping brofist daemon.

2. Edit start.sh with **nano start.sh**, and set your ipaddress.
For example if your vps ipaddress is 173.249.1.1 then the start.sh will look like this:

```bash
#!/bin/bash 
# usage
# ./start.sh <n>
# where n is a number.  
# example:   ./start.sh

ipaddress="173.249.1.1"   

if [ "$ipaddress" == "xx.xx.xx.xx" ]; then
   echo "Please set a ipaddress in file 'start.sh' "
   exit
fi
if [ ! -d "data$1" ]; then
  mkdir data$1
  echo "listen=1" >> data$1/brofist.conf 
  echo "daemon=1" >> data$1/brofist.conf 
  echo "server=1" >> data$1/brofist.conf 
  echo "rpcuser=pew" >> data$1/brofist.conf 
  echo "rpcpassword=password" >> data$1/brofist.conf 
  echo "rpcallowip=127.0.0.1" >> data$1/brofist.conf 
  echo "maxconnections=30" >> data$1/brofist.conf 
  echo "rpcport=127$1" >> data$1/brofist.conf    
  echo "bind=$ipaddress:11113" >> data$1/brofist.conf   
  cat addnodes.txt >> data$1/brofist.conf 
fi
./brofistd -deamon -datadir=data$1 ${@:2}

sleep 1

```

### 4. Start the wallet
In this guide, we will index each master node by numbers  1,2,3... 

1. First, to create the masternode no.1
```bash
./start.sh 1
```
After Brofist daemon starting, please wait at lease 2-3 seconds. 
You can start other masternode by calling **./start.sh n**
For example, to start the masternode no.2, and no.3
```bash
./start.sh 2
./start.sh 3
```

You can stop each node by ** ./stop.sh n **
For example, to stop the masternode no.2
```bash
./stop.sh 2
```

### 5. Setup the masternode
1. Get the wallet address of masternode no.1
```bash
./cli.sh 1 getaddressesbyaccount ""

```
You will see the address like this 
```json
[
  "PX8VB4pHG3M6acstLf45oBReNLhoaxjunq"
]
```
2. Send coin **1000 PEW** to the address
This must be exactly 1000.
Wait 10 minutes for confirmation.
Buy PEW from https://graviex.net/markets/pewbtc, if you don't have enougth coins. 

3. Generate the masternode private key
```bash
./cli.sh 1 masternode genkey
```
You will see the address like this: 
7eAKos41o7WgKQDQYGDc2oFmqsHhKfw7zDc9H8sFbHF8SwmQpZZ

4. Check the collateral output
```bash
./cli.sh 1 masternode outputs
```
You will see outputs like this:
```json
{
  "7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566": "1"
}
```

5. Edit  `data1\brofist.conf`  
Add these lines: 
```ini
masternode=1
masternodeprivkey=7eAKos41o7WgKQDQYGDc2oFmqsHhKfw7zDc9H8sFbHF8SwmQpZZ
```

Example data1\brofist.conf

```ini
listen=1
daemon=1
server=1
rpcuser=pew
rpcpassword=password
rpcallowip=127.0.0.1
maxconnections=30
rpcport=12131
bind=192.168.1.44:11113
addnode=pew.overemo.com
addnode=173.249.41.184
addnode=159.203.186.24
addnode=212.237.25.226
addnode=51.15.61.35
addnode=173.249.9.82
addnode=104.168.87.183
addnode=35.203.57.179
addnode=104.197.130.51
addnode=45.77.227.85
masternode=1
masternodeprivkey=7eAKos41o7WgKQDQYGDc2oFmqsHhKfw7zDc9H8sFbHF8SwmQpZZ

```

***change masternodeprivkey with the key from step 3.**

6. Edit  `data1\masternode.conf`  
`masternode.conf` is a space separated text file. Each line consists of an alias, IP address followed by port, masternode private key, collateral output transaction id and collateral output index.
Add this line:
```
master 173.249.1.1:11113 7eAKos41o7WgKQDQYGDc2oFmqsHhKfw7zDc9H8sFbHF8SwmQpZZ 7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566 1

```

_Note: Change IPs 173.249.1.1 to your VPS IPs 
_Note: Change 7eAKos41o7WgKQDQYGDc2oFmqsHhKfw7zDc9H8sFbHF8SwmQpZZ  with outputs from step 3.
_Note: Change 7603c20a05258c208b58b0a0d77603b9fc93d47cfa403035f87f3ce0af814566 1  with outputs from step 4.

### 6. Restart Masternode
You must wait for 15 confirmations of transection.

```bash
./stop.sh 1 
./start.sh 1
sleep 10
./cli.sh 1 masternode start-all
./cli.sh 1 masternode start

```

You can setup another node by replacing 1 with another number.
* The config files of masternode no.2 will be stored at `data2\brofist.conf` 

Controlling the masternode
==========================

### 1. Reindex
```bash
./stop.sh 1 
./start.sh 1 -reindex
```

### 2. Restart Masternode
```bash
./restart.sh 1 
```
_Note: After restart masternode, you need to wait 6-10 hours for getting the first reward.


Donate
========
### If this guide is useful for you, please donate at:
* BROFIST PEW : PAPdawvecLvc3MWqcSTpQ541jcS4uv3hYe
* DOGE : DDfQSen7rkXvtmUUm1PUXZhA68hquTFSGg
* LTC : LKzFet22xZvJ7GFypnSn2ncCgT6GSm4hao
* ONEX : XN9BPdSTgfwjekpt8Z2yhZH7gHkrQHQ68q
