# Blocknet liquidity multisig wallet utilities

The community liquidity multisig wallet was created to hold the funds granted in [superblock 1987200](https://explorer.blocknet.co/block/e02fa220f5941fb8eab2f3e897d262ce8e00e4d53e823f76819cd5fb204207aa) for proposal [1987200 BlockDX liquidity](https://bit.ly/3wpUJoS). It is actually not a wallet but rather a potential collection of P2SH multisig addresses where the co-signers are well-known members of the Blocknet Discord server.

Each of the co-signers owns one of the public keys used to create the multisig addresses(es) and the private keys needed to assemble and sign a spend transaction. Blocknet does not yet have a convenient multisig wallet so address generation and transaction assembly is a sequence of manual CLI (or QT debug window) operations.

Scripts are gradually being developed to simplify operation of the wallet. Extant so far are

* blockmultisig - used to create a new address in the wallet
* blockmultispend - used to create and sign a transaction to spend from a multisig address



## blockmultisig

Usage: blockmultisig a b c d e

This script generates a Blocknet 3 of 5 multisig address where 
 * a,b,c,d and e are numbers between 1 and 5 inclusive
 * a,b,c,d and e are indices into an array of public keys
 * each number between 1 and 5 can be used only once
 * the order of the keys (and their values) determines the generated address
 * the public keys are  
    03d26bfbaed9c1a283bba4a06cf50194c550c47b403ef8a91dbce7c78bb8096e32  
    03f4b539f127b640212a671a64fd6964fdb2bfec16629fe0a717fbf092dc92a860  
    028e3b41c094b710a7553ec2bb0407d312d595dfa9b79ea6c8883646ef6815361c  
    03511c0f9afd27f1897fcbf8f69fcf1be2bd5018d409408016fa2eddebd3e284d2  
    03a10859d11b83f1c55aacd9c7b4b6125bf1911aed794e065b2411016a6effdade

The multisig addresses created so far are

Purpose | Label | Key sequence | Address
---|---|---|---
testing and familiarisation | ms1 | 1,2,3,4,5 | CeRp3rFxD4Uzvax5hxc4FPk5aWDNrLzQnU
change address | ms2 | 1,2,3,5,4 | CLK7viCjGQtddvUigNpDYx3VXVH2MaT62u
Liquidity | ms3 | 5,4,3,2,1 | CTNq1KarBgQKZeDMdvj6pfB3tMH9arQspM
Sweeper | ms4 | 1,2,4,3,5 | CWPvJL5GbG7bFGqvi7cNh6MnLFuzAuo1g8
Marketing | ms5 | 1,2,4,5,3 | CSLi9gvmq8uF5ixBPKu2TgGLCTeV2rxTJ3
Exchanges | ms6 | 1,2,5,3,4 | CMxsm1pYiUVtqFo7aFukrafsPDuPG89hb2
Eth dev | ms7 | 1,2,5,4,3 | CdsFjjxEWXHsnnkjwRpDFT5EzC6JxFtNuu

### Desirable enhancements
 * automatically generate the next key combination and record the purpose of
all allocated addresses on the Blocknet blockchain (eg: as OP_RETURN data).



## blockmultispend

Usage: blockmultispend [-s|--sign] txid vout destination amount [change_address]

This script generates a raw transaction to spend from a particular UTXO. It
is expected that the UTXO is found in a multisig address to which the user
has one of the spending keys. With no options it creates and displays the 
raw transaction hex. If requested it will also sign the transaction and display
the raw hex to be passed on to the next co-signer.
 
 * **txid** and **vout** identify the source of funds from which to spend
 * **amount** BLOCK to
 * **destination** address
 * **change_address** is optional and defaults to the "liquidity" multisig
   address *ms3* (CTNq1KarBgQKZeDMdvj6pfB3tMH9arQspM).

### Desirable enhancements
 * automate extraction of the largest UTXO in the ms3 address and use that
as the default UTXO source  
 * allow more than one input



# License
The scripts are released under the [MIT license](LICENSE.md).


