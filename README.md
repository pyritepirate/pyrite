# <img align="left" width="42" height="42" src="/src/qt/res/icons/pyrite-48.png">1.0.5 (Work In Progress - Do Not Use)

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
#### Block Time: 10 Minutes
#### Block Maturity: 200 Blocks
#### Block Halving: Every 105120 Blocks
#### Max supply: 10 Million*
#### P2P Port: 6996
#### RPC Port: 6997
:heavy_exclamation_mark:_*Max supply approximation is based on the assumption that ratio of PoW to PoS blocks remains 50:50._
### Building instructions for Ubuntu

#### Install dependencies for QT wallet:

  `$ sudo apt-get install git qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools build-essential libboost-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libminiupnpc-dev libqrencode-dev`

#### Download and install Berkeley DB 6.2.32:

1. `$ wget http://download.oracle.com/berkeley-db/db-6.2.32.tar.gz`

2. `$ tar -xzvf db-6.2.32.tar.gz && cd db-6.2.32/build_unix`

3. `$ ../dist/configure --enable-cxx --without-shared`

4. `$ make`

5. `$ sudo make install`

4. `$ sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb-6.2.so /usr/lib/libdb-6.2.so`

5. `$ sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb_cxx-6.2.so /usr/lib/libdb_cxx-6.2.so`

#### Clone Pyrite and build QT wallet:

1. `$ git clone https://github.com/pyritepirate/pyrite.git && cd pyrite`

2. `$ qmake`

3. `$ make`

#### Install dependencies for headless client:

   `$ sudo apt-get install git build-essential libssl-dev libboost-all-dev libqrencode-dev libminiupnpc-dev`
   
#### Download and install Berkeley DB 6.2.32:

1. `$ wget http://download.oracle.com/berkeley-db/db-6.2.32.tar.gz`

2. `$ tar -xzvf db-6.2.32.tar.gz && cd db-6.2.32/build_unix`

3. `$ ../dist/configure --enable-cxx --without-shared`

4. `$ make`

5. `$ sudo make install`

4. `$ sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb-6.2.so /usr/lib/libdb-6.2.so`

5. `$ sudo ln -s /usr/local/BerkeleyDB.6.2/lib/libdb_cxx-6.2.so /usr/lib/libdb_cxx-6.2.so`

#### Clone Pyrite and build headless client:

1. `$ git clone https://github.com/pyritepirate/pyrite.git && cd pyrite/src`

2. `$ make -f makefile.unix`
