# solana-tutorials
My notes from developing on the Solana blockchain

## Primer

The Solana Program Library is a set of on-chain programs. An SPL token is a token created on the solana protocol that runs against the [SeaLevel](https://medium.com/solana-labs/sealevel-parallel-processing-thousands-of-smart-contracts-d814b378192) runtime environment. One is generated using the SPL Token Program. Common Solana tokens are SPL tokens (RAY, SRM, MNDE, ATLAS, etc.)


ACCOUNT
### Useful Links

Official Solana 
* [Solana SPL Token Guide](https://spl.solana.com/token)
* [Solana block explorer](https://explorer.solana.com/?cluster=devnet)

Other Tutorials/Guids
* [Figment Tutorial](https://learn.figment.io/tutorials/sol-mint-token)
* https://solongwallet.medium.com/solana-development-tutorial-program-101-2b168bffd541

### Prerequisites

1. Install rust 

```curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh```

2. Install solana command line tools

```https://docs.solana.com/es/cli/install-solana-cli-tools```


Let's make sure that our tools are properly setup and we are configured to run on devnet NOT mainnet. Devnet is free to use and you can issue tokens, if you run on mainnet you'd better know what you're doing

####
Install the CLI
```
> sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
downloading stable installer
  ✨ stable commit d52dd97 initialized
> solana --version
solana-cli 1.8.13 (src:d52dd97a; feat:1006352700)  
```

Configure the CLI to use `devnet`
```
> solana config set --url https://api.devnet.solana.com
```

Create an account
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
Let's take a look on the block explorer [here](https://explorer.solana.com/address/G3mqR8ovgG1AVPw432zXUxWU8R5iqQ96pxfCPmvekg4Q?cluster=devnet)


jscott:~/solana-tutorials$ solana config get
Config File: /Users/jscott/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: test-keypair.json
Commitment: confirmed
```
## Creating Wallets and Funding


create a wallet
add sol
create a second wallet
send sol from 1>2

create a token
airdrop token to 1 & 2
txfer from 1/2