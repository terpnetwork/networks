# Terp-Core v3 - Headstash Upgrade

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Chain-id        | `morocco-1`                                                |
| Upgrade Version | `v3-pigeonfall`                                        |
| Upgrade Height  | `3039061`                                                      |



The target block for this upgrade is `3039061`, which is expected to arrive with 24 hours of Sunday, October 15th.. [Go Playground](https://go.dev/play/p/Q16cRTMICN1)

### Building Manually:
```
cd terp-core
git fetch --tags && git checkout v3-pigeonfall
make build && make install 

terpd version --long | grep "cosmos_sdk_veresion/|commit\|version:"
# cosmos_sdk_version: v0.47.5
# version: 3-pigeonfall

mkdir -P $DAEMON_HOME/cosmovisor/upgrades/v3/bin && mv build/terpd $DAEMON_HOME/cosmovisor/upgrades/v3/bin 

$DAEMON_HOME/cosmovisor/upgrades/v3/bin/terpd version
```
### Downloading Verified Build:
```
wget https://github.com/terpnetwork/terp-core/releases/download/v3-pigeonfall/terpd-v3.0.0-pigeonfall-amd64
sha256sum terpd_linux_amd64
# Output 
```