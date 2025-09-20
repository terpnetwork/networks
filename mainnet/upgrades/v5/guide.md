# Terp-Core v5 - Eudesmol Upgrade

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `morocco-1`                                                  |
| Upgrade Version | `v5`                                                     |
| Upgrade Height  | `14154953`                                                    |

The target block for this upgrade is `14154953`, which is expected to arrive at 11:00UTC Monday, September 28th ~ 1 PM UTC [Go Playground](https://go.dev/play/p/_sLXYhtcPGn)

## Building Manually

```sh
cd terp-core
cd terp-core && git pull && git checkout v5.0.0
make build && make install 

terpd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# commit:  
# cosmos_sdk_version: v0.53.4
# version: 5.0.0

mkdir -P $DAEMON_HOME/cosmovisor/upgrades/v5/bin && cp $HOME/go/bin/terpd $DAEMON_HOME/cosmovisor/upgrades/v5/bin 

$DAEMON_HOME/cosmovisor/upgrades/v5/bin/terpd version
```

## Downloading Precompiled Build

```sh
rm -rf terpd_linux_amd64.tar.gz # delete if exists
wget https://github.com/terpnetwork/terp-core/releases/download/v5.0.0/terpd-linux-amd64.tar.gz
sha256sum terpd-linux-amd64.tar.gz
# Output     terpd-linux-amd64.tar.gz
```
