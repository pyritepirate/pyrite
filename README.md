# <img align="left" width="42" height="42" src="/src/qt/res/icons/pyrite-48.png">1.0.4

[![Build Status](https://travis-ci.org/pyritepirate/pyrite.svg?branch=master)](https://travis-ci.org/pyritepirate/pyrite)

### Pyrite is a fairly launched, 100% decentralized cryptocurrency. Community involvement is encouraged. Pyrite, like most other altcoins, starts as an experiment - a fool's gold.

###  :globe_with_meridians: https://pyrite.pw
###  :mega: https://bitcointalk.org/index.php?topic=5055485
###  :speech_balloon: https://discord.gg/NJajNNx

#### Ticker: PYE
#### Reward Scheme: PoW/PoS Hybrid
#### PoW Mining Algorithm: Sha256q
#### PoW Block Reward: 88 Coins
#### PoS Block Reward: 0 Coins + Fees
#### Block Time: 10 Minutes (*effectively 5 minutes, since PoW and PoS blocks are targeted at 10 minutes*)
#### Block Maturity: 200 Blocks
#### Block Halving: Every 105120 Blocks
#### Max supply: 10 Million*
#### P2P Port: 6996
#### RPC Port: 6997
:heavy_exclamation_mark:_*Max supply approximation is based on the assumption that ratio of PoW to PoS blocks remains 50:50._
### Building instructions for Ubuntu

#### Install dependencies for QT wallet:

1. `$ sudo apt-get install git qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools build-essential libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libdb++-dev libminiupnpc-dev libqrencode-dev`
    
2. `$ git clone https://github.com/pyritepirate/pyrite.git`

3. `$ cd pyrite`

4. `$ qmake`

5. `$ make`

#### Install dependencies for headless client:

1. `$ sudo apt-get install git build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev libminiupnpc-dev`

2. `$ git clone https://github.com/pyritepirate/pyrite.git`

3. `$ cd pyrite/src`

4. `$ make -f makefile.unix`
