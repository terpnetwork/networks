# Terp-Core v4.1.testnet - Farnesene Upgrade

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `morocco-1`                                                  |
| Upgrade Version | `v4.1.0`                                                     |
| Upgrade Height  | `3698609`                                                    |



The target block for this upgrade is `3698609`, which is expected to arrive at 11:00UTC Monday, November 4th.. [Go Playground](https://go.dev/play/p/FNuKg0bbwyr)

### Building Manually:
```
cd terp-core
cd terp-core && git pull && git checkout v4.1.0
make build && make install 

terpd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# commit: 
# cosmos_sdk_version: v0.47.5
# version: 4.1.0

mkdir -P $DAEMON_HOME/cosmovisor/upgrades/v4_1_0/bin && cp $HOME/go/bin/terpd $DAEMON_HOME/cosmovisor/upgrades/v4_1_0/bin 

$DAEMON_HOME/cosmovisor/upgrades/v4_1_0/bin/terpd version
```
### Downloading Verified Build:
```
rm -rf terpd_linux_amd64.tar.gz # delete if exists
wget https://github.com/terpnetwork/terp-core/releases/download/v4.1.0/terpd-v4.1.0-linux-amd64.tar.gz
sha256sum terpd-v4.1.0-linux-amd64.tar.gz
# Output   terpd-linux-amd64.tar.gz
```