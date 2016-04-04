![Truffle and Metamask](http://i.imgur.com/hivuwcF.gif)
If you're interested in building web apps with [the Ethereum blockchain](https://www.ethereum.org/), you may have found [the Truffle web framework](http://truffle.readthedocs.org/en/latest/) to be a nice fit for your needs.

For many types of Dapps (Distributed Apps), Truffle does everything you could want:  It compiles your blockchain contracts, injects them into your web app, and can even run a test suite against them!

This is all great for you, but *what about your users?* Truffle has some great defaults for users who are willing to run a local [Ethereum JSON RPC server](https://github.com/ethereum/wiki/wiki/JSON-RPC) on their computer, but what about your users who just want to sign on and get started?

With Metamask, all your users need to do is [install our Chrome plugin](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?authuser=2), and they will have their own secure blockchain accounts right there in the convenience of their browsers.

![metamask accounts](http://i.imgur.com/oyAvIXZ.png)

Metamask is just a Developer Preview right now, and has not been released to the general public. We don't recommend putting serious funds in it, but instead encourage you to use it to help prepare your dapps for Ethereum browsers.

It's possible your Truffle Dapp is already compatible with Metamask, but if you're like me, you want to go through your project and see what it's like from your user's perspective.

Just in case you haven't used Truffle before, I'm going to start by describing how to scaffold a minimal Truffle dapp. If you already have one set up, feel free to jump ahead to [Setting up Metamask](./#settingupmetamask).

####Installing Truffle Dependencies

You're going to need to have installed [node.js](https://nodejs.org/).

From there, you need to install truffle (`npm install -g truffle`).

Also, you're going to need to run a local blockchain RPC server to test and develop against. I recommend using [testrpc](https://github.com/ethereumjs/testrpc), which you install by running `npm install -g ethereumjs-testrpc`.

Next let's make sure we have our `testrpc` running in the background.  Open your terminal and run the command `testrpc`. That's all!  It runs on port `8545` by default, just like most Ethereum RPCs, and so does Truffle.

####Setting up a simple Truffle Dapp

Next, let's generate a basic Truffle dapp. The default result of `truffle init` is a simple example currency.

To get it up and running, run these commands:
```
mkdir my-money  # Create a folder for your new dapp
cd my-money     # Move into that folder
truffle init    # Initialize a default truffle project in that folder
truffle build   # Compile the dapp
truffle deploy  # Publish the dapp on the blockchain
truffle serve   # Host your web interface on port 8080
```
We just deployed a simple alt-coin called `MetaCoin` to our local blockchain, and it's available to our browser on `http://localhost:8080`!

![MetaCoin default](http://i.imgur.com/Uou5raY.png)

If you visit it, you'll see that by default this new Dapp template signs you in with the first account on your `testrpc` account list, which happens to be the same account that got pre-populated with 10k shiny new Metacoins! That's because when you ran `truffle deploy`, Truffle used your first account as the contract publisher, and the contract says to fund the creator's account with 10k coins.

You can now send those coins to any account you want, for example, the second account in your `testrpc` list! If you enter an address and a value, and hit send, you'll see your balance go down!

If that seems a little too easy, I'd agree with you! That's why Metamask gives the user an opportunity to approve every transaction that a Dapp attempts, and that's more secure!

Let's try connecting to the same account through Metamask, and see how easy it is!

####Setting up Metamask

Now you'll want to install [Metamask from the Chrome store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?authuser=2).

*Metamask is currently not listed on the Chrome store, but you get that link because you're an early adopter who we want to support.*

When you first open Metamask, it will let you either create a new wallet *or* restore from a seed. Since both Metamask and `testrpc` use the [bip44 standard](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) for wallet generation, you can `Restore Existing Vault`, and enter the `Mnemonic` that `testrpc` output when you first started it. It should be 12 words long.

You'll also need to provide a password, which is used to encrypt your wallet.

By default you get three accounts, and they'll be the same as the first three accounts in your `testrpc` list.

To use Metamask with your `testrpc` accounts, you need to point it at your `testrpc` address as its RPC provider..

![setting metamask testrpc](http://i.imgur.com/D6o2Jq8.png)

  1. Open Metamask
  2. Click the gear icon in the bottom left
  3. Enter your `testrpc` address into the RPC field. It's probably `http://localhost:8545/`.

Metamask will close at this point to restart itself.

You can now sign into the dapp with Metamask.

 1. Open Metamask
 2. Enter your password
 3. Reload the Dapp page (some dapps will notice when you change accounts, but this basic one doesn't)

You should now see your first account's MetaCoin balance! If you switch accounts, you should see theirs (none, unless you've sent to one!).

To send some Metacoin to one of your Metamask accounts, you're going to need that account's address.

To copy a Metamask account's address:

 1. Open Metamask
 2. Click the details arrow next to the account whose address you want.
 3. Click the "Copy Address" button.

You now you have a copy of your address to send to!

####Sending Metacoin from Metamask: So Meta!

If you connect to your first account, you should see you have some MetaCoin, and if we look in our Metamask plugin, we should have some ether too!

It's important that we have ether, because it's not only a currency for trade, it's also the currency for processing transactions on the Ethereum blockchain. This processing fee is referred to as "gas".

Let's try sending some Metacoin from one of our Metamask accounts to another.

First select the account that has the Metacoin and Ether. Now click the details arrow for another account, and copy its address (`COPY ADDR`).

![Metamask account detail view](http://i.imgur.com/5vbrfuQ.png)

Paste the address into the Dapp's `To` field, along with how much Metacoin you'd like to send, and hit `send`!

You should see a notification pop-up, notifying you that you have a transaction to approve in Metamask.

![Approval notification](http://i.imgur.com/pRuKb9v.png)

You can either click "Approve" on the notification, or open the Metamask pop-up and review the transaction there.

This is one way that Metamask is a safer Ethereum browsing experience than running your own RPC. While a pre-authenticated RPC automatically approves all requests sent to it, Metamask gives the user an opportunity to review and approve or reject each transaction that's requested by the dapp. Long term, making transactions easy to intelligently review is an important priority for Ethereum developers.

####Wrapping Up

This has been a simple example, but hopefully shows how Truffle and Metamask work together. They are able to pretty much work out of the box! That's because Truffle helps you write [web3](https://github.com/ethereum/wiki/wiki/JavaScript-API)-compliant dapps. Web3 is a Javascript API declared by the core Ethereum team, and Metamask injects it directly into the Dapp's context!

This makes connecting to a Truffle Dapp with Metamask as easy as connecting with your own RPC, but it's **a lot** easier for your users.

That's because Metamask is a hyper-light client that doesn't replicate the entire blockchain locally, but it *does* let users manage their own accounts, so they can casually benefit from the security of private key management, while placing trust for block validation on Metamask's configured RPC provider.

We hope this has been a useful introduction to developing with Truffle and Metamask!

Please, leave a comment or question, [start a discussion on github](https://github.com/metamask/talk/issues), or [Tweet at us on Twitter](https://twitter.com/metamask_io). We're trying to make Metamask the easiest tool to let anyone benefit from using Distributed Apps on the Ethereum Blockchain.
