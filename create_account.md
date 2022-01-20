## Create an Account/Wallet
 This assumes you've gone though the setup [here](README.md). Now we'll create a wallet where the keypair is stored on our local machine. This will all use devnet so double check you're on devnet. Below, make sure that the `RPC URL` and `WebSocket URL` are on `devnet` not `mainnet`.
 
 ```
 solana config get
Config File: /Users/jscott/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: /Users/jscott/.config/solana/id.json
Commitment: confirmed
```

 We skip the BIP39 password below since it's just a test.

```
> solana-keygen new
Generating a new keypair

For added security, enter a BIP39 passphrase

NOTE! This passphrase improves security of the recovery seed phrase NOT the
keypair file itself, which is stored as insecure plain text

BIP39 Passphrase (empty for none):

Wrote new keypair to /Users/jscott/.config/solana/id.json
========================================================================
pubkey: G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q
========================================================================
Save this seed phrase and your BIP39 passphrase to recover your new keypair:
here are some words that are your actual seed phrase which you should never give to anyone
========================================================================
```

This is our Account, commonly referred to as a wallet. Let's get the public address and then view it on the Solana Block Explorer

```
solana-keygen pubkey /Users/jscott/.config/solana/id.json
G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q
```
Let's take a look on the block explorer [here](https://explorer.solana.com/address/G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q?cluster=devnet)

### Fund the account

Now let's airdrop some SOL into our wallet. On devnet, we can just do this ourselves and send SOL to our wallet.

```
> solana airdrop 1
Requesting airdrop of 1 SOL

Signature: dZcHW3TNGEtTATse79u6divZndL15Ka7sR3afcasSjokDdPQ4vAQDKcZBJgKQsGv9dA3yovctUwRmRdBySThDg4

1 SOL
```
Now we have 1 SOL, probably nothing. 

We can check our account on the explorer and see that we now have 1 SOL funded in the account and a transaction in our history. We can [view details](https://explorer.solana.com/tx/dZcHW3TNGEtTATse79u6divZndL15Ka7sR3afcasSjokDdPQ4vAQDKcZBJgKQsGv9dA3yovctUwRmRdBySThDg4?cluster=devnet) of the transaction (shown at the bottom of account page) as well.

## Second Wallet
Let's create an additional wallet and transfer tokens between the wallets and then display the public key (wallet address).

```
> solana-keygen new --outfile second-wallet-keypair.json
 ... similar output as above (seed phrase/public wallet key)
> solana-keygen pubkey second-wallet-keypair.json
BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR
```

Checking on [Solana Explorer](https://explorer.solana.com/address/BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR?cluster=devnet) we see that we have an empty wallet. Let's send some SOL from our first wallet to the newly generated one.

```
solana transfer --from ~/.config/solana/id.json second-wallet-keypair.json 1 --allow-unfunded-recipient

Signature: 34M38y6S1bxvy3ueUzeUW7mBkyDqe9Y6Fs2ZQNXRXst6mwzsid938D9VqGHu77HtFSzULRExcifqkjnfcJTBNBWh
```

On the [block explorer](34M38y6S1bxvy3ueUzeUW7mBkyDqe9Y6Fs2ZQNXRXst6mwzsid938D9VqGHu77HtFSzULRExcifqkjnfcJTBNBWh) we note that this is a transaction whereas the other links we viewed were Accounts. At the bottom (Account inputs) we note that our first account was debited `-◎1.000005` SOL, with `◎0.000005` taken as the transaction fee.

