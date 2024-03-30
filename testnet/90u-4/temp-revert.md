## Temporary Fallback 

in your `terp-core` folder:
```sh
# fetch the v4.1.testnet version
git checkout v4.1.testnet
```

build the new binary: 
```sh
make install
```

confirm binary is installed:
```sh
terpd version 
# should return: 
# commit: 4756161c4cb9993a12c33c40121862224a3e1eaa
# cosmos_sdk_version: v0.47.5
# go: go version go1.21.
# server_name: terpd
# version: 4.1.testnet
```

reset current state on your node. Make sure to backup your private-keys if your node is a validator and you want to be certain your keys are safe. 
```sh
terpd tendermint unsafe-reset-all
```

download previous genesis-file
```sh
wget -O $HOME/.terp/config/genesis.json https://raw.githubusercontent.com/terpnetwork/networks/main/testnet/90u-2/genesis.json
```

download the previous state snapshot (make sure you have `lz4` installed or this will error)
```sh
curl https://testnet-files.itrocket.net/terp_backup/snap_terp.tar.lz4 |lz4 -dc - | tar -xf - -C $HOME/.terp
```

setup peers & rpc 
```sh
SNAP_RPC="https://terp-testnet-rpc.itrocket.net:443"
peers="51d48be3809bb8907c1ef5f747e53cdd0c9ded1b@terp-testnet-peer.itrocket.net:13656,57d7ad4f7d482655c497ca61378df8333868d0a4@testnet-peer.terp.network:26656" 
```
add peers to `config.toml`
```sh
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.terp/config/config.toml 
```

your node should now be ready to be configure to 90u-2 again. make sure you reset your global config if you do so:
```sh
terpd config chain-id 90u-2
```
