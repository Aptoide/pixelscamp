# Pixels Camp 2019
Aptoide / AppCoins challenge for Pixels Camp

Need help ? [![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/AppCoinsProject/PixelsCamp)


## Challenge 1 - Game on: risk your AppCoins that you can win!

### Description

Every participant of Pixels Camp will have an AppCoins gift card with $5 worth of AppCoins credits.
AppCoins is a [cryptocurrency](https://coinmarketcap.com/currencies/appcoins/) used by Aptoide and other app stores for in-app purchases. [AppCoins credits](https://medium.com/@PauloTrezentos/what-are-appcoins-credits-appc-c-2217e8f8568c) is an easier way to use AppCoins without the need to pay Ethereum gas fees, using smart contracts to register the events in the blockchain and with collateral deposits.

> Aptoide / AppCoins team challenges the Pixels Camp participants to develop a game (any game) where at each round, the participants deposit some AppCoins credits and the winner takes it all.

![Game on: risk your appcoins](Pixels-camp-FG.png?raw=true "Risk your AppCoins!")


The steps would be as follow:

1. **Step 1** - Preparing the game

In the begin of the round of your game, you create a new wallet (ERC20) and ask the participants to transfer AppCoins credits to that wallet. The ammount of AppCoins should be the same among the participants. To make it easier, you can show a QR code with the wallet address, and the participant use their [AppCoins wallet](https://play.google.com/store/apps/details?id=com.appcoins.wallet&hl=en) to scan it and do the transfer.

2. **Step 2** - Waiting for the participants

After a certain time (e.g. 30 seconds), if you have 2 or more deposits, it means you have enough participants and the show can start.

3. **Step 3** - Game on: do your magic

This is the creative part. You can choose a skills or a game of chance.

In a skills game, the participants usually perform some kind of action to achieve a goal. Among skills games are, or instance, [Pong](https://pong-2.com), [Hangman](https://hangmanwordgame.com) or [Dominoes](https://dominoes.playdrift.com).

In a game of chance, the luck plays the main role. Some examples of games of chance are [Dices](https://cardgames.io/yahtzee/) and [Roulette](https://www.roulettesimulator.net).

The game can run in a browser or in a mobile app. Is up to you. In the first case, Pixels camp participants sit around a computer to play. In the second case, someone downloads the app and the players interact with that phone. Each participant needs to have the wallet installed in their phone to do the transfers.

4. **Step 4** - Game over: time to reward the winner

When the game is over, you transfer to the winner the amount of AppCoins credits deposited in the wallet in step 2. If you wish and the participants allow, you can keep a small margin to reward your effort. 
Besides wining Pixels Camp first prize, you go home with a lot of AppCoins credits to use in your favorite games.

What's next ?

Go develop your game and challenge the other Pixels camp participants to spend their AppCoins credits in it. Aptoide / AppCoins team is here to support you on the problems you have.


### Resources

**Step 1 - Preparing the game**

 - Create the wallet [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#generate-wallet) :
   - Endpoint (GET): https://apichain.blockchainds.com/transaction/generate
   - Response:
```sh
{
    wallet=<wallet>,
    private_key=<private_key>
}
```

 - Participants - Wallet installation:
   - AppCoins wallet installation: [Install from Aptoide](https://appcoins-wallet.en.aptoide.com) or [Install from Play](https://play.google.com/store/apps/details?id=com.appcoins.wallet&hl=en_US)
   - Description: After installing the wallet and redeem the Gift card, the participants may go to "Send" option in the navigation bar, and scan the QR code of the game wallet.
   
 **Step 2 - Waiting for the participants**

  - Monitor Wallet transactions [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#check-wallet-history):
    - Website: https://ropsten.appscan.ga/
    - Endpoint (GET): https://apichain.blockchainds.com/appc/wallethistory
    - Parameters: wallet
    - Response:
```sh
{
  "result": [
    {
      "TxID": <txid>,
      "amount": <amount_in_wei>,
      "block": <block>,
      "icon": <icon>,
      "receiver": <receiver>,
      "sender": <sender>,
      "ts": <timestamp>,
      "type": <type>
    },
    ...]
}
```

**Step 4 - Game over: time to reward the winner**

  - Obtain the nonce [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#check-wallet-nonce)
    - Description: Nonce represents the current number of transactions performed by a wallet. This is a relevant info since one has to sign his current nonce and provide that signature to transfer APPC Credits to another wallet.
    - Endpoint (GET): https://apichain.blockchainds.com/transaction/nonce
    - Parameters: wallet
    - Response:
```sh
{
    wallet=<wallet>,
    nonce=<nonce>
}
```

  - Sign [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#sign-a-message)
    - Description: Sign any given message by providing the private_key of the signer wallet
    - Endpoint (GET): https://apichain.blockchainds.com/transaction/sign
    - Parameters: message, private_key
    - Response:
```sh
{
    signer=<signer>,
    signature=<signature>
}
```

  - Verify [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#verify-a-message)
    - Description: Verify if a given signature indeed represents a specific message from a certain signer wallet
    - Endpoint (GET): https://apichain.blockchainds.com/transaction/verify
    - Parameters: message, signature
    - Response:
```sh
{
    signer=<signer>
}
```

  - Transfer (deposits) [+INFO](https://github.com/Aptoide/pixelscamp/blob/master/EXAMPLE.md#send-appc-credits)
    - Description: In order to transfer APPC Credits, the sender has to provide a signature to prove the ownership of that wallet. In order to avoid double spend, that signature can only be valid for one transaction, thus, the sender should sign his current nonce, as message, and provide that signature as an argument on this endpoint.
    - Endpoint (POST): https://apichain.blockchainds.com/transaction/transfer
    - Parameters: sender, receiver, amount, signature
    - Response:
```sh
{
    txid=<txid>,
    status="COMPLETED"
}
```


### Support

Aptoide / AppCoins team is at the event venue and on-line in Gitter to help you to overcome any seatback. Feel free to reach out anytime:

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/AppCoinsProject/PixelsCamp)

