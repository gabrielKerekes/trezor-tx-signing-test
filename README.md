## Create certificates

```
cardano-cli stake-address registration-certificate \
  --stake-script-file pub_key.script \
  --out-file registration.cert

cardano-cli stake-address deregistration-certificate \
  --stake-script-file pub_key.script \
  --out-file deregistration.cert

cardano-cli stake-address delegation-certificate \
  --stake-script-file pub_key.script \
  --stake-pool-id f61c42cbf7c8c53af3f520508212ad3e72f674f957fe23ff0acb4973 \
  --out-file delegation.cert
```

## Create tx body

```
cardano-cli transaction build-raw \
  --tx-in "3b40265111d8bb3c3c608d95b3a0bf83461ace32d79336579a1939b3aad1c0b7#0" \
  --tx-out "addr1q84sh2j72ux0l03fxndjnhctdg7hcppsaejafsa84vh7lwgmcs5wgus8qt4atk45lvt4xfxpjtwfhdmvchdf2m3u3hlsd5tq5r+2000000+7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.testCoin" \
  --fee 42 \
  --invalid-before 47 \
  --invalid-hereafter 10 \
  --certificate-file registration.cert \
  --certificate-script-file pub_key.script \
  --certificate-file deregistration.cert \
  --certificate-script-file pub_key.script \
  --certificate-file delegation.cert \
  --certificate-script-file pub_key.script \
  --withdrawal "stake17y5lkh7542x2m4nsttxgyc7wur7x9mw2ttpcmdvnlmp0nlglpuuef+1000" \
  --withdrawal-script-file pub_key.script \
  --metadata-json-file metadata.json \
  --mint "7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.testCoin+-7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.uestCoin" \
  --mint-script-file policy.script \
  --mary-era \
  --out-file tx.raw
```

```
cardano-cli transaction build-raw \
  --tx-in "3b40265111d8bb3c3c608d95b3a0bf83461ace32d79336579a1939b3aad1c0b7#0" \
  --tx-out "addr1q84sh2j72ux0l03fxndjnhctdg7hcppsaejafsa84vh7lwgmcs5wgus8qt4atk45lvt4xfxpjtwfhdmvchdf2m3u3hlsd5tq5r+2000000+7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.testCoin" \
  --fee 42 \
  --mint "7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.testCoin+-7878754 0d63e8d2c5a00cbcffbdf9112487c443466e1ea7d8c834df5ac5c425.uestCoin" \
  --mint-script-file policy.script \
  --mary-era \
  --out-file tx.raw
```

## Get tx ID

```
cardano-cli transaction txid --tx-body-file tx.raw
```

## Create witnesses

```
cardano-cli transaction witness \
  --tx-body-file tx.raw \
  --signing-key-file keys/1854stake_ext.skey \
  --out-file 1854stake.witness

cardano-cli transaction witness \
  --tx-body-file tx.raw \
  --signing-key-file keys/1854stake_ext.skey \
  --out-file 1854stake.witness

cardano-cli transaction witness \
  --tx-body-file tx.raw \
  --signing-key-file keys/1855mint_ext.skey \
  --out-file 1855.witness
```
