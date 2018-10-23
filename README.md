About the coin

Name: Pyrite 
Ticker: PYE
Reward scheme: PoW/PoS hybrid 
PoW mining algorithm: sha256q (ASICs won't work)
Block reward: 88 coins (PoS blocks are 0 reward + mempool fees)
Block time: 10 minutes (effectively 5 minutes, since PoW and PoS blocks are targeted at 10min)
Block maturation: 200 blocks
Block halving: Every 105120 blocks (approximately 1 year)
Max supply: 21 million (approximate)
P2P Port: 6996 
RPC Port: 6997

addnode=45.56.162.94
addnode=193.29.56.246

Building instructions for Ubuntu 16.04

Install dependencies for QT wallet:

1. sudo apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools \
    build-essential libboost-dev libboost-system-dev \
    libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev \
    libssl-dev libdb++-dev libminiupnpc-dev libqrencode-dev

2. cd pyrite
3. qmake 
4. make

Install dependencies for headless client:

1. sudo apt-get install build-essential libssl-dev libdb++-dev libboost-all-dev libqrencode-dev  libminiupnpc-dev

2. cd pyrite/src
3. make -f makefile.unix

Mining in wallet:

setgenerate true
