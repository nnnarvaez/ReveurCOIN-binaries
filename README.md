# ReveurCOIN-binaries
A test CHAIN based on the STEEM blockchain

**CHAIN ID** : 7bbc305bd2af8ca0ac072a6754a24023f66b81229b7ef760b929a91b8a3175c8

**SEED Nodes** : 

```
163.172.25.72:3333
```
**RCP Nodes** : 

```
163.172.25.72:8751
```
## Assets:

* STEEM -> DREAM
* VESTS -> VESTS
* SBD -> REV


You can explore it and see it working on: http://dev.rockdio.org/revex/

#### Accesing it:
* Request an account to play (here or in the STEEMit post: https://steemit.com/utopian-io/@nnnarvaez/exploring-the-economic-model-of-steem-like-blockchains )
* All STEEM libraries work. With just minor modifications 

#### What's next? (Or tasks you can help with)
* Make available a web interface for the Wallet operations based on STEEM Wallet from condenser
* Make the internal market available
* Try to make a simple WEB Interface to allow easier interaction (posting and stuff)
* Would be nice to have a custom Json editor interface to use the chain for other than blogging
 

**TO-DO:** 
* Add files to repo with updated ASSETs for BEEM, STEEM Python, steemJS 
* Submit PR to proper repos with the chain ID and assets




### Purpose / Objetive:
The idea would be to explore the options to improve the understanding of the economical management of the platform and its posible repercussions on price and value.

### Install and deployment

Clone

```
$ git clone https://github.com/nnnarvaez/ReveurCOIN-binaries.git
$ unzip reveurd.zip
```

**NOTE:** If you dont have steemd already, you should probably install the dependencies, don't panic here is the list for humans:
https://github.com/nnnarvaez/ReveurCOIN-binaries/blob/master/dependencies.md

```
$ cd data

``` 
Edit config.ini adding your witness name and active key

You can change the ports to suit your system
```
$ cd ..
$ reveurd -d data
```


You will see a lot of red and it will start receiving pushed blocks 
There is a constant warning of block size too small, it was a failed attemp to avoid writting empty blocks, it is just a warning ignore it, it will be removed in the next release.

# If you dont want to run a full node:

**NOTE:** you can just download the individual files 

* Low memory node and rev_wallet (**to do:**  forgot to add the config.ini to low memory node)
* rev_wallet only

---

**Run the wallet:**

If you are running a witness node:
```
$ rev_wallet -s ws://127.0.0.1:8752
```
Localhost and the port (8752 is the one used in the provided config.ini)

If you are not running a witness node:
```
$ rev_wallet -s ws://163.172.25.72:8752
```


```
set_password superSecure1234
unlock superSecure1234
import_key <yourverylongactivekey>
```
**Declare your witness intention to the network** (Unless you dont want to witness and just want to use your user to play and see)

  ```update_witness <YourWitnessName> "URL of your witness intention" REVpublicKEY {"account_creation_fee": "10.000 DREAM", "maximum_block_size": 131072, "bsd_interest_rate":1000} true```
  

### File contents
```
Archive:  reveurd.zip
 Length   Method    Size  Cmpr    Date    Time   CRC-32   Name
--------  ------  ------- ---- ---------- ----- --------  ----
       0  Stored        0   0% 2019-03-27 17:26 00000000  data/
    3940  Defl:N     1623  59% 2019-03-27 17:22 58196b20  data/config.ini
52026744  Defl:N 12432988  76% 2019-03-26 21:00 00cc7f95  reveurd
16265312  Defl:N  4913914  70% 2019-03-27 17:22 26997562  rev_wallet
--------          -------  ---                            -------
68295996         17348525  75%                            4 files

```
# Todo: 
* Match config.ini used ports to ports in rev_wallet (probably better to have ports different than the original steem B/C)
* Recompile rev_wallet with nice default port values
* ~Reupload single zip file with suggested folder structure~ **done**
* Recompile reveurd in low memory mode

```
  -h [ --help ]                                                                         Print this help message and exit.
  -s [ --server-rpc-endpoint ] [=arg(=ws://127.0.0.1:8090)]                             Server websocket RPC endpoint
  -a [ --cert-authority ] arg (=_default)                                               Trusted CA bundle file for connecting
                                                                                        To wss:// TLS server
  -r [ --rpc-endpoint ] [=arg(=127.0.0.1:8091)]                                         Endpoint for wallet websocket RPC to listen on
  -t [ --rpc-tls-endpoint ] [=arg(=127.0.0.1:8092)]                                     Endpoint for wallet websocket TLS RPC
                                        to listen on
  -c [ --rpc-tls-certificate ] [=arg(=server.pem)]                                      PEM certificate for wallet websocket TLS RPC
  -H [ --rpc-http-endpoint ] [=arg(=127.0.0.1:8093)]                                    Endpoint for wallet HTTP RPC to listen on
  -d [ --daemon ]                                                                       Run the wallet in daemon mode
  --rpc-http-allowip arg                                                                Allows only specified IPs to
                                                                                        connect to the HTTP endpoint
  -w [ --wallet-file ] [=arg(=wallet.json)]                                             wallet to load
  --chain-id arg (=7bbc305bd2af8ca0ac072a6754a24023f66b81229b7ef760b929a91b8a3175c8)    chain ID to connect to
```


# Economy:

Since the platform dilutes he value of VESTs on token emission and it is somehow designed to be SBD centric in its calculations, it is important to provide dynamic ways for the witnesses to act/react to the volatility of SBD and maintain the PEG, this requieres understanding of economic mechanisms from the TOP20. 

Those mechanisms are: SBD Interest Rate / SBD Stop % / Price feed / Price BIAS / Haircut price % 

* Migrate haircut % from hardcoded in database.hpp to a config.hpp
* Migrate both haircut % and SBD stop % to a witness setting es part of the PEG control mechanism (price feed + haircut + SBD_stop) 

### First step: 
add definitions and variables to 
`https://github.com/steemit/steem/blob/master/libraries/chain/include/steem/chain/witness_objects.hpp`
### From there:

- Update operation to set values 
- Update `global property object` adding the changes 
- Update `database.cpp` to take values from `global property object`
- Update `database.cpp` so **Witnesses** can update the `global property object` accordinly 
- Update `steem_evaluator.cpp` to evaluate the operations to set those variables
- Update `condenser_api` plugin and `database_api` plugin so **Witnesses** can update / set those values using http calls



### Friendly reminder:

Discover the purpose of:


```
STEEM_MIN_LIQUIDITY_REWARD

STEEM_START_MINER_VOTING_BLOCK

STEEM_CURATE_APR_PERCENT

STEEM_MIN_BLOCK_SIZE_LIMIT
```
