### In order to synchronize your node in the `nolus-rila` network, you can use our snapshots. 
### They are updated every 8 hours. Instructions are given below:

#### 1. Stop nolusd service and delete database

```bash
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/priv_validator_state.json
nolusd tendermint unsafe-reset-all --home $HOME/.nolus
```

#### 2. Download snapshot

```bash
wget http://207.180.238.180/nolus/data_nolus-rila.tar
wget http://207.180.238.180/nolus/wasm_nolus-rila.tar
tar -xf data_nolus-rila.tar -C $HOME/.nolus/data/
mkdir $HOME/.nolus/wasm/
tar -xf wasm_nolus-rila.tar -C $HOME/.nolus/wasm/
rm data_nolus-rila.tar
rm wasm_nolus-rila.tar
```

#### 3. Restore your priv_validator_state.json file

```bash
mv $HOME/priv_validator_state.json $HOME/.nolus/data/priv_validator_state.json
```

#### 4. Restart nolusd service and open journal

```bash
sudo systemctl restart nolusd
sudo journalctl -u nolusd -f -o cat
```
