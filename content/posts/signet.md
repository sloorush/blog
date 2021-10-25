+++
title = "Okay, but what exactly is Signet?"
date = "2021-08-10"
author = "sloorush"
cover = "img/signet.png"
authorTwitter = "_r_ush_"
tags = ["bitcoin", "signet", "blockchain"]
keywords = ["bitcoin", "signet", "blockchain"]
description = "Signet is a smaller, more centralized btc net made for being safe from the 10000 block re-orgs and unreliability of the testnet"
draft = false
+++

This is a log of my research while adding signet support to [utreexo](https://github.com/mit-dci/utreexo)

Signet (BIP 0325) is a new test network for Bitcoin which adds an additional signature requirement to block validation. Signet is similar in nature to testnet, but more reliable and centrally controlled. There is a default signet network ("Signet Global Test Net VI" as of this writing), but anyone can run their own signet network at their whim.

Originally build by Kalle Woof for wallet developers to easily test

### Differences

- Default Bitcoin network protocol listen port is 38333 (instead of 8333)
- Default RPC connection port is 38332 (instead of 8332)
- A different value of ADDRESSVERSION field ensures no signet Bitcoin addresses will work on the production network. (0x6F rather than 0x00)
- The protocol message header bytes are _dynamically generated_ based on the block challenge, i.e. every signet is different; the header for the current default signet is 0x0A03CF40 (that is reversed e.g. in Rust variables) (instead of 0xF9BEB4D9), but see #Genesis_Block_and_Message_Header
- Segwit is always enabled
- Additional consensus requirement that the coinbase witness commitment contains an extended signet commitment, which is a script satisfying the block script (usually a k-of-n multisig)

## How to set up a bitcoin node on signet

Checkout the stack exchange answer here [🔗](https://bitcoin.stackexchange.com/questions/98553/how-do-i-get-set-up-on-signet)
or
Signet Wiki [🔗](https://en.bitcoin.it/wiki/Signet)

## How does signet work?

It works exactly the same as testnet, but centralized and predictable.

## Relevant signet info

- Magic Bytes - magic byte 0x0a, 0x03, 0xcf, 0x40
- Genesis block has timestamp 1598918400, nonce 52613770, and difficulty 0x1e0377ae.
  - genesis block(#0): [🔗](https://explorer.bc-2.jp/block/00000008819873e925422c1ff0f99f7cc9bbb232af63a077a480a3633bee1ef6)
    - hash
      `00000008819873e925422c1ff0f99f7cc9bbb232af63a077a480a3633bee1ef6`
    - hex
      ```
      0xf6, 0x1e, 0xee, 0x3b, 0x63, 0xa3, 0x80, 0xa4,
      0x77, 0xa0, 0x63, 0xaf, 0x32, 0xb2, 0xbb, 0xc9,
      0x7c, 0x9f, 0xf9, 0xf0, 0x1f, 0x2c, 0x42, 0x25,
      0xe9, 0x73, 0x98, 0x81, 0x08, 0x00, 0x00, 0x00,
      ```

## Relevant URLs

- Original proposal [🔗](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-August/016348.html)
- PR review club #18267 [🔗](https://bitcoincore.reviews/18267)
- PR [🔗](https://github.com/bitcoin/bitcoin/pull/18267/files)
- BIP [🔗](https://github.com/bitcoin/bips/blob/master/bip-0325.mediawiki)
- Signet Wiki [🔗](https://en.bitcoin.it/wiki/Signet)
