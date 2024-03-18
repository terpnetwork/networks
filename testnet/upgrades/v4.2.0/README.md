# Upgrade Terp Network from v4.1.1 to v4.2.0

This upgrade follows the state export the network, so that we are using the same terpd version on the testnet as the mainnet. 

### Release Details
* Go version has been frozen at `1.21`. If you are going to build `terpd` binary from source, make sure you are using the right GO version!

### Exported state 

The snapshot of the state was taken at block height [], by the following command:
```sh
terpd export --height 3578710 --for-zero-height >> 90u-3-export.json
```

removing the logs from the result file, the snapshot's resulting checksum then becomes:
```sh
sha256sum 90u-3-export.json
#  8ef745fcbccbe4fe393a913fa71179e561cab82d45133003d0b454ce33f8d4c3  90u-3-export.json
```

# Performing the co-ordinated upgrade

This co-ordinated upgrades requires validators to stop their validators, remove all data from the node, download the new genesis file, and restart the node service.
The exact sequence of steps depends on your configuration. Please take care to modify your configuration appropriately if your setup is not included in the instructions.

# Manual steps
## Step 1: Backup previous state, restart the node.

backup local node directory
```sh
sudo cp -r $HOME/.terp $HOME/.terp.backup
```

reset local node directory
```sh 
terpd tendermint unsafe-reset-all --home $HOME/.terp
```
download the new genesis file 
```sh
wget -O $HOME/.terp/config/genesis.json https://raw.githubusercontent.com/hard-nett/networks/90u-3/testnet/90u-3/genesis.json
```
configure new peers 
```sh
SEEDS="e3f7a6a37f9b1bc7648603360b24312493c031f1@testnet-peer.terp.network:26656"
PEERS="e3f7a6a37f9b1bc7648603360b24312493c031f1@testnet-peer.terp.network:26656"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.terp/config/config.toml
```

### Build and start the binary

```shell
cd $HOME/terp-core
make install

# verify install
terpd version
# v4.2.0
```

start the new network node
```shell
terpd start # starts the v4.2.0 node
```

if all is well, remove the backup state 
```
rm -rf $HOME/.terp.backup
```