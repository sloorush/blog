+++
title = "The Incomplete History of Bitcoin Development"
date = "2021-08-09"
author = "r-ush and Aman"
cover = "/img/bitcoin-core.svg"
description = "Summary of our research about how Bitcoin is what it is now!"
tags = ["bitcoin", "blockchain"]
keywords = ["bitcoin", "blockchain", "btc"]
authorTwitter = "_r_ush_"
+++

## Timeline discussion

### Early 2007: Satoshi Nakamoto

_Context_:

- First no trusted third party P2P e-cash system. (Decentralized)
- Support from community.

#### Satoshi destroying haters: [🔗](https://satoshi.nakamotoinstitute.org/emails/cryptography/15/#selection-32.65-117.67)

> You have an outline and proposal for such a design, which is a big step forward, but the devil is in the little details.

I believe I've worked through all those little details over the last year and a half while coding it, and there were a lot of them.

#### People getting a chance to be a millionare: [🔗](https://satoshi.nakamotoinstitute.org/emails/cryptography/16/#selection-32.40-99.49)

I made the proof-of-work difficulty ridiculously easy to start with, so for a little while in the beginning a typical PC will be able to generate coins in just a few hours.

- 6th July 2010: Bitcoin v0.3.0 released 🔗
  Laszlo Hanyecz (Bitcoin pizza guy) adds support for macOS.
