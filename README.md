### Token Mining Pool  

Developed by the 0xBitcoin Community

(GNU PUBLIC LICENSE)

A pool for mining ERC20/EIP918 Tokens


Windows GPU Miner 1
https://bitbucket.org/LieutenantTofu/cosmic-v3/downloads/COSMiC-v4.1.1-MultiGPU-TMP.zip

Windows GPU Miner 2
 https://github.com/mining-visualizer/MVis-tokenminer/releases

 Windows GPU Miner 3
 https://github.com/lwYeo/SoliditySHA3MinerUI/releases/tag/1.0.2

 Linux GPU Miner
 https://github.com/lwYeo/SoliditySHA3Miner/releases


### BASIC SETUP  (needs Node8)
1. npm install -g node-gyp
1.1. sudo apt-get install build-essential

You may need to do..
1.2.sudo apt-get install python2.7
1.3.npm config set python python2.7

2. npm install
3. npm run webpack  #(to build the website files)
4. rename 'sample.account.config.js' to 'account.config.js' and fill it with the pool's ethereum account data

5. install redis-server and make sure it is running
6. Edit pool.config.js to your tastes
7. Edit the website files in /app  to change the look of the website
8. npm run server #(or npm run server test for Ropsten test net)


### CONFIGURING  - set up  account.config.js and pool.config.js

##### pool.config.js

var poolconfig = {
  minimumShareDifficulty: 5000,   //lowest miner share difficulty
  maximumShareDifficulty: 10000    //highest miner share difficulty
  solutionGasPriceWei: 10,   //ether paid by the pool for each mint
  transferGasPriceWei: 6,   //ether paid by the pool for each payment
  poolTokenFee: 5,     //percent of tokens the pool keeps for itself
  communityTokenFee: 2,   //percent of tokens the pool pledges to donate
  minBalanceForTransfer: 1500000000,   
  payoutWalletMinimum: 100000000000,
  allowCustomVardiff: true,
  web3provider: "http://127.0.0.1:8545"   //point at Geth or remove to use Infura
}


###### deployedContractInfo.json    found in app/assets/contracts
EDIT THIS FILE!!!

Replace 'mintforwarder' with your own deployed version of the contract !!!
Replace 'batch payments' contract as well !!! your own deployed contract !!
replace 'DoubleKingsReward' with your own deployed contract !

YOU DO NOT have to replace/redeploy the MiningKing contract as this is 'global' and for everyone


### HOW TO USE
1. Point a poolminer at your pool using http://localhost:8586  (or ipaddress:8586 or domain.com:8586)  (make sure firewall allows this port)
2. View website interface at http://localhost:3000 (you can set up nginx to serve the static files in /public)



## Installing MongoDB

https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04#step-3-%E2%80%94-adjusting-the-firewall-(optional)


## Installing Redis  
  1. sudo apt-get install redis
  2. sudo service redis-server start

   - Redis will serve/connect at localhost:6379 by default - the pool will use this port


   https://stackoverflow.com/questions/19581059/misconf-redis-is-configured-to-save-rdb-snapshots?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa




   redis-cli
   config set stop-writes-on-bgsave-error yes

   cron job to clean redis
   30 6 1 * * /home/andy/.nvm/versions/node/v8.9.4/bin/node /home/andy/deploy/tokenpool/clean-redis.js


## Redis Commands





## TODO / BUGS
- Add more clustering/workers and more JSONRPC/socket ports to handle heavy loads

#### MINT HELPER
- Tell miner to mine using ethaddress of the mint helper
- Submit mints to the minthelper instead of the actual token smart contract





*** The balance_transfers can get the wrong TXID in them!! need to store a record for EACH one or wait longer or implement mikers batching



** wipe out total_pool_hashrate with script (redis)
