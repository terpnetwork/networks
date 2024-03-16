# Upgrade Terp Network from v4.1.1 to v4.2.0

This upgrade follows the state export the network, so that we are using the same terpd version on the testnet as the mainnet.

### Release Details
* Go version has been frozen at `1.21`. If you are going to build `terpd` binary from source, make sure you are using the right GO version!

# Performing the co-ordinated upgrade

This co-ordinated upgrades requires validators to stop their validators at `halt-height`, remove all data from the node, download the new genesis file, and restart the node service.

The exact sequence of steps depends on your configuration. Please take care to modify your configuration appropriately if your setup is not included in the instructions.

# Manual steps

## Step 1: Configure `halt-height` and restart the node.

This upgrade requires `terpd` halting execution at a pre-selected `halt-height`. Failing to stop at `halt-height` may cause a consensus failure during chain execution at a later time.

### Option 1: Set the halt height by modifying `app.toml`

* Stop the terpd process.

* Edit the application configuration file at `~/.terp/config/app.toml` so that `halt-height` reflects the fork plan:

```toml
# Note: Commitment of state will be attempted on the corresponding block.
halt-height = TBD
```
* restart terpd process

* Wait for the upgrade height and confirm that the node has halted

* Remove existing data

* Download the new genesis file [here](https://raw.githubusercontent.com/terpnetwork/networks/main/testnet/90u-3/genesis.json)

### Build and start the binary

```shell
cd $HOME/terp-core
git pull
git fetch --tags
git checkout v4.2.0
make install

# verify install
terpd version
# v4.2.0
```

```shell
terpd start # starts the v4.2.0 node
```

## Cosmovisor steps

### Prerequisite: Alter systemd service configuration

Disable automatic restart of the node service. To do so please alter your `terpd.service` file configuration and set appropriate lines to following values.

```
Restart=no 

Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=false"
```

After that you will need to run `sudo systemctl daemon-reload` to apply changes in the service configuration.

There is no need to restart the node yet; these changes will get applied during the node restart in the next step.

# Setup Cosmovisor
## Create the updated terpd binary of v4.2.0

### Go to terpd directory if present else clone the repository

```shell
   git clone https://github.com/terpnetwork/terp-core.git
```

### Check the new terpd version, verify the latest commit hash
```shell
   $ terpd version --long
   name: terpd
   server_name: terpd
   version: 4.2.0
   commit: <commit-hash>
   ...
```

### Or check checksum of the binary if you decided to download it

```shell
$ shasum -a 256 terpd-v4.2.0-linux-amd64
<checksum>  terpd-v4.2.0-linux-amd64
```

## Copy the new terpd (v4.2.0) binary to cosmovisor current directory
```shell
   cp $GOPATH/bin/terpd ~/.terpd/cosmovisor/current/bin
```

## Restore service file settings

If you are using a service file, restore the previous `Restart` settings in your service file: 
```
Restart=On-failure 
```
Reload the service control `sudo systemctl daemon-reload`.

# Revert `terpd` configurations

Depending on which path you chose for Step 1, either:

* Reset `halt-height = 0` option in the `app.toml` or
* Remove it from start parameters of the terpd binary and start node again