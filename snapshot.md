# Snapshot

> Snapshots allows a new node to join the network by recovering application state from a backup file. Snapshot contains compressed copy of chain data directory. To keep backup files as small as plausible, snapshot server is periodically beeing state-synced.

> Snapshots are updated every 8 hours.

## Instructions

1. Stop the service and remove old data folder
```sh
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/priv_validator_state.json
rm -rf $HOME/.nolus/data
```
2. Download current `data` and `wasm` folders
```sh
curl -L http://94.250.202.17/nolus/data_nolus-rila.tar | tar -xf - -C $HOME/.nolus
curl -L http://94.250.202.17/nolus/wasm_nolus-rila.tar | tar -xf - -C $HOME/.nolus
```
3. Restore your `priv_validator_state.json`
```sh
mv $HOME/priv_validator_state.json $HOME/.nolus/data/priv_validator_state.json
```
4. Restart service
```sh
sudo systemctl restart nolusd && sudo journalctl -u nolusd -f -o cat
```