- 2010: v.3.2
  - **Checkpoints**: Add a checkpoint in the blockchain version as a security safeguard that locks a block height to a specific hash[🔗](https://github.com/bitcoin/bitcoin/commit/4110f33cded01bde5f01a6312248fa6fdd14cc76#diff-118fcbaaba162ba17933c7893247df3aR1344).
- v.3.3 :
  - Fixing of a _critical overflow bug_, exploited to create two high-value UTXOs [🔗](https://bitcointalk.org/index.php?topic=898.msg10722#msg10722).
  - Used an _alert_ system.
    - Includes a _safe mode_, disabling all money handling RPC methods in the entire network.
  - Issue: Causes a single point of failure
  - Dec 2010: Last talk with Satoshi [🔗](https://pastebin.com/syrmi3ET)
    ![](https://humornama.com/wp-content/uploads/2020/09/Thik-Hai-Bhai-Ab-Main-Chalta-Hu-meme-template-of-Phir-Hera-Pheri.jpg)

## Without Satoshi

- mid-2011 -> BIP introduced.
- august 2011 -> BIP 1 was announced [🔗](https://github.com/bitcoin/bips/blob/master/bip-0001.mediawiki)
- late-2011 - early 2012 -> Introduction of proposals for receiver to specify payment by using script needed to spend the UTXO. (Context (?))
- In fall 2012 the Bitcoin Foundation is announced. But was a threat to decentralization
- Spring 2013 -> Bitcoin v.8.0.
- After sometime, a _hard fork_ occurs and is resolved quickly. [🔗](https://bitcoinmagazine.com/technical/bitcoin-network-shaken-by-blockchain-fork-1363144448)
- 2013 -> bitcoin core.
- 2015 -> ChaincodeLabs, Blockstream and other companies evolve and the research flourishes with Lightning Whitepaper.
- 2016 -> Major revolution in the history of blockchain community,
- Child pays for the parent [🔗](https://bitcoincore.org/en/2016/08/23/release-0.13.0/)<br>
  ![](https://memegenerator.net/img/instances/62615337/congrats-now-go-get-a-job-and-pay-back-your-parents.jpg)
- 2017 -> Segwit Accepted.
- 2019 -> BIP Taproot proposal.

## How have show-stopping bugs or disruptions to the network been handled in the past?

### OverFlow Bug

We know that the sum of outputs of a transaction should be less than it's inputs. Hmm, what could go wrong?

> OVERFLOW

```json=
{
    "hash" : "0000000000790ab3f22ec756ad43b6ab569abf0bddeb97c67a6f7b1470a7ec1c",
    "ver" : 1,
    "prev_block" : "0000000000606865e679308edf079991764d88e8122ca9250aef5386962b6e84",
    "mrkl_root" : "618eba14419e13c8d08d38c346da7cd1c7c66fd8831421056ae56d8d80b6ec5e",
    "time" : 1281891957,
    "bits" : 469794830,
    "nonce" : 28192719,
    "n_tx" : 2,
    "tx" : [
        {
            "hash" : "012cd8f8910355da9dd214627a31acfeb61ac66e13560255bfd87d3e9c50e1ca",
            "ver" : 1,
            "vin_sz" : 1,
            "vout_sz" : 1,
            "lock_time" : 0,
            "in" : [
                {
                    "prev_out" : {
                        "hash" : "0000000000000000000000000000000000000000000000000000000000000000",
                        "n" : 4294967295
                    },
                    "coinbase" : "040e80001c028f00"
                }
            ],
            "out" : [
                {
                    "value" : 50.51000000,
                    "scriptPubKey" : "0x4F4BA55D1580F8C3A8A2C78E8B7963837C7EA2BD8654B9D96C51994E6FCF6E65E1CF9A844B044EEA125F26C26DBB1B207E4C3F2A098989DA9BA5BA455E830F7504 OP_CHECKSIG"
                }
            ]
        },
        {
            "hash" : "1d5e512a9723cbef373b970eb52f1e9598ad67e7408077a82fdac194b65333c9",
            "ver" : 1,
            "vin_sz" : 1,
            "vout_sz" : 2,
            "lock_time" : 0,
            "in" : [
                {
                    "prev_out" : {
                        "hash" : "237fe8348fc77ace11049931058abb034c99698c7fe99b1cc022b1365a705d39",
                        "n" : 0
                    },
                    "scriptSig" : "0xA87C02384E1F184B79C6ACF070BEA45D5B6A4739DBFF776A5D8CE11B23532DD05A20029387F6E4E77360692BB624EEC1664A21A42AA8FC16AEB9BD807A4698D0CA8CDB0021024530 0x965D33950A28B84C9C19AB64BAE9410875C537F0EB29D1D21A60DA7BAD2706FBADA7DF5E84F645063715B7D0472ABB9EBFDE5CE7D9A74C7F207929EDAE975D6B04"
                }
            ],
            "out" : [
                {
                    "value" : 92233720368.54277039,
                    "scriptPubKey" : "OP_DUP OP_HASH160 0xB7A73EB128D7EA3D388DB12418302A1CBAD5E890 OP_EQUALVERIFY OP_CHECKSIG"
                },
                {
                    "value" : 92233720368.54277039,
                    "scriptPubKey" : "OP_DUP OP_HASH160 0x151275508C66F89DEC2C5F43B6F9CBE0B5C4722C OP_EQUALVERIFY OP_CHECKSIG"
                }
            ]
        }
    ],
    "mrkl_tree" : [
        "012cd8f8910355da9dd214627a31acfeb61ac66e13560255bfd87d3e9c50e1ca",
        "1d5e512a9723cbef373b970eb52f1e9598ad67e7408077a82fdac194b65333c9",
        "618eba14419e13c8d08d38c346da7cd1c7c66fd8831421056ae56d8d80b6ec5e"
    ]
}
```

Notice something yet? My guy just treated himself with 92233720368.54277039 BTC(92 Billion BTC) (on each address).

> out Value 1: 92233720368.54(7ffffffffff85ee0)
> out Value 2: 92233720368.54(7ffffffffff85ee0)
> The sum would make -0.01 BTC.
> generated transaction "reward" including 51 bitcent "fee"
> out Value:50.51(000000012d1024c0)

    that implies the input value was 0.50 BTC

- Got invalidated by a soft fork (v.3.10)

### 2013 Bitcoin fork [🔗](https://freedom-to-tinker.com/2015/07/28/analyzing-the-2013-bitcoin-fork-centralized-decision-making-saved-the-day/)

The case when centralization saved the day

- Starting from block 225430, the blockchain literally split into two, with one half of the network adding blocks to one version of the chain, and the other half adding to the other. For the next six hours, there were effectively two Bitcoin networks operating at the same time, each with its own version of the transaction history. The split lasted for 24 blocks or 6 hours, finally resolving itself when one version of the chain conclusively pulled ahead of the other at block 225454, leaving the other chain largely abandoned

#### How did this happen?

- The latest version 0.8 release of bitcoind, by far the most popular implementation of Bitcoin used by miners, switched the database that it used to store blocks and transactions from BerkeleyDB to the more efficient LevelDB as part of an effort to reduce blockchain synchronization time. However, what the developers did not realize at the time was that by doing so they also accidentally introduced a change to the rules of the Bitcoin protocol.

This incident will go down in history as one of the closest moments that we have come to the underlying Bitcoin protocol actually failing.

The day was saved by the developers notifying on IRC channels to miners and merchants to shift back to v0.7.

In summary, we have a lot to learn from looking back at the fork. Bitcoin had a really close call, and another bug might well lead to a different outcome. Contrary to the view of the consensus protocol as fixed in stone by Satoshi, it is under active human stewardship, and the quality of that stewardship is essential to its security. _Centralized_ decision-making saved the day here, and for the most part it’s not in conflict with the decentralized nature of the network itself. The human element becomes crucial when the code fails or needs to adapt over time.

### Review Process

- There are currently six Bitcoin Core maintainers, distributed over three continents. Only they can merge commits by contributors. Before commits get merged, however, they have to go through a review process, which has gotten a lot stricter.
- `OP_EVAL` PR
  - The pull request implementing `OP_EVAL` was merged at the end of 2011. It had only one reviewer, though it changes consensus-critical code. Russell O’Connor opened an issue criticizing parts of the implementation and that such a big and consensus-critical change should have had a lot more review and testing.
  - Today each pull request should at least be reviewed by multiple developers. If a change touches security-critical or even consensus-critical code, the review process needs many reviewers, a lot of testing and usually spans over multiple months. John Newbery, an active Bitcoin Core contributor, told me that there is “no chance a consensus change would be merged with a single reviewer today”.
- There are unit-tests written in C++ and functional-test written in Python. Fuzz testing and benchmarking frameworks were also implemented lateron in bitcoin-core

# References

- [https://b10c.me/blog/004-the-incomplete-history-of-bitcoin-development/](https://b10c.me/blog/004-the-incomplete-history-of-bitcoin-development/)
