# Terp-Core v3 - Headstash Upgrade

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `90u-2`                                                |
| Upgrade Version | `v4.0.0`                                        |
| Upgrade Height  | `3268929`                                                      |



The target block for this upgrade is `3268929`, which is expected to arrive at 12:00UTC Monday, November 6th.. [Go Playground](https://go.dev/play/p/J_F56gVBWCN)

### Building Manually:
```
cd terp-core
cd terp-core && git pull && git checkout v4.0.0
make build && make install 

terpd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# commit: 
# cosmos_sdk_version: 
# version:

mkdir -P $DAEMON_HOME/cosmovisor/upgrades/v4/bin && cp $HOME/go/bin/terpd $DAEMON_HOME/cosmovisor/upgrades/v4/bin 

$DAEMON_HOME/cosmovisor/upgrades/v4/bin/terpd version
```
### Downloading Verified Build:
```
rm -rf terpd_linux_amd64.tar.gz # delete if exists
wget https://github.com/terpnetwork/terp-core/releases/download/v4.0.0/terpd-v4.0.0-linux-amd64.tar.gz
sha256sum terpd-v4.0.0-linux-amd64.tar.gz
# Output 
```