# Pixels Camp 2019: Aptoide / AppCoins 

## DEV Example 
For PROD use https://apichain.blockchainds.com instead

### Generate Wallet[Generate Wallet](#generate-wallet)
```sh
curl https://apichain-dev.blockchainds.com/transaction/generate
{
  "wallet": "0xd68b4cD23D2849Aa715372170cc434850A005ac3",
  "private_key": "0x74bbb090d3fd29487ba4d6bb16e202d860008519558bbcecd3a6c76df6387964"
}
```

### Check Wallet History - No Tx Received
```sh
curl https://apichain-dev.blockchainds.com/appc/wallethistory?wallet=0xd68b4cD23D2849Aa715372170cc434850A005ac3
{
  "result": []
}
```

### Check Wallet History - Two Tx Received (amount is in Wei, 1 APPC = 10^18 Wei)
```sh
curl https://apichain-dev.blockchainds.com/appc/wallethistory?wallet=0xd68b4cD23D2849Aa715372170cc434850A005ac3
{
  "result": [
    {
      "TxID": "0x44a138c3c47883fe042994ebce86927b78024ef91aceab5106cabb6809edb02a",
      "amount": 1000000000000000000,
      "block": 0,
      "icon": "https://apichain.blockchainds.com/icons/peer_copy.png",
      "receiver": "0xd68b4cd23d2849aa715372170cc434850a005ac3",
      "sender": "0x4fbcc5ce88493c3d9903701c143af65f54481119",
      "ts": "2019-03-13 15:57:01+0000",
      "type": "Transfer OffChain"
    },
    {
      "TxID": "0x836932835b5374226035bd6e150a962f16c8d5b099bf8486ba1d1f2f29ea4b19",
      "amount": 1000000000000000000,
      "block": 0,
      "icon": "https://apichain.blockchainds.com/icons/peer_copy.png",
      "receiver": "0xd68b4cd23d2849aa715372170cc434850a005ac3",
      "sender": "0x4fbcc5ce88493c3d9903701c143af65f54481119",
      "ts": "2019-03-13 15:53:49+0000",
      "type": "Transfer OffChain"
    }
  ]
}
```

### Check Wallet History - Wrong Arguments
```sh
curl https://apichain-dev.blockchainds.com/appc/wallethistory
{
  "message":"You must provide valid ethereum addresses",
  "status":"ERROR"
}
```

### Check Wallet Nonce
```sh
curl https://apichain-dev.blockchainds.com/transaction/nonce?wallet=0xd68b4cD23D2849Aa715372170cc434850A005ac3
{
  "nonce": 0,
  "wallet": "0xd68b4cD23D2849Aa715372170cc434850A005ac3"
}
```

### Check Wallet Nonce - Wrong Arguments
```sh
curl https://apichain-dev.blockchainds.com/transaction/nonce
{
  "message": "Not a valid wallet address",
  "status": "INVALID_WALLET"
}
```

### Sign A Message (signer == wallet)
```sh
curl "https://apichain-dev.blockchainds.com/transaction/sign?message=0&private_key=0x74bbb090d3fd29487ba4d6bb16e202d860008519558bbcecd3a6c76df6387964"
{
  "signature": "0x8b9c1b0bc5dc4fdc94769b580a64d1e96850355344b5d1cbb8a2bd843740be44352460d0e78421a73f0aa7d2162bd36eb61c40870c711e6a63a071499c40ae9a1b",
  "signer": "0xd68b4cD23D2849Aa715372170cc434850A005ac3"
}
```

### Sign A Message (signer == wallet) - Wrong Arguments
```sh
curl https://apichain-dev.blockchainds.com/transaction/sign?message=0
{
  "message": "Not a valid ethereum key",
  "status": "INVALID_KEY"
}
```

### Verify A Message (signer == wallet)
```sh
curl "https://apichain-dev.blockchainds.com/transaction/verify?message=0&signature=0x8b9c1b0bc5dc4fdc94769b580a64d1e96850355344b5d1cbb8a2bd843740be44352460d0e78421a73f0aa7d2162bd36eb61c40870c711e6a63a071499c40ae9a1b"
{
  "signer": "0xd68b4cD23D2849Aa715372170cc434850A005ac3",
}
```

### Verify A Message (signer == wallet) - Wrong Arguments
```sh
curl https://apichain-dev.blockchainds.com/transaction/verify?message=0
{
  "message": "Not a valid ethereum signature",
  "status": "INVALID_SIGNATURE"
}
```

### Send APPC Credits
```sh
curl -X POST https://apichain-dev.blockchainds.com/transaction/transfer -d "sender=0xd68b4cD23D2849Aa715372170cc434850A005ac3&receiver=0x4fbcc5ce88493c3d9903701c143af65f54481119&amount=2&signature=0x8b9c1b0bc5dc4fdc94769b580a64d1e96850355344b5d1cbb8a2bd843740be44352460d0e78421a73f0aa7d2162bd36eb61c40870c711e6a63a071499c40ae9a1b"
{
  "status": "COMPLETED",
  "txid": "0xa6999904e1a6c85e3a58d3905e5642ee7f3370e8eb50dc249f62765cabf224e3"
}
```

### Send APPC Credits - Wrong Arguments
```sh
curl -X POST https://apichain-dev.blockchainds.com/transaction/transfer -d "amount=-2"
{
  "message": "Invalid Input Parameters",
  "status": "ERROR"
}
```

### Send APPC Credits - Invalid Signature
```sh
curl -X POST https://apichain-dev.blockchainds.com/transaction/transfer -d "sender=0xd68b4cD23D2849Aa715372170cc434850A005ac3&receiver=0x4fbcc5ce88493c3d9903701c143af65f54481119&amount=2&signature=0x8b9c1b0bc5dc4fdc94769b580a64d1e96850355344b5d1cbb8a2bd843740be44352460d0e78421a73f0aa7d2162bd36eb61c40870c711e6a63a071499caaaaaaaa"
{
  "message": "You must provide a valid signature",
  "status": "INVALID_SIGNATURE"
}
```

### Send APPC Credits - Not Enough Funds
```sh
curl -X POST https://apichain-dev.blockchainds.com/transaction/transfer -d "sender=0xd68b4cD23D2849Aa715372170cc434850A005ac3&receiver=0x4fbcc5ce88493c3d9903701c143af65f54481119&amount=200&signature=0x8b9c1b0bc5dc4fdc94769b580a64d1e96850355344b5d1cbb8a2bd843740be44352460d0e78421a73f0aa7d2162bd36eb61c40870c711e6a63a071499c40ae9a1b"
{
  "message": "Not enough funds",
  "status": "REJECTED"
}
```
