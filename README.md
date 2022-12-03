The aim here is to streamline the creation and signing/broadcasting of multisig tx for OSL **THIS IS A WIP**

```
#This defines the multisig account number and sequence, pulls the tx file from the repo, autofills the current correct sequence and signs it and outputs to file. 
#From there you can either push the file to the repo or just manually enter it however you want.

AC=$(osmosisd q account osmo1rsc56qdxmkdequ4y00900xrf24xdkqzv8ap5ln -o json | jq .account_number -r) 
SQ=$(osmosisd q account osmo1rsc56qdxmkdequ4y00900xrf24xdkqzv8ap5ln | awk -F: '$1=="sequence"{print $2/1}') 
curl https://raw.githubusercontent.com/osmo-support-lab/transactions/<TXDIR>/<TXNAME>.json -o <TXNAME>.json 
osmosisd tx sign <TXNAME>.json --from <YOURKEYNAME> --multisig osmo1rsc56qdxmkdequ4y00900xrf24xdkqzv8ap5ln --chain-id osmosis-1 -s $SQ -a $AC --offline --output-document <TXNAME>-<YOURNAME>.json
```
