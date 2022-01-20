## Create an SPL Token

 This assumes you've gone though the setup [here](README.md). Now let's create our own SPL Token.

* main SOL account/wallet - G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q 
* token account/wallet - GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24
* token address - 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE
* secondary SOL account/wallet - BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR

### Create the token

 ```
 > spl-token create-token
Creating token 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE

Signature: 2q54pxZrEdJGWz6GHfJAb7KaUoVBd4x5rDpqAMMa95zJ6MCNMsiSjiLGmLmsafbrL55HM5CLA3CwpaxheUFguqfS
 ```

Boom, we have our own token. Let's [take a look](https://explorer.solana.com/address/6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE?cluster=devnet) on the explorer. We see the address of our token, the current supply of 0.0 and the `Mint Authority`. The `Mint Authority` is the main/first wallet we created in the initial tutorial. We can also look at the transaction that created the token [here](https://explorer.solana.com/tx/2q54pxZrEdJGWz6GHfJAb7KaUoVBd4x5rDpqAMMa95zJ6MCNMsiSjiLGmLmsafbrL55HM5CLA3CwpaxheUFguqfS?cluster=devnet).


### Create an account for the token
The terminology is a little confusing since you already have an account/wallet which holds your SOL. This is different from that account and looking at Solana Explorer makes this clear. Here you are creating a `token account` which is specific to the token we just created. The `token account` is owned by the main account. Each wallet that wants to hold your token will need to have an associated `token account` that is specific to your token. 

```
spl-token create-account
Create a new token account

USAGE:
    spl-token create-account [FLAGS] [OPTIONS] <TOKEN_ADDRESS>
```

Using our newly created token from above `6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE`

```
> spl-token create-account 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE
Creating account GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24

Signature: RqysGVJgEE9zVY72J8axiXptz1dHafYQ6wWaix8uRLSGWDnij5HKUrbiNTMk4NiDHgidFUQS3q3DMmZBHn63vu7
```

If we compare the explorer links for our [original wallet/account](https://explorer.solana.com/address/G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q?cluster=devnet) and our recently generated [token account](https://explorer.solana.com/address/GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24?cluster=devnet) we see that the meta-data fields are quite different and that the token account has an owner (main wallet) and mint address (token address).


### Mint Our Token

The minting command syntax is as follows:
```
spl-token mint <TOKEN_ADDRESS> <TOKEN_AMOUNT> <RECIPIENT_TOKEN_ACCOUNT_ADDRESS>
```

It will default to using the account we just created but let's be explicit.

```
> spl-token mint 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE 1000 GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24
Minting 1000 tokens
  Token: 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE
  Recipient: GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24

Signature: wbErCo1CvQCxknptjq68PuyizgoYVJbuVzVFsAbqS8RdhUa5KzGHrvKeejnsTpsJE4Th7Hqq3vTswBGHXVjsWM2
 ```

Let's take a look on the explorer to see what our minting [looks like](https://explorer.solana.com/tx/wbErCo1CvQCxknptjq68PuyizgoYVJbuVzVFsAbqS8RdhUa5KzGHrvKeejnsTpsJE4Th7Hqq3vTswBGHXVjsWM2?cluster=devnet). Let's also check our [token account](https://explorer.solana.com/address/GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24?cluster=devnet) to make sure our tokens are there.

 ### Transfer the Token

Before we transfer tokens to another wallet, look at our original wallet on the explorer, it will have our 1000 tokens in it. This is because it is the Mint Authority of our token.

Now let's send some of our newly minted token to the secondary wallet we created in [this tutorial](create_account.md). 

```
spl-token transfer 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE 100 BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR
Transfer 100 tokens
  Sender: GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24
  Recipient: BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR
  Recipient associated token account: 7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg
Error: Recipient's associated token account does not exist. Add `--fund-recipient` to fund their account
```
We get an error since there is no token account associated with this wallet address. This wallet can only hold SOL tokens, we need to associate an account with this wallet that can hold our token. Add the `--fund-recipient` flag and execute the command again.

```
spl-token transfer --fund-recipient 6oab5jByF5v81tYgZzaEjrgzh8QVQS3sogFE9jqWTxqE 100 BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR
Transfer 100 tokens
  Sender: GhQEYEJum2tyWzCXhiyMgqAXbfZjcyqeCUdahcL6Cg24
  Recipient: BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR
  Recipient associated token account: 7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg
  Funding recipient: 7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg (0.00203928 SOL)

Signature: 3DBmLTpKvtoPD9WGUD8zhiBtHA6Nx3ft2wf6NxXNPwcJmpsNaHDxssHPYbvzQwgoFkRtnPagumayGs67WmmzaemZ
```

If we [look at the wallet](https://explorer.solana.com/address/G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q?cluster=devnet) there is a `Tokens` tab near the bottom (History/Tokens/Domains). We should see our 100 tokens showed up in our wallet.

Another note about the `--fund-recipient` and the difference between account types. If we [look at the transaction](https://explorer.solana.com/tx/3DBmLTpKvtoPD9WGUD8zhiBtHA6Nx3ft2wf6NxXNPwcJmpsNaHDxssHPYbvzQwgoFkRtnPagumayGs67WmmzaemZ?cluster=devnet) for our tokens we can see that the address the tokens were transferred to is not the same as the address we gave.

`7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg` instead of `BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR` (our wallet)

Why is this? These tokens can only be transferred to an account that holds these tokens. If we look at the address that received the tokens [7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg](https://explorer.solana.com/address/7yN53pR94TyTvPyCpgiWfMdCGjGsrhReV9XH52wWiYBg?cluster=devnet) we can see that this is a `Token Account`, similar to the one we created above before minting our tokens. We can also see that the address we wanted to send our token to `BqPu...YokR` is the `Owner` of this token account. If we go to [our secondary wallet](https://explorer.solana.com/address/BqPukZTeTbXkcR6JwcVRgd71drFvqbCn2XPta2HdYokR/tokens?cluster=devnet) and go to the tokens tab toward the bottom, we can see that our 100 tokens are indeed there. 