# ReveurCOIN-binaries
A test CHAIN based on the STEEM blockchain

Clone

`git clone https://github.com/nnnarvaez/ReveurCOIN-binaries.git`

`unzip reveurd.zip` Unzip reveurd.zip

_Make sure all files are in the same directory_
_(Not sure how git will serve them gotta test)_

make a new folder inside folder
move `config.ini` to your new created folder
run `./reveurd -d <newdir>`

### Todo: 
* Match config.ini used ports to ports in rev_wallet (probably better to have ports different than the original steem B/C)
* Recompile rev_wallet with nice default port values
* Reupload single zip file with suggested folder structure
* Recompile reveurd in low memory mode

```
  -h [ --help ]                         Print this help message and exit.
  -s [ --server-rpc-endpoint ] [=arg(=ws://127.0.0.1:8090)]
                                        Server websocket RPC endpoint
  -a [ --cert-authority ] arg (=_default)
                                        Trusted CA bundle file for connecting
                                        to wss:// TLS server
  -r [ --rpc-endpoint ] [=arg(=127.0.0.1:8091)]
                                        Endpoint for wallet websocket RPC to
                                        listen on
  -t [ --rpc-tls-endpoint ] [=arg(=127.0.0.1:8092)]
                                        Endpoint for wallet websocket TLS RPC
                                        to listen on
  -c [ --rpc-tls-certificate ] [=arg(=server.pem)]
                                        PEM certificate for wallet websocket
                                        TLS RPC
  -H [ --rpc-http-endpoint ] [=arg(=127.0.0.1:8093)]
                                        Endpoint for wallet HTTP RPC to listen
                                        on
  -d [ --daemon ]                       Run the wallet in daemon mode
  --rpc-http-allowip arg                Allows only specified IPs to connect to
                                        the HTTP endpoint
  -w [ --wallet-file ] [=arg(=wallet.json)]
                                        wallet to load
  --chain-id arg (=7bbc305bd2af8ca0ac072a6754a24023f66b81229b7ef760b929a91b8a3175c8)
                                        chain ID to connect to
```
