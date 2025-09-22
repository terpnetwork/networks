# Terp-Core v5 - Eudesmol Upgrade

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `morocco-1`                                                  |
| Upgrade Version | [`v5`](https://github.com/terpnetwork/terp-core/releases/tag/v5.0.0)                                                  |
| Upgrade Height  | [`14170662`](https://ping.pub/terp/block/14170662)                                                    |

The target block for this upgrade is `14170662`, which is expected to arrive at 11:00UTC Monday, September 30th ~ 1 PM UTC [Go Playground](hthttps://go.dev/play/p/cyxyYqhGtRp)

## Building Manually

```sh
cd terp-core
cd terp-core && git pull && git checkout v5.0.0
make build && make install 

terpd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# commit:  1620a3086cef50a3e3acb592469b0ebad3981a3e
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
# Output  768b281a522bdff2781cc7c11177f756f44526e6e3388e8febb8a347481d0870 terpd-linux-amd64.tar.gz
```
