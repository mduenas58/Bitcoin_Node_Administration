Learning-Bitcoin-from-the-Command-Line

BlockchainCommons

Table of Contents

PART ONE: PREPARING FOR BITCOIN

Status: Finished. Updated for 0.20.

1.0: Introduction to Programming with Bitcoin Core and Lightning

Interlude: Introducing Bitcoin

2.0: Setting Up a Bitcoin-Core VPS

2.1: Setting Up a Bitcoin-Core VPS with Bitcoin Standup

2.2: Setting Up a Bitcoin-Core Machine via Other Means

PART TWO: USING BITCOIN-CLI

Status: Finished. Updated for 0.20.

3.0: Understanding Your Bitcoin Setup

3.1: Verifying Your Bitcoin Setup

3.2: Knowing Your Bitcoin Setup

3.3: Setting Up Your Wallet

Interlude: Using Command-Line Variables

3.4: Receiving a Transaction

3.5: Understanding the Descriptor

4.0: Sending Bitcoin Transactions

4.1: Sending Coins the Easy Way

4.2: Creating a Raw Transaction

Interlude: Using JQ

4.3: Creating a Raw Transaction with Named Arguments

4.4: Sending Coins with Raw Transactions

Interlude: Using Curl

4.5: Sending Coins with Automated Raw Transactions

4.6: Creating a Segwit Transaction

5.0: Controlling Bitcoin Transactions

5.1 Watching for Stuck Transactions

5.2: Resending a Transaction with RBF

5.3: Funding a Transaction with CPFP

6.0: Expanding Bitcoin Transactions with Multisigs

6.1: Sending a Transaction with a Multisig

6.2: Spending a Transaction with a Multisig

6.3: Sending & Spending an Automated Multisig

7.0: Expanding Bitcoin Transactions with PSBTs

7.1: Creating a Partially Signed Bitcoin Transaction

7.2: Using a Partially Signed Bitcoin Transaction

7.3: Integrating with Hardware Wallets

8.0: Expanding Bitcoin Transactions in Other Ways

8.1: Sending a Transaction with a Locktime

8.2: Sending a Transaction with Data

PART THREE: BITCOIN SCRIPTING

Status: Finished. Updated for 0.20 and btcdeb.

9.0: Introducing Bitcoin Scripts

9.1: Understanding the Foundation of Transactions

9.2: Running a Bitcoin Script

9.3: Testing a Bitcoin Script

9.4: Scripting a P2PKH

9.5: Scripting a P2WPKH

10.0: Embedding Bitcoin Scripts in P2SH Transactions

10.1: Understanding the Foundation of P2SH

10.2: Building the Structure of P2SH

10.3: Running a Bitcoin Script with P2SH

10.4: Scripting a Multisig

10.5: Scripting a Segwit Script

10.6: Spending a P2SH Transaction

11.0: Empowering Timelock with Bitcoin Scripts

11.1: Understanding Timelock Options

11.2: Using CLTV in Scripts

11.3: Using CSV in Scripts

12.0: Expanding Bitcoin Scripts

12.1: Using Script Conditionals

12.2: Using Other Script Commands

13.0: Designing Real Bitcoin Scripts

13.1: Writing Puzzles Scripts

13.2: Writing Complex Multisig Scripts

13.3: Empowering Bitcoin with Scripts

PART FOUR: PRIVACY

Status: Finished.

14.0: Using Tor

14.1: Verifying Your Tor Setup

14.2: Changing Your Bitcoin Hidden Services

14.3: Adding SSH Hidden Services

15.0: Using i2p

15.1: Bitcoin Core as an I2P (Invisible Internet Project) service

PART FIVE: PROGRAMMING WITH RPC

Status: Finished.

16.0: Talking to Bitcoind with C

16.1: Accessing Bitcoind in C with RPC Libraries

16.2: Programming Bitcoind in C with RPC Libraries

16.3: Receiving Notifications in C with ZMQ Libraries

17.0: Programming Bitcoin with Libwally

17.1: Setting Up Libwally

17.2: Using BIP39 in Libwally

17.3: Using BIP32 in Libwally

17.4: Using PSBTs in Libwally

17.5: Using Scripts in Libwally

17.6: Using Other Functions in Libwally

17.7: Integrating Libwally and Bitcoin-CLI

18.0: Talking to Bitcoind with Other Languages

18.1: Accessing Bitcoind with Go

18.2: Accessing Bitcoind with Java

18.3: Accessing Bitcoind with Node JS

18.4: Accessing Bitcoind with Python

18.5: Accessing Bitcoind with Rust

18.6: Accessing Bitcoind with Swift

PART SIX: USING LIGHTNING-CLI

Status: Finished.

19.0: Understanding Your Lightning Setup

19.1: Verifying Your core lightning Setup

19.2: Knowing Your core lightning Setup

Interlude: Accessing a Second Lightning Node

19.3: Creating a Lightning Channel

20.0: Using Lightning

20.1: Generating a Payment Request

20.2: Paying an Invoice

20.3: Closing a Lighnting Channel

20.4: Expanding the Lightning Network

APPENDICES

Status: Finished.

Appendices

Appendix I: Understanding Bitcoin Standup

Appendix II: Compiling Bitcoin from Source

Appendix III: Using Bitcoin Regtest

# Chapter One: Introduction to Learning Bitcoin Core (& Lightning) from the Command Line

## Introduction

The ways that we make payments for goods and services has been changing dramatically over the last several decades. Where once all transactions were conducted through cash or checks, now various electronic payment methods are the norm. However, most of these electronic payments still occur through centralized systems, where credit card companies, banks, or even internet-based financial institutions like Paypal keep long, individually correlated lists of transactions and have the power to censor transactions that they don't like.

These centralization risks were some of the prime catalysts behind the creation of cryptocurrencies, the first and most successful of which is Bitcoin. Bitcoin offers pseudonymity; it makes it difficult to correlate transactions; and it makes censorship by individual entities all but impossible. These advantages have made it one of the quickest growing currencies in the world. That growth in turn has made Bitcoin into a going concern among entrepreneurs and developers, eager to create new services for the Bitcoin community.

If you're one of those entrepreneurs or developers, then this course is for you, because it's all about learning to program Bitcoin. It's an introductory course that explains all the nuances and features of Bitcoin as it goes. It also takes a very specific tack, by offering lessons in how to work _directly_ with Bitcoin Core and with the core lightning server using their RPC interfaces.

Why not use some of the more fully featured libraries found in various programming languages? Why not create your own from scratch? It's because working with cryptocurrency is dangerous. There are no safety nets. If you accidentally overpay your fees or lose a signing key or create an invalid transaction or make any number of potential mistakes, then your cryptocurrency will be gone forever. Much of that responsibility will, of course, lie with you as a cryptocurrency programmer, but it can be minimized by working with the most robust, secure, and safe cryptocurrency interfaces around, the ones created by the cryptocurrency programming teams themselves: bitcoind and lightningd.

Much of this book thus discusses how to script Bitcoin (and Lightning) directly from the command line. Some later chapters deal with more sophisticated programming languages, but again they continue to interact directly with the bitcoind and lightningd daemons by using RPC or by interacting with the files they create. This allows you to stand on the shoulders of giants and use their trusted technology to learn how to create your own trusted systems.

## Required Skill Level

You do not need to be particularly technical for the majority of this course. All you need is the confidence to run basic commands on the UNIX command line. If you're familiar with things like ssh, cd, and ls, the course will supply you with the rest.

A minority of this course requires programming knowledge, and you should skip over those sections if needed, as discussed in the next section.

## Overview of Topics

This book is broadly divided into the following sections:

  
|Part|Description|Skills|
|---|---|---|
|**Part One: Preparing for Bitcoin**|Understanding the basics of Bitcoin and setting up a server for use.|Command Line|
|**Part Two: Using Bitcoin-CLI**|Using the Bitcoin-CLI for creating transactions.|Command Line|
|**Part Three: Bitcoin Scripting**|Expanding your Bitcoin work with scripts.|Programming Concepts|
|**Part Four: Using Tor**|Improving your node security with Tor|Command Line|
|**Part Five: Programming with RPC**|Accessing RPC from C and other languages.|Programming in C|
|**Part Six: Using Lightning-CLI**|Using the Lightning-CLI for creating transactions.|Command Line|
|**Appendices**|Utilizing less common Bitcoin setups.|Command Line|

  
  

## How To Use This Course

So where do you start? This book is primarily intended to be read sequentially. Just follow the "What's Next?" Links at the end of each section and/or click through the individual section links on each chapter page. You'll achieve the best understanding from this course if you actually build yourself a Bitcoin server (per Chapter 2) and then run through all the examples over the course of the book: trying out examples is an excellent learning methodology.

If you have different levels of skill or want to learn different things, you might skip to different parts of the book:

- If you've already got a Bitcoin environment ready to be used, jump to [Chapter Three: Understanding Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_0_Understanding_Your_Bitcoin_Setup.md).
    
- If you only care about Bitcoin scripting, jump to [Chapter Nine: Introducing Bitcoin Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_0_Introducing_Bitcoin_Scripts.md).
    
- If you just want to read about using programming languages, jump to [Chapter Sixteen: Talking to Bitcoin](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_0_Talking_to_Bitcoind.md).
    
- If you conversely don't want to do any programming, definitely skip chapters 15-17 while you're reading, and perhaps skip chapters 9-13. The rest of the course should still make sense without them.
    
- If you are only interested in Lightning, zap over to [Chapter Nineteen: Understanding Your Lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md).
    
- If you want to read the major new content added for v2 of the course (2020), following on v1 (2017), read [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md), [§4.6: Creating a SegWit Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md), [Chapter 7: Expanding Bitcoin with PSBTs](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_0_Expanding_Bitcoin_Transactions_PSBTs.md), [§9.5: Scripting a P2WPKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md), [§10.5: Scripting a SegWit Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_5_Scripting_a_Segwit_Script.md), [Chapter 14: Using Tor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_0_Using_Tor.md), [Chapter 15: Using i2p](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_0_Using_i2p.md), [Chapter 16: Talking to Bitcoind with C](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_0_Talking_to_Bitcoind.md), [Chapter 17: Programming with Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_0_Programming_with_Libwally.md), [Chapter 18: Talking to Bitcoind with Other Languages](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_0_Talking_to_Bitcoind_Other.md), [Chapter 19: Understanding Your Lighting Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md), and [Chapter 20: Using Lightning](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_0_Using_Lightning.md).
    

## Why to Use this Course

Obviously, you're working through this course because you're interested in Bitcoin. Besides imparting basic knowledge, it's also helped readers to join (or create) open-source projects and to get entry-level jobs in Bitcoin programming. A number of Blockchain Commons' interns learned about Bitcoin from this course, as have some members of our programming team.

## How to Support this Course

- Please use [Issues](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/issues) for any questions. Blockchain Commons does not have an active support team, and so we can't address individual problems or queries, but we will look over them in time, and use them to improve future iterations of the course.
    
- Please use [PRs](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/pulls) for any fixes of typos or incorrect (or changed) commands. For command-line or technical changes, it's very helpful if you also use the PR comments to explain why you did what you did, so that we don't have to research it.
    
- Please Use Our [Community discussions area](https://github.com/BlockchainCommons/Community/discussions) for talking about careers and skills. Blockchain Commons occasionally offers internships, as discussed in our Community repo.
    
- Please [become a patron](https://github.com/sponsors/BlockchainCommons) if you find this course helpful or if you want to help educate the next generation of blockchain programmers.
    

## What's Next?

If you'd like a basic introduction to Bitcoin, public-key cryptography, ECC, blockchains, and Lightning, read the [Introducing Bitcoin](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/01_1_Introducing_Bitcoin.md) interlude.

Otherwise, if you're ready to dive into the course, go to [Setting Up a Bitcoin-Core VPS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_0_Setting_Up_a_Bitcoin-Core_VPS.md).

# Interlude: Introducing Bitcoin

Before you can get started programming Bitcoin (and Lightning), you should have a basic understanding of what they are and how they work. This section provides that overview. Many more definitions will appear within the document itself; this is only intended to lay the foundation.

## About Bitcoin

Bitcoin is a programmatic system that allows for the transfer of the bitcoin currency. It is enabled by a decentralized, peer-to-peer system of nodes, which include full nodes, wallets, and miners. Working together, they ensure that bitcoin transactions are fast and non-repudiable. Thanks to the decentralized nature of the system, these transactions are also censor-resistant and can provide other advantages such as pseudonymity and non-correlation if used well.

Obviously, Bitcoin is the heart of this book, but it's also the originator of many other systems, including blockchains and Lightning, which are both detailed in this tutorial, and many other cryptocurrencies such as Ethereum and Litecoin, which are not.

_**How Are Coins Transferred?**_ Bitcoin currency isn't physical coins. Instead it's an endless series of ownership reassignments. When one person sends coins to another, that transfer is stored as a transaction. It's the transaction that actually records the ownership of the money, not any token local to the owner's wallet or their machine.

_**Who Can You Send Coins To?**_ The vast majority of bitcoin transactions involve coins being sent to individual people (or at least to individual Bitcoin addresses). However, more complex methodologies can be used to send bitcoins to groups of people or to scripts. These various methodologies have names like P2PKH, multisig, and P2SH.

_**How Are Transactions Stored?**_ Transactions are combined into larger blocks of data, which are then written to the blockchain ledger. A block is built in such a way that it cannot be replaced or rewritten once several blocks have been built atop (following) it. This is what makes bitcoins non-repudiable: the decentralized global ledger where everything is recorded is effectively a permanent and unchangeable database.

However, the process of building these blocks is stochastic: it's somewhat random, so you can never be assured that a transaction will be placed in a specific block. There can also be changes in blocks if they're very recent, but only if they're _very_ recent. So, things become non-repudiable (and permanent and unchangeable) after a little bit of time.

_**How Are Transactions Protected?**_ The funds contained in a Bitcoin transaction are locked with a cryptographic puzzle. These puzzles are designed so that they can be easily solved by the person who the funds were sent to. This is done using the power of public-key cryptography. Technically, a transaction is protected by a signature that proves you're the owner of the public key that a transaction was sent to: this proof of ownership is the puzzle that's being solved.

Funds are further protected by the use of hashes. Public keys aren't actually stored in the blockchain until the funds are spent: only public-key hashes are. This means that even if quantum computer were to come along, Bitcoin transactions would remain protected by this second level of cryptography.

_**How Are Transactions Created?**_ The heart of each Bitcoin transaction is a FORTH-like scripting language that is used to lock the transaction. To respend the money, the recipient provides specific information to the script that proves he's the intended recipient.

However, these Bitcoin scripts are the lowest level of Bitcoin functionality. Much Bitcoin work is done through the bitcoind Bitcoin daemon, which is controlled through RPC commands. Many people send those RPC commands through the bitcoin-cli program, which provides an even simpler interface. Non-programmers don't even worry about these minutia, but instead use programmed wallets with simpler interfaces.

### Bitcoin — In Short

One way to think of Bitcoin is as _a sequence of atomic transactions_. Each transaction is authenticated by a sender with the solution to a previous cryptographic puzzle that was stored as a script. The new transaction is locked for the recipient with a new cryptographic puzzle that is also stored as a script. Every transaction is recorded in an immutable global ledger.

## About Public-Key Cryptography

Public-key cryptography is a mathematical system for protecting data and proving ownership through an asymmetric pair of linked keys: the public key and the private key.

It's important to Bitcoin (and to most blockchain systems) because it's the basis of a lot of the cryptography that protects the cryptocurrency funds. A Bitcoin transaction is typically sent to an address that is a hashed public key. The recipient is then able to retrieve the money by revealing both the public key and the private key.

_**What Is a Public Key?**_ A public key is the key given out to other people. In a typical public-key system, a user generates a public key and a private key, then he gives the public key to all and sundry. Those recipients can encrypt information with the public key, but it can't be decrypted with the same public key because of the asymmetry of the key pair.

_**What Is a Private Key?**_ A private key is linked to a public key in a key pair. In a typical public-key system, a user keeps his private key secure and uses it to decrypt messages that were encrypted with his public key before being sent to him.

_**What Is a Signature?**_ A message (or more commonly, a hash of a message) can be signed with a private key, creating a signature. Anyone with the corresponding public key can then validate the signature, which verifies that the signer owns the private key associated with the public key in question. _SegWit_ is a specific format for storing a signature on the Bitcoin network that we'll meet down the line.

_**What Is a Hash Function?**_ A hash function is an algorithm frequently used with cryptography. It's a way to map a large, arbitrary amount of data to a small, fixed amount of data. Hash functions used in cryptography are one-way and collision-resistant, meaning that a hash can reliably be linked to the original data, but the original data can not be regenerated from the hash. Hashes thus allow the transmission of small amounts of data to represent large amounts of data, which can be important for efficiency and storage requirements.

Bitcoin takes advantage of a hash's ability to disguise the original data, which allows concealment of a user's actual public key, making transactions resistant to quantum computing.

### Public-Key Cryptography — In Short

One way to think of public-key cryptography is: _a way for anyone to protect data such that only an authorized person can access it, and such that the authorized person can prove that he will have that access._

## About ECC

ECC stands for elliptic-curve cryptography. It's a specific branch of public-key cryptography that depends on mathematical calculations conducted using elliptic curves defined over finite fields. It's more complex and harder to explain than classic public-key cryptography (which used prime numbers), but it has some nice advantages.

ECC does not receive much attention in this tutorial. That's because this tutorial is all about integrating with Bitcoin Core and Lightning servers, which have already taken care of the cryptography for you. In fact, this tutorial's intention is that you don't have to worry about cryptography at all, because that's something that you _really_ want experts to deal with.

_**What is an Elliptic Curve?**_ An elliptic curve is a geometric curve that takes the form y2 = x3 + ax + b. A specific elliptic curve is chosen by selecting specific values of a and b. The curve must then be carefully examined to determine if it works well for cryptography. For example, the secp256k1 curve used by Bitcoin is defined as a=0 and b=7.

Any line that intersects an elliptic curve will typically do so at 3 points (absent a few cases for infinity and intersections) ... and that's the basis of elliptic-curve cryptography.

_**What are Finite Fields?**_ A finite field is a finite set of numbers, where all addition, subtraction, multiplication, and division is defined so that it results in other numbers also in the same finite field. One simple way to create a finite field is through the use of a modulo function.

_**How is an Elliptic Curve Defined Over a Finite Field?**_ An elliptic curve defined over a finite field has all of the points on its curve drawn from a specific finite field. This takes the form: y2 % field-size = (x3 + ax + b) % field-size The finite field used for secp256k1 is 2256 - 232 - 29 - 28 - 27 - 26 - 24 - 1.

_**How Are Elliptic Curves Used in Cryptography?**_ In elliptic-curve cryptography, a user selects a very large (256-bit) number as his private key. He then adds a set base point on the curve to itself that many times. (In secp256k1, the base point is G = 04 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798 483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A6855419 9C47D08F FB10D4B8, which prefixes the two parts of the tuple with an 04 to say that the data point is in uncompressed form. If you prefer a straight geometric definition, it's the point "0x79BE667EF9DCBBAC55A06295CE870B07029BFCDB2DCE28D959F2815B16F81798,0x483ADA7726A3C4655DA4FBFC0E1108A8FD17B448A68554199C47D08FFB10D4B8") The resultant number is the public key. Various mathematical formula can then be used to prove ownership of the public key, given the private key. As with any cryptographic function, this one is a trap door: it's easy to go from private key to public key and largely impossible to go from public key to private key.

This particular methodology also explains why finite fields are used in elliptic curves: it ensures that the private key will not grow too large. Note that the finite field for secp256k1 is slightly smaller than 256 bits, which means that all public keys will be 256 bits long, just like the private keys are.

_**What Are the Advantages of ECC?**_ The main advantage of ECC is that it allows the same security as classic public-key cryptography with a much smaller key. A 256-bit elliptic-curve public key corresponds to a 3072-bit traditional (RSA) public key.

### ECC – In Short

One way to think of ECC is: _a way to enable public-key cryptography that uses very small keys and very obscure math._

## About Blockchains

Blockchain is the generalization of the methodology used by Bitcoin to create a distributed global ledger. Bitcoin is a blockchain as are any number of alt-coins, each of which lives on its own network and writes to its own chain. Sidechains like Liquid are blockchains too. Blockchains don't even need to have anything to do with finances. For example, there have been many discussions of using blockchains to protect self-sovereign identities.

Though you need to understand the basics of how a blockchain works to understand how transactions work in Bitcoin, you won't need to go any further than that. Because blockchains have become a wide category of technology, those basic concepts are likely to be applicable to many other projects in this growing technology sector. The specific programming commands learned in this book will not be, however, as they're fairly specific to Bitcoin (and Lightning).

_**Why Is It Called a Chain?**_ Each block in the blockchain stores a hash of the block before it. This links the current block all the way back to the original "genesis block" through an unbroken chain. It's a way to create absolute order among possibly conflicting data. This also provides the security of blockchain, because each block is stacked atop an old one makes it harder to recreate the old block due to the proof-of-work algorithms used in block creation. Once several blocks have been built atop a block in the chain, it's essentially irreversible.

_**What is a Fork?**_ Occasionally two blocks are created around the same time. This temporarily creates a one-block fork, where either of the current blocks could be the "real" one. Every once in a while, a fork might expand to become two blocks, three blocks, or even four blocks long, but pretty quickly one side of the fork is determined to be the real one, and the other is "orphaned". This is part of the stochastic process of block creation, and demonstrates why several blocks must be built atop a block before it can be considered truly trustworthy and non-repudiable.

### Blockchain — In Short

One way to think of blockchain is: _a linked series of blocks of unchangeable data, going back in time_. Another way is: _a linked series of blocks to absolutely order data that could be conflicting_.

## Is Blockchain Right for Me?

If you want to transact bitcoins, then obviously Bitcoin is right for you. However, more widely, blockchain has become a popular buzz-word even though it's not a magic bullet for all technical problems. With that said, there are many specific situations where blockchain is a superior technology.

Blockchains probably _will_ be helpful if:

- Users don't trust each other.
    
    - Or: Users exist across various borders.
        
- Users don't trust central authorities.
    
    - And: Users want to control their own destinies.
        
- Users want transparent technology.
    
- Users want to share something.
    
    - And: Users want what's shared to be permanently recorded.
        
- Users want fast transaction finality.
    
    - But: Users don't need instant transaction finality.
        

Blockchains probably _will not_ be helpful if:

- Users are trusted:
    
    - e.g.: transactions occur within a business or organization.
        
    - e.g.: transactions are overseen by a central authority.
        
- Secrecy is required:
    
    - e.g.: Information should be secret.
        
    - e.g.: Transactions should be secret.
        
    - e.g.: Transactors should be secret.
        
    - Unless: A methodology for cryptographic secrecy is carefully considered, analyzed, and tested.
        
- Users need instant transaction finality.
    
    - e.g.: in less than 10 minutes on a Bitcoin-like network, in less than 2.5 minutes on a Litecoin-like network, in less than 15 seconds on an Ethereum-like network
        

Do note that there may still be solutions for some of these situations within the Bitcoin ecosystem. For example, payment channels are rapidly addressing questions of liquidity and payment finality.

## About Lightning

Lightning is a layer-2 protocol that interacts with Bitcoin to allow users to exchange their bitcoins "off-chain". It has both advantages and disadvantages over using Bitcoin on its own.

Lightning is also the secondary focus of this tutorial. Though it's mostly about interacting directly with Bitcoin (and the bitcoind), it pays some attention to Lightning because it's an upcoming technology that is likely to become a popular alternative to Bitcoin in the near future. This book takes the same approach to Lightning as to Bitcoin: it teaches how to interact directly with a trusted Lightning daemon from the command line.

Unlike with Bitcoin, there are actually several variants of Lightning. This tutorial uses the standard-compliant [core lightning](https://github.com/ElementsProject/lightning) implementation as its trusted Lightning server.

_**What is a Layer-2 Protocol?**_ A layer-2 Bitcoin protocol works on top of Bitcoin. In this case, Lightning works atop Bitcoin, interacting with it through smart contracts.

_**What is a Lightning Channel?**_ A Lightning Channel is a connection between two Lightning users. Each of the users locks up some number of bitcoins on the Bitcoin blockchain using a multi-sig signed by both of them. The two users can then exchange bitcoins through their Lightning channel without ever writing to the Bitcoin blockchain. Only when they want to close out their channel do they settle their bitcoins, based on the final division of coins.

_**What is a Lightning Network?**_ Putting together a number of Lightning Channels creates the Lightning Network. This allows two users who have not created a channel between themselves to exchange bitcoins using Lightning: the protocol forms a chain of Channels between the two users, then exchanges the coins through the chain using time-locked transactions.

_**What are the Advantages of Lightning?**_ Lightning allows for faster transactions with lower fees. This creates the real possibility of bitcoin-funded micropayments. It also offers better privacy, since it's off-chain with only the first and last states of the transaction being written to the immutable Bitcoin ledger.

_**What are the Disadvantages of Lightning?**_ Lightning is still a very new technology and hasn't been tested as thoroughly as Bitcoin. That's not just a question of the technological implementation, but also whether the design itself can be gamed in any unexpected ways.

### Lightning – In Short

One way to think of Lightning is: _a way to transact bitcoins using off-chain channels between pairs of people, so that only a first and final state have to be written to the blockchain_.

## Summary: Introducing Bitcoin

Bitcoin is a peer-to-peer system that allows for the transfer of funds through transactions that are locked with puzzles. These puzzles are dependent upon public-key elliptic-curve cryptography. When you generalize the ideas behind Bitcoin, you get blockchains, a technology that's currently growing and innovating. When you expand the ideas behind Bitcoin, you get layer-2 protocols such as Lightning, which expand the currency's potential.

## What's Next?

Advance through "Preparing for Bitcoin" with [Chapter Two: Setting Up a Bitcoin-Core VPS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_0_Setting_Up_a_Bitcoin-Core_VPS.md).

# Chapter Two: Creating a Bitcoin-Core VPS

To get started with Bitcoin, you first need to set up a machine running Bitcoin. The articles in this chapter describe how to do so, primarily by using a VPS (Virtual Private Server).

## Objectives for this Chapter

After working through this chapter, a developer will be able to:

- Decide Between the Five Major Types of Bitcoin Nodes
    
- Create a Bitcoin Node for Development
    
- Create a Local Instance of the Bitcoin Blockchain
    

Supporting objectives include the ability to:

- Understand the Basic Network Setup of the VPS
    
- Decide Which Security Priorities to Implement
    
- Understand the Difference between Pruned and Unpruned Nodes
    
- Understand the Difference between Mainnet, Testnet, and Regtest Nodes
    
- Interpret the Basics of the Bitcoin Configuration File
    

## Table of Contents

You don't actually need to read this entire chapter. Decide if you want to run a StackScript to set a node up on a Linode VPS (§2.2); or you want to set up on a different environment, such as on an AWS machine or a Mac (§2.3). Then, jump to the appropriate section. Additional information on our suggested setups may also be found in [Appendix I](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A1_0_Understanding_Bitcoin_Standup.md).

- [Section One: Setting Up a Bitcoin Core VPS with Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md)
    
- [Section Two: Setting Up a Bitcoin Core Machine via Other Means](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_2_Setting_Up_Bitcoin_Core_Other.md)
    

# 2.1: Setting Up a Bitcoin-Core VPS with Bitcoin Standup

This document explains how to set up a VPS (Virtual Private Sever) to run a Bitcoin node on Linode.com using an automated StackScript from the [Bitcoin Standup project](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). You just need to enter a few commands and boot your VPS. Almost immediately after you boot, you'll find your new Bitcoin node happily downloading blocks.

> :warning: **WARNING:** Don’t use a VPS for a bitcoin wallet with significant real funds; see [http://blog.thestateofme.com/2012/03/03/lessons-to-be-learned-from-the-linode-bitcoin-incident/](http://blog.thestateofme.com/2012/03/03/lessons-to-be-learned-from-the-linode-bitcoin-incident/) . It is very nice to be able experiment with real bitcoin transactions on a live node without tying up a self-hosted server on a local network. It's also useful to be able to use an iPhone or iPad to communicate via SSH to your VPS to do some simple bitcoin tasks. But a higher level of safety is required for significant funds.

- If you want to understand what this setup does, read [Appendix I: Understanding Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A1_0_Understanding_Bitcoin_Standup.md) as you install.
    
- If you want to instead setup on a machine other than a Linode VPS, such as an AWS machine or a Mac, goto [§2.2: Setting Up a Bitcoin-Core via Other Means](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_2_Setting_Up_Bitcoin_Core_Other.md)
    
- If you already have a Bitcoin node running, goto [Chapter Three: Understanding Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_0_Understanding_Your_Bitcoin_Setup.md).
    

## Getting Started with Linode

Linode (now Akamai Cloud) is a Cloud Hosting service that offers quick, cheap Linux servers with SSD storage. We use them for this tutorial primarily because their BASH-driven StackScripts offer an easy way to automatically set up a Bitcoin node with no fuss and no muss.

### Set Up a Linode Account

You can create a Linode account by going here:

[https://www.linode.com](https://www.linode.com/)

If you prefer, the following referral code will give you two months worth of free usage (up to $100), great for learning Bitcoin:

[https://www.linode.com/?r=3c7fa15a78407c9a3d4aefb027539db2557b3765](https://www.linode.com/?r=3c7fa15a78407c9a3d4aefb027539db2557b3765)

You'll need to provide an email address and later preload money from a credit card or PayPal for future costs.

When you're done, you should land on [https://cloud.linode.com/linodes](https://cloud.linode.com/linodes).

### Consider Two-Factor Authentication

Your server security won't be complete if people can break into your Linode account, so consider setting up Two-Factor Authentication for it. You can find this setting on your [My Profile: Password & Authentication page](https://cloud.linode.com/profile/auth). If you don't do this now, make a TODO item to come back and do it later.

## Creating the Linode Image using a StackScript

### Load the StackScript

Download the [Linode Standup Script](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) from the [Bitcoin Standup Scripts repo](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). This script basically automates all Bitcoin VPS setup instructions. If you want to be particulary prudent, read it over carefully. If you are satisfied, you can copy that StackScript into your own account by going to the [Stackscripts page](https://cloud.linode.com/stackscripts) on your Linode account and selecting to [Create New Stackscript](https://cloud.linode.com/stackscripts/create). Give it a good name (we use Bitcoin Standup), then copy and paste the script. Choose Debian 13 for your target image and "Save" it.

### Do the Initial Setup

You're now ready to create a node based on the Stackscript.

1. On the [Stackscripts page](https://cloud.linode.com/stackscripts?type=account), click on the "..." to the right of your new script and choose "Deploy New Linode".
    
2. Enter the password for the "standup" user. This will be the account that runs bitcoind.
    
3. Fill in a short and a fully qualified hostname
    

- **Short Hostname.** Pick a name for your VPS. For example, "mybtctest".
    
- **Fully Qualified Hostname.** If you're going to include this VPS as part of a network with full DNS records, type in the hostname with its domain. For example, "mybtctest.mydomain.com". Otherwise, just repeat the short hostname and add ".local", for example "mybtctest.local".
    

1. Fill in the appropriate advanced options.
    

- **Installation Type.** This is likely "Mainnet" or "Pruned Mainnet" if you are setting up a node for usage and "Signet" or "Pruned Signet" if you're just playing around. The bulk of this tutorial will assume you chose "Pruned Signet", but you should still be able to follow along with other types. See the [Synopsis](#synopsis-bitcoin-installation-types) for more information on these options. (Note that if you plan to try out the Lightning chapters, you'll probably want to use an Unpruned node, as working with Pruned nodes on Lightning is iffy. See [§18.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_1_Verifying_Your_Lightning_Setup.md#compiling-the-source-code) for the specifics.)
    
- **Timezone.** The timezone your machine is set to.
    
- **Security: Tor X25519 Public Key.** This is a public key to add to Tor's list of authorized clients. If you don't use it, anyone who gets the QR code for your node can access it. You'll get this public key from whichever client you're using to connect to your node. For example, if you use [FullyNoded 2](https://github.com/BlockchainCommons/FullyNoded-2), you can go to its settings and "Export Tor V3 Authentication Public Key" for use here.
    
- **Security: Standup SSH Key.** Copy your local computer's SSH key here; this allows you be able to automatically login in via SSH to the standup account. If you haven't setup an SSH key on your local computer yet, there are good instructions for it on [Github](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/). Using an SSH key will give you a simpler and safer way to log in to your server.
    
- **Security: SSH-Allowed IPs.** This is a comma-separated list of IPs that will be allowed to SSH into the VPS. For example "192.168.1.15,192.168.1.16". If you do not enter any IPs, _your VPS will not be very secure_. It will constantly be bombarded by attackers trying to find their way in, and they may very well succeed.
    
- **Cypherpunkpay.** These are options to install Cypherpunkpay on your server. They're primarily intended for other users of the Standup software and aren't used in this course, so you can just leave them be.
    

1. Choose a region for where the Linode will be located.
    
2. Select an Image
    

- **Target Image.** If you followed the instructions, this will only allow you to select "Debian 13" (though previous versions of this Stackscript worked with Debian 9 through 12, and might still.)
    

### Choose a Linode Plan

You'll next need to choose a Linode plan.

Linode will default to Dedicated-CPU plans, but you can select the more cost-efficient Shared-CPU instead. A Shared-CPU Linode 4GB will suffice for most setups, including: Pruned Mainnet, Pruned Testnet, Pruned Signet, and even non-Pruned Signet. They all use less than 50G of storage and 4GB is a comfortable amount of memory. This is the setup we suggest. It runs $20 per month.

If you want to instead have a non-Pruned Mainnet in a VPS, you'll need to install a Linode with a disk in excess of 715G(!), which is currently the Linode 64 GB, which has 1280G of storage and 64G of memory and costs approximately $384 per month. We do _not_ suggest this. (But see below for alternatives.)

The following chart shows minimum requirements

   
|Setup|Memory|Storage|Linode|
|---|---|---|---|
|Mainnet|2G|~715G|Linode 64GB|
|Pruned Mainnet|2G|~5G|Linode 4GB|
|Signet|2G|~15G|Linode 4GB|
|Pruned Signet|2G|~5G|Linode 4GB|
|Testnet|2G|~170G|Linode 16GB|
|Pruned Testnet|2G|~5G|Linode 4GB|
|Regtest|2G|~|Linode 4GB|

  
  

Note, there may be ways to reduce both costs.

- For the setups we suggest as **Linode 4GB**, you may be able to reduce that to a Linode 2GB. Some versions of Bitcoin Core have worked well at that size, some have occasionally run out of memory and then recovered, and some have continuously run out of memory. Remember to up that swap space to maximize the odds of this working. Use at your own risk.
    
- For the Unpruned Mainnet, which we suggest as a **Linode 64GB**, you can probably get by with a Linode 4GB, but add [Block Storage](https://cloud.linode.com/volumes/create) sufficient to store the blockchain. This is certainly a better long-term solution since the Bitcoin blockchain's storage requirements continuously increase if you don't prune, while the CPU requirements don't (or don't to the same degree). A 750 GibiByte storage would be $75 a month, which combined with a Linode 4GB is $95 a month, instead of $384, and more importantly you can keep growing it. We don't fully document this setup for two reasons (1) we don't suggest the unpruned mainnet setup, and so we suspect it's a much less common setup; and (2) we haven't tested how Linodes volumes compare to their intrinic SSDs for performance and usage. But there's full documentation on the Block Storage page. You'd need to set up the Linode, run its stackscript, but then interrupt it to move the blockchain storage over to a newly commissioned volume before continuing.
    

If you are running a deployment that will be transacting real Bitcoins, you may want to alternatively consider a Dedicated-CPU Linode, which tends to run 50% more expensive than the Shared-CPU Linode. We've generally found the Shared CPUs to be entirely sufficient, but for a wide deployment, you may wish to consider higher levels of reliability.

### Do the Final Setup

You may now want to change your Linode VPS's name from the default linodexxxxxxxx. For instance you might name it bitcoin-signet-pruned to differentiate it from other VPSs in your account.

The last thing you need to do is enter a root password. (If you missed anything, you'll be told so now!). You'll also have the option to add an SSH key for the root user aat this point. We again suggest doing so for both security and convenience purposes.

Linode at this point offers a few choices that have changed over time, but currently include: disk encryption, VPC, firewall, and VLAN. These are generally security features that you would want to consider for a real-world deployment, but don't need to worry about for a testing deployment. (We'd suggest at least a firewall and the disk encryption for a real-world deployment, but we leave that to you and your security people.)

Click "Deploy" to initialize your disks and to prepare your VPS. The whole queue should run in less than a minute. When it's done you should see in the "Host Job Queue", green "Success" buttons stating "Disk Create from StackScript - Setting password for root… done." and "Create Filesystem - 256MB Swap Image".

## Login to Your VPS

If you watch your Linode control panel, you should see the new computer spin up. When the job has reached 100%, you'll be able to login.

First, you'll need the IP address. Click on the "Linodes" tab and you should see a listing of your VPS, the fact that it's running, its "plan", its IP address, and some other information.

Go to your local console and login to the standup account using that address:

ssh standup@[IP-ADDRESS]

For example:

ssh [standup@192.168.33.11](mailto:standup@192.168.33.11)

If you configured your VPS to use an SSH key, the login should be automatic (possibly requiring your SSH password to unlock your key). If you didn't configure a SSH key, then you'll need to type in the user1 password.

### Wait a Few Minutes

Here's a little catch: _your StackScript is running right now_. The BASH script gets executed the first time the VPS is booted. That means your VPS isn't ready yet.

The total run time is about 10 minutes. So, go take a break, get an espresso, or otherwise relax for a few minutes. There are two parts of the script that take a while: the updating of all the Debian packages; and the downloading of the Bitcoin code. They shouldn't take more than 5 minutes each, which means if you come back in 10 minutes, you'll probably be ready to go.

If you're impatient you can jump ahead and sudo tail -f /standup.log which will display the current progress of installation, as described in the next section.

## Verify Your Installation

You'll know that stackscrpit is done when the tail of the standup.log says something like the following:

/root/StackScript - Bitcoin is setup as a service and will automatically start if your VPS reboots and so is Tor  
/root/StackScript - You can manually stop Bitcoin with: sudo systemctl stop bitcoind.service  
/root/StackScript - You can manually start Bitcoin with: sudo systemctl start bitcoind.service

At that point, your home directory should look like this:

$ ls  
bitcoin-30.2-x86_64-linux-gnu.tar.gz wget-btc-output.txt  
SHA256SUMS wget-btc-sha-asc-output.txt  
SHA256SUMS.asc wget-btc-sha-output.txt

These are the various files that were used to install Bitcoin on your VPS. _None_ of them are necessary. We've just left them in case you want to do any additional verification. Otherwise, you can delete them:

$ rm *

### Verify the Bitcoin Setup

In order to ensure that the downloaded Bitcoin release is valid, the StackScript checks both the signature and the SHA checksum. You should verify that both of those tests came back right:

$ sudo grep VERIFICATION /standup.log

If you see something like the following, all should be well:

/root/StackScript - SIG VERIFICATION SUCCESS: 8 GOOD SIGNATURES FOUND.  
/root/StackScript - SHA VERIFICATION SUCCESS / SHA: bitcoin-30.2-x86_64-linux-gnu.tar.gz: OK

If either of those two checks instead reads "VERIFICATION ERROR", then there's a problem.

The log also contains more information on the Signatures, if you want to make sure you know _who_ signed the Bitcoin release:

$ sudo grep -i good /standup.log  
/root/StackScript - SIG VERIFICATION SUCCESS: 8 GOOD SIGNATURES FOUND.  
gpg: Good signature from ".0xB10C [b10c@b10c.me](mailto:b10c@b10c.me)" [unknown]  
gpg: Good signature from "Ava Chow [me@achow101.com](mailto:me@achow101.com)" [unknown]  
gpg: Good signature from "Stephan Oeste (it) [it@oeste.de](mailto:it@oeste.de)" [unknown]  
gpg: Good signature from "Michael Ford (bitcoin-otc) [fanquake@gmail.com](mailto:fanquake@gmail.com)" [unknown]  
gpg: Good signature from "Oliver Gugger [gugger@gmail.com](mailto:gugger@gmail.com)" [unknown]  
gpg: Good signature from "Hennadii Stepanov (GitHub key) [32963518+hebasto@users.noreply.github.com](mailto:32963518+hebasto@users.noreply.github.com)" [unknown]  
gpg: Good signature from "Matthew Zipkin (GitHub Signing Key) [pinheadmz@gmail.com](mailto:pinheadmz@gmail.com)" [unknown]  
gpg: Good signature from "Sjors Provoost [sjors@sprovoost.nl](mailto:sjors@sprovoost.nl)" [unknown]

Since this is all scripted, it's possible that there's just been a minor change that has caused the script's checks not to work right. (This has happened a few times over the existence of the script that became Standup.) But, it's also possible that someone is trying to encourage you to run a fake copy of the Bitcoin daemon. So, _be very sure you know what happened before you make use of Bitcoin!_

### Read the Logs

You may also want to read through all of the setup log files, to make sure that nothing unexpected happened during the installation.

It's best to look through the standard StackScript log file, which has all of the output, including errors:

$ sudo more /standup.log

Note that it is totally normal to see _some_ errors, particularly when running the very noisy gpg software and when various things try to access the non-existant /dev/tty device.

If you want instead to look at a smaller set of info, all of the errors should be in:

$ sudo more /standup.err

It still has a fair amount of information that isn't errors, but it's a quicker read.

If all look good, congratulations, you have a functioning Bitcoin node using Linode!

## What We Have Wrought

Although the default Debian 13 image that we are using for your VPS has been modified by Linode to be relatively secure, your Bitcoin node as installed through the Linode StackScript is set up with an even higher level of security. You may find this limiting, or be unable to do things that you expect. Here are a few notes on that:

### Protected Services

Your Bitcoin VPS installation is minimal and allows almost no communication. This is done through the uncomplicated firewall (ufw), which blocks everything except SSH connections. There's also some additional security possible for your RFC ports, thanks to the hidden services installed by Tor.

**Adjusting UFW.** You should probably leave UFW in its super-protected stage! You don't want to use a Bitcoin machine for other services, because everyone increases your vulnerability! If you decide otherwise, there are several [guides to UFW](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands) that will allow you to add services. As advertised, it's uncomplicated. For example adding mail services would just require opening the mail port: sudo ufw allow 25. But don't do that.

**Adjusting Tor.** You might want to better protect services like SSH. See [Chapter 14: Using Tor](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/14_0_Using_Tor.md) for more on Tor.

### Protected Shells

If you defined "SSH-allowed IPs", SSH (and SCP) access to the server is severely restricted. /etc/hosts.deny disallows anyone from logging in. _We do not suggest changing this_. /etc/hosts.allow then allows specific IP addresses. Just add more IP addresses in a comma-separated list if you need to offer more access.

For example:

sshd: 127.0.0.1, 192.128.23.1

### Automated Upgrades

Debian is also set up to automatically upgrade itself, to ensure that it remains abreast of the newest security patches.

If for some reason you wanted to change this (_we don't suggest it_), you can do this:

echo "unattended-upgrades unattended-upgrades/enable_auto_updates boolean false" | debconf-set-selections

_If you'd like to know more about what the Bitcoin Standup stackscript does, please see_ _[Appendix I: Understanding Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A1_0_Understanding_Bitcoin_Standup.md)._

## Playing with Bitcoin

So now you probably want to play with Bitcoin!

But wait, your Bitcoin daemon is probably still downloading blocks. The bitcoin-cli getblockcount will tell you how you're currently doing:

$ bitcoin-cli getblockcount  
288191

If it's different every time you type the command, you need to wait before working with Bitcoin. This can take hours for a mainnet setup, but if you're using our suggested setup of pruned signet, it should be done in 15 minutes or so.

But, once it settles at a number, you're ready to continue!

Still, it might be time for a few more espressos. But soon enough, your system will be ready to go, and you'll be read to start experimenting.

## Summary: Setting Up a Bitcoin-Core VPS by Hand

Creating a Bitcoin-Core VPS with the Standup scripts made the whole process quick, simple and (hopefully) painless.

## What's Next?

You have a few options for what's next:

- Read the [StackScript](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) to understand your setup.
    
- Read what the StackScript does in [Appendix I](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A1_0_Understanding_Bitcoin_Standup.md).
    
- Choose an entirely alternate methodology in [§2.2: Setting Up a Bitcoin-Core Machine via Other Means](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_2_Setting_Up_Bitcoin_Core_Other.md).
    
- Move on to "bitcoin-cli" with [Chapter Three: Understanding Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_0_Understanding_Your_Bitcoin_Setup.md).
    

## Synopsis: Bitcoin Installation Types

**Mainnet.** This will download the entirety of the Bitcoin blockchain. That's 280G of data (and getting more every day).

**Pruned Mainnet.** This will cut the blockchain you're storing down to just the last 550 blocks. If you're not mining or running some other Bitcoin service, this should be plenty for validation.

**Signet.** This is the newest iteration of a testing network, where Bitcoins don't actually have value, and has largely surpassed Testnet. It's intended for experimentation and testing. Its big advantage is that its block production is more reliable that Testnet, where Testnet could stall out for a while, then produce a bunch of blocks together.

**Pruned Signet.** The last 550 blocks of Signet.

**Testnet.** The older testing network, still useful to some for the ability for miners to force block reorgs (and likely for other specific testing purposes). It's currently testnet3, but we expect it to be updated to testnet4 in the near future (which should drop down the current large size of the blockchain).

**Pruned Testnet.** This is just the last 550 blocks of Testnet ... because the Testnet blockchain is pretty big now too.

**Private Regtest.** This is Regression Testing Mode, which lets you run a totally local Bitcoin server. It allows for even more in-depth testing. There's no pruning needed here, because you'll be starting from scratch. This is a very different setup, and so is covered in [Appendix 3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A3_0_Using_Bitcoin_Regtest.md).

# 2.2: Setting Up a Bitcoin-Core Machine via Other Means

The previous section, [§2.1: Setting Up a Bitcoin-Core VPS with Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md), presumed that you would be creating a full node on a VPS using a Linode Stackscript. However, you can actually create a Bitcoin-Core instance via any methodology of your choice and still follow along with the later steps of this tutorial.

Following are other setup methodologies that we are aware of:

- _[Compiling from Source](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A2_0_Compiling_Bitcoin_from_Source.md)._ If you prefer to compile Bitcoin Core by hand, that's covered in Appendix 2.
    
- _[Using GordianServer-macOS](https://github.com/BlockchainCommons/GordianServer-macOS)._ If you have a modern Mac, you can use Blockchain Commons' _GordianNode_ app, powered by _BitcoinStandup_, to install a full node on your Mac.
    
- _[Using Other Bitcoin Standup Scripts](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts)._ Blockchain Commons also offers a version of the Linode script that you used that can be run from the command line on any Debian or Ubuntu machine. This tends to be the leading-edge script, which means that it's more likely to feature new functions, like Lightning installation.
    
- _[Setting Up a Bitcoin Node on AWS](https://wolfmcnally.com/115/developer-notes-setting-up-a-bitcoin-node-on-aws/)._ @wolfmcnally has written a step-by-step tutorial for setting up Bitcoin-Core with Amazon Web Services (AWS).
    
- _[Setting Up a Bitcoin Node on a Raspberry Pi 3](https://medium.com/@meeDamian/bitcoin-full-node-on-rbp3-revised-88bb7c8ef1d1)._ Damian Mee explains how to set up a headless full node on a Raspberry Pi 3.
    

Be sure that you are installing on a current version of your OS, to avoid problems down the line. As of this writing, this course is tested on Debian 11.

## What's Next?

Unless you want to return to one of the other methodologies for creating a Bitcoin-Core node, you should:

- Move on to "bitcoin-cli" with [Chapter Three: Understanding Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_0_Understanding_Your_Bitcoin_Setup.md).
    

# Chapter Three: Understanding Your Bitcoin Setup

You're now ready to begin working with the bitcoin-cli command-line interface. But that first requires that you understand your Bitcoin setup and its wallet features, which is what will be explained in this chapter.

For this and future chapters, we presume that you have a VPS with Bitcoin installed, running bitcoind. We also presume that you are connected to testnet, allowing for access to bitcoins without using real funds. You can either do this with Bitcoin Standup at Linode.com, per [§2.1: Setting up a Bitcoin-Core VPS with Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md), or via other means, per [§2.2: Setting up a Bitcoin-Core Machine via Other Means](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_2_Setting_Up_Bitcoin_Core_Other.md).

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Demonstrate that Their Bitcoin Node is Installed and Up-to-date
    
- Create an Address to Receive Bitcoin Funds
    
- Use Basic Wallet Commands
    
- Create an Address from a Descriptor
    

Supporting objectives include the ability to:

- Understand the Basic Bitcoin File Layout
    
- Use Basic Informational Commands
    
- Understand What a Bitcoin Address Is
    
- Understand What a Wallet Is
    
- Understand How to Import Addresses
    

## Table of Contents

- [Section One: Verifying Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_1_Verifying_Your_Bitcoin_Setup.md)
    
- [Section Two: Knowing Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_2_Knowing_Your_Bitcoin_Setup.md)
    
- [Section Three: Setting Up Your Wallet](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_3_Setting_Up_Your_Wallet.md)
    
    - [Interlude: Using Command-Line Variables](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_3__Interlude_Using_Command-Line_Variables.md)
        
- [Section Four: Receiving a Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_4_Receiving_a_Transaction.md)
    
- [Section Five: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md)
    

# 3.1: Verifying Your Bitcoin Setup

Before you start playing with Bitcoin, you should ensure that everything is setup correctly.

## Create Your Aliases

We suggest creating some aliases to make it easier to use Bitcoin.

You can do so by putting them in your .bash_profile, .bashrc or .profile.

cat >> ~/.bash_profile <<EOF  
alias btcdir="cd ~/.bitcoin/" #linux default bitcoind path  
alias bc="bitcoin-cli"  
alias bd="bitcoind"  
alias btcinfo='bitcoin-cli getwalletinfo | egrep ""balance""; bitcoin-cli getnetworkinfo | egrep ""version"|connections"; bitcoin-cli getmininginfo | egrep ""blocks"|errors"'  
EOF

After you enter these aliases you can either source .bash_profile to input them or just log out and back in.

Note that these aliases includes shortcuts for running bitcoin-cli, for running bitcoind, and for going to the Bitcoin directory. These aliases are mainly meant to make your life easier. We suggest you create other aliases to ease your use of frequent commands (and arguments) and to minimize errors. Aliases of this sort can be even more useful if you have a complex setup where you regularly run commands associated with Mainnet, with Testnet, _and_ with Regtest, as explained further below.

With that said, use of these aliases in _this_ document might accidentally obscure the core lessons being taught about Bitcoin, so the only alias directly used here is btcinfo because it encapsulates much longer and more complex command. Otherwise, we show the full commands; adjust for your own use as appropriate.

## Run Bitcoind

You'll begin your exploration of the Bitcoin network with the bitcoin-cli command. However, bitcoind _must_ be running to use bitcoin-cli, as bitcoin-cli sends JSON-RPC commands to the bitcoind. If you used our standard setup, bitcoind should already be up and running. You can double check by looking at the process table.

$ ps auxww | grep bitcoind  
standup 455 1.3 34.4 3387536 1392904 ? SLsl Jun16 59:30 /usr/local/bin/bitcoind -conf=/home/standup/.bitcoin/bitcoin.conf

If it's not running, you'll want to run /usr/local/bin/bitcoind -daemon by hand and also place it in your crontab.

## Verify Your Blocks

You should have the whole blockchain downloaded before you start playing. Just run the bitcoin-cli getblockcount alias to see if it's all loaded.

$ bitcoin-cli getblockcount  
1772384

That tells you what's loaded; you'll then need to check that against an online service that tells you the current block height.

> :book: _**What is Block Height?**_ Block height is the the distance that a particular block is removed from the genesis block. The current block height is the block height of the newest block added to a blockchain.

You can do this by looking at a blocknet explorer, such as [the Blockcypher Testnet explorer](https://live.blockcypher.com/btc-testnet/). Does its most recent number match your getblockcount? If so, you're up to date.

If you'd like an alias to look at everything at once, the following currently works for Testnet, but may disappear at some time in the future:

$ echo "alias btcblock='echo $(bitcoin-cli -testnet getblockcount)/$(curl -s [https://blockstream.info/testnet/api/blocks/tip/height](https://blockstream.info/testnet/api/blocks/tip/height))'" >> .bash_profile  
$ source .bash_profile  
$ btcblock  
1804372/1804372

> :link: **TESTNET vs MAINNET:** Remember that this tutorial generally assumes that you are using testnet. If you're using the mainnet instead, you can retrieve the current block height with: curl -s [https://blockchain.info/q/getblockcount](https://blockchain.info/q/getblockcount). You can replace the latter half of the btcblock alias (after /$() with that.

If you're not up-to-date, but your getblockcount is increasing, no problem. Total download time can take from an hour to several hours, depending on your setup.

## Optional: Know Your Server Types

> **TESTNET vs MAINNET:** When you set up your node, you choose to create it as either a Mainnet, Testnet, or Regtest node. Though this document presumes a testnet setup, it's worth understanding how you might access and use the other setup types — even all on the same machine! But, if you're a first-time user, skip on past this, as it's not necessary for a basic setup.

The type of setup is mainly controlled through the ~/.bitcoin/bitcoin.conf file. If you're running testnet, it probably contains this line:

testnet=1

If you're running regtest, it probably contains this line:

regtest=1

However, if you want to run several different sorts of nodes simultaneously, you should leave the testnet (or regtest) flag out of your configuration file. You can then choose whether you're using the mainnet, the testnet, or your regtest every time you run bitcoind or bitcoin-cli.

Here's a set of aliases that would make that easier by creating a specific alias for starting and stopping the bitcoind, for going to the bitcoin directory, and for running bitcoin-cli, for each of the mainnet (which has no extra flags), the testnet (which is -testnet), or your regtest (which is -regtest).

cat >> ~/.bash_profile <<EOF  
alias bcstart="bitcoind -daemon"  
alias btstart="bitcoind -testnet -daemon"  
alias brstart="bitcoind -regtest -daemon"

alias bcstop="bitcoin-cli stop"  
alias btstop="bitcoin-cli -testnet stop"  
alias brstop="bitcoin-cli -regtest stop"

alias bcdir="cd ~/.bitcoin/" #linux default bitcoin path  
alias btdir="cd ~/.bitcoin/testnet" #linux default bitcoin testnet path  
alias brdir="cd ~/.bitcoin/regtest" #linux default bitcoin regtest path

alias bc="bitcoin-cli"  
alias bt="bitcoin-cli -testnet"  
alias br="bitcoin-cli -regtest"  
EOF

For even more complexity, you could have each of your 'start' aliases use the -conf flag to load configuration from a different file. This goes far beyond the scope of this tutorial, but we offer it as a starting point for when your explorations of Bitcoin reaches the next level.

## Summary: Verifying Your Bitcoin Setup

Before you start playing with bitcoin, you should make sure that your aliases are set up, your bitcoind is running, and your blocks are downloaded. You may also want to set up some access to alternative Bitcoin setups, if you're an advanced user.

## What's Next?

Continue "Understanding Your Bitcoin Setup" with [§3.2: Knowing Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_2_Knowing_Your_Bitcoin_Setup.md).

# 3.2: Knowing Your Bitcoin Setup

Before you start playing with Bitcoin, you may always want to come to a better understanding of your setup.

## Know Your Bitcoin Directory

To start with, you should understand where everything is kept: the ~/.bitcoin directory.

The main directory just contains your config file and the testnet directory:

$ ls ~/.bitcoin  
bitcoin.conf testnet3

The setup guides in [Chapter Two: Creating a Bitcoin-Core VPS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_0_Setting_Up_a_Bitcoin-Core_VPS.md) laid out a standardized config file. [§3.1: Verifying Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_1_Verifying_Your_Bitcoin_Setup.md) suggested how to change it to support more advanced setups. If you're interested in learning even more about the config file, you may wish to consult [Jameson Lopp's Bitcoin Core Config Generator](https://jlopp.github.io/bitcoin-core-config-generator/).

Moving back to your ~/.bitcoin directory, you'll find that the testnet3 directory contains all of the guts:

$ ls ~/.bitcoin/testnet3  
banlist.json blocks debug.log mempool.dat peers.dat  
bitcoind.pid chainstate fee_estimates.dat onion_private_key wallets

You shouldn't mess with most of these files and directories — particularly not the blocks and chainstate directories, which contain all of the blockchain data, and the information in your wallets directory, which contains your personal wallet. However, do take careful note of the debug.log file, which you should refer to if you ever have problems with your setup.

> :link: **TESTNET vs MAINNET:** If you're using mainnet, then _everything_ will instead be placed in the main ~/.bitcoin directory. These various setups _do_ elegantly stack, so if you are using mainnet, testnet, and regtest, you'll find that ~/.bitcoin contains your config file and your mainnet data, the ~/.bitcoin/testnet3 directory contains your testnet data, and the ~/.bitcoin/regtest directory contains your regtest data.

## Know Your Bitcoin-cli Commands

Most of your early work will be done with the bitcoin-cli command, which offers an easy interface to bitcoind. If you ever want more information on its usage, just run it with the help argument. Without any other arguments, it shows you every possible command:

$ bitcoin-cli help  
== Blockchain ==  
getbestblockhash  
getblock "blockhash" ( verbosity )  
getblockchaininfo  
getblockcount  
getblockfilter "blockhash" ( "filtertype" )  
getblockhash height  
getblockheader "blockhash" ( verbose )  
getblockstats hash_or_height ( stats )  
getchaintips  
getchaintxstats ( nblocks "blockhash" )  
getdifficulty  
getmempoolancestors "txid" ( verbose )  
getmempooldescendants "txid" ( verbose )  
getmempoolentry "txid"  
getmempoolinfo  
getrawmempool ( verbose )  
gettxout "txid" n ( include_mempool )  
gettxoutproof ["txid",...] ( "blockhash" )  
gettxoutsetinfo  
preciousblock "blockhash"  
pruneblockchain height  
savemempool  
scantxoutset "action" ( [scanobjects,...] )  
verifychain ( checklevel nblocks )  
verifytxoutproof "proof"

== Control ==  
getmemoryinfo ( "mode" )  
getrpcinfo  
help ( "command" )  
logging ( ["include_category",...] ["exclude_category",...] )  
stop  
uptime

== Generating ==  
generatetoaddress nblocks "address" ( maxtries )  
generatetodescriptor num_blocks "descriptor" ( maxtries )

== Mining ==  
getblocktemplate ( "template_request" )  
getmininginfo  
getnetworkhashps ( nblocks height )  
prioritisetransaction "txid" ( dummy ) fee_delta  
submitblock "hexdata" ( "dummy" )  
submitheader "hexdata"

== Network ==  
addnode "node" "command"  
clearbanned  
disconnectnode ( "address" nodeid )  
getaddednodeinfo ( "node" )  
getconnectioncount  
getnettotals  
getnetworkinfo  
getnodeaddresses ( count )  
getpeerinfo  
listbanned  
ping  
setban "subnet" "command" ( bantime absolute )  
setnetworkactive state

== Rawtransactions ==  
analyzepsbt "psbt"  
combinepsbt ["psbt",...]  
combinerawtransaction ["hexstring",...]  
converttopsbt "hexstring" ( permitsigdata iswitness )  
createpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )  
createrawtransaction [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime replaceable )  
decodepsbt "psbt"  
decoderawtransaction "hexstring" ( iswitness )  
decodescript "hexstring"  
finalizepsbt "psbt" ( extract )  
fundrawtransaction "hexstring" ( options iswitness )  
getrawtransaction "txid" ( verbose "blockhash" )  
joinpsbts ["psbt",...]  
sendrawtransaction "hexstring" ( maxfeerate )  
signrawtransactionwithkey "hexstring" ["privatekey",...] ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )  
testmempoolaccept ["rawtx",...] ( maxfeerate )  
utxoupdatepsbt "psbt" ( ["",{"desc":"str","range":n or [n,n]},...] )

== Util ==  
createmultisig nrequired ["key",...] ( "address_type" )  
deriveaddresses "descriptor" ( range )  
estimatesmartfee conf_target ( "estimate_mode" )  
getdescriptorinfo "descriptor"  
signmessagewithprivkey "privkey" "message"  
validateaddress "address"  
verifymessage "address" "signature" "message"

== Wallet ==  
abandontransaction "txid"  
abortrescan  
addmultisigaddress nrequired ["key",...] ( "label" "address_type" )  
backupwallet "destination"  
bumpfee "txid" ( options )  
createwallet "wallet_name" ( disable_private_keys blank "passphrase" avoid_reuse )  
dumpprivkey "address"  
dumpwallet "filename"  
encryptwallet "passphrase"  
getaddressesbylabel "label"  
getaddressinfo "address"  
getbalance ( "dummy" minconf include_watchonly avoid_reuse )  
getbalances  
getnewaddress ( "label" "address_type" )  
getrawchangeaddress ( "address_type" )  
getreceivedbyaddress "address" ( minconf )  
getreceivedbylabel "label" ( minconf )  
gettransaction "txid" ( include_watchonly verbose )  
getunconfirmedbalance  
getwalletinfo  
importaddress "address" ( "label" rescan p2sh )  
importmulti "requests" ( "options" )  
importprivkey "privkey" ( "label" rescan )  
importprunedfunds "rawtransaction" "txoutproof"  
importpubkey "pubkey" ( "label" rescan )  
importwallet "filename"  
keypoolrefill ( newsize )  
listaddressgroupings  
listlabels ( "purpose" )  
listlockunspent  
listreceivedbyaddress ( minconf include_empty include_watchonly "address_filter" )  
listreceivedbylabel ( minconf include_empty include_watchonly )  
listsinceblock ( "blockhash" target_confirmations include_watchonly include_removed )  
listtransactions ( "label" count skip include_watchonly )  
listunspent ( minconf maxconf ["address",...] include_unsafe query_options )  
listwalletdir  
listwallets  
loadwallet "filename"  
lockunspent unlock ( [{"txid":"hex","vout":n},...] )  
removeprunedfunds "txid"  
rescanblockchain ( start_height stop_height )  
sendmany "" {"address":amount} ( minconf "comment" ["address",...] replaceable conf_target "estimate_mode" )  
sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount replaceable conf_target "estimate_mode" avoid_reuse )  
sethdseed ( newkeypool "seed" )  
setlabel "address" "label"  
settxfee amount  
setwalletflag "flag" ( value )  
signmessage "address" "message"  
signrawtransactionwithwallet "hexstring" ( [{"txid":"hex","vout":n,"scriptPubKey":"hex","redeemScript":"hex","witnessScript":"hex","amount":amount},...] "sighashtype" )  
unloadwallet ( "wallet_name" )  
walletcreatefundedpsbt [{"txid":"hex","vout":n,"sequence":n},...] [{"address":amount},{"data":"hex"},...] ( locktime options bip32derivs )  
walletlock  
walletpassphrase "passphrase" timeout  
walletpassphrasechange "oldpassphrase" "newpassphrase"  
walletprocesspsbt "psbt" ( sign "sighashtype" bip32derivs )

== Zmq ==  
getzmqnotifications

You can also type bitcoin-cli help [command] to get even more extensive info on that command. For example:

$ bitcoin-cli help getmininginfo  
...  
Returns a json object containing mining-related information.  
Result:  
{ (json object)  
"blocks" : n, (numeric) The current block  
"currentblockweight" : n, (numeric, optional) The block weight of the last assembled block (only present if a block was ever assembled)  
"currentblocktx" : n, (numeric, optional) The number of block transactions of the last assembled block (only present if a block was ever assembled)  
"difficulty" : n, (numeric) The current difficulty  
"networkhashps" : n, (numeric) The network hashes per second  
"pooledtx" : n, (numeric) The size of the mempool  
"chain" : "str", (string) current network name (main, test, regtest)  
"warnings" : "str" (string) any network and blockchain warnings  
}

Examples:

> bitcoin-cli getmininginfo  
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id": "curltest", "method": "getmininginfo", "params": []}' -H 'content-type: text/plain;' http://127.0.0.1:8332/

> :book: _**What is RPC?**_ bitcoin-cli is just a handy interface that lets you send commands to the bitcoind. More specifically, it's an interface that lets you send RPC (or Remote Procedure Protocol) commands to the bitcoind. Often, the bitcoin-cli command and the RPC command have identical names and interfaces, but some bitcoin-cli commands instead provide shortcuts for more complex RPC requests. Generally, the bitcoin-cli interface is much cleaner and simpler than trying to send RPC commands by hand, using curl or some other method. However, it also has limitations as to what you can ultimately do.

## Optional: Know Your Bitcoin Info

A variety of bitcoin-cli commands can give you additional information on your bitcoin data. The most general ones are:

bitcoin-cli -getinfo returns information from different RPCs (user-friendly)

$ bitcoin-cli -getinfo

! Chain: test  
Blocks: 1977694  
Headers: 1977694  
Verification progress: 0.9999993275374796  
Difficulty: 1

- Network: in 0, out 8, total 8  
    Version: 219900  
    Time offset (s): 0  
    Proxy: N/A  
    Min tx relay fee rate (BTC/kvB): 0.00001000
    

@@ Wallet: ""@@  
Keypool size: 1000  
Unlocked until: 0  
Transaction fee rate (-paytxfee) (BTC/kvB): 0.00000000

# Balance: 0.02853102

- Warnings: unknown new rules activated (versionbit 28)
    

Other commands to get information about blockchain, mining, network, wallet etc.

$ bitcoin-cli getblockchaininfo  
$ bitcoin-cli getmininginfo  
$ bitcoin-cli getnetworkinfo  
$ bitcoin-cli getnettotals  
$ bitcoin-cli getwalletinfo

For example bitcoin-cli getnetworkinfo gives you a variety of information on your setup and its access to various networks:

$ bitcoin-cli getnetworkinfo  
{  
"version": 200000,  
"subversion": "/Satoshi:0.20.0/",  
"protocolversion": 70015,  
"localservices": "0000000000000408",  
"localservicesnames": [  
"WITNESS",  
"NETWORK_LIMITED"  
],  
"localrelay": true,  
"timeoffset": 0,  
"networkactive": true,  
"connections": 10,  
"networks": [  
{  
"name": "ipv4",  
"limited": false,  
"reachable": true,  
"proxy": "",  
"proxy_randomize_credentials": false  
},  
{  
"name": "ipv6",  
"limited": false,  
"reachable": true,  
"proxy": "",  
"proxy_randomize_credentials": false  
},  
{  
"name": "onion",  
"limited": false,  
"reachable": true,  
"proxy": "127.0.0.1:9050",  
"proxy_randomize_credentials": true  
}  
],  
"relayfee": 0.00001000,  
"incrementalfee": 0.00001000,  
"localaddresses": [  
{  
"address": "45.79.111.171",  
"port": 18333,  
"score": 1  
},  
{  
"address": "2600:3c01::f03c:92ff:fecc:fdb7",  
"port": 18333,  
"score": 1  
},  
{  
"address": "4wrr3ktm6gl4sojx.onion",  
"port": 18333,  
"score": 4  
}  
],  
"warnings": "Warning: unknown new rules activated (versionbit 28)"  
}

Feel free to reference any of these and to use "bitcoin-cli help" if you want more information on what any of them do.

## Summary: Knowing Your Bitcoin Setup

The ~/.bitcoin directory contains all of your files, while bitcoin-cli help and a variety of info commands can be used to get more information on how your setup and Bitcoin work.

## What's Next?

Continue "Understanding Your Bitcoin Setup" with [§3.3: Setting Up Your Wallet](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_3_Setting_Up_Your_Wallet.md).

# Interlude: Using Command-Line Variables

The previous section demonstrated a number of command-line commands used without obfuscation or interference. However, that's often not the best way to run Bitcoin from the command line. Because you're dealing with long, complex, and unreadable variables, it's easy to make a mistake if you're copying those variables around (or, satoshi forfend, if you're typing them in by hand). Because those variables can mean the difference between receiving and losing real money, you don't _want_ to make mistakes. For these reasons, we strongly suggest using command-line variables to save addresses, signatures, or other long strings of information whenever it's reasonable to do so.

If you're using bash, you can save information to a variable like this:

$ VARIABLE=$(command)

That's a simple command substitution, the equivalent to VARIABLE=command . The command inside the parentheses is run, then assigned to the VARIABLE.

To create a new address would then look like this:

$ unset NEW_ADDRESS_1  
$ NEW_ADDRESS_1=$(bitcoin-cli getnewaddress "" legacy)

These commands clear the NEW_ADDRESS_1 variable, just to be sure, then fill it with the results of the bitcoin-cli getnewaddress command.

You can then use your shell's echo command to look at your (new) address:

$ echo $NEW_ADDRESS_1  
mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE

Because you have your address in a variable, you can now easily sign a message for that address, without worrying about mistyping the address. You'll of course save that signature into a variable too!

$ NEW_SIG_1=$(bitcoin-cli signmessage $NEW_ADDRESS_1 "Hello, World")  
$ echo $NEW_SIG_1  
IPYIzgj+Rg4bxDwCyoPiFiNNcxWHYxgVcklhmN8aB2XRRJqV731Xu9XkfZ6oxj+QGCRmTe80X81EpXtmGUpXOM4=

The rest of this tutorial will use this style of saving information to variables when it's practical.

> :book: _**When is it not practical to use command-line variables?**_ Command-line variables aren't practical if you need to use the information somewhere other than on the command line. For example, saving your signature may not actually be useful if you're just going to have to send it to someone else in an email. In addition, some future commands will output JSON objects instead of simple information, and variables can't be used to capture that information ... at least not without a _little_ more work.

## Summary: Using Command-Line Variables

Shell variables can be used to hold long Bitcoin strings, minimizing the chances of mistakes.

## What's Next?

Continue "Understanding Your Bitcoin Setup" with [§3.4: Receiving a Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_4_Receiving_a_Transaction.md).

# 3.3: Setting Up Your Wallet

You're now ready to start working with Bitcoin. To begin with, you'll need to create a wallet for sending and receiving funds.

## Create a Wallet

> :warning: **VERSION WARNING:** Newer versions of Bitcoin Core, starting with v0.21.0, will no longer automatically create a default wallet on startup. So, you will need to manually create one. But if you're running an older version of Bitcoin Core, a new wallet has already been created for you, in which case you can skip ahead to [Create an Address](#create-an-address).

The first thing you need to do is create a new wallet, which can be done with the bitcoin-cli createwallet command. By creating a new wallet, you'll be creating your public-private key pair. Your public key is the source from which your addresses will be created, and your private key is what will allow you to spend any funds you receive into your addresses. Bitcoin Core will automatically save that information into a wallet.dat file in your ~/.bitcoin/testnet3/wallets directory.

If you check your wallets directory, you'll see that it's currently empty.

$ ls ~/.bitcoin/testnet3/wallets  
$

Although Bitcoin Core won't create a new wallet for you, it will still load a top-level unnamed ("") wallet on startup by default. You can take advantage of this by creating a new unnamed wallet.

$ bitcoin-cli -named createwallet wallet_name="" descriptors=false

{  
"name": "",  
"warning": ""  
}

Now, your wallets directory should be populated.

$ ls ~/.bitcoin/testnet3/wallets  
database db.log wallet.dat

> :book: _**What is a Bitcoin wallet?**_ A Bitcoin wallet is the digital equivalent of a physical wallet on the Bitcoin network. It stores information on the amount of bitcoins you have and where it's located (addresses), as well as the ways you can use to spend it. Spending physical money is intuitive, but to spend bitcoins users need to provide the correct _private key_. We will explain this in more detail throughout the course, but what you should know for now is that this public-private key dynamic is part of what makes Bitcoin secure and trustless. Your key pair information is saved in the wallet.dat file, in addition to data about preferences and transactions. For the most part, you won't have to worry about that private key: bitcoind will use it when it's needed. However, this makes the wallet.dat file extremely important: if you lose it, you lose your private keys, and if you lose your private keys, you lose your funds!

Sweet, now you have a Bitcoin wallet. But a wallet will be of little use for receiving bitcoins if you don't create an address first.

> :warning: **VERSION WARNING:** Starting in Bitcoin Core v 23.0, descriptor wallets became the default. That's great, because descriptor wallets are very powerful, except they don't currently work with multisigs! So, we turn them off with the "descriptors=false" argument. See [§3.5](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/03_5_Understanding_the_Descriptor.md) for more on descriptors.

## Create an Address

The next thing you need to do is create an address for receiving payments. This is done with the bitcoin-cli getnewaddress command. Remember that if you want more information on this command, you should type bitcoin-cli help getnewaddress. Currently, there are three types of addresses: legacy and the two types of SegWit address, p2sh-segwit and bech32. If you do not otherwise specify, you'll get the default, which is currently bech32.

However, for the next few sections we're instead going to be using legacy addresses, both because bitcoin-cli had some teething problems with its early versions of SegWit addresses, and because other people might not be able to send to bech32 addresses. This is all unlikely to be a problem for you now, but for the moment we want to get your started with transaction examples that are (mostly) guaranteed to work.

First, restart bitcoind so your new unnamed wallet is set as default and automatically loaded.

$ bitcoin-cli stop  
Bitcoin Core stopping # wait a minute so it stops completely  
$ bitcoind -daemon  
Bitcoin Core starting # wait a minute so it starts completely

You can now create an address. You can require legacy address either with the second argument to getnewaddress or with the named addresstype argument.

$ bitcoin-cli getnewaddress -addresstype legacy  
moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B

Note that this address begins with an "m" (or sometimes an "n") to signify a testnet Legacy address. It would be a "2" for a P2SH address or a "tb1" for a Bech32 address.

> :link: **TESTNET vs MAINNET:** The equivalent mainnet address would start with a "1" (for Legacy), "3" (for P2SH), or "bc1" (for Bech32).

Take careful note of the address. You'll need to give it to whomever will be sending you funds.

> :book: _**What is a Bitcoin address?**_ A Bitcoin address is literally where you receive money. It's like an email address, but for funds. Technically, it's a public key, though different address schemes adjust that in different ways. However unlike an email address, a Bitcoin address should be considered single use: use it to receive funds just _once_. When you want to receive funds from someone else or at some other time, generate a new address. This is suggested in large part to improve your privacy. The whole blockchain is immutable, which means that explorers can look at long chains of transactions over time, making it possible to statistically determine who you and your contacts are, no matter how careful you are. However, if you keep reusing the same address, then this becomes even easier. By creating your first Bitcoin address, you've also begun to fill in your Bitcoin wallet. More precisely, you've begun to fill the wallet.dat file in your ~/.bitcoin/testnet3 /wallets directory.

With a single address in hand, you could jump straight to the next section and begin receiving funds. However, before we get there, we're going to briefly discuss the other sorts of addresses that you'll meet in the future and talk about a few other wallet commands that you might want to use in the future.

### Knowing Your Bitcoin Addresses

There are three types of Bitcoin addresses that you can create with the getnewaddress RPC command. You'll be using a legacy (P2PKH) address here, while you'll move over to a SegWit (P2SH-SegWit) or Bech32 address in [§4.6: Creating a Segwit Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md).

As noted above, the foundation of a Bitcoin address is a public key: someone sends funds to your public key, and then you use your private key to redeem it. Easy? Except putting your public key out there isn't entirely secure. At the moment, if someone has your public key, then they can't retrieve your private key (and thus your funds); that's the basis of cryptography, which uses a trap-door function to ensure that you can only go from private to public key, and not vice-versa. But the problem is that we don't know what the future might bring. Except we do know that cryptography systems eventually get broken by the relentless advance of technology, so it's better not to put raw public keys on the 'net, to future-proof your transactions.

Classic Bitcoin transactions created P2PKH addresses that added an additional cryptographic step to protect public keys.

> :book: _**What is a Legacy (P2PKH) address?**_ This is a Legacy address of the sort used by the early Bitcoin network. We'll be using it in examples for the next few sections. It's called a Pay to PubKey Hash (or P2PKH) address because the address is a 160-bit hash of a public key. Using a hash of your public key as your address creates a two-step process where to spend funds you need to reveal both the private key and the public key, and it increases future security accordingly. This sort of address remains important for receiving funds from people with out-of-date wallet software.

As described more fully in [§4.6: Creating a Segwit Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md), the Block Size Wars of the late '10s resulted in a new sort of address: SegWit. This is the preferred sort of address currently, and should be fully integrated into Bitcoin-Core at this point, but nonetheless we're saving it for §4.6.

SegWit simply means "segregated witness" and it's a way of separating the transaction signatures out from the rest of the transaction to reduce transaction size. Some SegWit addresses will sneak into some of our examples prior to §4.6 as change addresses, which you'll see as addresses that begin with "tb". This is fine because the bitcoin-cli entirely supports their usage. But we won't use them otherwise.

There are two addresses of this sort:

> :book: _**What is a P2SH-SegWit (aka Nested SegWit) address?**_ This is the first generation of SegWit. It wraps the SegWit address in a Script hash to ensure backward compatibility. The result creates transactions that are about 25%+ smaller (with corresponding reductions in transaction fees). :book: _**What is a Bech32 (aka Native SegWit, aka P2WPKH) address?**_ This is the second generation of SegWit. It's fully described in [BIP 173](https://en.bitcoin.it/wiki/BIP_0173). It creates transactions that are even smaller but more notably also has some advantages in creating addresses that are less prone to human error and have some implicit error-correction beyond that. It is _not_ backward compatible like P2SH-SegWit was, and so some people may not be able to send to it.

There are other sorts of Bitcoin addresses, such as P2PK (which paid to a bare public key, and is deprecated because of its future insecurity) and P2SH (which pays to a Script Hash, and which is used by the first-generation Nested SegWit addresses; we'll meet it more fully in a few chapters).

## Optional: Sign a Message

Sometimes you'll need to prove that you control a Bitcoin address (or rather, that you control its private key). This is important because it lets people know that they're sending funds to the right person. This can be done by creating a signature with the bitcoin-cli signmessage command, in the form bitcoin-cli signmessage [address] [message]. For example:

$ bitcoin-cli signmessage "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "Hello, World"  
HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=

You'll get the signature as a return.

> :book: _**What is a signature?**_ A digital signature is a combination of a message and a private key that can then be unlocked with a public key. Since there's a one-to-one correspendence between the elements of a keypair, unlocking with a public key proves that the signer controlled the corresponding private key.

Another person can then use the bitcoin-cli verifymessage command to verify the signature. He inputs the address in question, the signature, and the message:

$ bitcoin-cli verifymessage "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=" "Hello, World"  
true

If they all match up, then the other person knows that he can safely transfer funds to the person who signed the message by sending to the address.

If some black hat was making up signatures, this would instead produce a negative result:

$ bitcoin-cli verifymessage "FAKEV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B" "HyIP0nzdcH12aNbQ2s2rUxLwzG832HxiO1vt8S/jw+W4Ia29lw6hyyaqYOsliYdxne70C6SZ5Utma6QY/trHZBI=" "Hello, World"  
error code: -3  
error message:  
Invalid address

## Optional: Dump Your Wallet

It might seem dangerous having all of your irreplaceable private keys in a single file. That's what bitcoin-cli dumpwallet is for. It lets you make a copy of your wallet.dat:

$ bitcoin-cli dumpwallet ~/mywallet.txt

The mywallet.txt file in your home directory will have a long list of private keys, addresses, and other information. Mind you, you'd never want to put this data out in a plain text file on a Bitcoin setup with real funds!

You can then recover it with bitcoin-cli importwallet.

$ bitcoin-cli importwallet ~/mywallet.txt

But note this requires an unpruned node!

$ bitcoin-cli importwallet ~/mywallet.txt  
error code: -4  
error message:  
Importing wallets is disabled when blocks are pruned

## Optional: View Your Private Keys

Sometimes, you might want to actually look at the private keys associated with your Bitcoin addresses. Perhaps you want to be able to sign a message or spend bitcoins from a different machine. Perhaps you just want to back up certain important private keys. You can also do this with your dump file, since it's human readable.

$ bitcoin-cli dumpwallet ~/mywallet.txt  
{  
"filename": "/home/standup/mywallet.txt"  
}

More likely, you just want to look at the private key associated with a specific address. This can be done with the bitcoin-cli dumpprivkey command.

$ bitcoin-cli dumpprivkey "moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B"  
cTv75T4B3NsG92tdSxSfzhuaGrzrmc1rJjLKscoQZXqNRs5tpYhH

You can then save that key somewhere safe, preferably somewhere not connected to the internet.

You can also import any private key, from a wallet dump or an individual key dump, as follows:

$ bitcoin-cli importprivkey cW4s4MdW7BkUmqiKgYzSJdmvnzq8QDrf6gszPMC7eLmfcdoRHtHh

Again, expect this to require an unpruned node. Expect this to take a while, as bitcoind needs to reread all past transactions, to see if there are any new ones that it should pay attention to.

> :information_source: **NOTE:** Many modern wallets prefer [mnemonic codes](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) to generate the seeds necessary to create the private keys. This methodology is not used bitcoin-cli, so you won't be able to generate handy word lists to remember your private keys.

_You've been typing that Bitcoin address you generated a lot, while you were signing messages and now dumping keys. If you think it's a pain, we agree. It's also prone to errors, a topic that we'll address in the very next section._

## Summary: Setting Up Your Wallet

You need to create an address to receive funds. Your address is stored in a wallet, which you can back up. You can also do lots more with an address, like dumping its private key or using it to sign messages. But really, creating that address is _all_ you need to do in order to receive Bitcoin funds.

## What's Next?

Step back from "Understanding Your Bitcoin Setup" with [Interlude: Using Command-Line Variables](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_3__Interlude_Using_Command-Line_Variables.md).

# 3.4: Receiving a Transaction

You're now ready to receive some money at the new address you set up.

## Get Some Money

To do anything more, you need to get some money. On testnet this is done through faucets. Since the money is all pretend, you just go to a faucet, request some money, and it will be sent over to you. We suggest using the faucet at [https://testnet-faucet.mempool.co/](https://testnet-faucet.mempool.co/), [https://bitcoinfaucet.uo1.net/](https://bitcoinfaucet.uo1.net/), or [https://testnet.coinfaucet.eu/en/](https://testnet.coinfaucet.eu/en/). If they're not available for some reason, search for "bitcoin testnet faucet", and you should find others.

To use a faucet, you'll usually need to go to a URL and copy and paste in your address. Note that this is one of those cases where you won't be able to use command-line variables, alas. Afterward, a transaction will be created that sends money from the faucet to you.

> :book: _**What is a transaction?**_ A transaction is a bitcoin exchange. The owner of some bitcoins uses his private key to access those coins, then locks the transaction using the recipient's public key. :link: **TESTNET vs MAINNET:** Sadly, there are no faucets in real life. If you were playing on the mainnet, you'd need to go and actually buy bitcoins at a bitcoin exchange or ATM, or you'd need to get someone to send them to you. Testnet life is much easier.

## Verify Your Money

After you've requested your money, you should be able to verify it with the bitcoin-cli getbalance command:

$ bitcoin-cli getbalance  
0.00000000

But wait, there's no balance yet!?

Welcome to the world of Bitcoin latency. The problem is that your transaction hasn't yet been recorded in a block!

> :book: _**What is a block?**_ Transactions are transmitted across the network and gathered into blocks by miners. These blocks are secured with a mathematical proof-of-work, which proves that computing power has been expended as part of the block creation. It's that proof-of-work (multiplied over many blocks, each built atop the last) that ultimately keeps Bitcoin secure. :book: _**What is a miner?**_ A miner is a participant of the Bitcoin network who works to create blocks. It's a paying job: when a miner successfully creates a block, he is paid a one-time reward plus the fees for the transactions in his block. Mining is big business. Miners tend to run on special hardware, accelerated in ways that make it more likely that they'll be able to create blocks. They also tend to be part of mining pools, where the miners all agree to share out the rewards when one of them successfully creates a block.

Fortunately, bitcoin-cli getunconfirmedbalance should still show your updated balance as long as the initial transaction has been created:

$ bitcoin-cli getunconfirmedbalance  
0.01010000

If that's still showing a zero too, you're probably moving through this tutorial too fast. Wait a second. The coins should show up unconfirmed, then rapidly move to confirmed. Do note that a coin can move from unconfirmedbalance to confirmedbalance almost immediately, so make sure you check both. However, if your getbalance and your getunconfirmedbalance both still show zero in ten minutes, then there's probably something wrong with the faucet, and you'll need to pick another.

### Gain Confidence in Your Money

You can use bitcoin-cli getbalance "*" [n], where you replace [n] with an integer, to see if a confirmed balance is 'n' blocks deep.

> :book: _**What is block depth?**_ After a block is built and confirmed, another block is built on top of it, and another ... Because this is a stochastic process, there's some chance for reversal when a block is still new. Thus, a block has to be buried several blocks deep in a chain before you can feel totally confident in your funds. Each of those blocks tends to be built in an average of 10 minutes ... so it usually takes about an hour for a confirmed transaction to receive six blocks deep, which is the measure for full confidence in Bitcoin.

The following shows that our transactions have been confirmed one time, but not twice:

$ bitcoin-cli getbalance "_" 1_  
_0.01010000_  
_$ bitcoin-cli getbalance "_" 2  
0.00000000

Obviously, every ten minutes or so this depth will increase.

Of course, on the testnet, no one is that worried about how reliable your funds are. You'll be able to spend your money as soon as it's confirmed.

## Verify Your Wallet

The bitcoin-cli getwalletinfo command gives you more information on the balance of your wallet:

$ bitcoin-cli getwalletinfo  
{  
"walletname": "",  
"walletversion": 169900,  
"balance": 0.01010000,  
"unconfirmed_balance": 0.00000000,  
"immature_balance": 0.00000000,  
"txcount": 2,  
"keypoololdest": 1592335137,  
"keypoolsize": 999,  
"hdseedid": "fdea8e2630f00d29a9d6ff2af7bf5b358d061078",  
"keypoolsize_hd_internal": 1000,  
"paytxfee": 0.00000000,  
"private_keys_enabled": true,  
"avoid_reuse": false,  
"scanning": false  
}

## Discover Your Transaction ID

Your money came into your wallet via a transaction. You can discover that transactionid (txid) with the bitcoin-cli listtransactions command:

$ bitcoin-cli listtransactions  
[  
{  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"category": "receive",  
"amount": 0.01000000,  
"label": "",  
"vout": 1,  
"confirmations": 1,  
"blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",  
"blockheight": 1772396,  
"blockindex": 73,  
"blocktime": 1592600085,  
"txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",  
"walletconflicts": [  
],  
"time": 1592599884,  
"timereceived": 1592599884,  
"bip125-replaceable": "no"  
},  
{  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"category": "receive",  
"amount": 0.00010000,  
"label": "",  
"vout": 0,  
"confirmations": 1,  
"blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",  
"blockheight": 1772396,  
"blockindex": 72,  
"blocktime": 1592600085,  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"walletconflicts": [  
],  
"time": 1592599938,  
"timereceived": 1592599938,  
"bip125-replaceable": "no"  
}  
]

This shows two transactions (8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9) and (ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36) for a specific amount (0.01000000 and 0.00010000), which were both received (receive) by the same address in our wallet (mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE). That's bad key hygeine, by the way: you should use a new address for every single Bitcoin you ever receive. In this case, we got impatient because the first faucet didn't seem to be working.

You can access similar information with the bitcoin-cli listunspent command, but it only shows the transactions for the money that you haven't spent. These are called UTXOs, and will be vitally important when you're sending money back out into the Bitcoin world:

$ bitcoin-cli listunspent  
[  
{  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"vout": 0,  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"label": "",  
"scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",  
"amount": 0.00010000,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",  
"safe": true  
},  
{  
"txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",  
"vout": 1,  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"label": "",  
"scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",  
"amount": 0.01000000,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",  
"safe": true  
}  
]

Note that bitcoins are not just a homogeneous mess of cash jammed into your pocket. Each individual transaction that you receive or that you send is placed into the immutable blockchain ledger, in a block. You can see these individual transactions when you look at your unspent money. This means that bitcoin spending isn't quite as anonymous as you'd think. Though the addresses are fairly private, transactions can be examined as they go in and out of addresses. This makes privacy vulnerable to statistical analysis. It also introduces some potential non-fungibility to bitcoins, as you can track back through series of transactions, even if you can't track a specific "bitcoin".

> :book: _**Why are all of these bitcoin amounts in fractions?**_ Bitcoins are produced slowly, and so there are relatively few in circulation. As a result, each bitcoin over on the mainnet is worth quite a bit (~ $9,000 at the time of this writing). This means that people usually work in fractions. In fact, the .0101 in Testnet coins would be worth about $100 if they were on the mainnet. For this reason, names have appeared for smaller amounts of bitcoins, including millibitcoins or mBTCs (one-thousandth of a bitcoin), microbitcoins or bits or μBTCs (one-millionth of a bitcoin), and satoshis (one hundred millionth of a bitcoin).

## Examine Your Transaction

You can get more information on a transaction with the bitcoin-cli gettransaction command:

$ bitcoin-cli gettransaction "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9"  
{  
"amount": 0.01000000,  
"confirmations": 1,  
"blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",  
"blockheight": 1772396,  
"blockindex": 73,  
"blocktime": 1592600085,  
"txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",  
"walletconflicts": [  
],  
"time": 1592599884,  
"timereceived": 1592599884,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"category": "receive",  
"amount": 0.01000000,  
"label": "",  
"vout": 1  
}  
],  
"hex": "0200000000010114d04977d1b0137adbf51dd5d79944b9465a2619f3fa7287eb69a779977bf5800100000017160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4ffeffffff02df690f000000000017a9145c3bfb36b03f279967977ca9d1e35185e39917788740420f00000000001976a9141b72503639a13f190bf79acf6d76255d772360b788ac0247304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e1330121022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c270b1b00"  
}

The gettransaction command will detail transactions that are in your wallet, such as this one, that was sent to us.

Note that gettransaction has two optional arguments:

$ bitcoin-cli help gettransaction  
gettransaction "txid" ( include_watchonly verbose )

Get detailed information about in-wallet transaction

Arguments:

1. txid (string, required) The transaction id
    
2. include_watchonly (boolean, optional, default=true for watch-only wallets, otherwise false) Whether to include watch-only addresses in balance calculation and details[]
    
3. verbose (boolean, optional, default=false) Whether to include a decoded field containing the decoded transaction (equivalent to RPC decoderawtransaction)
    

By setting these two true or false, we can choose to include watch-only addresses in the output (which we don't care about) or look at more verbose output (which we do).

Here's what this data instead looks at when we set include_watchonly to false and verbose to true.

$ bitcoin-cli gettransaction "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9" false true  
{  
"amount": 0.01000000,  
"confirmations": 3,  
"blockhash": "00000000000001753b24411d0e4726212f6a53aeda481ceff058ffb49e1cd969",  
"blockheight": 1772396,  
"blockindex": 73,  
"blocktime": 1592600085,  
"txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",  
"walletconflicts": [  
],  
"time": 1592599884,  
"timereceived": 1592599884,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"category": "receive",  
"amount": 0.01000000,  
"label": "",  
"vout": 1  
}  
],  
"hex": "0200000000010114d04977d1b0137adbf51dd5d79944b9465a2619f3fa7287eb69a779977bf5800100000017160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4ffeffffff02df690f000000000017a9145c3bfb36b03f279967977ca9d1e35185e39917788740420f00000000001976a9141b72503639a13f190bf79acf6d76255d772360b788ac0247304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e1330121022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c270b1b00",  
"decoded": {  
"txid": "8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9",  
"hash": "d4ae2b009c43bfe9eba96dcd16e136ceba2842df3d76a67d689fae5975ce49cb",  
"version": 2,  
"size": 249,  
"vsize": 168,  
"weight": 669,  
"locktime": 1772327,  
"vin": [  
{  
"txid": "80f57b9779a769eb8772faf319265a46b94499d7d51df5db7a13b0d17749d014",  
"vout": 1,  
"scriptSig": {  
"asm": "0014e85ba02862dbadabd6d204fcc8bb5d54658c7d4f",  
"hex": "160014e85ba02862dbadabd6d204fcc8bb5d54658c7d4f"  
},  
"txinwitness": [  
"304402201e74bdfc330fc2e093a8eabe95b6c5633c8d6767249fa25baf62541a129359c202204d462bd932ee5c15c7f082ad7a6b5a41c68addc473786a0a9a232093fde8e13301",  
"022897dfbf085ecc6ad7e22fc91593414a845659429a7bbb44e2e536258d2cbc0c"  
],  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01010143,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 5c3bfb36b03f279967977ca9d1e35185e3991778 OP_EQUAL",  
"hex": "a9145c3bfb36b03f279967977ca9d1e35185e399177887",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N1ev1WKevSsdmAvRqZf7JjvDg223tPrVCm"  
]  
}  
},  
{  
"value": 0.01000000,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 1b72503639a13f190bf79acf6d76255d772360b7 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE"  
]  
}  
}  
]  
}  
}

Now you can see the full information on the transaction, including all of the inputs ("vin") and all the outputs ("vout). One of the interesting things to note is that although we received .01 BTC in the transaction, another .01010143 was sent to another address. That was probably a change address, a concept that is explored in the next section. It is quite typical for a transaction to have multiple inputs and/or multiple outputs.

There is another command, getrawtransaction, which allows you to look at transactions that are not in your wallet. However, it requires you to have an unpruned node and txindex=1 in your bitcoin.conf file. Unless you have a serious need for information not in your wallet, it's probably just better to use a Bitcoin explorer for this sort of thing ...

## Optional: Use a Block Explorer

Even looking at the verbose information for a transaction can be a little intimidating. The main goal of this tutorial is to teach how to deal with raw transactions from the command line, but we're happy to talk about other tools when they're applicable. One of those tools is a block explorer, which you can use to look at transactions from a web browser in a much friendlier format.

Currently, our preferred block explorer is [https://live.blockcypher.com/](https://live.blockcypher.com/).

You can use it to look up transactions for an address:

[https://live.blockcypher.com/btc-testnet/address/mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE/](https://live.blockcypher.com/btc-testnet/address/mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE/)

You can also use it to look at individual transactions:

[https://live.blockcypher.com/btc-testnet/tx/8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9/](https://live.blockcypher.com/btc-testnet/tx/8e2ab10cabe9ec04ed438086a80b1ac72558cc05bb206e48fc9a18b01b9282e9/)

A block explorer doesn't generally provide any more information than a command line look at a raw transaction; it just does a good job of highlighting the important information and putting together the puzzle pieces, including the transaction fees behind a transaction — another concept that we'll be covering in future sections.

## Summary: Receiving a Transaction

Faucets will give you money on the testnet. They come in as raw transactions, which can be examined with gettransaction or a block explorer. Once you've receive a transaction, you can see it in your balance and your wallet.

## What's Next?

For a deep dive into how addresses are described, so that they can be transferred or made into parts of a multi-signature, see [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md).

But if that's too in-depth, continue on to [Chapter Four: Sending Bitcoin Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_0_Sending_Bitcoin_Transactions.md).

# 3.5: Understanding the Descriptor

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

You may have noticed a weird desc: field in the listunspent command of the previous section. Here's what's all about (and how it can be used to transfer addresses).

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.17.0 that had continued to be expanded through Bitcoin Core 0.20.0. Most of the commands in this section are from 0.17.0, but the updated importmulti that support descriptors is from 0.18.0.

## Know about Transferring Addresses

Most of this course presumes that you're working entirely from a single node where you manage your own wallet, sending and receiving payments with the addresses created by that wallet. However, that's not necessarily how the larger Bitcoin ecosystem works. There, you're more likely to be moving addresses between wallets and even setting up wallets to watch over funds controlled by different wallets.

That's where descriptors come in. They're most useful if you're interacting with software _other_ than Bitcoin Core, and really need to lean on this sort of compatibility function: see [§6.1](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/06_1_Sending_a_Transaction_to_a_Multisig.md) for a real-world example of how having the capability of descriptors is critical.

Moving addresses between wallets used to focus on xpub and xprv, and those are still supported.

> :book: _**What is xprv?**_ An extended private key. This is the combination of a private key and a chain code. It's a private key that a whole sequence of children private keys can be derived from. :book: _**What is xpub?**_ An extended public key. This is the combination of a public key and a chain code. It's a public key that a whole sequence of children public keys can be derived from.

The fact that you can have a "whole sequence of children ... keys" reveals the fact that "xpub" and "xprv" aren't standard keys like we've been talking about so far. They're instead hierarchical keys that can be used to create whole families of keys, built on the idea of HD Wallets.

> :book: _**What is an HD Wallet?**_ Most modern wallets are built on [BIP32: Hierarchical Deterministic Wallets](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki). This is a hierarchical design where a single seed can be used to generate a whole sequence of keys. The entire wallet may then be restored from that seed, rather than requiring the restoring of every single private key. :book: _**What is a Derivation Path?**_ When you have hierarchical keys, you need to be able to define individual keys as descendents of a seed. For example [0] is the 0th key, [0/1] is the first son of the 0th key, [1/0/1] is the first grandson of the zeroth son of the 1st key. Some keys also contain a ' after the number, to show they're hardened, which protects them from a specific attack that can be used to derive an xprv from an xpub. You don't need to worry about the specifics, other than the fact that those 's will cause you formatting troubles when working from the command line. :information_source: **NOTE:** a derivation path defines a key, which means that a key represents a derivation path. They're equivalent. In the case of a descriptor, the derivation path lets bitcoind know where the key that follows in the descriptor came from!

xpubs and xprvs proved insufficient when the types of public keys multiplied under the [SegWit expansion](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/04_6_Creating_a_Segwit_Transaction.md), thus the need for "output descriptors".

> :book: _**What is an output descriptor?**_ A precise description of how to derive a Bitcoin address from a combination of a function and one or more inputs to that function.

The introduction of functions into descriptors is what makes them powerful, because they can be used to transfer all sorts of addresses, from the Legacy addresses that we're working with now to the Segwit and multisig addresses that we'll meet down the road. An individual function matches a particular type of address and correlates with specific rules to generate that address.

## Capture a Descriptor

Descriptors are visible in several commands such as listunspent and getaddressinfo:

$ bitcoin-cli getaddressinfo ms7ruzvL4atCu77n47dStMb3of6iScS8kZ  
{  
"address": "ms7ruzvL4atCu77n47dStMb3of6iScS8kZ",  
"scriptPubKey": "76a9147f437379bcc66c40745edc1891ea6b3830e1975d88ac",  
"ismine": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",  
"iswatchonly": false,  
"isscript": false,  
"iswitness": false,  
"pubkey": "03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388",  
"iscompressed": true,  
"ischange": false,  
"timestamp": 1592335136,  
"hdkeypath": "m/0'/0'/18'",  
"hdseedid": "fdea8e2630f00d29a9d6ff2af7bf5b358d061078",  
"hdmasterfingerprint": "d6043800",  
"labels": [  
""  
]  
}

Here the descriptor is pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk.

## Understand a Descriptor

A descriptor is broken into several parts:

function([derivation-path]key)#checksum

Here's what that all means:

- **Function.** The function that is used to create an address from that key. In this cases it's pkh, which is the standard P2PKH legacy address that you met in [§3.3: Setting Up Your Wallet](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_3_Setting_Up_Your_Wallet.md). Similarly, a P2WSH SegWit address would use wsh and a P2WPKH address would use wpkh.
    
- **Derivation Path.** This describes what part of an HD wallet is being exported. In this case it's a seed with the fingerprint d6043800 and then the 18th child of the 0th child of the 0th child (0'/0'/18') of that seed. There may also be a further derivation after the key: function([derivation-path]key/more-derivation)#checksum
    
    - It's worth noting here that if you ever get a derivation path without a fingerprint, you can make it up. It's just that if there's an existing one, you should match it, because if you ever go back to the device that created the fingerprint, you'll need to have the same one.
        
- **Key**. The key or keys that are being transferred. This could be something traditional like an xpub or xprv, it could just be a public key for an address as in this case, it could be a set of addresses for a multi-signature, or it could be something else. This is the core data: the function explains what to do with it.
    
- **Checksum**. Descriptors are meant to be human transferrable. This checksum makes sure you got it right.
    

See [Bitcoin Core's Info on Descriptor Support](https://github.com/bitcoin/bitcoin/blob/master/doc/descriptors.md) for more information.

## Examine a Descriptor

You can look at a descriptor with the getdescriptorinfo RPC:

$ bitcoin-cli getdescriptorinfo "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk"  
{  
"descriptor": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",  
"checksum": "4ahsl9pk",  
"isrange": false,  
"issolvable": true,  
"hasprivatekeys": false  
}

Note that it returns a checksum. If you're ever given a descriptor without a checksum, you can learn it with this command:

$ bitcoin-cli getdescriptorinfo "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)"  
{  
"descriptor": "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk",  
"checksum": "4ahsl9pk",  
"isrange": false,  
"issolvable": true,  
"hasprivatekeys": false  
}

Besides giving you the checksum, this command also verifies the validity of the descriptor and provides useful information like whether a descriptor contains private keys.

One of the powers of a descriptor is being able to derive an address in a regular way. This is done with the deriveaddresses RPC.

$ bitcoin-cli deriveaddresses "pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk"  
[  
"ms7ruzvL4atCu77n47dStMb3of6iScS8kZ"  
]

You'll note it loops back to the address we started with (as it should).

## Import a Descriptor

But, the really important thing about a descriptor is that you can take it to another (remote) machine and import it. This is done with the importmulti RPC using the desc option:

remote$ bitcoin-cli importmulti '[{"desc": "pkh([d6043800/0'"'"'/0'"'"'/18'"'"']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk", "timestamp": "now", "watchonly": true}]'  
[  
{  
"success": true  
}  
]

First, you'll note our first really ugly use of quotes. Every ' in the derivation path had to be replaced with '"'"'. Just expect to have to do that if you're manipulating a descriptor that contains a derivation path. (The other option is to exchange the ' with a h for hardened, but that will change you checksum, so if you prefer that for its ease of use, you'll need to get a new checksum with getdescriptorinfo.)

Second, you'll note that we flagged this as watchonly. That's because we know that it's a public key, so we can't spend with it. If we'd failed to enter this flag, importmulti would helpfully have told us something like: Some private keys are missing, outputs will be considered watchonly. If this is intentional, specify the watchonly flag..

> :book: _**What is a watch-only address?**_ A watch-only address allows you to watch for transactions related to an address (or to a whole family of addresses if you used an xpub), but not to spend funds on those addresses.

Using getaddressesbylabel, we can now see that our address has correctly been imported into our remote machine!

remote$ bitcoin-cli getaddressesbylabel ""  
{  
"ms7ruzvL4atCu77n47dStMb3of6iScS8kZ": {  
"purpose": "receive"  
}  
}

## Summary: Understanding the Descriptor

Descriptors let you pass public keys and private keys among wallets, but more than that, they allow you to precisely and correctly to define addresses and to derive addresses of a lot of different sorts from a standardized description format.

> :fire: _**What is the power of descriptors?**_ Descriptors allow you to import and export seeds and keys. That's great if you want to move between different wallets. As a developer, they also allow you to build up the precise sort of addresses that you're interested in creating. For example, we use it in [FullyNoded 2](https://github.com/BlockchainCommons/FullyNoded-2/blob/master/Docs/How-it-works.md) to generate a multi-sig from three seeds.

We'll make real use of descriptors in [§7.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_3_Integrating_with_Hardware_Wallets.md), when we're importing addresses from a hardware wallet.

## What's Next?

Advance through "bitcoin-cli" with [Chapter Four: Sending Bitcoin Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_0_Sending_Bitcoin_Transactions.md).

# Chapter Four: Sending Bitcoin Transactions

This chapter describes three different methods for sending bitcoins to normal P2PKH addresses from the command line, using only the bitcoin-cli interface.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Decide How to Send Money Through Bitcoin
    
- Create a Raw Transaction
    
- Use Arithmetic to Calculate Fees
    

Supporting objectives include the ability to:

- Understand Transactions & Transaction Fees
    
- Understand Legacy & SegWit Transactions
    
- Use Basic Methods to Send Money
    
- Use Auto Fee Calculation Methods to Send Money
    
- Understand the Dangers of Raw Transactions
    

## Table of Contents

- [Section One: Sending Coins the Easy Way](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_1_Sending_Coins_The_Easy_Way.md)
    
- [Section Two: Creating a Raw Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2_Creating_a_Raw_Transaction.md)
    
    - [Interlude: Using JQ](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2__Interlude_Using_JQ.md)
        
- [Section Three: Creating a Raw Transaction with Named Arguments](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_3_Creating_a_Raw_Transaction_with_Named_Arguments.md)
    
- [Section Four: Sending Coins with Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4_Sending_Coins_with_a_Raw_Transaction.md)
    
    - [Interlude: Using Curl](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md)
        
- [Section Five: Sending Coins with Automated Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_5_Sending_Coins_with_Automated_Raw_Transactions.md)
    
- [Section Six: Creating a SegWit Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md)
    

# 4.1: Sending Coins the Easy Way

The bitcoin-cli offers three major ways to send coins: as a simple command; as a raw transaction; and as a raw transaction with calculation. Each has their own advantages and disadvantages. This first method for sending coins is also the simplest.

## Set Your Transaction Fee

Before you send any money on the Bitcoin network, you should think about what transaction fees you're going to pay.

> :book: _**What is a transaction fee?**_ There's no such thing as a free lunch. Miners incorporate transactions into blocks because they're paid to do so. Not only do they get paid by the network for making the block, but they also get paid by transactors for including their transactions. If you don't pay a fee, your transaction might get stuck ... forever (or, until saved by some of the tricks in [Chapter Five](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_0_Controlling_Bitcoin_Transactions.md)).

When you're using the simple and automated methods for creating transactions, as outlined here and in [§4.5: Sending Coins with Automated Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_5_Sending_Coins_with_Automated_Raw_Transactions.md), Bitcoin will calculate transaction fees for you. This is done using Floating Fees, where the bitcoind watches how long transactions are taking to confirm and automatically calculates for you what to spend.

You can help control this by putting rational values into your ~/.bitcoin/bitcoin.conf. The following low-cost values would ensure that there was a minimum transaction fee of 10,000 satoshis per kByte of data in your transaction and request that the floating fees figure out a good amount to get your transaction somewhere into the next six blocks.

mintxfee=0.0001  
txconfirmtarget=6

However, under the theory that you don't want to wait around while working on a tutorial, we've adopted the following higher values:

mintxfee=0.001  
txconfirmtarget=1

You should enter these into ~/.bitcoin/bitcoin.conf, in the main section, toward the top of the file or if you want to be sure you never use it elsewhere, under the [test] section.

In order to get through this tutorial, we're willing to spend 100,000 satoshis per kB on every transaction (about $10!), and we want to get each transaction into the next block! (To put that in perspective, a typical transaction runs between .25 kB and 1 kB, so you'll actually be paying more like $2.50 than $10 ... if this were real money.)

After you've edited your bitcoin.conf file, you'll want to kill and restart bitcoind.

$ bitcoin-cli stop  
$ bitcoind -daemon

## Get an Address

You need somewhere to send your coins to. Usually, someone would send you an address, and perhaps give you a signature to prove they own that address. Alternatively, they might give you a QR code to scan, so that you can't make mistakes when typing in the address. In our case, we're going to send coins to n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi, which is a return address for an old Tesetnet faucet.

> :book: _**What is a QR code?**_ A QR code is just an encoding of a Bitcoin address. Many wallets will generate QR codes for you, while some sites will convert from an address to a QR code. Obviously, you should only accept a QR code from a site that you absolutely trust. A payer can use a bar-code scanner to read in the QR code, then pay to it.

## Send the Coins

You're now ready to send some coins. This is actually quite simple via the command line. You just use bitcoin-cli sendtoaddress [address] [amount]. So, to send a little coinage to the address n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi just requires:

$ txid=$(bitcoin-cli sendtoaddress n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi 0.001)  
$ echo $txid  
93250d0cacb0361b8e21030ac65bc4c2159a53de1075425d800b2d7a8ab13ba8

> 🙏 To help keep testnet faucets alive, try to use the return address of the same faucet you used in the previous chapter on receiving transactions.

Make sure the address you write in is where you want the money to go. Make _double_ sure. If you make mistakes in Bitcoin, there's no going back.

You'll receive a txid back when you issue this command.

> ❕ You may end up with an error code if you don't have enough funds in your wallet to send the transaction. Depending on your current balance bitcoin-cli getbalance you may need to adjust the amount to be sent to account for the amount being sent along with the transaction fee. If your current balance is 0.001, then you could try sending 0.0001. Alternatively, it would be better to instead subtract the expected fee given in the error message from your current balance. This is good practice as many wallets expect you to calculate your own amount + fees when withdrawing, even among popular exchanges. :warning: **WARNING:** The bitcoin-cli command actually generates JSON-RPC commands when it's talking to the bitcoind. They can be really picky. This is an example: if you list the bitcoin amount without the leading zero (i.e. ".1" instead of "0.1"), then bitcoin-cli will fail with a mysterious message. :warning: **WARNING:** Even if you're careful with your inputs, you could see "Fee estimation failed. Fallbackfee is disabled." Fundamentally, this means that your local bitcoind doesn't have enough information to estimate fees. You should really never see it if you've waited for your blockchain to sync and set up your system with Bitcoin Standup. But if you're not entirely synced, you may see this. It also could be that you're not using a standard bitcoin.conf: the entry blocksonly=1 will cause your bitcoind to be unable to estimate fees.

## Examine Your Transaction

You can look at your transaction using your transaction id:

{  
"amount": -0.00100000,  
"fee": -0.00022200,  
"confirmations": 0,  
"trusted": true,  
"txid": "93250d0cacb0361b8e21030ac65bc4c2159a53de1075425d800b2d7a8ab13ba8",  
"walletconflicts": [  
],  
"time": 1592604194,  
"timereceived": 1592604194,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi",  
"category": "send",  
"amount": -0.00100000,  
"vout": 1,  
"fee": -0.00022200,  
"abandoned": false  
}  
],  
"hex": "0200000001e982921bb0189afc486e20bb05cc5825c71a0ba8868043ed04ece9ab0cb12a8e010000006a47304402200fc493a01c5c9d9574f7c321cee6880f7f1df847be71039e2d996f7f75c17b3d02203057f5baa48745ba7ab5f1d4eed11585bd8beab838b1ca03a4138516fe52b3b8012102fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9bafeffffff02e8640d0000000000160014d37b6ae4a917bcc873f6395741155f565e2dc7c4a0860100000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac780b1b00"  
}

You can see not only the amount transferred (.001 BTC) but also a transaction fee (.000222 BTC), which is about a quarter of the .001 BTC/kB minimum fee that was set, which suggests that the transaction was about a quarter of a kB in size.

While you are waiting for this transaction to clear, you'll note that bitcoin-cli getbalance shows that all of your money is gone (or, at least, all of your money from a single incoming transaction). Similarly, bitcoin-cli listunspent will show that an entire transaction is gone, even if it was more than what you wanted to send. There's a reason for this: whenever you get money in, you have to send it _all_ out together, and you have to perform some gymnastics if you actually want to keep some of it! Once again, sendtoaddress takes care of this all for you, which means you don't have to worry about making change until you send a raw transaction. In this case, a new transaction will appear with your change when your spend is incorporated into a block.

## Summary: Sending Coins the Easy Way

To send coins the easy way, make sure your transaction defaults are rationale, get an address, and send coins there. That's why they call it easy!

> :fire: _**What is the power of sending coins the easy way?**_ _The advantages._ It's easy. You don't have to worry about arcane things like UTXOs. You don't have to calculate transaction fees by hand, so you're not likely to make mistakes that cost you large amounts of money. If your sole goal is to sit down at your computer and send some money, this is the way to go. _The disadvantages._ It's high level. You have very little control over what's happening, and you can't do anything fancy. If you're planning to write more complex Bitcoin software or want a deeper understanding of how Bitcoin works, then the easy way is just a dull diversion before you get to the real stuff.

## What's Next?

Continue "Sending Bitcoin Transactions" with [§4.2 Creating a Raw Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2_Creating_a_Raw_Transaction.md).

# Interlude: Using JQ

Creating a raw transaction revealed how more complex bitcoin-cli results can't easily be saved into command-line variables. The answer is JQ, which allows you to filter out individual elements from more complex JSON data.

## Install JQ

For modern versions of Debian, you should be able to install JQ using apt-get:

# apt-get install jq

> :book: _**What is JQ?**_ The repository explains it best, saying "jq is like sed for JSON data - you can use it to slice and filter and map and transform structured data with the same ease that sed, awk, grep and friends let you play with text."

If that works, you're done!

Otherwise, you can download JQ from a [Github repository](https://stedolan.github.io/jq/). Just download a binary for Linux, OS X, or Windows, as appropriate.

Once you've downloaded the binary, you can install it on your system. If you're working on a Debian VPS as we suggest, your installation will look like this:

$ mv jq-linux64 jq  
$ sudo /usr/bin/install -m 0755 -o root -g root -t /usr/local/bin jq

## Use JQ to Access a JSON Object Value by Key

**Usage Example:** _Capture the hex from a signed raw transaction._

In the previous section, the use of signrawtransaction offered an example of not being able to easily capture data into variables due to the use of JSON output:

$ bitcoin-cli signrawtransactionwithwallet $rawtxhex  
{  
"hex": "02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f361010000006a4730440220335d15a2a2ca3ce6a302ce041686739d4a38eb0599a5ea08305de71965268d05022015f77a33cf7d613015b2aba5beb03088033625505ad5d4d0624defdbea22262b01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000",  
"complete": true  
}

Fortunately, JQ can easily capture data of that sort!

To use JQ, run jq at the backend of a pipe, and always use the standard invocation of jq -r '.'. The -r tells JQ to produce raw output, which will work for command-line variables, while the . tells jq to output. We protect that argument in ' ' because we'll need that protection later as our jq invocations get more complex.

To capture a specific value from a JSON object, you just list the key after the .:

$ bitcoin-cli signrawtransactionwithwallet $rawtxhex | jq -r '.hex'  
02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f361010000006a4730440220335d15a2a2ca3ce6a302ce041686739d4a38eb0599a5ea08305de71965268d05022015f77a33cf7d613015b2aba5beb03088033625505ad5d4d0624defdbea22262b01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000

With that tool in hand, you can capture information from JSON objects to command-line variables:

$ signedtx=$(bitcoin-cli signrawtransactionwithwallet $rawtxhex | jq -r '.hex')  
$ echo $signedtx  
02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f361010000006a4730440220335d15a2a2ca3ce6a302ce041686739d4a38eb0599a5ea08305de71965268d05022015f77a33cf7d613015b2aba5beb03088033625505ad5d4d0624defdbea22262b01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000

You can then use those variables easily and without error:

$ bitcoin-cli sendrawtransaction $signedtx  
3f9ccb6e16663e66dc119de1866610cc4f7a83079bfec2abf0598ed3adf10a78

## Use JQ to Access Single JSON Object Values in an Array by Key

**Usage Example:** _Capture the txid and vout for a selected UTXO._

Grabbing data out of a JSON object is easy, but what if that JSON object is in a JSON array? The listunspent command offers a great example, because it'll usually contain a number of different transactions. What if you want to capture specific information from _one_ of them?

When working with a JSON array, the first thing you need to do is tell JQ which index to access. For example, you might have looked through your transactions in listunspent and decided that you wanted to work with the second of them. You use '.[1]' to access that second element. The [] says that we're referencing a JSON array and the 1 says we want the 1st index.

$ bitcoin-cli listunspent | jq -r '.[1]'  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022,  
"confirmations": 9,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}

You can then capture an individual value from that selected array by (1) using a pipe _within_ the JQ arguments; and then (2) requesting the specific value afterward, as in the previous example. The following would capture the txid from the 1st JSON object in the JSON array produced by listunspent:

$ bitcoin-cli listunspent | jq -r '.[1] | .txid'  
91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c

Carefully note how the ' 's go around the whole JQ expression _including_ the pipe.

This method can be used to fill in variables for a UTXO that you want to use:

$ newtxid=$(bitcoin-cli listunspent | jq -r '.[1] | .txid')  
$ newvout=$(bitcoin-cli listunspent | jq -r '.[1] | .vout')  
$ echo $newtxid  
91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c  
$ echo $newvout  
0

Voila! We could now create a new raw transaction using our 1st UTXO as an input, without having to type in any of the UTXO info by hand!

## Use JQ to Access Matching JSON Object Values in an Array by Key

**Usage Example:** _List the value of all unspent UTXOs._

Instead of accessing a single, specific value in a specific JSON object, you could instead access all of a specific value across all the JSON objects. This is done with .[], where no index is specified. For example, this would list all unspent funds:

$ bitcoin-cli listunspent | jq -r '.[] | .amount'  
0.0001  
0.00022

## Use JQ for Simple Calculations by Key

**Usage Example:** _Sum the value of all unspent UTXOs._

At this point, you can start using JQ output for simple math. For example, adding up the values of those unspent transactions with a simple awk script would give you the equivalent of getbalance:

$ bitcoin-cli listunspent | jq -r '.[] | .amount' | awk '{s+=$1} END {print s}'  
0.00032  
$ bitcoin-cli getbalance  
0.00032000

## Use JQ to Display Multiple JSON Object Values in an Array by Multiple Keys

**Usage Example:** _List usage information for all UTXOs._

JQ can easily capture individual elements from JSON objects and arrays and place those elements into variables. That will be its prime use in future sections. However, it can also be used to cut down huge amounts of information output by bitcoin-cli into reasonable amounts of information.

For example, you might want to see a listing of all your UTXOs (.[]) and get a listing of all of their most important information (.txid, .vout, .amount):

$ bitcoin-cli listunspent | jq -r '.[] | .txid, .vout, .amount'  
ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36  
0  
0.0001  
91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c  
0  
0.00022

This makes it easy to decide which UTXOs to spend in a raw transaction, but it's not very pretty.

Fortunately, JQ also lets you be fancy. You can use {}s to create new JSON objects (either for additional parsing or for pretty output). You also get to define the name of the new key for each of your values. The resulting output should be much more intuitive and less prone to error (though obviously, less useful for dumping info straight into variables).

The following example shows the exact same parsing of listunspent, but with the each old JSON object rebuilt as a new, abridged JSON object, with all of the new values named with their old keys:

$ bitcoin-cli listunspent | jq -r '.[] | { txid: .txid, vout: .vout, amount: .amount }'  
{  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"vout": 0,  
"amount": 0.0001  
}  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"amount": 0.00022  
}

You could of course rename your new keys as you see fit. There's nothing magic in the original names:

$ bitcoin-cli listunspent | jq -r '.[] | { tx: .txid, output: .vout, bitcoins: .amount }'  
{  
"tx": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"output": 0,  
"bitcoins": 0.0001  
}  
{  
"tx": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"output": 0,  
"bitcoins": 0.00022  
}

## Use JQ to Access JSON Objects by Looked-Up Value

**Usage Example:** _Automatically look up UTXOs being used in a transaction._

The JQ lookups so far have been fairly simple: you use a key to look up one or more values in a JSON object or array. But what if you instead want to look up a value in a JSON object ... by another value? This sort of indirect lookup has real applicability when you're working with transactions built on existing UTXOs. For example, it can allow you to calculate the sum value of the UTXOs being used in a transaction, something that is vitally important.

This example uses the following raw transaction. Note that this is a more complex raw transaction with two inputs and two outputs. We'll learn about making those in a few sections; for now, it's necessary to be able to offer robust examples. Note that unlike our previous examples, this one has two objects in its vin array and two in its vout array.

$ bitcoin-cli decoderawtransaction $rawtxhex  
{  
"txid": "6f83a0b78c598de01915554688592da1d7a3047eacacc8a9be39f5396bf0a07e",  
"hash": "6f83a0b78c598de01915554688592da1d7a3047eacacc8a9be39f5396bf0a07e",  
"size": 160,  
"vsize": 160,  
"version": 2,  
"locktime": 0,  
"vin": [  
{  
"txid": "d261b9494eb29084f668e1abd75d331fc2d6525dd206b2f5236753b5448ca12c",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
},  
{  
"txid": "c7c7f6371ec19330527325908a544bbf8401191645598301d24b54d37e209e7b",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 1.00000000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 cfc39be7ea3337c450a0c77a839ad0e160739058 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a914cfc39be7ea3337c450a0c77a839ad0e16073905888ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mzTWVv2QSgBNqXx7RC56zEhaQPve8C8VS9"  
]  
}  
},  
{  
"value": 0.04500000,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 166692bda9f25ced145267bb44286e8ee3963d26 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a914166692bda9f25ced145267bb44286e8ee3963d2688ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mhZQ3Bih6wi7jP1tpFZrCcyr4NsfCapiZP"  
]  
}  
}  
]  
}

### Retrieve the Value(s)

Assume that we know exactly how this transaction is constructed: we know that it uses two UTXOs as input. To retrieve the txid for the two UTXOs, we could use jq to look up the transaction's .vin value, then reference the .vin's 0th array, then that array's .txid value. Afterward, we could do the same with the 1st array, then the same with the .vin's two .vout values. Easy:

$ usedtxid1=$(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[0] | .txid')  
$ echo $usedtxid1  
d261b9494eb29084f668e1abd75d331fc2d6525dd206b2f5236753b5448ca12c  
$ usedtxid2=$(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[1] | .txid')  
$ echo $usedtxid2  
c7c7f6371ec19330527325908a544bbf8401191645598301d24b54d37e209e7b

$ usedvout1=$(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[0] | .vout')  
$ echo $usedvout1  
1  
$ usedvout2=$(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[1] | .vout')  
$ echo $usedvout2  
1

However, it would be better to have a general case that _automatically_ saved all the txids of our UTXOs.

We already know that we can access all of the .txids by using an .[] array value. We can use that to build a general .txid lookup:

$ usedtxid=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .txid'))  
$ echo ${usedtxid[0]}  
d261b9494eb29084f668e1abd75d331fc2d6525dd206b2f5236753b5448ca12c  
$ echo ${usedtxid[1]}  
c7c7f6371ec19330527325908a544bbf8401191645598301d24b54d37e209e7b

$ usedvout=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .vout'))  
$ echo ${usedvout[0]}  
1  
$ echo ${usedvout[1]}  
1

The only real trick here is how we saved the information using the bash shell. Rather than saving to a variable with $(command), we instead saved to an array with ($(command)). We were then able to access the individual bash array elements with a ${variable[n]} construction. We could instead access the whole array with ${variable[@]}. (Yeah, no one ever said bash was pretty.)

> :warning: **WARNING:** Always remember that a UTXO is a transaction _plus_ a vout. We missed the vout the first time we wrote this JQ example, and it stopped working when we ended up with a situation where we'd been sent two vouts from the same transaction.

### Retrieve the Related Object(s)

You can now use your saved txid and vout information to reference UTXOs in listunspent. To find the information on the UTXOs being used by the raw transaction, you need to look through the entire JSON array ([]) of unspent transactions. You can then choose (select) individual JSON objects that include (contains) the txids. You _then_ select (select) the transactions among those that _also_ contains (contain) the correct vout.

The use of another level of pipe is the standard methodology of JQ: you grab a set of data, then you whittle it down to all the relevant transactions, then you whittle it down to the vouts that were actually used from those transactions. However, the select and contains arguments are something new. They show off some of the complexity of JSON that goes beyond the scope of this tutorial; for now just know that this particular invocation will work to grab matching objects.

To start simply, this picks out the two UTXOs one at a time:

$ bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${usedtxid[0]}'")) | select(.vout | contains('${usedvout[0]}'))'  
{  
"txid": "d261b9494eb29084f668e1abd75d331fc2d6525dd206b2f5236753b5448ca12c",  
"vout": 1,  
"address": "miSrC3FvkPPZgqqvCiQycq7io7wTSVsAFH",  
"scriptPubKey": "76a91420219e4f3c6bc0f6524d538009e980091b3613e888ac",  
"amount": 0.9,  
"confirmations": 6,  
"spendable": true,  
"solvable": true  
}  
$ bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${usedtxid[1]}'")) | select(.vout | contains('${usedvout[1]}'))'  
{  
"txid": "c7c7f6371ec19330527325908a544bbf8401191645598301d24b54d37e209e7b",  
"vout": 1,  
"address": "mzizSuAy8aL1ytFijds7pm4MuDPx5aYH5Q",  
"scriptPubKey": "76a914d2b12da30320e81f2dfa416c5d9499d08f778f9888ac",  
"amount": 0.4,  
"confirmations": 5,  
"spendable": true,  
"solvable": true  
}

A simple bash for-loop could instead give you _all_ of your UTXOs:

$ for ((i=0; i<${#usedtxid[*]}; i++)); do txid=${usedtxid[i]}; vout=${usedvout[i]}; bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${txid}'")) | select(.vout | contains('$vout'))'; done;  
{  
"txid": "d261b9494eb29084f668e1abd75d331fc2d6525dd206b2f5236753b5448ca12c",  
"vout": 1,  
"address": "miSrC3FvkPPZgqqvCiQycq7io7wTSVsAFH",  
"scriptPubKey": "76a91420219e4f3c6bc0f6524d538009e980091b3613e888ac",  
"amount": 0.9,  
"confirmations": 7,  
"spendable": true,  
"solvable": true  
}  
{  
"txid": "c7c7f6371ec19330527325908a544bbf8401191645598301d24b54d37e209e7b",  
"vout": 1,  
"address": "mzizSuAy8aL1ytFijds7pm4MuDPx5aYH5Q",  
"scriptPubKey": "76a914d2b12da30320e81f2dfa416c5d9499d08f778f9888ac",  
"amount": 0.4,  
"confirmations": 6,  
"spendable": true,  
"solvable": true  
}

Note that we used yet another bit of array ugliness ${#usedtxid[*]} to determine the size of the array, then accessed each value in the usedtxid array and each value in the parallel usedvout array, putting them into simpler variables for less-ugly access.

## Use JSON for Simple Calculation by Value

**Usage Example:** _Automatically calculate the value of the UTXOs used in a transaction._

You can now go one step further, and request the .amount (or any other JSON key-value) from the UTXOs you're retrieving.

This example repeats the usage the $usedtxid and $usedvout arrays that were set as follows:

$ usedtxid=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .txid'))  
$ usedvout=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .vout'))

The same for script can be used to step through those arrays, but with an added pipe in the JQ that outputs the amount value for each of the UTXOs selected.

$ for ((i=0; i<${#usedtxid[*]}; i++)); do txid=${usedtxid[i]}; vout=${usedvout[i]}; bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${txid}'")) | select(.vout | contains('$vout')) | .amount'; done;  
0.9  
0.4

At this point, you can also sum up the .amounts with an awk script, to really see how much money is in the UTXOs that the transaction is spending:

$ for ((i=0; i<${#usedtxid[*]}; i++)); do txid=${usedtxid[i]}; vout=${usedvout[i]}; bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${txid}'")) | select(.vout | contains('$vout')) | .amount'; done | awk '{s+=$1} END {print s}'  
1.3

Whew!

## Use JQ for Complex Calculations

**Usage Example:** _Calculate the fee for a transaction._

Figuring out the complete transaction fee at this point just requires one more bit of math: determining how much money is going through the .vout. That's a simple use of JQ where you just use awk to sum up the value of all the vout information:

$ bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vout [] | .value' | awk '{s+=$1} END {print s}'  
1.045

To complete the transaction fee calculation, you subtract the .vout .amount (1.045) from the .vin .amount (1.3).

To do this, you'll need to install bc:

$ sudo apt-get install bc

Putting it all together creates a complete calculator in just five lines of script:

$ usedtxid=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .txid'))  
$ usedvout=($(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vin | .[] | .vout'))  
$ btcin=$(for ((i=0; i<${#usedtxid[*]}; i++)); do txid=${usedtxid[i]}; vout=${usedvout[i]}; bitcoin-cli listunspent | jq -r '.[] | select (.txid | contains("'${txid}'")) | select(.vout | contains('$vout')) | .amount'; done | awk '{s+=$1} END {print s}')  
$ btcout=$(bitcoin-cli decoderawtransaction $rawtxhex | jq -r '.vout [] | .value' | awk '{s+=$1} END {print s}')  
$ echo $(printf '%.8f-%.8f' $btcin $btcout_f) | /usr/bin/bc  
.255

And that's also a good example of why you double-check your fees: we'd intended to send a transaction fee of 5,000 satoshis, but sent 255,000 satoshis instead. Whoops!

> :warning: **WARNING:** The first time we wrote up this lesson, we genuinely miscalculated our fee and didn't see it until we ran our fee calculator. It's _that_ easy, then your money is gone. (The example above is actually from our second iteration of the calculator, and that time we made the mistake on purpose.)

For more JSON magic (and if any of this isn't clear), please read the [JSON Manual](https://stedolan.github.io/jq/manual/) and the [JSON Cookbook](https://github.com/stedolan/jq/wiki/Cookbook). We'll be regularly using JQ in future examples.

## Make Some New Aliases

JQ code can be a little unwieldy, so you should consider adding some longer and more interesting invocations to your ~/.bash_profile.

Any time you're looking through a large mass of information in a JSON object output by a bitcoin-cli command, consider writing an alias to strip it down to just what you want to see.

alias btcunspent="bitcoin-cli listunspent | jq -r '.[] | { txid: .txid, vout: .vout, amount: .amount }'"

## Run The Transaction Fee Script

The [Fee Calculation Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/04_2_i_txfee-calc.sh) is available in src-code directory. You can download it and save it as txfee-calc.sh.

> :warning: **WARNING:** This script has not been robustly checked. If you are going to use it to verify real transaction fees you should only do it as a triple-check after you've already done all the math yourself.

Be sure the permissions on the script are right:

$ chmod 755 txfee-calc.sh

You can then run the script as follows:

$ ./txfee-calc.sh $rawtxhex  
.255

You may also want to create an alias:

alias btctxfee="~/txfee-calc.sh"

## Summary: Using JQ

JQ makes it easy to extract information from JSON arrays and objects. It can also be used in shell scripts for fairly complex calculations that will make your life easier.

## What's Next?

Continue "Sending Bitcoin Transactions" with [§4.3 Creating a Raw Transaction with Named Arguments](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_3_Creating_a_Raw_Transaction_with_Named_Arguments.md).

# 4.2 Creating a Raw Transaction

You're now ready to create Bitcoin raw transactions. This allows you to send money but to craft the transactions as precisely as you want. This first section focuses on a simple one-input, one-output transaction. This sort of transaction _isn't_ actually that useful, because you're rarely going to want to send all of your money to one person (unless you're actually just forwarding it on, such as if you're moving things from one wallet to another). Thus, we don't label this section as a way to send money. It's just a foundational stepping stone to _actually_ sending money with a raw transaction.

## Understand the Bitcoin Transaction

Before you dive into actually creating raw transactions, you should make sure you understand how a Bitcoin transaction works. It's all about the UTXOs.

> :book: _**What is a UTXO?**_ When you receive cash in your Bitcoin wallet, it appears as an individual transaction. Each of these transactions is called a Unspent Transaction Output (UTXO). It doesn't matter if various payments were made to the same address or to multiple addresses: each incoming transaction remains distinct in your wallet as a UTXO.

When you create a new outgoing transaction, you gather together one or more UTXOs, each of which represents a blob of money that you received. You use these as inputs for a new transaction. Together their amount must equal what you want to spend _or more_. Then, you generate one or more outputs, which give the money represented by the inputs to one or more people. This creates new UTXOs for the recipients, which may then use _those_ to fund future transactions.

Here's the trick: _all of the UTXOs that you gather are spent in full!_ That means that if you want to send just part of the money in a UTXO to someone else, then you also have to generate an additional output that sends the rest back to you! For now, we won't worry about that, but the use of a change address will be vital when moving on from the theory of this chapter to more practical transactions.

## List Your Unspent Transactions

In order to create a new raw transaction, you must know what UTXOs you have on-hand to spend. You can determine this information with the bitcoin-cli listunspent command:

$ bitcoin-cli listunspent  
[  
{  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"vout": 0,  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"label": "",  
"scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",  
"amount": 0.00010000,  
"confirmations": 20,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",  
"safe": true  
},  
{  
"txid": "61f3b7016bf1ecc3987b8805207e79362e4de8026682e149107999b779426e3a",  
"vout": 1,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00050000,  
"confirmations": 3,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
},  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022000,  
"confirmations": 3,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}  
]

This listing shows three different UTXOs, worth .0001, .0005 and .00022 BTC. Note that each has its own distinct txid and remains distinct in the wallet, even the last two, which were sent to the same address.

When you want to spend a UTXO, it's not sufficient to just know the transaction id. That's because each transaction can have multiple outputs! Remember that first chunk of money that the faucet sent us? In the transaction, some money went to us and some went to someone else. The txid refers to the overall transaction, while a vout says which of multiple outputs you've received. In this list, each of these transactions is the 0th vout of a previous transaction, but _that doesn't have to be the case_.

So, txid+vout=UTXO. This will be the foundation of any raw transaction.

## Write a Raw Transaction with One Output

You're now ready to write a simple, example raw transaction that shows how to send the entirety of a UTXO to another party. As noted, this is not necessarily a very realistic real-world case.

> :warning: **WARNING:** It is very easy to lose money with a raw transaction. Consider all instructions on sending bitcoins via raw transactions to be _very_, _very_ dangerous. Whenever you're actually sending real money to other people, you should instead use one of the other methods explained in this chapter. Creating raw transactions is extremely useful if you're writing bitcoin programs, but _only_ when you're writing bitcoin programs. (For example: in writing this example for one version of this tutorial, we accidentally spent the wrong transaction, even though it had about 10x as much value. Almost all of that was lost to the miners.)

### Prepare the Raw Transaction

For best practices, we'll start out each transaction by carefully recording the txids and vouts that we'll be spending.

In this case, we're going to spend the one worth .00050000 BTC because it's the only one with a decent value.

$ utxo_txid="61f3b7016bf1ecc3987b8805207e79362e4de8026682e149107999b779426e3a"  
$ utxo_vout="1"

You should similarly record your recipient address, to make sure you have it right. We're again sending some money back to the TP faucet:

$ recipient="n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi"

As always, check your variables carefully, to make sure they're what you expect!

$ echo $utxo_txid  
61f3b7016bf1ecc3987b8805207e79362e4de8026682e149107999b779426e3a  
$ echo $utxo_vout  
1  
$ echo $recipient  
n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi

That recipient is particularly important, because if you mess it up, your money is _gone_! (And as we already saw, choosing the wrong transaction can result in lost money!) So triple check it all.

### Understand the Transaction Fee

Each transaction has a fee associated with. It's _implicit_ when you send a raw transaction: the amount that you will pay as a fee is always equal to the amount of your input minus the amount of your output. So, you have to decrease your output a little bit from your input to make sure that your transaction goes out.

> :warning: **WARNING:** This is the very dangerous part of raw transactions!! Because you automatically expend all of the amount in the UTXOs that you use, it's critically important to make sure that you know: (1) precisely what UTXOs you're using; (2) exactly how much money they contain; (3) exactly how much money you're sending out; and (4) what the difference is. If you mess up and you use the wrong UTXO (with more money than you thought) or if you send out too little money, the excess is lost. Forever. Don't make that mistake! Know your inputs and outputs _precisely_. Or better, don't use raw transactions except as part of a carefully considered and triple-checked program. :book: _**How much should you spend on transaction fees?**_ [Bitcoin Fees](https://bitcoinfees.21.co/) has a nice live assessment. It says that the "fastest and cheapest transaction fee is currently 42 satoshis/byte" and that "For the median transaction size of 224 bytes, this results in a fee of 9,408 satoshis".

Currently Bitcoin Fees suggests a transaction fee of about 10,000 satoshis, which is the same as .0001 BTC. Yes, that's for the mainnet, not the testnet, but we want to test out things realistically, so that's what we're going to use.

In this case, that means taking the .0005 BTC in the UTXO we're selected, reducing it by .0001 BTC for the transaction fee, and sending the remaining .0004 BTC. (And this is an example of why micropayments don't work on the Bitcoin network, because a $1 or so transaction fee is pretty expensive when you're sending $4, let alone if you were trying to make a micropayment of $0.50. But that's always why we have Lightning.)

> :warning: **WARNING:** The lower that you set your transaction fee, the longer before your transaction is built into a block. The Bitcoin Fees site lists expected times, from an expected 0 blocks, to 22. Since blocks are built on average every 10 minutes, that's the difference between a few minutes and a few hours! So, choose a transaction fee that's appropriate for what you're sending. Note that you should never drop below the minimum relay fee, which is .0001 BTC.

### Write the Raw Transaction

You're now ready to create the raw transaction. This uses the createrawtransaction command, which might look a little intimidating. That's because the createrawtransaction command doesn't entirely shield you from the JSON RPC that the bitcoin-cli uses. Instead, you are going to input a JSON array to list the UTXOs that you're spending and a JSON object to list the outputs.

Here's the standard format:

$ bitcoin-cli createrawtransaction  
'''[  
{  
"txid": "'$your_txid'",  
"vout": '$your_vout'  
}  
]'''  
'''{  
"'$your_recipient'": bitcoin_amount  
}'''

Yeah, there are all kinds of crazy quotes there, but trust that they'll do the right thing. Use ''' to mark the start and end of the JSON array and the JSON object. Protect normal words like "this", but you don't need to protect normal numbers: 0. If they're variables, insert single quotes, like "'$this_word'" and '$this_num'. (Whew. You'll get used to it.)

Here's a command that creates a raw transaction to send your $utxo to your $recipient

$ rawtxhex=$(bitcoin-cli createrawtransaction '''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' '''{ "'$recipient'": 0.0004 }''')  
$ echo $rawtxhex  
02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f3610100000000ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000

### Verify Your Raw Transaction

You should next verify your rawtransaction with decoderawtransaction to make sure that it will do the right thing.

$ bitcoin-cli decoderawtransaction $rawtxhex  
{  
"txid": "dcd2d8f0ec5581b806a1fbe00325e1680c4da67033761b478a26895380cc1298",  
"hash": "dcd2d8f0ec5581b806a1fbe00325e1680c4da67033761b478a26895380cc1298",  
"version": 2,  
"size": 85,  
"vsize": 85,  
"weight": 340,  
"locktime": 0,  
"vin": [  
{  
"txid": "61f3b7016bf1ecc3987b8805207e79362e4de8026682e149107999b779426e3a",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00040000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 e7c1345fc8f87c68170b3aa798a956c2fe6a9eff OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi"  
]  
}  
}  
]  
}

Check the vin. Are you spending the right transaction? Does it contain the expected amount of money? (Check with bitcoin-cli gettransaction and be sure to look at the right vout.) Check your vout. Are you sending the right amount? Is it going to the right address? Finally, do the math to make sure the money balances. Does the value of the UTXO minus the amount being spent equal the expected transaction fee?

> :information_source: **NOTE - SEQUENCE:** You may note that each input has a sequence number, set here to 4294967295, which is 0xFFFFFFFF. This is the last frontier of Bitcoin transactions, because it's a standard field in transactions that was originally intended for a specific purpose, but was never fully implemented. So now there's this integer sitting around in transactions that could be repurposed for other uses. And, in fact, it has been. As of this writing there are three different uses for the variable that's called nSequence in the Bitcoin Core code: it enables RBF, nLockTime, and relative timelocks. If there's nothing weird going on, nSequence will be set to 4294967295. Setting it to a lower value signals that special stuff is going on.

### Sign the Raw Transaction

To date, your raw transaction is just something theoretical: you _could_ send it, but nothing has been promised. You have to do a few things to get it out onto the network.

First, you need to sign your raw transaction:

$ bitcoin-cli signrawtransactionwithwallet $rawtxhex  
{  
"hex": "02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f361010000006a4730440220335d15a2a2ca3ce6a302ce041686739d4a38eb0599a5ea08305de71965268d05022015f77a33cf7d613015b2aba5beb03088033625505ad5d4d0624defdbea22262b01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000",  
"complete": true  
}  
$ signedtx="02000000013a6e4279b799791049e1826602e84d2e36797e2005887b98c3ecf16b01b7f361010000006a4730440220335d15a2a2ca3ce6a302ce041686739d4a38eb0599a5ea08305de71965268d05022015f77a33cf7d613015b2aba5beb03088033625505ad5d4d0624defdbea22262b01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff01409c0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac00000000"

Note that we captured the signed hex by hand, rather than trying to parse it out of the JSON object. A software package called "JQ" could do better, as we'll explain in an upcoming interlude.

### Send the Raw Transaction

You've now got a ready-to-go raw transaction, but it doesn't count until you actually put it on the network, which you do with the sendrawtransaction command. You'll get back a txid:

$ bitcoin-cli sendrawtransaction $signedtx  
a1fd550d1de727eccde6108c90d4ffec11ed83691e96e119d842b3f390e2f19a

You'll immediately see that the UTXO and its money have been removed from your wallet:

$ bitcoin-cli listunspent  
[  
{  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"vout": 0,  
"address": "mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
"label": "",  
"scriptPubKey": "76a9141b72503639a13f190bf79acf6d76255d772360b788ac",  
"amount": 0.00010000,  
"confirmations": 23,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/1']02fd5740996d853ea51a6904cf03257fc11204b0179f344c49739ec5b20b39c9ba)#62rud39c",  
"safe": true  
},  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022000,  
"confirmations": 6,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}  
]

$ bitcoin-cli getbalance  
0.00032000

Soon listtransactions should show a confirmed transaction of category 'send".

{  
"address": "n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi",  
"category": "send",  
"amount": -0.00040000,  
"vout": 0,  
"fee": -0.00010000,  
"confirmations": 1,  
"trusted": true,  
"txid": "a1fd550d1de727eccde6108c90d4ffec11ed83691e96e119d842b3f390e2f19a",  
"walletconflicts": [  
],  
"time": 1592608574,  
"timereceived": 1592608574,  
"bip125-replaceable": "no",  
"abandoned": false  
}

You can see that it matches the txid and the recipient address. Not only does it show the amount sent, but it also shows the transaction fee. And, it's already received a confirmation, because we offered a fee that would get it swept up into a block quickly.

Congratulations! You're now a few satoshis poorer!

## Summary: Creating a Raw Transaction

When money comes into your Bitcoin wallet, it remains as distinct amounts, called UTXOs. When you create a raw transaction to send that money back out, you use one or more UTXOs to fund it. You then can create a raw transaction, sign it, and send it on the Bitcoin network. However, this is just a foundation: you'll usually need to create a raw transaction with multiple outputs to actually send something on the bitcoin network!

## What's Next?

Step Back from "Sending Bitcoin Transactions" with [Interlude: Using JQ](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2__Interlude_Using_JQ.md).

# 4.3 Creating a Raw Transaction with Named Arguments

It can sometimes be daunting to figure out the right order for the arguments to a bitcoin-cli command. Fortunately, you can use _named arguments_ as an alternative.

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.14.0. If you used our setup scripts, that's what you should have, but double-check your version if you have any problems. There is also a bug in the createrawtransaction command's use of named arguments that will presumably be fixed in 0.14.1.

## Create a Named Argument Alias

To use a named argument you must run bitcoin-cli with the -named argument. If you plan to do this regularly, you'll probably want to create an alias:

alias bitcoin-cli="bitcoin-cli -named"

As usual, that's for your ease of use, but we'll continue using the whole commands to maintain clarity.

## Test Out a Named Argument

To learn what the names are for the arguments of a command, consult bitcoin-cli help. It will list the arguments in their proper order, but will now also give names for each of them.

For example, bitcoin-cli help getbalance lists these arguments:

1. dummy [used to be account]
    
2. minconf
    
3. include_watchonly
    
4. avoid_reuse
    

The following shows a traditional, unintuitive usage of getbalance using the minimum confirmation argument:

$ bitcoin-cli getbalance "*" 1

With named arguments, you can clarify what you're doing, which also minimizes mistakes:

$ bitcoin-cli -named getbalance minconf=1

## Test Out a Raw Transaction

Here's what the commands for sending a raw transaction would look like with named arguments:

$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ recipient="n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi"

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.00001 }''')  
$ bitcoin-cli -named decoderawtransaction hexstring=$rawtxhex  
{  
"txid": "2b59c31bc232c0399acee4c2a381b564b6fec295c21044fbcbb899ffa56c3da5",  
"hash": "2b59c31bc232c0399acee4c2a381b564b6fec295c21044fbcbb899ffa56c3da5",  
"version": 2,  
"size": 85,  
"vsize": 85,  
"weight": 340,  
"locktime": 0,  
"vin": [  
{  
"txid": "ca4898d8f950df03d6bfaa00578bd0305d041d24788b630d0c4a32debcac9f36",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00001000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 e7c1345fc8f87c68170b3aa798a956c2fe6a9eff OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi"  
]  
}  
}  
]  
}

$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
e70dd2aa13422d12c222481c17ca21a57071f92ff86bdcffd7eaca71772ba172

Voila! You've sent out another raw transaction, but this time using named arguments for clarity and to reduce errors.

> :warning: **VERSION WARNING:** There is where the bug in Bitcoin Core 0.14 shows up: the 'inputs' argument for 'createrawtransaction' is misnamed 'transactions'. So, if you're on Bitcoin Core 0.14.0, substitute the named argument 'inputs' with 'transactions' for this and future examples. However, as of Bitcoin Core 0.14.1, this code should work as shown.

## Summary: Creating a Raw Transaction with Named Arguments

By running bitcoin-cli with the -named flag, you can use named arguments rather than depending on ordered arguments. bitcoin-cli help will always show you the right name for each argument. This can result in more robust, easier-to-read, less error-prone code.

_These docs will use named arguments for all future examples, for clarity and to establish best practices. However, it will also show all arguments in the correct order. So, if you prefer not to use named args, just strip out the '-named' flag and all of the "name="s and the examples should continue to work correctly._

## What's Next?

Continue "Sending Bitcoin Transactions" with [§4.4: Sending Coins with Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4_Sending_Coins_with_a_Raw_Transaction.md).

# Interlude: Using Curl

bitcoin-cli is ultimately just a wrapper. It's a way to interface with bitcoind from the command line, providing simplified access to its many RPC commands. But RPC can, of course, be accessed directly. That's what this interlude is about: directly connecting to RPC with the curl command.

It won't be used much in the future chapters, but it's an important building block that you can see as an alternative access to bitcoind is you so prefer.

## Know Your Curl

curl, short for "see URL", is a command-line tool that allows you to directly access URLs in a programmatic way. It's an easy way to interact with servers like bitcoind that listen to ports on the internet and that speak a variety of protocols. Curl is also available as a library for many programming languages, such as C, Java, PHP, and Python. So, once you know how to work with Curl, you'll have a strong foundation for using a lot of different API.

In order to use curl with bitcoind, you must know three things: the standard format, the user name and password, and the correct port.

### Know Your Format

The bitcoin-cli commands are all linked to RPC commands in bitcoind. That makes the transition from using bitcoin-cli to using curl very simple. In fact, if you look at any of the help pages for bitcoin-cli, you'll see that they list not only the bitcoin-cli commands, but also parallel curl commands. For example, here is bitcoin-cli help getmininginfo:

$ bitcoin-cli help getmininginfo  
getmininginfo

Returns a json object containing mining-related information.  
Result:  
{ (json object)  
"blocks" : n, (numeric) The current block  
"currentblockweight" : n, (numeric, optional) The block weight of the last assembled block (only present if a block was ever assembled)  
"currentblocktx" : n, (numeric, optional) The number of block transactions of the last assembled block (only present if a block was ever assembled)  
"difficulty" : n, (numeric) The current difficulty  
"networkhashps" : n, (numeric) The network hashes per second  
"pooledtx" : n, (numeric) The size of the mempool  
"chain" : "str", (string) current network name (main, test, regtest)  
"warnings" : "str" (string) any network and blockchain warnings  
}

Examples:

> bitcoin-cli getmininginfo  
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id": "curltest", "method": "getmininginfo", "params": []}' -H 'content-type: text/plain;' http://127.0.0.1:8332/

And there's the curl command, at the end of the help screen! This somewhat lengthy command has four major parts: (1) a listing of your user name; (2) a --data-binary flag; (3) a JSON object that tells bitcoind what to do, including a JSON array of parameters; and (4) an HTTP header that includes the bitcoind URL.

When you are working with curl, most of these arguments to curl will stay the same from command to command; only the method and params entries in the JSON array will typically change. However, you need to know how to fill in your username and your URL address in order to make it work in the first place!

_Whenever you're unsure about how to curl an RPC command, just look at the bitcoin-cli help and go from there._

### Know Your User Name

In order to speak with the bitcoind port, you need a user name and password. These were created as part of your initial Bitcoin setup, and can be found in ~/.bitcoin/bitcoin.conf.

For example, here's our current setup:

$ cat ~/.bitcoin/bitcoin.conf  
server=1  
dbcache=1536  
par=1  
maxuploadtarget=137  
maxconnections=16  
rpcuser=StandUp  
rpcpassword=8eaf562eaf45c33c3328bc66008f2dd1  
rpcallowip=127.0.0.1  
debug=tor  
prune=550  
testnet=1  
mintxfee=0.001  
txconfirmtarget=1  
[test]  
rpcbind=127.0.0.1  
rpcport=18332  
[main]  
rpcbind=127.0.0.1  
rpcport=8332  
[regtest]  
rpcbind=127.0.0.1  
rpcport=18443

Our user name is StandUp and our password is 8eaf562eaf45c33c3328bc66008f2dd1.

> **WARNING:** Clearly, it's not very secure to have this information in a plain text file. As of Bitcoin Core 0.12, you can instead omit the rpcpassword from your bitcoin.conf file, and have bitcoind generate a new cookie whenever it starts up. The downside of this is that it makes use of RPC commands by other applications, such as the ones detailed in this chapter, more difficult. So, we're going to stick with the plain rpcuser and rpcpassword information for now, but for production software, consider moving to cookies.

The secure way to RPC with bitcoind is as follows:

$ curl --user StandUp --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/  
Enter host password for user 'bitcoinrpc':

As noted, you will be prompted for your password.

> :link: **TESTNET vs MAINNET:** Testnet uses a URL with port 18332 and mainnet uses a URL with port 8332. Take a look in your bitcoin.conf, it's all laid out there.

The insecure way to do so is as follows:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/

> **WARNING:** Entering your password on the command line may put your password into the process table and/or save it into a history. This is even less recommended than putting it in a file, except for testing on testnet. If you want to do it anywhere else, make sure you know what you're doing!

### Know Your Command & Parameters

With all of that in hand, you're ready to send off standard RPC commands with curl ... but you still need to know how to incorporate the two elements that tend to change in the curl command.

The first is method, which is the RPC method being used. This should generally match the command names you've been feeding into bitcoin-cli for ages.

The second is params, which is a JSON array of parameters. These are the same as the arguments (or named arguments) that you've been using. They're also the most confusing part of curl, in large part because they're a structured array rather than a simple list.

Here's what some parameter arrays will look like:

- [] — An empty array
    
- ["000b4430a7a2ba60891b01b718747eaf9665cb93fbc0c619c99419b5b5cf3ad2"] — An array with data
    
- ["'$signedhex'"] — An array with a variable
    
- [6, 9999999] — An array with two parameters
    
- {} - An empty object
    
- [''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]'', ''{ "'$recipient'": 0.298, "'$changeaddress'": 1.0}''] — An array with an array containing an object and a bare object
    

## Get Information

You can now send your first curl command by accessing the getmininginfo RPC:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/  
{"result":{"blocks":1772428,"difficulty":10178811.40698772,"networkhashps":91963587385939.06,"pooledtx":61,"chain":"test","warnings":"Warning: unknown new rules activated (versionbit 28)"},"error":null,"id":"curltest"}

Note that we provided the method, getmininginfo, and the parameter, [], but that everything else was the standard curl command line.

> **WARNING:** If you get a result like "Failed to connect to 127.0.0.1 port 8332: Connection refused", be sure that a line like rpcallowip=127.0.0.1 is in your ~/.bitcoin/bitcoin.conf. If things still don't work, be sure that you're allowing access to port 18332 (or 8332) from localhost. Our standard setup from [Chapter Two: Creating a Bitcoin-Core VPS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_0_Setting_Up_a_Bitcoin-Core_VPS.md) should do all of this.

The result is another JSON array, which is unfortunately ugly to read if you're using curl by hand. Fortunately, you can clean it up simply by piping it through jq:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
% Total % Received % Xferd Average Speed Time Time Time Current  
Dload Upload Total Spent Left Speed  
100 295 100 218 100 77 72666 25666 --:--:-- --:--:-- --:--:-- 98333  
{  
"result": {  
"blocks": 1772429,  
"difficulty": 10178811.40698772,  
"networkhashps": 90580030969896.44,  
"pooledtx": 4,  
"chain": "test",  
"warnings": "Warning: unknown new rules activated (versionbit 28)"  
},  
"error": null,  
"id": "curltest"  
}

You'll see a bit of connectivity reporting as the data is downloaded, then when that data hits jq, everything will be output in a correctly indented form. (We'll be omitting the download information in future examples.)

## Manipulate Your Wallet

Though you're accessing bitcoind directly, you'll still get access to wallet functionality, because that's largely stored in bitcoind itself.

### Look Up Addresses

Use the getaddressesbylabel RPC to list all of your current addresses:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbylabel", "params": [""] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
{  
"result": {  
"mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE": {  
"purpose": "receive"  
},  
"mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff": {  
"purpose": "receive"  
},  
"moKVV6XEhfrBCE3QCYq6ppT7AaMF8KsZ1B": {  
"purpose": "receive"  
},  
"mwJL7cRiW2bUnY81r1thSu3D4jtMmwyU6d": {  
"purpose": "receive"  
},  
"tb1q5gnwrh7ss5mmqt0qfan85jdagmumnatcscwpk6": {  
"purpose": "receive"  
},  
"tb1qmtucvjtga68kgrvkl7q05x4t9lylxhku7kqdpr": {  
"purpose": "receive"  
}  
},  
"error": null,  
"id": "curltest"  
}

This is our first example of a real parameter, "". This is the required label parameter for getaddressesbylabel, but all of our addresses are under the default label, so nothing special was required here.

The result is a list of all the addresses that have been used by this wallet ... some of which presumably contain funds.

### Look Up Funds

Use the listunspent RPC to list the funds that you have available:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
{  
"result": [  
{  
"txid": "e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d",  
"vout": 1,  
"address": "mk9ry5VVy8mrA8SygxSQQUDNSSXyGFot6h",  
"scriptPubKey": "76a91432db726320e4ad170c9c1ee83cd4d8a243c3435988ac",  
"amount": 0.0009,  
"confirmations": 4,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/1'/2']02881697d252d8bf181d08c58de1f02aec088cd2d468fc5fd888c6e39909f7fabf)#p6k7dptk",  
"safe": true  
},  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022,  
"confirmations": 19,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}  
],  
"error": null,  
"id": "curltest"  
}

This is almost exactly the same output that you receive when you type bitcoin-cli listunspent, showing how closely tied the two interfaces are. If no cleanup or extra help is needed, then bitcoin-cli just outputs the RPC. Easy!

### Create an Address

After you know where your funds are, the next step in crafting a transaction is to get a change address. By now you've probably got the hang of this, and you know that for simple RPC commands, all you need to do is adjust the method is the curl command:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": ["legacy"] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
{  
"result": "mrSqN37TPs89GcidSZTvXmMzjxoJZ6RKoz",  
"error": null,  
"id": "curltest"  
}

> **WARNING:** The parameters order is important when you are sending RPC commands using curl. There's only one argument for getrawchangeaddress, but consider its close cousin getnewaddress. That takes two arguments: first label, then type. If we sent that same "params": ["legacy"] instead of "params": ["", "legacy"], we would get a bech32 address with a label of "legacy" instead of a legacy address, so pay attention to the order!

At this point, we can even revert to our standard practice of saving results to variables with additional help from jq:

$ newaddress=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": ["legacy"] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result')  
$ echo $newaddress  
mqdfnjgWr2r3sCCeuTDfe8fJ1CnycF2e6R

No need to worry about the downloading info. It'll go to STDERR and be displayed on your screen, while the results go to STDOUT and are saved in your variable.

## Create a Transaction

You're now ready to create a transaction with curl.

### Ready Your Variables

Just as with bitcoin-cli, in order to create a transaction by curling RPC commands, you should first save your variables. The only change here is that curl creates a JSON object that includes a result key-value, so you always need to pipe through the .result tag before you do anything else.

This example sets up our variables for using the 1.2985 BTC in funds listed in the first unspent transaction above:

$ utxo_txid=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result | .[0] | .txid')  
$ utxo_vout=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result | .[0] | .vout')  
$ recipient=mwCwTceJvYV27KXBc3NJZys6CjsgsoeHmf  
$ changeaddress=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": ["legacy"] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result')

$ echo $utxo_txid  
e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d  
$ echo $utxo_vout  
1  
$ echo $recipient  
mwCwTceJvYV27KXBc3NJZys6CjsgsoeHmf  
$ echo $changeaddress  
n2jf3MzeFpFGa7wq8rXKVnVuv5FoNSJZ1N

### Create the Transaction

The transaction created with curl is very similar to the transaction created with bitcoin-cli, but with a few subtle differences:

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": [''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]'', ''{ "'$recipient'": 0.0003, "'$changeaddress'": 0.0005}'']}' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
{  
"result": "02000000010d6acd0356db222ca3a7ee7fa1e3044316223ceec1f64b58aeb2e0de921007e70100000000ffffffff0230750000000000001976a914ac19d3fd17710e6b9a331022fe92c693fdf6659588ac50c30000000000001976a9147021efec134057043386decfaa6a6aa4ee5f19eb88ac00000000",  
"error": null,  
"id": "curltest"  
}

The heart of the transaction is, of course, the params JSON array, which we're putting to full use for the first time.

Note that the entire params is lodged in []s to mark the parameters array.

We've also varied up the quoting from how things worked in bitcoin-cli, to start and end each array and object within the params array with '' instead of our traditional '''. That's because the entire set of JSON arguments already has a ' around it. As usual, just take a look at the bizarre shell quoting and get used to it.

However, there's one last thing of note in this example, and it can be _maddening_ if you miss it. When you executed a createrawtransaction command with bitcoin-cli the JSON array of inputs and the JSON object of outputs were each distinct parameters, so they were separated by a space. Now, because they're part of that params JSON array, they're separated by a comma (,). Miss that and you'll get a parse error without much additional information.

> **WARNING:** Ever having troubles debugging your curl? Add the argument --trace-ascii /tmp/foo. Full information on what's being sent to the server will be saved in /tmp/foo (or whatever file name you provide).

Having verified that things work, you probably want to save the hex code into a variable:

$ hexcode=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": [''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]'', ''{ "'$recipient'": 0.0003, "'$changeaddress'": 0.0005}'']}' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result')

### Sign and Send

Signing and sending your transaction using curl is an easy use of the signrawtransactionwithwallet and sendrawtransaction RPC:

$ signedhex=$(curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signrawtransactionwithwallet", "params": ["'$hexcode'"] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.result | .hex')

$ curl --user StandUp:8eaf562eaf45c33c3328bc66008f2dd1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["'$signedhex'"] }' -H 'content-type: text/plain;' http://127.0.0.1:18332/ | jq -r '.'  
{  
"result": "eb84c5008038d760805d4d9644ace67849542864220cb2685a1ea2c64176b82d",  
"error": null,  
"id": "curltest"  
}

## Summary: Accessing Bitcoind with Curl

Having finished this section, you may feel that accessing bitcoind via curl is very much like accessing it through bitcoin-cli ... but more cumbersome. And, you'd be right. bitcoin-cli has pretty complete RPC functionality, so anything that you do through curl you can probably do through bitcoin-cli. Which is why we're going to continue concentrating on bitcoin-cli following this digression.

But there are still reasons you'd use curl instead of bitcoin-cli:

_What is the power of curl?_ Most obviously, curl takes out one level of indirection. Instead of working with bitcoin-cli which sends RPC commands to bitcoind, you're sending those RPC commands directly. This allows for more robust programming, because you don't have to worry about what unexpected things that bitcoin-cli might do or how it might change over time. However, you're also taking your first steps toward using a more comprehensive programming language than the poor options offered by a shell script. As you'll see in the last few chapters of this, you might actually see curl libraries are other functions to access the RPC commands in a variety of programming languages: but that's still a long ways away.

## What's Next?

Learn one more way to "Send Bitcoin Transactions" with [§4.5 Sending Coins with Automated Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_5_Sending_Coins_with_Automated_Raw_Transactions.md).

# 4.4: Sending Coins with Raw Transactions

As noted at the start of this chapter, the bitcoin-cli interface offers three major ways to send coins. [§4.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_1_Sending_Coins_The_Easy_Way.md) talked about sending them the first way, using the sendtoaddress command. Since then, we've been building details on how to send coins a second way, with raw transactions. [§4.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2_Creating_a_Raw_Transaction.md) taught how to create a raw transaction, an [Interlude](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_2__Interlude_Using_JQ.md) explained JQ, and [§4.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_3_Creating_a_Raw_Transaction_with_Named_Arguments.md) demonstrated named arguments.

We can now put those together and actually send funds using a raw transaction.

## Create a Change Address

Our sample raw transaction in section §4.2 was very simplistic: we sent the entirety of a UTXO to a new address. More frequently, you'll want to send someone an amount of money that doesn't match a UTXO. But, you'll recall that the excess money from a UTXO that's not sent to your recipient just becomes a transaction fee. So, how do you send someone just part of a UTXO, while keeping the rest for yourself?

The solution is to _send_ the rest of the funds to a second address, a change address that you've created in your wallet specifically to receive them:

$ changeaddress=$(bitcoin-cli getrawchangeaddress legacy)  
$ echo $changeaddress  
mk9ry5VVy8mrA8SygxSQQUDNSSXyGFot6h

Note that this uses a new function: getrawchangeaddress. It's largely the same as getnewaddress but is optimized for use as a change address in a raw transaction, so it doesn't do things like make entries in your address book. We again selected the legacy address, instead of going with the default of bech32, simply for consistency. This is a situation where it would have been entirely safe to generate a default Bech32 address, just by using bitcoin-cli getrawchangeaddress, because it would being sent and received by you on your Bitcoin Core node which fully supports this. But, hobgoblins; we'll shift this over to Bech32 as well in [§4.6](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md).

You now have an additional address inside your wallet, so that you can receive change from a UTXO! In order to use it, you'll need to create a raw transaction with two outputs.

## Pick Sufficient UTXOs

Our sample raw transaction was simple in another way: it assumed that there was enough money in a single UTXO to cover the transaction. Often this will be the case, but sometimes you'll want to create transactions that spends more money than you have in a single UTXO. To do so, you must create a raw transaction with two (or more) inputs.

## Write a Real Raw Transaction

To summarize: creating a real raw transaction to send coins will sometimes require multiple inputs and will almost always require multiple outputs, one of which is a change address. We'll be creating that sort of more realistic transaction here, in a new example that shows a real-life example of sending funds via Bitcoin's second methodology, raw transactions.

We're going to use our 0th and 2nd UTXOs:

$ bitcoin-cli listunspent  
[  
[  
{  
"txid": "0619fecf6b2668fab1308fbd7b291ac210932602a6ac6b8cc11c7ae22c43701e",  
"vout": 1,  
"address": "mwJL7cRiW2bUnY81r1thSu3D4jtMmwyU6d",  
"label": "",  
"scriptPubKey": "76a914ad1ed1c5971b2308f89c1362d4705d020a40e8e788ac",  
"amount": 0.00899999,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/4']03eae28c93035f95a620dd96e1822f2a96e0357263fa1f87606a5254d5b9e6698f)#wwnfx2sp",  
"safe": true  
},  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022000,  
"confirmations": 15,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
},  
{  
"txid": "0df23a9dba49e822bbc558f15516f33021a64a5c2e48962cec541e0bcc79854d",  
"vout": 0,  
"address": "mwJL7cRiW2bUnY81r1thSu3D4jtMmwyU6d",  
"label": "",  
"scriptPubKey": "76a914ad1ed1c5971b2308f89c1362d4705d020a40e8e788ac",  
"amount": 0.00100000,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/4']03eae28c93035f95a620dd96e1822f2a96e0357263fa1f87606a5254d5b9e6698f)#wwnfx2sp",  
"safe": true  
}  
]

In our example, we're going to send .009 BTC, which is (barely) larger than either of our UTXOs. This requires combining them, then using our change address to retrieve the unspent funds.

### Set Up Your Variables

We already have $changeaddress and $recipient variables from previous examples:

$ echo $changeaddress  
mk9ry5VVy8mrA8SygxSQQUDNSSXyGFot6h  
$ echo $recipient  
n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi

We also need to record the txid and vout for each of our two UTXOs. Having identified the UTXOs that we want to spend, we can use our JQ techniques to make sure accessing them is error free:

$ utxo_txid_1=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout_1=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ utxo_txid_2=$(bitcoin-cli listunspent | jq -r '.[2] | .txid')  
$ utxo_vout_2=$(bitcoin-cli listunspent | jq -r '.[2] | .vout')

### Write the Transaction

Writing the actual raw transaction is surprisingly simple. All you need to do is include an additional, comma-separated JSON object in the JSON array of inputs and an additional, comma-separated key-value pair in the JSON object of outputs.

Here's the example. Note the multiple inputs after the inputs arg and the multiple outputs after the outputs arg.

$ rawtxhex2=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' } ]''' outputs='''{ "'$recipient'": 0.009, "'$changeaddress'": 0.0009 }''')

We were _very_ careful figuring out our money math. These two UTXOs contain 0.00999999 BTC. After sending 0.009 BTC, we'll have .00099999 BTC left. We chose .00009999 BTC the transaction fee. To accommodate that fee, we set our change to .0009 BTC. If we'd messed up our math and instead set our change to .00009 BTC, that additional BTC would be lost to the miners! If we'd forgot to make change at all, then the whole excess would have disappeared. So, again, _be careful_.

Fortunately, we can triple-check with the btctxfee alias from the JQ Interlude:

$ ./txfee-calc.sh $rawtxhex2  
.00009999

### Finish It Up

You can now sign, seal, and deliver your transaction, and it's yours (and the faucet's):

$ signedtx2=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex2 | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx2  
e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d

### Wait

As usual, your money will be in flux for a while: the change will be unavailable until the transaction actually gets confirmed and a new UTXO is given to you.

But, in 10 minutes or less (probably), you'll have your remaining money back and fully spendable again. For now, we're still waiting:

$ bitcoin-cli listunspent  
[  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022000,  
"confirmations": 15,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}  
]

And the change will eventuall arrive:

[  
{  
"txid": "e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d",  
"vout": 1,  
"address": "mk9ry5VVy8mrA8SygxSQQUDNSSXyGFot6h",  
"scriptPubKey": "76a91432db726320e4ad170c9c1ee83cd4d8a243c3435988ac",  
"amount": 0.00090000,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/1'/2']02881697d252d8bf181d08c58de1f02aec088cd2d468fc5fd888c6e39909f7fabf)#p6k7dptk",  
"safe": true  
},  
{  
"txid": "91261eafae15ea53dedbea7c1db748c52bbc04a85859ffd0d839bda1421fda4c",  
"vout": 0,  
"address": "mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
"label": "",  
"scriptPubKey": "76a9142d573900aa357a38afd741fbf24b075d263ea6e088ac",  
"amount": 0.00022000,  
"confirmations": 16,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([d6043800/0'/0'/3']0278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132)#nhjc3f8y",  
"safe": true  
}  
]

This also might be a good time to revisit a blockchain explorer, so that you can see more intuitively how the inputs, outputs, and transaction fee are all laid out: [e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d](https://live.blockcypher.com/btc-testnet/tx/e7071092dee0b2ae584bf6c1ee3c22164304e3a17feea7a32c22db5603cd6a0d/).

## Summary: Sending Coins with Raw Transactions

To send coins with raw transactions, you need to create a raw transaction with one or more inputs (to have sufficient funds) and one or more outputs (to retrieve change). Then, you can follow your normal procedure of using createrawtransaction with named arguments and JQ, as laid out in previous sections.

> :fire: _**What is the power of sending coins with raw transactions?**_ _The advantages._ It gives you the best control. If your goal is to write a more intricate Bitcoin script or program, you'll probably use raw transactions so that you know exactly what's going on. This is also the _safest_ situation to use raw transactions, because you can programmatically ensure that you don't make mistakes. _The disadvantages._ It's easy to lose money. There are no warnings, no safeguards, and no programmatic backstops unless you write them. It's also arcane. The formatting is obnoxious, even using the easy-to-use bitcoin-cli interface, and you have to do a lot of lookup and calculation by hand.

## What's Next?

See another alternative way to input commands with [Interlude: Using Curl](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md).

Or, you prefer to skip what's frankly a digression, learn one more way to "Send Bitcoin Transactions" with [§4.5 Sending Coins with Automated Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_5_Sending_Coins_with_Automated_Raw_Transactions.md).

# 4.5: Sending Coins with Automated Raw Transactions

This chapter lays out three ways to send funds via Bitcoin's cli interface. [§4.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_1_Sending_Coins_The_Easy_Way.md) described how to do so with a simple command, and [§4.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4_Sending_Coins_with_a_Raw_Transaction.md) detailed how to use a more dangerous raw transaction. This final section splits the difference by showing how to make raw transactions simpler and safer.

## Let Bitcoin Calculate For You

The methodology for automated raw transactions is simple: you create a raw transaction, but you use the fundrawtransaction command to ask the bitcoind to run the calculations for you.

In order to use this command, you'll need to ensure that your ~/.bitcoin/bitcoin.conf file contains rational variables for calculating transaction fees. Please see [§4.1: Sending Coins The Easy Way](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_1_Sending_Coins_The_Easy_Way.md) for more information on this.

For very conservative numbers, we suggested adding the following to the bitcoin.conf:

mintxfee=0.0001  
txconfirmtarget=6

To keep the tutorial moving along (and more generally to move money fast) we suggested the following:

mintxfee=0.001  
txconfirmtarget=1

## Create a Bare Bones Raw Transaction

To use fundrawtransaction you first need to create a bare-bones raw transaction that lists _no_ inputs and _no_ change address. You'll just list your recipient and how much you want to send them, in this case $recipient and 0.0002 BTC.

$ recipient=n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi  
$ unfinishedtx=$(bitcoin-cli -named createrawtransaction inputs='''[]''' outputs='''{ "'$recipient'": 0.0002 }''')

## Fund Your Bare Bones Transaction

You then tell bitcoin-cli to fund that bare-bones transaction:

$ bitcoin-cli -named fundrawtransaction hexstring=$unfinishedtx  
{  
"hex": "02000000012db87641c6a21e5a68b20c226428544978e6ac44964d5d8060d7388000c584eb0100000000feffffff02204e0000000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac781e0000000000001600140cc9cdcf45d4ea17f5227a7ead52367aad10a88400000000",  
"fee": 0.00022200,  
"changepos": 1  
}

That provides a lot of useful information, but once you're confident with how it works, you'll want to use JQ to save your hex to a variable, as usual:

$ rawtxhex3=$(bitcoin-cli -named fundrawtransaction hexstring=$unfinishedtx | jq -r '.hex')

## Verify Your Funded Transaction

It seems like magic, so the first few times you use fundrawtransaction, you'll probably want to verify it.

Running decoderawtransaction will show that the raw transaction is now laid out correctly, using one or more of your UTXOs and sending excess funds back to a change address:

$ bitcoin-cli -named decoderawtransaction hexstring=$rawtxhex3  
{  
"txid": "b3b4c2057dbfbef6690e975ede92fde805ddea13c730f58401939a52c9ac1b99",  
"hash": "b3b4c2057dbfbef6690e975ede92fde805ddea13c730f58401939a52c9ac1b99",  
"version": 2,  
"size": 116,  
"vsize": 116,  
"weight": 464,  
"locktime": 0,  
"vin": [  
{  
"txid": "eb84c5008038d760805d4d9644ace67849542864220cb2685a1ea2c64176b82d",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.00020000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 e7c1345fc8f87c68170b3aa798a956c2fe6a9eff OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi"  
]  
}  
},  
{  
"value": 0.00007800,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 a782f4c6e1e75a5b24f3d675d6f11b5ebf3b2142",  
"hex": "0014a782f4c6e1e75a5b24f3d675d6f11b5ebf3b2142",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q57p0f3hpuad9kf8n6e6adugmt6lnkg2zzr592r"  
]  
}  
}  
]  
}

One thing of interest here is the change address, which is the second vout. Note that it's a tb1 address, which means that it's Bech32; when we gave Bitcoin Core the total ability to manage our change, it did so using its default address type, Bech32, and it worked fine. That's why our change to SegWit addresses in [§4.6](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md) really isn't that big of a deal, but there are some gotchas for wider usage, which we'll talk about there.

Though we saw the fee in the fundrawtransaction output, it's not visible here. However, you can verify it with the txfee-calc.sh JQ script created in the [JQ Interlude](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/04_2__Interlude_Using_JQ.md):

$ ~/txfee-calc.sh $rawtxhex3  
.000222

Finally, you can use getaddressinfo to see that the generated change address really belongs to you:

$ bitcoin-cli -named getaddressinfo address=tb1q57p0f3hpuad9kf8n6e6adugmt6lnkg2zzr592r  
{  
"address": "tb1q57p0f3hpuad9kf8n6e6adugmt6lnkg2zzr592r",  
"scriptPubKey": "0014a782f4c6e1e75a5b24f3d675d6f11b5ebf3b2142",  
"ismine": true,  
"solvable": true,  
"desc": "wpkh([d6043800/0'/1'/10']038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec5)#zpv26nar",  
"iswatchonly": false,  
"isscript": false,  
"iswitness": true,  
"witness_version": 0,  
"witness_program": "a782f4c6e1e75a5b24f3d675d6f11b5ebf3b2142",  
"pubkey": "038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec5",  
"ischange": true,  
"timestamp": 1592335137,  
"hdkeypath": "m/0'/1'/10'",  
"hdseedid": "fdea8e2630f00d29a9d6ff2af7bf5b358d061078",  
"hdmasterfingerprint": "d6043800",  
"labels": [  
]  
}

Note the ismine results.

## Send Your Funded Transaction

At this point you can sign and send the transaction as usual.

$ signedtx3=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex3 | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx3  
8b9dd66c999966462a3d88d6ac9405d09e2aa409c0aa830bdd08dbcbd34a36fa

In several minutes, you'll have your change back:

$ bitcoin-cli listunspent  
[  
{  
"txid": "8b9dd66c999966462a3d88d6ac9405d09e2aa409c0aa830bdd08dbcbd34a36fa",  
"vout": 1,  
"address": "tb1q57p0f3hpuad9kf8n6e6adugmt6lnkg2zzr592r",  
"scriptPubKey": "0014a782f4c6e1e75a5b24f3d675d6f11b5ebf3b2142",  
"amount": 0.00007800,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "wpkh([d6043800/0'/1'/10']038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec5)#zpv26nar",  
"safe": true  
}  
]

## Summary: Sending Coins with Automated Raw Transactions

If you must send funds with raw transactions then fundrawtransaction gives you a nice alternative where fees, inputs, and outputs are calculated for you, so you don't accidentally lose a bunch of money.

> :fire: _**What is the power of sending coins with automated raw transactions?**_ _The advantages._ It provides a nice balance. If you're sending funds by hand and sendtoaddress doesn't offer enough control for whatever reason, you can get some of the advantages of raw transactions without the dangers. This methodology should be used whenever possible if you're sending raw transactions by hand. _The disadvantages._ It's a hodge-podge. Though there are a few additional options for the fundrawtransaction command that weren't mentioned here, your control is still limited. You'd probably never want to use this method if you were writing a program where the whole goal is to know exactly what's going on.

## What's Next?

Complete your "Sending of Bitcoin Transactions" with [§4.6: Creating a Segwit Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md).

# 4.6: Creating a SegWit Transaction

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Once upon a time, the Bitcoin heavens shook with the blocksize wars. Fees were skyrocketing, and users were worried about scaling. The Bitcoin Core developers were reluctant to simply increase the blocksize, but they came upon a compromise: SegWit, the Segregated Witness. Segregated Witness is a fancy way of saying "Separated Signature". It creates new sorts of transactions that remove signatures to the end of the transaction. By combining this with increased block sizes that only are visible to upgraded nodes, SegWit resolved the scaling problems for Bitcoin at the time (and also resolved a nasty malleability bug that had previously made even better scaling with layer-2 protocols like Lightning impractical).

The catch? SegWit uses different addresses, some of which are compatible with older nodes, and some of which are not.

> :warning: **VERSION WARNING:** SegWit was introduced in BitCoin 0.16.0 with what was described at the time as "full support". With that said, there were some flaws in its integration with bitcoin-cli at the time which prevented signing from working correctly on new P2SH-SegWit addresses. The non-backward-compatible Bech32 address was also introduced in Bitcoin 0.16.0 and was made the default addresstype in Bitcoin 0.19.0. All of this functionality should now fully work with regard to bitcoin-cli functions (and thus this tutorial). The catch comes in interacting with the wider world. Everyone should be able to send to a P2SH-SegWit address because it was purposefully built to support backward compatibility by wrapping the SegWit functionality in a Bitcoin Script. The same isn't true for Bech32 addresses: if someone tells you that they're unable to send to your Bech32 address, this is why, and you need to generate a legacy or P2SH-SegWit address for their usage. (Many sites, particularly exchanges, can also not generate or receive on SegWit addresses, particularly Bech32 addresses, but that's a whole different issue and doesn't affect your usage of them.)

## Understand a SegWit Transaction

In classic transactions, signature (witness) information was stored toward the middle of the transaction, while in SegWit transactions, it's at the bottom. This goes hand-in-hand with the blocksize increases that were introduced in the SegWit upgrade. The blocksize was increased from 1M to a variable amount based on how many SegWit transactions are in a block, starting as low as 1M (no SegWit transactions) and going as high as 4M (all SegWit transactions). This variable size was created to accomodate classic nodes, so that everything remains backward compatible. If a classic node sees a SegWit transaction, it throws out the witness information (resulting in a smaller sized block, under the old 1M limit), while if a new node sees a SegWit transaction, it keeps the witness information (resulting in a larger sized block, up to the new 4M limit).

So that's the what and how of SegWit transactions. Not that you need to know any of it to use them. Most transactions on the Bitcoin network are now SegWit. They're what you're going to natively use for more transactions and receipts of money. The details are no more relevant at this point than the details of how most of Bitcoin works.

## Create a SegWit Address

You create a SegWit address the same way as any other address, with the getnewaddress and the getrawchangeaddress commands.

If you need to create an address for someone who can't send to the newer Bech32 addresses, then use the p2sh-segwit addresstype:

$ bitcoin-cli -named getnewaddress address_type=p2sh-segwit  
2N5h2r4karVqN7uFtpcn8xnA3t5cbpszgyN

Seeing an address with a "2" prefix means that you did it right.

> :link: **TESTNET vs MAINNET:** "3" for Mainnet.

However, if the person you're interacting with has a fully mature client, they'll be able to send to a Bech32 address, which you create using the commands in the default way:

$ bitcoin-cli getnewaddress  
tb1q5gnwrh7ss5mmqt0qfan85jdagmumnatcscwpk6

As we've already seen, change addresses generated from within bitcoin-cli interact fine with Bech32 addresses, so there's no point in using the legacy flag there either:

$ bitcoin-cli getrawchangeaddress  
tb1q05wx5tyadm8qe83exdqdyqvqqzjt3m38vfu8ff

Here, note that the unique "tb1" prefix denoted Bech32.

> :link: **TESTNET vs MAINNET:** "bc1" for mainnet.

Bitcoin-cli doesn't care which address type you're using. You can run a command like listaddressgroupings and it will freely mix addresses of the different types:

$ bitcoin-cli listaddressgroupings  
[  
[  
[  
"mfsiRhxbQxcD7HLS4PiAim99oeGyb9QY7m",  
0.01000000,  
""  
]  
],  
[  
[  
"mi25UrzHnvn3bpEfFCNqJhPWJn5b77a5NE",  
0.00000000,  
""  
],  
[  
"tb1q6dak4e9fz77vsulk89t5z92l2e0zm37yvre4gt",  
0.00000000  
]  
],  
[  
[  
"mjehC2KHzXcBDcwTd4LhZ2GzyzrZ3Kd3ff",  
0.00022000,  
""  
]  
],  
[  
[  
"mk9ry5VVy8mrA8SygxSQQUDNSSXyGFot6h",  
0.00000000  
],  
[  
"mqjrdY5raxKzXQf5t2VvVvzhvFAgersu9B",  
0.00000000  
],  
[  
"mwJL7cRiW2bUnY81r1thSu3D4jtMmwyU6d",  
0.00000000,  
""  
],  
[  
"tb1q57p0f3hpuad9kf8n6e6adugmt6lnkg2zzr592r",  
0.00007800  
]  
],  
[  
[  
"mpVLL7iqPr4d7BJkEG54mcdm7WmrAhaW6q",  
0.01000000,  
""  
]  
],  
[  
[  
"tb1q5gnwrh7ss5mmqt0qfan85jdagmumnatcscwpk6",  
0.01000000,  
""  
]  
]  
]

## Send a SegWit Transaction The Easy Way

So how do you send a Segwit transaction? Exactly like any other transaction. It doesn't matter if the UTXO is SegWit, the address is SegWit, or some combination thereof. You can expect bitcoin-cli to do the right thing. Though you can tell the differences via the addresses, they don't matter for interacting with things at the bitcoin-cli or RPC level. (And this is one of the advantages of using the command line and the RPC interface, as suggested in this tutorial: experts have already done the hard work for you, including things like how to send to both legacy and Bech32 addresses. You just get to use that functionality to your own advantage.)

Here's an example of sending to a SegWit address, the easy way:

$ bitcoin-cli sendtoaddress tb1qw508d6qejxtdg4y5r3zarvary0c5xw7kxpjzsx 0.005  
854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42

If you look at your transaction, you can see the use of the Bech32 address:

$ bitcoin-cli -named gettransaction txid="854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42" verbose=true  
{  
"amount": -0.00500000,  
"fee": -0.00036600,  
"confirmations": 0,  
"trusted": true,  
"txid": "854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42",  
"walletconflicts": [  
],  
"time": 1592948795,  
"timereceived": 1592948795,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "tb1qw508d6qejxtdg4y5r3zarvary0c5xw7kxpjzsx",  
"category": "send",  
"amount": -0.00500000,  
"vout": 1,  
"fee": -0.00036600,  
"abandoned": false  
}  
],  
"hex": "0200000002114d5a4c3b847bc796b2dc166ca7120607b874aa6904d4a43dd5f9e0ea79d4ba010000006a47304402200a3cc08b9778e7b616340d4cf7841180321d2fa019e43f25e7f710d9a628b55c02200541fc200a07f2eb073ad8554357777d5f1364c5a96afe5e77c6185d66a40fa7012103ee18c598bafc5fbea72d345329803a40ebfcf34014d0e96aac4f504d54e7042dfeffffffa71321e81ef039af490251379143f7247ad91613c26c8f3e3404184218361733000000006a47304402200dd80206b57beb5fa38a3c3578f4b0e40d56d4079116fd2a6fe28e5b8ece72310220298a8c3a1193ea805b27608ff67a2d8b01e347e33a4222edfba499bb1b64a31601210339c001b00dd607eeafd4c117cfcf86be8efbb0ca0a33700cffc0ae0c6ee69d7efeffffff026854160000000000160014d591091b8074a2375ed9985a9c4b18efecfd416520a1070000000000160014751e76e8199196d454941c45d1b3a323f1433bd6c60e1b00",  
"decoded": {  
"txid": "854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42",  
"hash": "854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42",  
"version": 2,  
"size": 366,  
"vsize": 366,  
"weight": 1464,  
"locktime": 1773254,  
"vin": [  
{  
"txid": "bad479eae0f9d53da4d40469aa74b8070612a76c16dcb296c77b843b4c5a4d11",  
"vout": 1,  
"scriptSig": {  
"asm": "304402200a3cc08b9778e7b616340d4cf7841180321d2fa019e43f25e7f710d9a628b55c02200541fc200a07f2eb073ad8554357777d5f1364c5a96afe5e77c6185d66a40fa7[ALL] 03ee18c598bafc5fbea72d345329803a40ebfcf34014d0e96aac4f504d54e7042d",  
"hex": "47304402200a3cc08b9778e7b616340d4cf7841180321d2fa019e43f25e7f710d9a628b55c02200541fc200a07f2eb073ad8554357777d5f1364c5a96afe5e77c6185d66a40fa7012103ee18c598bafc5fbea72d345329803a40ebfcf34014d0e96aac4f504d54e7042d"  
},  
"sequence": 4294967294  
},  
{  
"txid": "33173618421804343e8f6cc21316d97a24f7439137510249af39f01ee82113a7",  
"vout": 0,  
"scriptSig": {  
"asm": "304402200dd80206b57beb5fa38a3c3578f4b0e40d56d4079116fd2a6fe28e5b8ece72310220298a8c3a1193ea805b27608ff67a2d8b01e347e33a4222edfba499bb1b64a316[ALL] 0339c001b00dd607eeafd4c117cfcf86be8efbb0ca0a33700cffc0ae0c6ee69d7e",  
"hex": "47304402200dd80206b57beb5fa38a3c3578f4b0e40d56d4079116fd2a6fe28e5b8ece72310220298a8c3a1193ea805b27608ff67a2d8b01e347e33a4222edfba499bb1b64a31601210339c001b00dd607eeafd4c117cfcf86be8efbb0ca0a33700cffc0ae0c6ee69d7e"  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01463400,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 d591091b8074a2375ed9985a9c4b18efecfd4165",  
"hex": "0014d591091b8074a2375ed9985a9c4b18efecfd4165",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q6kgsjxuqwj3rwhkenpdfcjccalk06st9z0k0kh"  
]  
}  
},  
{  
"value": 0.00500000,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 751e76e8199196d454941c45d1b3a323f1433bd6",  
"hex": "0014751e76e8199196d454941c45d1b3a323f1433bd6",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qw508d6qejxtdg4y5r3zarvary0c5xw7kxpjzsx"  
]  
}  
}  
]  
}  
}

In fact, both of the vouts use Bech32 addresses: your recipient and the automatically generated change address.

But when we backtrack our vin, we discover that came from a legacy address. Because it doesn't matter:

$ bitcoin-cli -named gettransaction txid="33173618421804343e8f6cc21316d97a24f7439137510249af39f01ee82113a7"  
{  
"amount": 0.01000000,  
"confirmations": 43,  
"blockhash": "00000000000000e2365d2f814d1774b063d9a04356f482010cdfdd537b1a24bb",  
"blockheight": 1773212,  
"blockindex": 103,  
"blocktime": 1592937103,  
"txid": "33173618421804343e8f6cc21316d97a24f7439137510249af39f01ee82113a7",  
"walletconflicts": [  
],  
"time": 1592936845,  
"timereceived": 1592936845,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "mpVLL7iqPr4d7BJkEG54mcdm7WmrAhaW6q",  
"category": "receive",  
"amount": 0.01000000,  
"label": "",  
"vout": 0  
}  
],  
"hex": "020000000001016a66efa334f06e2c54963e48d049a35d7a1bda44633b7464621cae302f35174a0100000017160014f17b16c6404e85165af6f123173e0705ba31ec25feffffff0240420f00000000001976a914626ab1ca41d98f597d18d1ff8151e31a40d4967288acd2125d000000000017a914d5e76abfe5362704ff6bbb000db9cdfa43cd2881870247304402203b3ba83f51c1895b5f639e9bfc40124715e2495ef2c79d4e49c0f8f70fbf2feb02203d50710abe3cf37df4d2a73680dadf3cecbe4f2b5d0b276dbe7711d0c2fa971a012102e64f83ee1c6548bcf44cb965ffdb803f30224459bd2e57a5df97cb41ba476b119b0e1b00"  
}

## Send a SegWit Transaction The Hard Way

You can similarly fund a transaction with a Bech32 address with no difference to the techniques you've learned so far. Here's an exactly of doing so with a complete raw transaction:

$ changeaddress=$(bitcoin-cli getrawchangeaddress)  
$ echo $changeaddress  
tb1q4xje3mx9xn7f8khv7p69ekfn0q72kfs8x3ay4j  
$ bitcoin-cli listunspent  
[  
...  
{  
"txid": "003bfdca5578c0045a76768281f05d5e6f57774be399a76f387e2a0e99e4e452",  
"vout": 0,  
"address": "tb1q5gnwrh7ss5mmqt0qfan85jdagmumnatcscwpk6",  
"label": "",  
"scriptPubKey": "0014a226e1dfd08537b02de04f667a49bd46f9b9f578",  
"amount": 0.01000000,  
"confirmations": 5,  
"spendable": true,  
"solvable": true,  
"desc": "wpkh([d6043800/0'/0'/5']0327dbe2d58d9ed2dbeca28cd26e18f48aa94c127fa6fb4b60e4188f6360317640)#hd66hknp",  
"safe": true  
}  
]  
$ recipient=tb1qw508d6qejxtdg4y5r3zarvary0c5xw7kxpjzsx  
$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[2] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[2] | .vout')  
$ echo $utxo_txid $utxo_vout  
003bfdca5578c0045a76768281f05d5e6f57774be399a76f387e2a0e99e4e452 0  
$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.002, "'$changeaddress'": 0.007 }''')  
$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
e02568b706b21bcb56fcf9c4bb7ba63fdbdec1cf2866168c4f50bc0ad693f26c

It all works exactly the same as other sorts of transactions!

### Recognize the New Descriptor

If you look at the desc field, you'll note that the SegWit address has a different style descriptor than those encountered in [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md). A legacy descriptor described in that section looked like this: pkh([d6043800/0'/0'/18']03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388)#4ahsl9pk. Our new SegWit descriptor instead looks like this: wpkh([d6043800/0'/0'/5']0327dbe2d58d9ed2dbeca28cd26e18f48aa94c127fa6fb4b60e4188f6360317640)#hd66hknp".

The big thing to note is that function has changed. It was previously pkh, which is a standard P2PKH hashed public-key address. The SegWit address is instead wpkh, which means that it's a P2WPKH native SegWit address. This underlines the :fire: _**power of descriptors**_. They describe how to create an address from a key or other information, with the functions unambiguously defining how to make the address based on its type.

## Summary: Creating a SegWit Transaction

There's really no complexity to creating SegWit transactions. Internally, they're structured differently from legacy transactions, but from the command line there's no difference: you just use an address with a different prefix. The only thing to watch for is that some people may not be able to send to a Bech32 address if they're using obsolete software.

> :fire: _**What's the power of sending coins with SegWit?**_ _The Advantages._ SegWit transactions are smaller, and so will be cheaper to send than legacy transactions due to lower fees. Bech32 doubles down on this advantage, and also creates addresses that are harder to foul up when transcribing — and that's pretty important, given that user error is one of the most likely ways to lose your bitcoins. _The Disadvantages._ SegWit addresses may not be supported by obsolete Bitcoin software. In particular, people may not be able to send to your Bech32 address.

## What's Next?

Advance through "bitcoin-cli" with [Chapter Five: Controlling Bitcoin Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_0_Controlling_Bitcoin_Transactions.md).

# Chapter Five: Controlling Bitcoin Transactions

Sending a transaction isn't always the end of the story. Using the RBF (replace-by-fee) and CPFP (child-pays-for-parent) protocols, a developer can continue to control the transaction after it's been sent, to improve efficiency or to recover transactions that get stuck. These methods will begin to spotlight the true power of Bitcoin.

## Objectives for This Section

After working through this chapter, a developer will be able to:

- Decide Whether RBF or CPFP Might Help a Transaction
    
- Create Replacement Transaction Using RBF
    
- Create New Transactions Using CPFP
    

Supporting objectives include the ability to:

- Understand the Mempool
    
- Understand the Difference Between RBF and CPFP
    
- Plan for the Power of RBF
    

## Table of Contents

- [Section One: Watching for Stuck Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_1_Watching_for_Stuck_Transactions.md)
    
- [Section Two: Resending a Transaction with RBF](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_2_Resending_a_Transaction_with_RBF.md)
    
- [Section Three: Funding a Transaction with CPFP](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_3_Funding_a_Transaction_with_CPFP.md)
    

# 5.1: Watching for Stuck Transactions

Sometimes a Bitcoin transaction can get stuck. Usually it's because there wasn't sufficient transaction fee, but it can also be because of a one-time network or software glitch.

## Watch Your Transactions

You should _always_ watch to ensure that your transactions go out. bitcoin-cli listtransactions will show all of your incoming and outgoing transactions, while bitcoin-cli gettransaction with a txid will show a specific transaction.

The following shows a transaction that has not been put into a block. You can tell this because it has no confirmations.

$ bitcoin-cli -named gettransaction txid=fa2ddf84a4a632586d435e10880a2921db6310dfbd6f0f8f583aa0feacb74c8e  
{  
"amount": -0.00020000,  
"fee": -0.00001000,  
"confirmations": 0,  
"trusted": true,  
"txid": "fa2ddf84a4a632586d435e10880a2921db6310dfbd6f0f8f583aa0feacb74c8e",  
"walletconflicts": [  
],  
"time": 1592953220,  
"timereceived": 1592953220,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "tb1qw508d6qejxtdg4y5r3zarvary0c5xw7kxpjzsx",  
"category": "send",  
"amount": -0.00020000,  
"vout": 0,  
"fee": -0.00001000,  
"abandoned": false  
}  
],  
"hex": "02000000014cda1f42a1bd39d8d0ff5958a804bc2bc548b71d7ceadbde53ea15aeaf1e2691000000006a473044022016a7a9f045a0f6a52129f48adb7da35c2f54a0741d6614e9d55b8a3bc3e1490a0220391e9085a3697bc790e94bb924d5310e16f23489d9c600864a32674e871f523c01210278608b54b8fb0d8379d3823d31f03a7c6ab0adffb07dd3811819fdfc34f8c132ffffffff02204e000000000000160014751e76e8199196d454941c45d1b3a323f1433bd6e8030000000000001600146c45d3afa8762086c4bd76d8a71ac7c976e1919600000000"

A transaction can be considered stuck if it stays in this state for an extended amount of time. Not too many years ago, you could be sure that every transaction would go out _eventually_. But, that's no longer the case due to the increased usage of Bitcoin. Now, if a transaction is stuck too long, it will drop out of the mempool and then be lost from the Bitcoin network.

> :book: _**What is mempool?**_ Mempool (or Memory Pool) is a pool of all unconfirmed transactions at a bitcoin node. These are the transactions that a node has received from the p2p network which are not yet included in a block. Each bitcoin node can have a slightly different set of transactions in its mempool: different transactions might have propogated to a specific node. This depends on when the node was last started and also its limits on how much it's willing to store. When a miner makes a block, he uses transactions from his mempool. Then, when a block is verified, all the miners remove the transactions it contains from their pools. As of Bitcoin 0.12, unconfirmed transactions can also expire from mempools if they're old enough, typically, 72 hours, and as of version 0.14.0 eviction time was increased to 2 weeks. Mining pools might have their own mempool-management mechanisms.

This list of all [unconfirmed transactions](https://blockchain.info/unconfirmed-transactions) might not match any individual machine's mempool, but it should (mostly) be a superset of them.

## Decide What to Do

If your transaction is stuck longer than you want, you can typically do one of four things:

**1. Wait Until it Clears.** If you sent your transaction with a low or medium fee, it should eventually go through. As shown at [Mempool Space](https://mempool.space/), those with lower fees _will_ get delayed. (Take a look at the leftmost transaction, and see how long it's been waiting and how much it paid for its fee.)

**2. Wait Until it Expires.** If you accidentally sent with no transaction fee, or if any number or other conditions are met, then your transaction might never go through. However, your coins aren't lost. As long as you don't have a wallet that purposefully resends unconfirmed transactions, it should clear from the mempool in three days or so, and then you can try again.

**3. Use RBF as the Sender.** If you are the sender of the transaction, and you opted-in to RBF (Replace-By-Fee), then you can try again with a higher fee. See [§5.2: Resending a Transaction with RBF](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_2_Resending_a_Transaction_with_RBF.md).

**4. Use CPFP as the Receiver.** Alternatively, if you are the receiver of the transaction, you can use CPFP (Child-pays-for-parent) to use the unconfirmed transaction as an input to a new transaction. See [§5.3: Funding a Transaction with CPFP](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_3_Funding_a_Transaction_with_CPFP.md).

## Summary: Watching for Stuck Transactions

This is an introduction to the power of Bitcoin transactions. If you know that a transaction is stuck, then you can decide to free it up with features like RBF or CPFP.

## What's Next?

Continue "Controlling Bitcoin Transactions" with [§5.2: Resending a Transaction with RBF](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_2_Resending_a_Transaction_with_RBF.md).

# 5.2: Resending a Transaction with RBF

If your Bitcoin transaction is stuck, and you're the sender, you can resend it using RBF (replace-by-fee). However, that's not all that RBF can do: it's generally a powerful and multipurpose feature that allows Bitcoin senders to recreate transactions for a variety of reasons.

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.12.0, that reached full maturity in the Bitcoin Core wallet with Bitcoin Core v 0.14.0. Obviously, most people should be using it by now.

## Opt-In for RBF

RBF is an opt-in Bitcoin feature. Transactions are only eligible for using RBF if they've been created with a special RBF flag. This is done by setting any of the transaction's UTXO sequence numbers (which are typically set automatically), so that it's more than 0 and less than 0xffffffff-1 (4294967294).

This is accomplished simply by adding a sequence variable to your UTXO inputs:

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "sequence": 1 } ]''' outputs='''{ "'$recipient'": 0.00007658, "'$changeaddress'": 0.00000001 }''')

You should of course sign and send your transaction as usual:

$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375

Now, when you look at your transaction, you should see something new: the bip125-replaceable line, which has always been marked no before, is now marked yes:

$ bitcoin-cli -named gettransaction txid=5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375

{  
"amount": 0.00000000,  
"fee": -0.00000141,  
"confirmations": 0,  
"trusted": true,  
"txid": "5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375",  
"walletconflicts": [  
],  
"time": 1592954399,  
"timereceived": 1592954399,  
"bip125-replaceable": "yes",  
"details": [  
],  
"hex": "02000000000101fa364ad3cbdb08dd0b83aac009a42a9ed00594acd6883d2a466699996cd69d8b01000000000100000002ea1d000000000000160014d591091b8074a2375ed9985a9c4b18efecfd416501000000000000001600146c45d3afa8762086c4bd76d8a71ac7c976e1919602473044022077007dff4df9ce75430e3065c82321dca9f6bdcfd5812f8dc0daeb957d3dfd1602203a624d4e9720a06def613eeea67fbf13ce1fb6188d3b7e780ce6e40e859f275d0121038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec500000000"  
}

The bip125-replaceable flag will stay yes until the transaction receives confirmations. At that point, it is no longer replaceable.

> :book: _**Should I trust transactions with no confirmations?**_ No, never. This was true before RBF and it was true after RBF. Transactions must receive confirmations before they are trustworthy. This is especially true if a transaction is marked as bip125-replaceable, because then it can be ... replaced. :information_source: **NOTE — SEQUENCE:** This is the first use of the nSequence value in Bitcoin. You can set it between 1 and 0xffffffff-2 (4294967293) and enable RBF, but if you're not careful you can run up against the parallel use of nSequence for relative timelocks. We suggest always setting it to "1", which is what Bitcoin Core does, but the other option is to set it to a value between 0xf0000000 (4026531840) and 0xffffffff-2 (4294967293). Setting it to "1" effectively makes relative timelocks irrelevent and setting it to 0xf0000000 or higher deactivates them. This is all explained further in [§11.3: Using CSV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md). For now, just choose one of the non-conflicting values for nSequence.

### Optional: Always Opt-In for RBF

If you prefer, you can _always_ opt in for RBF. Do so by running your bitcoind with the -walletrbf command. Once you've done this (and restarted your bitcoind), then all UTXOs should have a lower sequence number and the transaction should be marked as bip125-replaceable.

> :warning: **VERSION WARNING:** The walletrbf flag require Bitcoin Core v.0.14.0.

## Understand How RBF Works

The RBF functionality is based on [BIP 125](https://github.com/bitcoin/bips/blob/master/bip-0125.mediawiki), which lists the following rules for using RBF:

1. The original transactions signal replaceability explicitly or through inheritance as described in the above Summary section.
    

This means that the sequence number must be set to less than 0xffffffff-1. (4294967294), or the same is true of unconfirmed parent transactions.

1. The replacement transaction pays an absolute higher fee than the sum paid by the original transactions.
    
2. The replacement transaction does not contain any new unconfirmed inputs that did not previously appear in the mempool. (Unconfirmed inputs are inputs spending outputs from currently unconfirmed transactions.)
    
3. The replacement transaction must pay for its own bandwidth in addition to the amount paid by the original transactions at or above the rate set by the node's minimum relay fee setting. For example, if the minimum relay fee is 1 satoshi/byte and the replacement transaction is 500 bytes total, then the replacement must pay a fee at least 500 satoshis higher than the sum of the originals.
    
4. The number of original transactions to be replaced and their descendant transactions which will be evicted from the mempool must not exceed a total of 100 transactions.
    

> :book: _**What is a BIP?**_ A BIP is a Bitcoin Improvement Proposal. It's an in-depth suggestion for a change to the Bitcoin Core code. Often, when a BIP has been sufficiently discussed and updated, it will become an actual part of the Bitcoin Core code. For example, BIP 125 was implemented in Bitcoin Core 0.12.0.

The other thing to understand about RBF is that in order to use it, you must double-spend, reusing one or more the same UTXOs. Just sending another transaction with a different UTXO to the same recipient won't do the trick (and will likely result in your losing money). Instead, you must purposefully create a conflict, where the same UTXO is used in two different transactions.

Faced with this conflict, the miners will know to use the one with the higher fee, and they'll be incentivized to do so by that higher fee.

> :book: _**What is a double-spend?**_ A double-spend occurs when someone sends the same electronic funds to two different people (or, to the same person twice, in two different transactions). This is a central problem for any e-cash system. It's solved in Bitcoin by the immutable ledger: once a transaction is sufficiently confirmed, no miners will verify transactions that reuse the same UTXO. However, it's possible to double-spend _before_ a transaction has been confirmed — which is why you always want one or more confirmations before you finalize a transaction. In the case of RBF, you purposefully double-spend because an initial transaction has stalled, and the miners accept your double-spend if you meet the specific criteria laid out by BIP 125. :warning: **WARNING:** Some early discussions of this policy suggested that the nSequence number also be increased. This in fact was the intended use of nSequence in its original form. This is _not_ a part of the published policy in BIP 125. In fact, increasing your sequence number can accidentally lock your transaction with a relative timelock, unless you use sequence numbers in the range of 0xf0000000 (4026531840) to 0xffffffff-2 (4294967293).

## Replace a Transaction the Hard Way: By Hand

In order to create an RBF transaction by hand, all you have to do is create a raw transaction that: (1) replaces a previous raw transaction that opted-in to RBF and that is not confirmed; (2) reuses one or more of the same UTXOs; (3) increases fees; and (4) pays the minimum bandwidth of both transactions [which already may be taken care of by (3)].

The following example just reuses our existing variables, but decreases the amount sent to the change address, to increase the fee from the accidental 0 BTC of the original transaction to an overly generous 0.01 BTC in the new transaction:

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "sequence": 1 } ]''' outputs='''{ "'$recipient'": 0.000075, "'$changeaddress'": 0.00000001 }''')

We of course must re-sign it and resend it:

$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b

You can now look at your original transaction and see that it has walletconflicts:

$ bitcoin-cli -named gettransaction txid=5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375  
{  
"amount": 0.00000000,  
"fee": -0.00000141,  
"confirmations": 0,  
"trusted": false,  
"txid": "5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375",  
"walletconflicts": [  
"c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b"  
],  
"time": 1592954399,  
"timereceived": 1592954399,  
"bip125-replaceable": "yes",  
"details": [  
],  
"hex": "02000000000101fa364ad3cbdb08dd0b83aac009a42a9ed00594acd6883d2a466699996cd69d8b01000000000100000002ea1d000000000000160014d591091b8074a2375ed9985a9c4b18efecfd416501000000000000001600146c45d3afa8762086c4bd76d8a71ac7c976e1919602473044022077007dff4df9ce75430e3065c82321dca9f6bdcfd5812f8dc0daeb957d3dfd1602203a624d4e9720a06def613eeea67fbf13ce1fb6188d3b7e780ce6e40e859f275d0121038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec500000000"  
}

This represents the fact that two different transactions are both trying to use the same UTXO.

Eventually, the transaction with the larger fee should be accepted:

$ bitcoin-cli -named gettransaction txid=c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b  
{  
"amount": 0.00000000,  
"fee": -0.00000299,  
"confirmations": 2,  
"blockhash": "0000000000000055ac4b6578d7ffb83b0eccef383ca74500b00f59ddfaa1acab",  
"blockheight": 1773266,  
"blockindex": 9,  
"blocktime": 1592955002,  
"txid": "c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b",  
"walletconflicts": [  
"5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375"  
],  
"time": 1592954467,  
"timereceived": 1592954467,  
"bip125-replaceable": "no",  
"details": [  
],  
"hex": "02000000000101fa364ad3cbdb08dd0b83aac009a42a9ed00594acd6883d2a466699996cd69d8b010000000001000000024c1d000000000000160014d591091b8074a2375ed9985a9c4b18efecfd416501000000000000001600146c45d3afa8762086c4bd76d8a71ac7c976e1919602473044022077dcdd98d85f6247450185c2b918a0f434d9b2e647330d741944ecae60d6ff790220424f85628cebe0ffe9fa11029b8240d08bdbfcc0c11f799483e63b437841b1cd0121038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec500000000"  
}

Meanwhile, the original transaction with the lower fee starts picking up negative confirmations, to show its divergence from the blockchain:

$ bitcoin-cli -named gettransaction txid=5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375  
{  
"amount": 0.00000000,  
"fee": -0.00000141,  
"confirmations": -2,  
"trusted": false,  
"txid": "5b953a0bdfae0d11d20d195ea43ab7c31a5471d2385c258394f3bb9bb3089375",  
"walletconflicts": [  
"c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b"  
],  
"time": 1592954399,  
"timereceived": 1592954399,  
"bip125-replaceable": "yes",  
"details": [  
],  
"hex": "02000000000101fa364ad3cbdb08dd0b83aac009a42a9ed00594acd6883d2a466699996cd69d8b01000000000100000002ea1d000000000000160014d591091b8074a2375ed9985a9c4b18efecfd416501000000000000001600146c45d3afa8762086c4bd76d8a71ac7c976e1919602473044022077007dff4df9ce75430e3065c82321dca9f6bdcfd5812f8dc0daeb957d3dfd1602203a624d4e9720a06def613eeea67fbf13ce1fb6188d3b7e780ce6e40e859f275d0121038a2702938e548eaec28feb92c7e4722042cfd1ea16bec9fc274640dc5be05ec500000000"  
}

Our recipients have their money, and the original, failed transaction will eventually fall out of the mempool.

## Replace a Transaction the Easy Way: By bumpfee

Raw transactions are very powerful, and you can do a lot of interesting things by combining them with RBF. However, sometimes _all_ you want to do is free up a transaction that's been hanging. You can now do that with a simple command, bumpfee.

For example, to increase the fee of transaction 4460175e8276d5a1935f6136e36868a0a3561532d44ddffb09b7cb878f76f927 you would run:

$ bitcoin-cli -named bumpfee txid=4460175e8276d5a1935f6136e36868a0a3561532d44ddffb09b7cb878f76f927  
{  
"txid": "75208c5c8cbd83081a0085cd050fc7a4064d87c7d73176ad9a7e3aee5e70095f",  
"origfee": 0.00000000,  
"fee": 0.00022600,  
"errors": [  
]  
}

The result is the automatic generation of a new transaction that has a fee determined by your bitcoin.conf file:

$ bitcoin-cli -named gettransaction txid=75208c5c8cbd83081a0085cd050fc7a4064d87c7d73176ad9a7e3aee5e70095f  
{  
"amount": -0.10000000,  
"fee": -0.00022600,  
"confirmations": 0,  
"trusted": false,  
"txid": "75208c5c8cbd83081a0085cd050fc7a4064d87c7d73176ad9a7e3aee5e70095f",  
"walletconflicts": [  
"4460175e8276d5a1935f6136e36868a0a3561532d44ddffb09b7cb878f76f927"  
],  
"time": 1491605676,  
"timereceived": 1491605676,  
"bip125-replaceable": "yes",  
"replaces_txid": "4460175e8276d5a1935f6136e36868a0a3561532d44ddffb09b7cb878f76f927",  
"details": [  
{  
"account": "",  
"address": "n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi",  
"category": "send",  
"amount": -0.10000000,  
"vout": 0,  
"fee": -0.00022600,  
"abandoned": false  
}  
],  
"hex": "02000000014e843e22cb8ee522fbf4d8a0967a733685d2ad92697e63f52ce41bec8f7c8ac0020000006b48304502210094e54afafce093008172768d205d99ee2e9681b498326c077f0b6a845d9bbef702206d90256d5a2edee3cab1017b9b1c30b302530b0dd568e4af6f2d35380bbfaa280121029f39b2a19943fadbceb6697dbc859d4a53fcd3f9a8d2c8d523df2037e7c32a71010000000280969800000000001976a914e7c1345fc8f87c68170b3aa798a956c2fe6a9eff88ac38f25c05000000001976a914c101d8c34de7b8d83b3f8d75416ffaea871d664988ac00000000"  
}

> :warning: **VERSION WARNING:** The bumpfee RPC requires Bitcoin Core v.0.14.0.

## Summary: Resending a Transaction with RBF

If a transaction is stuck, and you don't want to wait for it to expire entirely, if you opted-in to RBF, then you can double-spend using RBF to create a replacement transaction (or just use bumpfee).

> :fire: _**What is the power of RBF?**_ Obviously, RBF is very helpful if you created a transaction with too low of a fee and you need to get those funds through. However, the ability to generally replace unconfirmed transactions with updated ones has more power than just that (and is why you might want to continue using RBF with raw transactions, even following the advent of bumpfee). For example, you might send a transaction, and then before it's confirmed, combine it with a second transaction. This allows you to compress multiple transactions down into a single one, decreasing overall fees. It might also offer benefits to privacy. There are other reasons to use RBF too, for smart contracts or transaction cut-throughs, as described in the [Opt-in RBF FAQ](https://bitcoincore.org/en/faq/optin_rbf/).

## What's Next?

Continue "Controlling Bitcoin Transactions" with [§5.3: Funding a Transaction with CPFP](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_3_Funding_a_Transaction_with_CPFP.md).

# 5.3: Funding a Transaction with CPFP

If your Bitcoin transaction is stuck, and you're the _recipient_, you can clear it using CPFP (child-pays-for-parent). This is alternative to the _sender's_ ability to do so with RBF.

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.13.0, which again means that most people should be using it by now.

## Understand How CPFP Works

RBF was all about the sender. He messed up and needed to increase the fee, or he wanted to be smart and combine transactions for a variety of reasons. It was a powerful sender-oriented feature. In some ways, CPFP is RBF's opposite, because it empowers the recipient who knows that his money hasn't arrived yet and wants to speed it up. However, it's also a much simpler feature, with less wide applicability.

Basically, the idea of CPFP is that a recipient has a transaction that hasn't been confirmed in a block that he wants to spend. So, he includes that unconfirmed transaction in a new transaction and pays a high-enough fee to encourage a miner to include both the original (parent) transaction and the new (child) transaction in a block. As a result, the parent and child transactions clear simultaneously.

It should be noted that CPFP is not a new protocol feature, like RBF. It's just a new incentivization scheme that can be used for transaction selection by miners. This also means that it's not as reliable as a protocol change like RBF: there might be reasons that the child is not selected to be put into a block, and that will prevent the parent from ever being put into a block.

## Spend Unconfirmed UTXOs

Funding a transaction with CPFP is a very simple process using the methods you're already familiar with:

1. Find the txid and vout of the unconfirmed transaction. This may be the trickiest part, as bitcoin-cli generally tries to protect you from unconfirmed transactions. The sender might be able to send you this info; even with just the txid, you should be able to figure out the vout in a blockchain explorer.
    

You do have one other option: use bitcoin-cli getrawmempool, which can be used to list the contents of your entire mempool, where the unconfirmed transactions will be. You may have to dig through several if the mempool is particularly busy. You can then get more information on a specific transaction with bitcoin-cli getrawtransaction with the verbose flag set to true:

$ bitcoin-cli getrawmempool  
[  
"95d51e813daeb9a861b2dcdddf1da8c198d06452bbbecfd827447881ff79e061"  
]

$ bitcoin-cli getrawtransaction 95d51e813daeb9a861b2dcdddf1da8c198d06452bbbecfd827447881ff79e061 true  
{  
"txid": "95d51e813daeb9a861b2dcdddf1da8c198d06452bbbecfd827447881ff79e061",  
"hash": "9729e47b8aee776112a82cec46df7638d112ca51856c53e238a9b1f7af3be4ce",  
"version": 2,  
"size": 247,  
"vsize": 166,  
"weight": 661,  
"locktime": 1773277,  
"vin": [  
{  
"txid": "7a0178472300247d423ac4a04ff9165fa5b944104f6d6f9ebc557c6d207e7524",  
"vout": 0,  
"scriptSig": {  
"asm": "0014334f3a112df0f22e743ad97eec8195a00faa59a0",  
"hex": "160014334f3a112df0f22e743ad97eec8195a00faa59a0"  
},  
"txinwitness": [  
"304402207966aa87db340841d76d3c3596d8b4858e02aed1c02d87098dcedbc60721d8940220218aac9d728c9a485820b074804a8c5936fa3145ce68e24dcf477024b19e88ae01",  
"03574b1328a5dc2d648498fc12523cdf708efd091c28722a422d122f8a0db8daa9"  
],  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01000000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 f079f77f2ef0ef1187093379d128ec28d0b4bf76 OP_EQUAL",  
"hex": "a914f079f77f2ef0ef1187093379d128ec28d0b4bf7687",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2NFAkGiwnp8wvCodRBx3smJwxncuG3hndn5"  
]  
}  
},  
{  
"value": 0.02598722,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_HASH160 8799be12fb9eae6644659d95b9602ddfbb4b2aff OP_EQUAL",  
"hex": "a9148799be12fb9eae6644659d95b9602ddfbb4b2aff87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N5cDPPuCTtYq13oXw8RfpY9dHJW8sL64U2"  
]  
}  
}  
],  
"hex": "0200000000010124757e206d7c55bc9e6f6d4f1044b9a55f16f94fa0c43a427d2400234778017a0000000017160014334f3a112df0f22e743ad97eec8195a00faa59a0feffffff0240420f000000000017a914f079f77f2ef0ef1187093379d128ec28d0b4bf768742a727000000000017a9148799be12fb9eae6644659d95b9602ddfbb4b2aff870247304402207966aa87db340841d76d3c3596d8b4858e02aed1c02d87098dcedbc60721d8940220218aac9d728c9a485820b074804a8c5936fa3145ce68e24dcf477024b19e88ae012103574b1328a5dc2d648498fc12523cdf708efd091c28722a422d122f8a0db8daa9dd0e1b00"  
}

Look through the vout array. Find the object that matches your address. (Here, it's the only one.) The n value is your vout. You now have everything you need to create a new CPFP transaction.

$ utxo_txid=95d51e813daeb9a861b2dcdddf1da8c198d06452bbbecfd827447881ff79e061  
$ utxo_vout=0  
$ recipient2=$(bitcoin-cli getrawchangeaddress)

1. Create a raw transaction using your unconfirmed transaction as an input.
    
2. Double the transaction fees (or more).
    

When you take these steps, everything should look totally normal, despite the fact that you're working with an unconfirmed transaction. To verify that all was well, we even looked at the results of our signature before we saved off the information to a variable:

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient2'": 0.03597 }''')

$ bitcoin-cli -named signrawtransaction hexstring=$rawtxhex | jq -r '.hex'  
02000000012b137ef780666ba214842ff6ea2c3a0b36711bcaba839c3710f763e3d9687fed000000006a473044022003ca1f6797d781ef121ba7c2d1d41d763a815e9dad52aa8bc5ea61e4d521f68e022036b992e8e6bf2c44748219ca6e0056a88e8250f6fd0794dc69f79a2e8993671601210317b163ab8c8862e09c71767112b828abd3852e315441893fa0f535de4fa39b8dffffffff01905abd07000000001976a91450b1d90a130c4f3f1e5fbfa7320fd36b7265db0488ac00000000

$ signedtx=$(bitcoin-cli -named signrawtransaction hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
6a184a2f07fa30189f4831d6f041d52653a103b3883d2bec2f79187331fd7f0e

1. Crossing your fingers is not needed. You have verified your data is correct. From this point on, things are out of your hands.
    

Your transactions may go through quickly. They may not. It all depends on whether the miners who are randomly generating the current blocks have the CPFP patch or not. But you've given your transactions the best chance.

That's really all there is to it.

### Be Aware of Nuances

Though CPFP is usually described as being about a recipient using a new transaction to pay for an old one that hasn't been confirmed, there's nuance to this.

A _sender_ could use CPFP to free up a transaction if he received change from it. He would just use that change as his input, and the resultant use of CPFP would free up the entire transaction. Mind you, he'd do better to use RBF as long as it was enabled, as the total fees would then be lower.

A _recipient_ could use CPFP even if he wasn't planning on immediately spending the money, for example if he's worried that the funds may not be resent if the transaction expires. In this case, he just creates a child transaction that sends all the money (minus a transaction fee) to a change address. That's what we did in our example, above.

## Summary: Funding a Transaction with CPFP

You can take advantage of the CPFP incentives to free up funds that have been sent to you but have not been confirmed. Just use the unconfirmed transaction as UTXO and pay a higher-than-average transaction fee.

> :fire: _**What is the power of CPFP?**_ Mostly, CPFP is just useful to get funds unstuck when you're the recipient and the sender isn't being helpful for whatever reason. It doesn't have the more powerful possibilities of RBF, but is an alternatve way to exert control over a transaction after it's been placed in the mempool, but before it's confirmed in a block.

## What's Next?

Advance through "bitcoin-cli" with [Chapter Six: Expanding Bitcoin Transactions with Multisigs](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_0_Expanding_Bitcoin_Transactions_Multisigs.md).

# Chapter Six: Expanding Bitcoin Transactions with Multisigs

Basic bitcoin transactions: (1) send funds; (2) to a single P2PKH or SegWit recipient; (3) from a single machine; (4) immediately. However, all four parts of this definition can be expanded using more complex Bitcoin transactions. This first chapter on "Expansion" shows how to vary points (2) and (3) by sending money to an address that represents multiple recipients (or at least, multiple signers).

## Objectives for This Section

After working through this chapter, a developer will be able to:

- Create Multisignature Bitcoin Addresses Using Bitcoin Fundamentals
    
- Create Multisignature Bitcoin Addresses Using Easier Mechanisms
    

Supporting objectives include the ability to:

- Understand How to Spend Funds Sent to a Multisignature
    
- Plan for the Power of Multisignatures
    

## Table of Contents

- [Section One: Sending a Transaction with a Multsig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md)
    
- [Section Two: Spending a Transaction with a Multsig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_2_Spending_a_Transaction_to_a_Multisig.md)
    
- [Section Three: Sending & Spending an Automated Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_3_Sending_an_Automated_Multisig.md)
    

# 6.1: Sending a Transaction with a Multisig

The first way to vary how you send a basic transaction is to use a multisig. This gives you the ability to require that multiple people (or at least multiple private keys) authorize the use of funds.

## Understand How Multisigs Work

In a typical P2PKH or SegWit transaction, bitcoins are sent to an address based on your public key, which in turn means that the related private key is required to unlock the transaction, solving the cryptographic puzzle and allowing you to reuse the funds. But what if you could instead lock a transaction with _multiple_ private keys? This would effectively allow funds to be sent to a group of people, where those people all have to agree to reuse the funds.

> :book: _**What is a multisignature?**_ A multisignature is a methodology that allows more than one person to jointly create a digital signature. It's a general technique for the cryptographic use of keys that goes far beyond Bitcoin.

Technically, a multisignature cryptographic puzzle is created by Bitcoin using the OP_CHECKMULTISIG command, and typically that's encapsulated in a P2SH address. [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md) will detail how that works more precisely. For now, all you need to know is that you can use bitcoin-cli command to create multisignature addresses; funds can be sent to these addresses just like any normal P2PKH or Segwit address, but multiple private keys will be required for the redemption of the funds.

> :book: _**What is a multisignature transaction?**_ A multisignature transaction is a Bitcoin transaction that has been sent to a multisignature address, thus requiring the signatures of certain people from the multisignature group to reuse the funds.

Simple multisignatures require everyone in the group to sign the UTXO when it's spent. However, there's more complexity possible. Multisignatures are generally described as being "m of n". That means that the transaction is locked with a group of "n" keys, but only "m" of them are required to unlock the transaction.

> :book: _**What is a m-of-n multisignature?**_ In a multisignature, "m" signatures out of a group of "n" are required to form the signature, where "m ≤ n".

## Create a Multisig Address

In order to lock a UTXO with multiple private keys, you must first create a multisignature address. The examples used here show the creation (and usage) of a 2-of-2 multisignature.

### Create the Addresses

To create a multisignature address, you must first ready the addresses that the multisig will combine. Best practice suggests that you always create new addresses. This means that the participants will each run the getnewaddress command on their own machine:

machine1$ address1=$(bitcoin-cli getnewaddress)

And:

machine2$ address2=$(bitcoin-cli getnewaddress)

Afterwards, one of the recipients (or perhaps some third party) will need to combine the addresses.

#### Collect Public Keys

However, you can't create a multi-sig with the addresses, as those are the hashes of public keys: you instead need the public keys themselves.

This information is readily available with the getaddressinfo command.

Over on the remote machine, which we assume here is machine2, you can get the information out of the listing.

machine2$ bitcoin-cli -named getaddressinfo address=$address2  
{  
"address": "tb1qr2tkjh8rs9xn5xaktf5phct0wxqufplawrfd9q",  
"scriptPubKey": "00141a97695ce3814d3a1bb65a681be16f7181c487fd",  
"ismine": true,  
"solvable": true,  
"desc": "wpkh([fe6f2292/0'/0'/1']02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3)#zc64l8dw",  
"iswatchonly": false,  
"isscript": false,  
"iswitness": true,  
"witness_version": 0,  
"witness_program": "1a97695ce3814d3a1bb65a681be16f7181c487fd",  
"pubkey": "02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3",  
"ischange": false,  
"timestamp": 1592957904,  
"hdkeypath": "m/0'/0'/1'",  
"hdseedid": "1dc70547f2b80e9bb5fde5f34fb3d85f8d8d1dab",  
"hdmasterfingerprint": "fe6f2292",  
"labels": [  
""  
]  
}

The pubkey address (02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3) is what's required. Copy it over to your local machine by whatever means you find most efficient and _least error prone_.

This process needs to be undertaken for _every_ address from a machine other than the one where the multisig is being built. Obviously, if some third-party is creating the address, then you'll need to do this for every address.

> :warning: **WARNING:** Bitcoin's use of public-key hashes as addresses, instead of public keys, actually represents an additional layer of security. Thus, sending a public key slightly increases the vulnerability of the associated address, for some far-future possibility of a compromise of the elliptic curve. You shouldn't worry about having to occasionally send out a public key for a usage such as this, but you should be aware that the public-key hashes represent security, and so the actual public keys should not be sent around willy nilly.

If one of the addresses was created on your local machine, which we assume here is machine1, you can just dump the pubkey address into a new variable.

machine1$ pubkey1=$(bitcoin-cli -named getaddressinfo address=$address1 | jq -r '.pubkey')

### Create the Address

A multisig can now be created with the createmultisig command:

machine1$ bitcoin-cli -named createmultisig nrequired=2 keys='''["'$pubkey1'","02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3"]'''  
{  
"address": "2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr",  
"redeemScript": "522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae",  
"descriptor": "sh(multi(2,02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191,02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3))#0pazcr4y"  
}

> :warning: **VERSION WARNING:** Some versions of createmultisig have allowed entry of public keys or addresses, some have required public keys only. Currently, either one seems to be allowed.

When creating the multisignature address, you list how many signatures are required with the nrequired argument (that's "m" in a "m-of-n" multisignature), then you list the total set of possible signatures with the keys argument (that's "n"). Note that the the keys entries likely came from different places. In this case, we included $pubkey1 from the local machine and 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 from a remote machine.

> :information_source: **NOTE — M-OF-N VS N-OF-N:** This example shows the creation of a simple 2-of-2 multisig. If you instead want to create an m-of-n signature where "m < n", you adjust the nrequired field and/or the number of signatures in the keys JSON object. For a 1-of-2 multisig, you'd set nrequired=1 and also list two keys, while for a 2-of-3 multisig, you'd leave nrequired=2, but add one more public key to the keys listing.

When used correctly, createmultisig returns three results, all of which are critically important.

The _address_ is what you'll give out to people who want to send funds. You'll notice that it has a new prefix of 2, exactly like those P2SH-SegWit addresses. That's because, like them, createmultisig is actually creating a totally new type of address called a P2SH address. It works exactly like a standard P2PKH address for sending funds, but since this one has been built to require multiple addresses, you'll need to do a little more work to spend them.

> :link: **TESTNET vs MAINNET:** On testnet, the prefix for P2SH addresses is 2, while on mainnet, it's 3.

The _redeemScript_ is what you need to redeem the funds (along with the private keys for "m" of the "n" addresses). This script is another special feature of P2SH addresses and will be fully explained in [§10.3: Running a Bitcoin Script with P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_3_Running_a_Bitcoin_Script_with_P2SH.md). For now, just be aware that it's a bit of data that's required to get your money.

The _descriptor_ is the standardized description for an address that we met in [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md). It provides one way that you could import this address back to the other machine, using the importmulti RPC.

> :book: _**What is a P2SH address?**_ P2SH stands for Pay-to-script-hash. It's a different type of recipient than a standard P2PKH address or even a Bech32, used for funds whose redemption are based on more complex Bitcoin Scripts. bitcoin-cli uses P2SH encapsulation to help standardize and simplify its multisigs as "P2SH multisigs", just like P2SH-SegWit was using P2SH to standardize its SegWit addresses and make them fully backward compatible. :warning: **WARNING:** P2SH multisig addresses, like the ones created by bitcoin-cli, have a limit for "m" and "n" in multisigs based on the maximum size of the redeem script, which is currently 520 bytes. Practically, you won't hit this unless you're doing something excessive.

### Save Your Work

Here's an important caveat: nothing about your multisig is saved into your wallet using these basic techniques. In order to later redeem money sent to this multisignature address, you're going to need to retain two crucial bits of information:

- A list of the Bitcoin addresses used in the multisig.
    
- The redeemScript output by createmultsig.
    

Technically, the redeemScript can be recreated by rerunning createmultisig with the complete list of public keys _in the same order_ and with the right m-of-n count. But, it's better to hold onto it and save yourself stress and grief.

### Watch the Order

Here's one thing to be very wary of: _order matters_. The order of keys used to create a multi-sig creates a unique hash, which is to say if you put the keys in a different order, they'll produce a different address, as shown:

$ bitcoin-cli -named createmultisig nrequired=2 keys='''["'$pubkey1'","'$pubkey2'"]'''  
{  
"address": "2NFBQvz57UzKWDr2Vx5D667epVZifjGixkm",  
"redeemScript": "52210342b306e410283065ffed38c3139a9bb8805b9f9fa6c16386e7ea96b1ba54da0321039cd6842869c1bfec13cfdbb7d8285bc4c501d413e6633e3ff75d9f13424d99b352ae",  
"descriptor": "sh(multi(2,0342b306e410283065ffed38c3139a9bb8805b9f9fa6c16386e7ea96b1ba54da03,039cd6842869c1bfec13cfdbb7d8285bc4c501d413e6633e3ff75d9f13424d99b3))#8l6hvjsk"  
}  
standup@btctest20:~$ bitcoin-cli -named createmultisig nrequired=2 keys='''["'$pubkey2'","'$pubkey1'"]'''  
{  
"address": "2N5bC4Yc5Pqept1y8nPRqvWmFSejkVeRb1k",  
"redeemScript": "5221039cd6842869c1bfec13cfdbb7d8285bc4c501d413e6633e3ff75d9f13424d99b3210342b306e410283065ffed38c3139a9bb8805b9f9fa6c16386e7ea96b1ba54da0352ae",  
"descriptor": "sh(multi(2,039cd6842869c1bfec13cfdbb7d8285bc4c501d413e6633e3ff75d9f13424d99b3,0342b306e410283065ffed38c3139a9bb8805b9f9fa6c16386e7ea96b1ba54da03))#audl88kg"  
}

More notably, each ordering creates a different _redeemScript_. That means that if you used these basic techniques and failed to save the redeemScript as you were instructed, you'll have to walk through an ever-increasing number of variations to find the right one when you try and spend your funds!

[BIP67](https://github.com/bitcoin/bips/blob/master/bip-0067.mediawiki) suggests a way to lexicographically order keys, so that they always generate the same multisignatures. ColdCard and Electrum are among the wallets that already support this. Of course, this can cause troubles on its own if you don't know if a multisig address was created with sorted or unsorted keys. Once more, [descriptors](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md) come to the rescue. If a multisig is unsorted, it's built with the function multi and if it's sorted it's built with the function sortedmulti.

If you look at the descriptor for the multisig that you created above, you'll see that Bitcoin Core doesn't currently sort its multisigs:

"descriptor": "sh(multi(2,02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191,02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3))#0pazcr4y"

However, if it imports an address with type sortedmulti, it'll do the right thing, which is the whole point of descriptors!

> :warning: **VERSION WARNING:** Bitcoin Core only understands the sortedmulti descriptor function beginning with v 0.20.0. Try and access the descriptor on an earlier version of Bitcoin Core and you'll get an error such as A function is needed within P2WSH.

## Send to a Multisig Address

If you've got a multisignature in a convenient P2SH format, like the one generated by bitcoin-cli, it can be sent to exactly like a normal address.

$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ recipient="2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr"

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.000065}''')  
$ bitcoin-cli -named decoderawtransaction hexstring=$rawtxhex  
{  
"txid": "b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521",  
"hash": "b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521",  
"version": 2,  
"size": 83,  
"vsize": 83,  
"weight": 332,  
"locktime": 0,  
"vin": [  
{  
"txid": "c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00006500,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL",  
"hex": "a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr"  
]  
}  
}  
]  
}

$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521

As you can see, there was nothing unusual in the creation of the transaction, and it looked entirely normal, albeit with an address with a different prefix than normal (2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr). No surprise, as we similarly saw no difference when we sent to Bech32 addresses for the first time in [§4.6](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_6_Creating_a_Segwit_Transaction.md).

## Summary: Sending a Transaction with a Multisig

Multisig addresses lock funds to multiple private keys — possibly requiring all of those private keys for redemption, and possibly requiring just some from the set. They're easy enough to create with bitcoin-cli and they're entirely normal to send to. This ease is due in large part to the invisible use of P2SH (pay-to-script-hash) addresses, a large topic that we've touched upon twice now, with P2SH-SegWit and multisig addresses, and one that will get more coverage in the future.

> :fire: _**What is the power of multisignatures?**_ Multisignatures allow the modeling of a variety of financial arrangements such as corporations, partnerships, committees, and other groups. A 1-of-2 multisig might be a married couple's joint bank account, while a 2-of-2 multisig might be used for large expenditures by a Limited Liability Partnership. Multisignatures also form one of the bases of Smart Contracts. For example, a real estate deal could be closed with a 2-of-3 multisig, where the signatures are submitted by the buyer, the seller, and a licensed escrow agent. Once the escrow agent agrees that all of the conditions have been met, he frees up the funds for the seller; or alternatively, the buyer and seller can jointly free the funds.

## What's Next?

Continue "Expanding Bitcoin Transactions" with [§6.2: Spending a Transaction with a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_2_Spending_a_Transaction_to_a_Multisig.md).

# 6.2: Spending a Transaction with a Multisig

The classic, and complex, way of spending funds sent to a multisignature address using bitcoin-cli requires that you do a lot of foot work.

## Find Your Funds

To start with, you need to find your funds; your computer doesn't know to look for them, because they're not associated with any addresses in your wallet. You can alert bitcoind to do so using the importaddress command:

$ bitcoin-cli -named importaddress address=2NAGfA4nW6nrZkD5je8tSiAcYB9xL2xYMCz

If you've got a pruned node (and you probably do), you'll instead need to tell it not to rescan:

$ bitcoin-cli -named importaddress address=2NAGfA4nW6nrZkD5je8tSiAcYB9xL2xYMCz rescan="false"

If you prefer, you can import the address using its descriptor (and this is generally the better, more standardized answer):

$ bitcoin-cli importmulti '[{"desc": "sh(multi(2,02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191,02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3))#0pazcr4y", "timestamp": "now", "watchonly": true}]'  
[  
{  
"success": true  
}  
]

Afterward the funds should show up when you listunspent ... but they still aren't easily spendable. (In fact, your wallet may claim they're not spendable at all!)

If for some reason you're not able to incorporate the address into your wallet, you can use gettransaction to get info instead (or look at a block explorer).

$ bitcoin-cli -named gettransaction txid=b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521 verbose=true  
{  
"amount": -0.00006500,  
"fee": -0.00001000,  
"confirmations": 3,  
"blockhash": "0000000000000165b5f602920088a7e36b11214161d6aaebf5229e3ed4f10adc",  
"blockheight": 1773282,  
"blockindex": 9,  
"blocktime": 1592959320,  
"txid": "b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521",  
"walletconflicts": [  
],  
"time": 1592958753,  
"timereceived": 1592958753,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr",  
"category": "send",  
"amount": -0.00006500,  
"vout": 0,  
"fee": -0.00001000,  
"abandoned": false  
}  
],  
"hex": "020000000001011b95a6055174ec64b82ef05b6aefc38f34d0e57197e40281ecd8287b4260dec60000000000ffffffff01641900000000000017a914a5d106eb8ee51b23cf60d8bd98bc285695f233f38702473044022070275f81ac4129e1d167ef7e700739f2899ea4c7f1adef3a4da29436f14fb97e02207310d4ec449eba49f0fa404ae45b9c82431d883490c7a0ed882ad0b5d7a623d0012102883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb00000000",  
"decoded": {  
"txid": "b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521",  
"hash": "bdf4e3bc5d354a5dfa5528f172480976321d989d7e5806ac14f1fe9b0b1c093a",  
"version": 2,  
"size": 192,  
"vsize": 111,  
"weight": 441,  
"locktime": 0,  
"vin": [  
{  
"txid": "c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"txinwitness": [  
"3044022070275f81ac4129e1d167ef7e700739f2899ea4c7f1adef3a4da29436f14fb97e02207310d4ec449eba49f0fa404ae45b9c82431d883490c7a0ed882ad0b5d7a623d001",  
"02883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb"  
],  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00006500,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL",  
"hex": "a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr"  
]  
}  
}  
]  
}  
}

## Set Up Your Variables

When you're ready to spend the funds received by a multisignature address, you're going need to collect a _lot_ of data: much more than you need when you spend a normal P2PKH or SegWit UTXO. That's in part because the info on the multisig address isn't in your wallet, and in part because you're spending money that was sent to a P2SH (pay-to-script-hash) address, and that's a lot more demanding.

In total, you're going to need to collect three things: extended information about the UTXO; the redeemScript; and all the private keys involved. You'll of course need a new recipient address too. The private keys need to wait for the signing step, but everything else can be done now.

### Access the UTXO information

To start with, grab the txid and the vout for the transaction that you want to spend, as usual. In this case, it was retrieved from the gettransaction info, above:

$ utxo_txid=b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521  
$ utxo_vout=0

However, you need to also access a third bit of information about the UTXO, its scriptPubKey/hex, which is the script that locked the transaction. Again, you're probably doing this by looking at the details of the transaction:

$ utxo_spk=a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387

### Record the Redeem Script

Hopefully, you saved the redeemScript. Now you should record it in a variable.

This was drawn from our creation of the address in the previous section.

redeem_script="522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae"

### Decide Your Recipient

We're just going to send the money back to ourself. This is useful because it frees the funds up from the multisig, converting them into a normal P2PKH transaction that can later be confirmed by a single private key:

$ recipient=$(bitcoin-cli getrawchangeaddress)

## Create Your Transaction

You can now create your transaction. This is no different than usual.

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.00005}''')  
$ echo $rawtxhex  
020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b10000000000ffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000

## Sign Your Transaction

You're now ready to sign your transaction. This is a multi-step process because you'll need to do it on multiple machines, each of which will contribute their own private keys.

### Dump Your First Private Key

Because this transaction isn't making full use of your wallet, you're going to need to directly access your private keys. Start on machine1, where you should retrieve any of that user's private keys that were involved in the multisig:

machine1$ bitcoin-cli -named dumpprivkey address=$address1  
cNPhhGjatADfhLD5gLfrR2JZKDE99Mn26NCbERsvnr24B3PcSbtR

> :warning: **WARNING:** Directly accessing your private keys from the shell is very dangerous behavior and should be done with extreme care if you're using real money. At the least, don't save the information into a variable that could be accessed from your machine. Removing your shell's history is another great step. At the most, don't do it.

### Make Your First Signature

You can now make your first signature with the signrawtransactionwithkey command. Here's where things are different: you're going to need to coach the command on how to sign. You do these by adding the following new information:

- Include a prevtxs argument that includes the txid, the vout, the scriptPubKey, and the redeemScript that you recorded, each of them an individual key-value pair in the JSON object.
    
- Include a privkeys argument that lists the private keys you dumped on this machine.
    

machine1$ bitcoin-cli -named signrawtransactionwithkey hexstring=$rawtxhex prevtxs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "scriptPubKey": "'$utxo_spk'", "redeemScript": "'$redeem_script'" } ]''' privkeys='["cNPhhGjatADfhLD5gLfrR2JZKDE99Mn26NCbERsvnr24B3PcSbtR"]'  
{  
"hex": "020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b100000000920047304402201c97b48215f261055e41b765ab025e77a849b349698ed742b305f2c845c69b3f022013a5142ef61db1ff425fbdcdeb3ea370aaff5265eee0956cff9aa97ad9a357e3010047522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352aeffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000",  
"complete": false,  
"errors": [  
{  
"txid": "b164388854f9701051809eed166d9f6cedba92327e4296bf8a265a5da94f6521",  
"vout": 0,  
"witness": [  
],  
"scriptSig": "0047304402201c97b48215f261055e41b765ab025e77a849b349698ed742b305f2c845c69b3f022013a5142ef61db1ff425fbdcdeb3ea370aaff5265eee0956cff9aa97ad9a357e3010047522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae",  
"sequence": 4294967295,  
"error": "CHECK(MULTI)SIG failing with non-zero signature (possibly need more signatures)"  
}  
]  
}

That produces scary errors and says that it's failing. This is all fine. You can see that the signature has been partially successfully because the hex has gotten longer. Though the transaction has been partially signed, it's not done because it needs more signatures.

### Repeat for Other Signers

You can now pass the transaction on, to be signed again by anyone else required for the multisig. They do this by running the same signing command that you did but: (1) with the longer hex that you output from (bitcoin-cli -named signrawtransactionwithkey hexstring=$rawtxhex prevtxs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "scriptPubKey": "'$utxo_spk'", "redeemScript": "'$redeem_script'" } ]''' privkeys='["cMgb3KM8hPATCtgMKarKMiFesLft6eEw3DY6BB8d97fkeXeqQagw"]' | jq -r '.hex'); and (2) with their own private key.

> :information_source: **NOTE — M-OF-N VS N-OF-N:** Obviously, if you have an n-of-n signature (like the 2-of-2 multisignature in this example), then everyone has to sign, but if you hae a m-of-n multisignature where "m < n", then the signature will be complete when only some ("m") of the signers have signed.

To do so first they access their private keys:

machine2$ bitcoin-cli -named dumpprivkey address=$address2  
cVhqpKhx2jgfLUWmyR22JnichoctJCHPtPERm11a2yxnVFKWEKyz

Second, they sign the new hex using all the same prevtxs values:

machine1$ bitcoin-cli -named signrawtransactionwithkey hexstring=020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b100000000920047304402201c97b48215f261055e41b765ab025e77a849b349698ed742b305f2c845c69b3f022013a5142ef61db1ff425fbdcdeb3ea370aaff5265eee0956cff9aa97ad9a357e3010047522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352aeffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000 prevtxs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "scriptPubKey": "'$utxo_spk'", "redeemScript": "'$redeem_script'" } ]''' privkeys='["cVhqpKhx2jgfLUWmyR22JnichoctJCHPtPERm11a2yxnVFKWEKyz"]'  
{  
"hex": "020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b100000000d90047304402201c97b48215f261055e41b765ab025e77a849b349698ed742b305f2c845c69b3f022013a5142ef61db1ff425fbdcdeb3ea370aaff5265eee0956cff9aa97ad9a357e301473044022000a402ec4549a65799688dd531d7b18b03c6379416cc8c29b92011987084e9f402205470e24781509c70e2410aaa6d827aa133d6df2c578e96a496b885584fb039200147522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352aeffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000",  
"complete": true  
}

Third, they may need to send on the even longer hexstring they produce to additional signers.

But in this case, we now see that the signature is complete!

## Send Your Transaction

When done, you should fall back on the standard JQ methodology to save your hexstring and then to send it:

$ signedtx=$(bitcoin-cli -named signrawtransactionwithkey hexstring=020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b100000000920047304402201c97b48215f261055e41b765ab025e77a849b349698ed742b305f2c845c69b3f022013a5142ef61db1ff425fbdcdeb3ea370aaff5265eee0956cff9aa97ad9a357e3010047522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352aeffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000 prevtxs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "scriptPubKey": "'$utxo_spk'", "redeemScript": "'$redeem_script'" } ]''' privkeys='["cVhqpKhx2jgfLUWmyR22JnichoctJCHPtPERm11a2yxnVFKWEKyz"]' | jq -r .hex)  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
99d2b5717fed8875a1ed3b2827dd60ae3089f9caa7c7c23d47635f6f5b397c04

## Understand the Importance of This Expanded Signing Methodology

This took some work, and as you'll soon learn, the foolishness with the private keys, the redeem script, and the scriptpubkey isn't actually required to redeem from multisignature addresses using newer versions of Bitcoin Core. So, what was the point?

This redemption methodology shows a standard way to sign and reuse P2SH transactions. In short, to redeem P2SH funds, a signrawtransactionwithkey needs to:

1. Include the scriptPubKey, which explains the P2SH cryptographic puzzle.
    
2. Include the redeemScript, which solves the P2SH cryptographic puzzle, and introduces a new puzzle of its own.
    
3. Be run on each machine holding required private keys.
    
4. Include the relevant signatures, which solve the redeemScript puzzle.
    

Here, we saw this methodology used to redeem multisig funds. In the future you can also use it to redeem funds that were locked with other, more complex P2SH scripts, as explained starting in Chapter 9.

## Summary: Spending a Transaction with a Multisig

It turns out that spending money sent to a multisig address can take quite a bit of work. But as long as you have your original addresses and your redeemScript, you can do it by signing a raw transaction with each different address, and providing some more information along the way.

## What's Next?

Continue "Expanding Bitcoin Transactions" with [§6.3: Sending & Spending an Automated Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_3_Sending_an_Automated_Multisig.md).

# 6.3: Sending & Spending an Automated Multisig

The standard technique for creating multisignature addresses and for spending their funds is complex, but it's a worthwhile exercise for understanding a bit more about how they work, and how you can manipulate them at a relatively low level. However, Bitcoin Core has made multisigs a little bit easier in new releases.

> :warning: **VERSION WARNING:** The addmultisigaddress command is available in Bitcoin Core v 0.10 or higher.

## Create a Multisig Address in Your Wallet

In order to make funds sent to multisig addresses easier to spend, you just need to do some prep using the addmultisigaddress command. It's probably not what you'd want to do if you were writing multisig wallet programs, but if you were just trying to receive some funds by hand, it might save you some hair-pulling.

### Collect the Keys

You start off creating P2PKH addresses and retrieving public keys, as usual, for each user who will be part of the multisig:

machine1$ address3=$(bitcoin-cli getnewaddress)  
machine1$ echo $address3  
tb1q4ep2vmakpkkj6mflu94x5f94q662m0u5ad0t4w  
machine1$ bitcoin-cli -named getaddressinfo address=$address3 | jq -r '.pubkey'  
0297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc

machine2$ address4=$(bitcoin-cli getnewaddress)  
machine2$ echo $address4  
tb1qa9v5h6zkhq8wh0etnv3ae9cdurkh085xufl3de  
machine2$ bitcoin-cli -named getaddressinfo address=$address4 | jq -r '.pubkey'  
02a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f

### Create the Multisig Address Everywhere

Next you create the multisig on _each machine that contributes signatures_ using a new command, addmultisigaddress, instead of createmultisig. This new command saves some of the information into your wallet, making it a lot easier to spend the money afterward.

machine1$ bitcoin-cli -named addmultisigaddress nrequired=2 keys='''["'$address3'","02a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f"]'''  
{  
"address": "tb1q9as46kupwcxancdx82gw65365svlzdwmjal4uxs23t3zz3rgg3wqpqlhex",  
"redeemScript": "52210297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc2102a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f52ae",  
"descriptor": "wsh(multi(2,[d6043800/0'/0'/15']0297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc,[e9594be8]02a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f))#wxn4tdju"  
}

machine2$ bitcoin-cli -named addmultisigaddress nrequired=2 keys='''["0297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc","'$address4'"]'''  
{  
"address": "tb1q9as46kupwcxancdx82gw65365svlzdwmjal4uxs23t3zz3rgg3wqpqlhex",  
"redeemScript": "52210297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc2102a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f52ae",  
"descriptor": "wsh(multi(2,[ae42a66f]0297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc,[fe6f2292/0'/0'/2']02a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f))#cc96c5n6"  
}

As noted in the previous section, it currently doesn't matter whether you use addresses or public keys, so we've shown the other mechanism here, mixing the two. You will get the same multisig address either way. However, _you must use the same order_. Thus, it's best for the members of the multisig to check amongst themselves to make sure they all got the same result.

### Watch for Funds

Afterward, the members of the multisig will still need to run importaddress to watch for funds received on the multisig address:

machine1$ bitcoin-cli -named importaddress address=tb1q9as46kupwcxancdx82gw65365svlzdwmjal4uxs23t3zz3rgg3wqpqlhex rescan="false"

machine2$ bitcoin-cli -named importaddress address=tb1q9as46kupwcxancdx82gw65365svlzdwmjal4uxs23t3zz3rgg3wqpqlhex rescan="false"

## Respend with an Automated Transaction

Afterward, you will be able to receive funds on the multisignature address as normal. The use of addmultisigaddress is simply a bureaucratic issue on the part of the recipients: a bit of bookkeeping to make life easier for them when they want to spend their funds.

But, it makes life a lot easier. Because information was saved into the wallet, the signers will be able to respend the funds sent to the multisignature address exactly the same as any other address ... other than the need to sign on multiple machines.

You start by collecting your variables, but you no longer need to worry about scriptPubKey or redeemScript.

Here's a new transaction sent to our new multisig address:

machine1$ utxo_txid=b9f3c4756ef8159d6a66414a4317f865882ee04beb57a0f8349dafcc98f5acbc  
machine1$ utxo_vout=0  
machine1$ recipient=$(bitcoin-cli getrawchangeaddress)

You create a raw transaction:

machine1$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.00005}''')

Then you sign it:

machine1$ bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex  
{  
"hex": "02000000000101bcacf598ccaf9d34f8a057eb4be02e8865f817434a41666a9d15f86e75c4f3b90000000000ffffffff0188130000000000001600144f93c831ec739166ea425984170f4dc6bac75829040047304402205f84d40ba16ff49e60a7fc9228ef5917473aae1ab667dad01e113ca0fef3008b02201a50da2c65f38798aea94bcbd5bbf065bc1e38de44bacee69d525dcddcc11bba01004752210297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc2102a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f52ae00000000",  
"complete": false,  
"errors": [  
{  
"txid": "b9f3c4756ef8159d6a66414a4317f865882ee04beb57a0f8349dafcc98f5acbc",  
"vout": 0,  
"witness": [  
"",  
"304402205f84d40ba16ff49e60a7fc9228ef5917473aae1ab667dad01e113ca0fef3008b02201a50da2c65f38798aea94bcbd5bbf065bc1e38de44bacee69d525dcddcc11bba01",  
"",  
"52210297e681bff16cd4600138449e2527db4b2f83955c691a1b84254ecffddb9bfbfc2102a0d96e16458ff0c90db4826f86408f2cfa0e960514c0db547ff152d3e567738f52ae"  
],  
"scriptSig": "",  
"sequence": 4294967295,  
"error": "CHECK(MULTI)SIG failing with non-zero signature (possibly need more signatures)"  
}  
]  
}

Note that you no longer had to give signrawtransactionwithkey extra help, because all of that extra information was already in your wallet. Most importantly, you didn't make your private keys vulnerable by directly manipulating them. Instead the process was _exactly_ the same as respending a normal UTXO, except that the transaction wasn't fully signed at the end.

### Sign It On Other Machines

The final step is exporting the partially signed hex to any other machines and signing it again:

machine2$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=02000000014ecda61c45f488e35c613a7c4ae26335a8d7bfd0a942f026d0fb1050e744a67d000000009100473044022025decef887fe2e3eb1c4b3edaa155e5755102d1570716f1467bb0b518b777ddf022017e97f8853af8acab4853ccf502213b7ff4cc3bd9502941369905371545de28d0147522102e7356952f4bb1daf475c04b95a2f7e0d9a12cf5b5c48a25b2303783d91849ba421030186d2b55de166389aefe209f508ce1fbd79966d9ac417adef74b7c1b5e0777652aeffffffff0130e1be07000000001976a9148dfbf103e48df7d1993448aa387dc31a2ebd522d88ac00000000 | jq -r '.hex')

When everyone that's required has signed, you're off to the races:

machine2$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
3ce88839ac6165aeadcfb188c490e1b850468eff571b4ca78fac64342751510d

As with the shortcut discussed in [§4.5: Sending Coins with Automated Raw Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_5_Sending_Coins_with_Automated_Raw_Transactions.md), the result is a lot easier, but you lose some control in the process.

## Summary: Sending & Spending an Automated Multisig

There's an easier way to respend funds sent to multisig addresses that simply requires use of the addmultisigaddress command when you create your address. It doesn't demonstrate the intricacies of P2SH respending, and it doesn't give you expansive control, but if you just want to get your money, this is the way to go.

## What's Next?

Learn more about "Expanding Bitcoin Transactions" with [Chapter Seven: Expanding Bitcoin Transactions with PSBTs](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_0_Expanding_Bitcoin_Transactions_PSBTs.md).

# Chapter Seven: Expanding Bitcoin Transactions with PSBTs

The previous chapter discussed how to use multisigs to collaboratively determine consent among multiple parties. It's not the only way to collaborate in the creation of Bitcoin transactions. PSBTs are a much newer technology that allow you to collaborate at a variety of stages, including the creation, funding, and authentication of a Bitcoin transaction.

## Objectives for This Section

After working through this chapter, a developer will be able to:

- Create Transactions with PSBTs
    
- Use Command Line Tools to Complete PSBTs
    
- Use HWI to Interact with a Hardware Wallet
    

Supporting objectives include the ability to:

- Understand How PSBTs Differ from Multisignatures
    
- Understand the Full Workflow of Working with PSBTs
    
- Plan for the Power of PSBTs
    
- Understand The Use of a Hardware Wallet
    

## Table of Contents

- [Section One: Creating a Partially Signed Bitcoin Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md)
    
- [Section Two: Using a Partially Signed Bitcoin Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_2_Using_a_Partially_Signed_Bitcoin_Transaction.md)
    
- [Section Three: Integrating with Hardware Wallets](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_3_Integrating_with_Hardware_Wallets.md)
    

# 7.1: Creating a Partially Signed Bitcoin Transaction

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Partially Signed Bitcoin Transactions (PSBTs) are the newest way to vary the creation of basic Bitcoin transactions. They do so by introducing collaboration into every step of the process, allowing people (or programs) to not just authenticate transactions together (as with multisigs), but also to easily create, fund, and broadcast collaboratively.

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.17.0. Earlier versions of Bitcoin Core will not be able to work with the PSBT while it is in progress (though they will still be able to recognize the final transaction). Some updates and upgrades for PSBTs have continued through 0.20.0.

## Understand How PSBTs Work

Multisignatures were great for the very specific case of jointly holding funds and setting rules for whom among the joint signers could authenticate the use of those funds. There are many use cases, such as: a spousal joint bank account (a 1-of-2 signature); a fiduciary requirement for dual control (a 2-of-2 signature); and an escrow (a 2-of-3 signature).

> :book: _**What is a PSBT?**_ As the name suggests, a PSBT is a transaction that has not been fully signed. That's important, because once a transaction is signed, its content is locked in. [BIP174](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki) defined an abstracted methodology for putting PSBTs together that describes and standardizes roles in their collaborative creation. A _Creator_ proposes a transaction; one or more _Updaters_ supplement it; and one or more _Signers_ authenticate it; before a _Finalizer_ completes it; and an _Extracter_ turns it into a transaction for the Bitcoin network. There may also be a _Combiner_ who merges parallel PSBTs from different users.

PSBTs may initially look sort of the same as multi-sigs because they have a single overlapping bit of functionality: the ability to jointly sign a transaction. However, they were created for a totally different use case. PSBTs recognize the need for multiple programs to jointly create a transaction for a number of different reasons, and they provide a regularized format for doing so. They're especially useful for use cases involving hardware wallets (for which, see [§7.3](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/07_3_Integrating_with_Hardware_Wallets.md)), which are protected from full access to the internet and tend to have minimal transaction history.

In general, PSBTs provide a number of functional elements that improve this use case:

1. They provide a _standard_ for collaboratively creating transactions, whereas previous methodologies (including the multi-sig one from the previous chapter) were implementation dependent.
    
2. They support a _wider variety of use cases_, including simple joint funding.
    
3. They support _hardware wallets_ and other cases where a node may not have full transaction history.
    
4. They optionally allow for the combination of _non-serialized transactions_, not requiring an ever-bigger hex code to be passed from user to user.
    

PSBTs do their work by supplementing normal transaction information with a set of inputs and outputs, each of which defines everything you need to know about those UTXOs, so that even an airgapped wallet can make an informed decision about signatures. Thus, an input lists out the amount of money in a UTXO and what needs to be done to spend it, while an output does the same for the UTXOs it's creating.

This first section will outline the standard PSBT process of: Creator, Updater, Signer, Finalizer, Extractor. It'll do so from one machine, which will sort of make this look like a convoluted way to create a raw transaction. But, have faith, there's a purpose to this! [§7.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_2_Using_a_Partially_Signed_Bitcoin_Transaction.md) and [§7.3](file:///../07_3_Integrating_with_Hardware_Wallets.md) will show some real-life examples of using PSBTs and will turn this simple system into a collaborative process shared between multiple machines that has real effects and creates real opportunities.

## Create a PSBT the Old-Fashioned Way

#### PSBT Role: Creator

The easiest way to create a PSBT is to take an existing transaction and use converttopsbt to turn it into a PSBT. This is certainly not the _best_ way since it requires you to make a transaction for one format (a raw transaction) then convert it to another (PSBT), but if you've got old software that can only generate a raw transaction, you may need to use it.

You just create your raw transaction normally:

$ utxo_txid_1=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout_1=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ utxo_txid_2=$(bitcoin-cli listunspent | jq -r '.[1] | .txid')  
$ utxo_vout_2=$(bitcoin-cli listunspent | jq -r '.[1] | .vout')  
$ echo $utxo_txid_1 $utxo_vout_1 $utxo_txid_2 $utxo_vout_2  
c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b 1 8748eff5f12ca886e3603d9e30227dcb3f0332e0706c4322fec96001f7c7f41c 0  
$ recipient=tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd  
$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' } ]''' outputs='''{ "'$recipient'": 0.0000065 }''')

Then you convert it:

$ psbt=$(bitcoin-cli -named converttopsbt hexstring=$rawtxhex)  
$ echo $psbt  
cHNidP8BAHsCAAAAAhuVpgVRdOxkuC7wW2rvw4800OVxl+QCgezYKHtCYN7GAQAAAAD/////HPTH9wFgyf4iQ2xw4DIDP8t9IjCePWDjhqgs8fXvSIcAAAAAAP////8BigIAAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBQAAAAAAAAAA

You'll note that the PSBT encoding looks very different from the transaction hex.

But if you can, you want to create the PSBT directly instead ...

## Create a PSBT the Hard Way

#### PSBT Role: Creator

The first methodology for creating a PSBT without going through another format is the PSBT-equivalent of createrawtransaction. It's called createpsbt and it gives you maximal control at the cost of maximal labor and the maximal opportunity for error.

The CLI should look quite familiar, just with a new RPC command:

$ psbt_1=$(bitcoin-cli -named createpsbt inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' } ]''' outputs='''{ "'$recipient'": 0.0000065 }''')

The Bitcoin Core team made sure that createpsbt worked much like createrawtransaction, so you don't need to learn a different creation format.

You can verify that the new PSBT is the same as the one created by converttopsbt:

$ echo $psbt_1  
cHNidP8BAHsCAAAAAhuVpgVRdOxkuC7wW2rvw4800OVxl+QCgezYKHtCYN7GAQAAAAD/////HPTH9wFgyf4iQ2xw4DIDP8t9IjCePWDjhqgs8fXvSIcAAAAAAP////8BigIAAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBQAAAAAAAAAA  
$ if [ "$psbt" == "$psbt_1" ]; then echo "PSBTs are equal"; else echo "PSBTs are not equal"; fi  
PSBTs are equal

## Examine a PSBT

#### PSBT Role: Any

So what does your PSBT actually look like? You can see that with the decodepsbt command:

$ bitcoin-cli -named decodepsbt psbt=$psbt  
{  
"tx": {  
"txid": "ea73a631b456d2b041ed73bf5767946408c6ff067716929a68ecda2e3e4de6d3",  
"hash": "ea73a631b456d2b041ed73bf5767946408c6ff067716929a68ecda2e3e4de6d3",  
"version": 2,  
"size": 123,  
"vsize": 123,  
"weight": 492,  
"locktime": 0,  
"vin": [  
{  
"txid": "c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
},  
{  
"txid": "8748eff5f12ca886e3603d9e30227dcb3f0332e0706c4322fec96001f7c7f41c",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00000650,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"hex": "0014c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
},  
{  
}  
],  
"outputs": [  
{  
}  
]  
}

It's important to note that even though we've defined the fundamentals of the transaction: the vins of where the money is coming from and the vouts of where it's going to, we haven't yet defined the inputs and outputs that are the heart of a PSBT and that are required for offline users to assess them. This is expected: the role of the Creator as defined in [BIP174](https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki) is to outline the transaction, while the role of the Updater is to start filling in the PSBT-specific data. (Other commands combine the Creator and Updater roles, but createpsbt doesn't because it doesn't have access to your wallet.)

You can also use the analyzepsbt command to look at its current state:

standup@btctest20:~$ bitcoin-cli -named analyzepsbt psbt=$psbt  
{  
"inputs": [  
{  
"has_utxo": false,  
"is_final": false,  
"next": "updater"  
},  
{  
"has_utxo": false,  
"is_final": false,  
"next": "updater"  
}  
],  
"next": "updater"  
}

Similarly, analyzepsbt shows us a PSBT that needs work. We get a look at each of the two inputs (corresponding to the two vins), and neither one has the information it needs.

## Finalize a PSBT

#### PSBT Role: Updater, Signer, Finalizer

There is a utxoupdatepsbt command that can be used to Update UTXOs, importing their descriptor information by hand, but you don't want to use it unless you have a use case where you don't have all of that information in the wallets of everyone who will be signing the PSBT.

> :information_source: **NOTE:** If you choose to Update the PSBT with utxoupdatepsbt, you would still need to use walletprocesspsbt to Sign it: it's the only Signer-role command for PSBTs that's available in bitcoin-cli.

Instead, you should use walletprocesspsbt, which will Update, Sign, and Finalize:

$ bitcoin-cli walletprocesspsbt $psbt  
{  
"psbt": "cHNidP8BAHsCAAAAAhuVpgVRdOxkuC7wW2rvw4800OVxl+QCgezYKHtCYN7GAQAAAAD/////HPTH9wFgyf4iQ2xw4DIDP8t9IjCePWDjhqgs8fXvSIcAAAAAAP////8BigIAAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBQAAAAAAAQEfAQAAAAAAAAAWABRsRdOvqHYghsS9dtinGsfJduGRlgEIawJHMEQCIAqJbxz6dBzNpfaDu4XZXb+DbDkM3UWnhezh9UdmeVghAiBRxMlW2o0wEtphtUZRWIiJOaGtXfsQbB4lovkvE4eRIgEhArrDpkX9egpTfGJ6039faVBYxY0ZzrADPpE/Gpl14A3uAAEBH0gDAAAAAAAAFgAU1ZEJG4B0ojde2ZhanEsY7+z9QWUBCGsCRzBEAiB+sNNCO4xiFQ+DoHVrqqk9yM0V4H9ZSyExx1PW7RbjsgIgUeWkQ3L7aAv1xIe7h+8PZb8ECsXg1UzbtPW8wd2qx0UBIQKIO7VGPjfVUlLYs9XCFBsAezfIp9tiEfdclVrMXqMl6wAA",  
"complete": true  
}

Obviously, you're going to need to save that psbt information using jq:

$ psbt_f=$(bitcoin-cli walletprocesspsbt $psbt | jq -r '.psbt')

You can see the inputs have now been filled in:

$ bitcoin-cli decodepsbt $psbt_f  
{  
"tx": {  
"txid": "ea73a631b456d2b041ed73bf5767946408c6ff067716929a68ecda2e3e4de6d3",  
"hash": "ea73a631b456d2b041ed73bf5767946408c6ff067716929a68ecda2e3e4de6d3",  
"version": 2,  
"size": 123,  
"vsize": 123,  
"weight": 492,  
"locktime": 0,  
"vin": [  
{  
"txid": "c6de60427b28d8ec8102e49771e5d0348fc3ef6a5bf02eb864ec745105a6951b",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
},  
{  
"txid": "8748eff5f12ca886e3603d9e30227dcb3f0332e0706c4322fec96001f7c7f41c",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00000650,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"hex": "0014c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.00000001,  
"scriptPubKey": {  
"asm": "0 6c45d3afa8762086c4bd76d8a71ac7c976e19196",  
"hex": "00146c45d3afa8762086c4bd76d8a71ac7c976e19196",  
"type": "witness_v0_keyhash",  
"address": "tb1qd3za8tagwcsgd39awmv2wxk8e9mwryvktqmkkg"  
}  
},  
"final_scriptwitness": [  
"304402200a896f1cfa741ccda5f683bb85d95dbf836c390cdd45a785ece1f54766795821022051c4c956da8d3012da61b5465158888939a1ad5dfb106c1e25a2f92f1387912201",  
"02bac3a645fd7a0a537c627ad37f5f695058c58d19ceb0033e913f1a9975e00dee"  
]  
},  
{  
"witness_utxo": {  
"amount": 0.00000840,  
"scriptPubKey": {  
"asm": "0 d591091b8074a2375ed9985a9c4b18efecfd4165",  
"hex": "0014d591091b8074a2375ed9985a9c4b18efecfd4165",  
"type": "witness_v0_keyhash",  
"address": "tb1q6kgsjxuqwj3rwhkenpdfcjccalk06st9z0k0kh"  
}  
},  
"final_scriptwitness": [  
"304402207eb0d3423b8c62150f83a0756baaa93dc8cd15e07f594b2131c753d6ed16e3b2022051e5a44372fb680bf5c487bb87ef0f65bf040ac5e0d54cdbb4f5bcc1ddaac74501",  
"02883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb"  
]  
}  
],  
"outputs": [  
{  
}  
],  
"fee": 0.00000191  
}

Or to be more precise: (1) the PSBT has been updated with the witness_utxo information; (2) the PSBT has been signed; and (3) the PSBT has been finalized.

## Create a PSBT the Easy Way

#### PSBT Role: Creator, Updater

If you think that there should be a command that's the equivalent of fundrawtransaction, you'll be pleased to know there is: walletcreatefundedpsbt. You could use it just the same as createpsbt:

$ bitcoin-cli -named walletcreatefundedpsbt inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' } ]''' outputs='''{ "'$recipient'": 0.0000065 }'''  
{  
"psbt": "cHNidP8BAOwCAAAABBuVpgVRdOxkuC7wW2rvw4800OVxl+QCgezYKHtCYN7GAQAAAAD/////HPTH9wFgyf4iQ2xw4DIDP8t9IjCePWDjhqgs8fXvSIcAAAAAAP/////uFwerANKjyVK6WaR7gzlX+lOf+ORsfjP5LYCSNIbhaAAAAAAA/v///4XjOeey0NyGpJYpszNWF8AFNiuFaWsjkOrk35Jp+9kKAAAAAAD+////AtYjEAAAAAAAFgAUMPsier2ey1eH48oGqrbbYGzNHgKKAgAAAAAAABYAFMdy1vlVQuEe8R6O/Hx6aYMK04oFAAAAAAABAR8BAAAAAAAAABYAFGxF06+odiCGxL122Kcax8l24ZGWIgYCusOmRf16ClN8YnrTf19pUFjFjRnOsAM+kT8amXXgDe4Q1gQ4AAAAAIABAACADgAAgAABAR9IAwAAAAAAABYAFNWRCRuAdKI3XtmYWpxLGO/s/UFlIgYCiDu1Rj431VJS2LPVwhQbAHs3yKfbYhH3XJVazF6jJesQ1gQ4AAAAAIABAACADAAAgAABAIwCAAAAAdVmsvkSBmfeHqNAe/wDCQ5lEp9F/587ftzCD1UL60nMAQAAABcWABRzFxRJfFPl8FJ6SxjAJzy3mCAMXf7///8CQEIPAAAAAAAZdqkUf0NzebzGbEB0XtwYkeprODDhl12IrMEwLQAAAAAAF6kU/d+kMX6XijmD+jWdUrLZlJUnH2iHPhQbACIGA+/e40wACf0XXzsgteWlUX/V0WdG8uY1tEYXra/q68OIENYEOAAAAACAAAAAgBIAAIAAAQEfE4YBAAAAAAAWABTVkQkbgHSiN17ZmFqcSxjv7P1BZSIGAog7tUY+N9VSUtiz1cIUGwB7N8in22IR91yVWsxeoyXrENYEOAAAAACAAQAAgAwAAIAAIgICKMavAB+71Adqsbf+XtC1g/OlmLEuTp3U0axyeu/LAI0Q1gQ4AAAAAIABAACAGgAAgAAA",  
"fee": 0.00042300,  
"changepos": 0  
}

However, the big advantage is that you can use it to self-fund by leaving out the inputs, just like fundrawtransaction.

$ psbt_new=$(bitcoin-cli -named walletcreatefundedpsbt inputs='''[]''' outputs='''{ "'$recipient'": 0.0000065 }''' | jq -r '.psbt')  
$ bitcoin-cli decodepsbt $psbt_new  
{  
"tx": {  
"txid": "9f2c6205ac797c1020f7f261e3ab71cd0699ff4b1a8934f68b273c71547e235f",  
"hash": "9f2c6205ac797c1020f7f261e3ab71cd0699ff4b1a8934f68b273c71547e235f",  
"version": 2,  
"size": 154,  
"vsize": 154,  
"weight": 616,  
"locktime": 0,  
"vin": [  
{  
"txid": "8748eff5f12ca886e3603d9e30227dcb3f0332e0706c4322fec96001f7c7f41c",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
},  
{  
"txid": "68e1863492802df9337e6ce4f89f53fa5739837ba459ba52c9a3d200ab0717ee",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.00971390,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 09a74ef0bae4d68b0b2ec9a7c4557a2b5c85bd8b",  
"hex": "001409a74ef0bae4d68b0b2ec9a7c4557a2b5c85bd8b",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qpxn5au96untgkzewexnug4t69dwgt0vtfahcv6"  
]  
}  
},  
{  
"value": 0.00000650,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"hex": "0014c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.00000840,  
"scriptPubKey": {  
"asm": "0 d591091b8074a2375ed9985a9c4b18efecfd4165",  
"hex": "0014d591091b8074a2375ed9985a9c4b18efecfd4165",  
"type": "witness_v0_keyhash",  
"address": "tb1q6kgsjxuqwj3rwhkenpdfcjccalk06st9z0k0kh"  
}  
},  
"bip32_derivs": [  
{  
"pubkey": "02883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb",  
"master_fingerprint": "d6043800",  
"path": "m/0'/1'/12'"  
}  
]  
},  
{  
"non_witness_utxo": {  
"txid": "68e1863492802df9337e6ce4f89f53fa5739837ba459ba52c9a3d200ab0717ee",  
"hash": "68e1863492802df9337e6ce4f89f53fa5739837ba459ba52c9a3d200ab0717ee",  
"version": 2,  
"size": 140,  
"vsize": 140,  
"weight": 560,  
"locktime": 1774654,  
"vin": [  
{  
"txid": "cc49eb0b550fc2dc7e3b9fff459f12650e0903fc7b40a31ede670612f9b266d5",  
"vout": 1,  
"scriptSig": {  
"asm": "0014731714497c53e5f0527a4b18c0273cb798200c5d",  
"hex": "160014731714497c53e5f0527a4b18c0273cb798200c5d"  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01000000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 7f437379bcc66c40745edc1891ea6b3830e1975d OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a9147f437379bcc66c40745edc1891ea6b3830e1975d88ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"ms7ruzvL4atCu77n47dStMb3of6iScS8kZ"  
]  
}  
},  
{  
"value": 0.02961601,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_HASH160 fddfa4317e978a3983fa359d52b2d99495271f68 OP_EQUAL",  
"hex": "a914fddfa4317e978a3983fa359d52b2d99495271f6887",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2NGParh82hE2Zif5PVK3AfLpYhfwF5FyRGr"  
]  
}  
}  
]  
},  
"bip32_derivs": [  
{  
"pubkey": "03efdee34c0009fd175f3b20b5e5a5517fd5d16746f2e635b44617adafeaebc388",  
"master_fingerprint": "d6043800",  
"path": "m/0'/0'/18'"  
}  
]  
}  
],  
"outputs": [  
{  
"bip32_derivs": [  
{  
"pubkey": "029bb586a52657dd98852cecef78552a4e21d081a7a30e4008ce9b419840d4deac",  
"master_fingerprint": "d6043800",  
"path": "m/0'/1'/27'"  
}  
]  
},  
{  
}  
],  
"fee": 0.00028800  
}

As you can see it Created the PSBT, and then Updated it with all the information it could find locally.

From there, you need to use walletprocesspsbt to Finalize, as usual:

$ psbt_new_f=$(bitcoin-cli walletprocesspsbt $psbt_new | jq -r '.psbt')

Afterward, an analysis will show it's about ready to go too:

$ bitcoin-cli analyzepsbt $psbt_new_f  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": true,  
"next": "extractor"  
},  
{  
"has_utxo": true,  
"is_final": true,  
"next": "extractor"  
}  
],  
"estimated_vsize": 288,  
"estimated_feerate": 0.00100000,  
"fee": 0.00028800,  
"next": "extractor"  
}

Now would you really want to use walletcreatefundedpsbt if you were creating a bitcoin-cli program? Probably not. But it's the same analysis as whether to use fundrawtransaction. Do you let Bitcoin Core do the analysis and calculation and decisions, or do you take that on yourself?

## Send a PSBT

#### PSBT Role: Extractor

To finalize the PSBT, you use finalizepsbt, which will turn your PSBT back into hex. (It'll also take on the Finalizer role, if that didn't happen already.)

$ bitcoin-cli finalizepsbt $psbt_f  
{  
"hex": "020000000001021b95a6055174ec64b82ef05b6aefc38f34d0e57197e40281ecd8287b4260dec60100000000ffffffff1cf4c7f70160c9fe22436c70e032033fcb7d22309e3d60e386a82cf1f5ef48870000000000ffffffff018a02000000000000160014c772d6f95542e11ef11e8efc7c7a69830ad38a050247304402200a896f1cfa741ccda5f683bb85d95dbf836c390cdd45a785ece1f54766795821022051c4c956da8d3012da61b5465158888939a1ad5dfb106c1e25a2f92f13879122012102bac3a645fd7a0a537c627ad37f5f695058c58d19ceb0033e913f1a9975e00dee0247304402207eb0d3423b8c62150f83a0756baaa93dc8cd15e07f594b2131c753d6ed16e3b2022051e5a44372fb680bf5c487bb87ef0f65bf040ac5e0d54cdbb4f5bcc1ddaac745012102883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb00000000",  
"complete": true  
}

As usual you'll want to save that and then you can send it out

$ psbt_hex=$(bitcoin-cli finalizepsbt $psbt_f | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$psbt_hex  
ea73a631b456d2b041ed73bf5767946408c6ff067716929a68ecda2e3e4de6d3

## Review the Workflow

When creating bitcoin-cli software, it's most likely that you'll fulfill the five core roles of PSBTs with createpsbt, walletprocesspsbt, and finalizepsbt. Here's what that flow looks like:

![](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/images/psbt-roles-for-cli-1.png)

If you choose to use the shortcut of walletcreatefundedpsbt, this is what it looks like instead:

![](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/images/psbt-roles-for-cli-2.png)

Finally, if you instead need more control and choose to use utxoupdatepsbt (which is largely undocumented here), you instead have this workflow:

![](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/images/psbt-roles-for-cli-3.png)

## Summary: Creating a Partially Signed Bitcoin Transaction

Creating a PSBT involves a somewhat complex workflow of Creating, Updating, Signing, Finalizing, and Extracting a PSBT, after which it converts back into a raw transaction. Why would you go to all that trouble? Because you want to collaborate between multiple users or multiple programs. Now that you understand this workflow, the next section has some real-life examples of doing so.

## What's Next?

Continue "Expanding Bitcoin Transactions with PSBTs" with [§7.2: Using a Partially Signed Bitcoin Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_2_Using_a_Partially_Signed_Bitcoin_Transaction.md).

# 7.2: Using a Partially Signed Bitcoin Transaction

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Now that you've learned the basic workflow of generating a PSBT, you probably want to do something with it. What can PSBTs do that multi-sigs (and normal raw transactions) can't? To start with, you've got the ease of use of a standardized format, which means that you can use your bitcoin-cli transactions and meld them with transactions generated by people (or programs) on other platforms. Beyond that, you can do some things that just weren't easy using other mechanics.

Following are three examples of using PSBTs for: multi-sigs, pooling money, and joining coins.

> :warning: **VERSION WARNING:** This is an innovation from Bitcoin Core v 0.17.0. Earlier versions of Bitcoin Core will not be able to work with the PSBT while it is in progress (though they will still be able to recognize the final transaction).

## Use a PSBT to Spend MultiSig Funds

Assume you've created a multisig address, just like you did in [§6.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_3_Sending_an_Automated_Multisig.md).

machine1$ bitcoin-cli -named addmultisigaddress nrequired=2 keys='''["'$pubkey1'","'$pubkey2'"]'''  
{  
"address": "tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0",  
"redeemScript": "5221038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e2103789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd063652ae",  
"descriptor": "wsh(multi(2,[d6043800/0'/0'/26']038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e,[be686772]03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636))#07zyayfk"  
}  
machine1$ bitcoin-cli -named importaddress address="tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0" rescan=false

machine2$ bitcoin-cli -named addmultisigaddress nrequired=2 keys='''["'$pubkey1'","'$pubkey2'"]'''  
{  
"address": "tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0",  
"redeemScript": "5221038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e2103789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd063652ae",  
"descriptor": "wsh(multi(2,[d6043800/0'/0'/26']038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e,[be686772]03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636))#07zyayfk"  
}  
machine2$ bitcoin-cli -named importaddress address="tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0" rescan=false

And, you've got some money in it:

$ bitcoin-cli listunspent  
[  
{  
"txid": "53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5",  
"vout": 0,  
"address": "tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0",  
"label": "",  
"witnessScript": "5221038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e2103789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd063652ae",  
"scriptPubKey": "0020224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"amount": 0.01999800,  
"confirmations": 2,  
"spendable": false,  
"solvable": true,  
"desc": "wsh(multi(2,[d6043800/0'/0'/26']038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e,[be686772]03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636))#07zyayfk",  
"safe": true  
}  
]

You _could_ spend this using the mechanisms in [Chapter 6](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_0_Expanding_Bitcoin_Transactions_Multisigs.md), where you serially signed a transaction, but instead we're going to show the advantage of PSBTs for multi-sigs: you can generate a single PSBT, allow everyone to sign that in parallel, and then combine the results! There's no more laboriously passing an ever-expanding hex from person to person, which speeds things up and reduces the chances of errors.

To demonstrate this methodology, we're going to pull that 0.02 BTC out of the multi-sig and divide it between the two signers, who each generated a new address for that purpose:

machine1$ bitcoin-cli getnewaddress  
tb1qem5l3q5g5h6fsqv352xh4cy07kzq2rd8gphqma  
machine2$ bitcoin-cli getnewaddress  
tb1q3krplahg4ncu523m8h2eephjazs2hf6ur8r6zp

The first thing we do is create a PSBT on the machine of our choice. (It doesn't matter which.) We need to use createpsbt from [§7.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md) for this, not the simpler walletcreatefundedpsbt, because we need the extra control of selecting the money protected by the multi-sig. (This will be the case for all three examples in this section, which demonstrates why you usually need to use createpsbt for the complex stuff.)

machine1$ utxo_txid=53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5  
machine1$ utxo_vout=0  
machine1$ split1=tb1qem5l3q5g5h6fsqv352xh4cy07kzq2rd8gphqma  
machine1$ split2=tb1q3krplahg4ncu523m8h2eephjazs2hf6ur8r6zp  
machine1$ psbt=$(bitcoin-cli -named createpsbt inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$split1'": 0.009998,"'$split2'": 0.009998 }''')

You then need to send that $psbt to everyone for signing:

machine1$ echo $psbt  
cHNidP8BAHECAAAAAbU5tQSXtwlf5ZamU+wwrLjHFp1p6WQh7haL/sLFYuxTAAAAAAD/////AnhBDwAAAAAAFgAUzun4goil9JgBkaKNeuCP9YQFDad4QQ8AAAAAABYAFI2GH/borPHKKjs91ZyG8uigq6dcAAAAAAAAAAA=

But you just have to send it once! And you do it simulataneously.

Here's the result on the first machine, where we generated the PSBT:

machine1$ psbt_p1=$(bitcoin-cli walletprocesspsbt $psbt | jq -r '.psbt')  
machine1$ bitcoin-cli decodepsbt $psbt_p1  
{  
"tx": {  
"txid": "1687e89fcb9dd3067f75495b4884dc1d4d1cf05a6c272b783cfe29eb5d22e985",  
"hash": "1687e89fcb9dd3067f75495b4884dc1d4d1cf05a6c272b783cfe29eb5d22e985",  
"version": 2,  
"size": 113,  
"vsize": 113,  
"weight": 452,  
"locktime": 0,  
"vin": [  
{  
"txid": "25e8a26f60cf485768a1e6953b983675c867b7ab126b02e753c47b7db0c4be5e",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00499900,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 cee9f88288a5f4980191a28d7ae08ff584050da7",  
"hex": "0014cee9f88288a5f4980191a28d7ae08ff584050da7",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qem5l3q5g5h6fsqv352xh4cy07kzq2rd8gphqma"  
]  
}  
},  
{  
"value": 0.00049990,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 8d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"hex": "00148d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q3krplahg4ncu523m8h2eephjazs2hf6ur8r6zp"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.01000000,  
"scriptPubKey": {  
"asm": "0 2abb5d49ce7e753cbf5a9ffa8cdaf815bf1074f5c0bf495a93df8eb5112f65aa",  
"hex": "00202abb5d49ce7e753cbf5a9ffa8cdaf815bf1074f5c0bf495a93df8eb5112f65aa",  
"type": "witness_v0_scripthash",  
"address": "tb1q92a46jww0e6ne066nlagekhczkl3qa84czl5jk5nm78t2yf0vk4qte328m"  
}  
},  
"partial_signatures": {  
"03f52980d322acaf084bcef3216f3d84bfb672d1db26ce2861de3ec047bede140d": "304402203abb95d1965e4cea630a8b4890456d56698ff2dd5544cb79303cc28cb011cbb40220701faa927f8a19ca79b09d35c78d8d0a2187872117d9308805f7a896b07733f901"  
},  
"witness_script": {  
"asm": "2 033055ec2da9bbb34c2acb343692bfbecdef8fab8d114f0036eba01baec3888aa0 03f52980d322acaf084bcef3216f3d84bfb672d1db26ce2861de3ec047bede140d 2 OP_CHECKMULTISIG",  
"hex": "5221033055ec2da9bbb34c2acb343692bfbecdef8fab8d114f0036eba01baec3888aa02103f52980d322acaf084bcef3216f3d84bfb672d1db26ce2861de3ec047bede140d52ae",  
"type": "multisig"  
},  
"bip32_derivs": [  
{  
"pubkey": "033055ec2da9bbb34c2acb343692bfbecdef8fab8d114f0036eba01baec3888aa0",  
"master_fingerprint": "c1fdfe64",  
"path": "m"  
{  
"tx": {  
"txid": "ee82d3e0d225e0fb919130d68c5052b6e3c362c866acc54d89af975330bb4d16",  
"hash": "ee82d3e0d225e0fb919130d68c5052b6e3c362c866acc54d89af975330bb4d16",  
"version": 2,  
"size": 113,  
"vsize": 113,  
"weight": 452,  
"locktime": 0,  
"vin": [  
{  
"txid": "53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00999800,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 cee9f88288a5f4980191a28d7ae08ff584050da7",  
"hex": "0014cee9f88288a5f4980191a28d7ae08ff584050da7",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qem5l3q5g5h6fsqv352xh4cy07kzq2rd8gphqma"  
]  
}  
},  
{  
"value": 0.00999800,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 8d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"hex": "00148d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q3krplahg4ncu523m8h2eephjazs2hf6ur8r6zp"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.01999800,  
"scriptPubKey": {  
"asm": "0 224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"hex": "0020224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"type": "witness_v0_scripthash",  
"address": "tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0"  
}  
},  
"partial_signatures": {  
"038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e": "3044022040aae4f2ba37b1526524195f4a325d97d1317227b3c82aea55c5abd66810a7ec0220416e7c03e70a31232044addba454d6b37b6ace39ab163315d3293e343ae9513301"  
},  
"witness_script": {  
"asm": "2 038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e 03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636 2 OP_CHECKMULTISIG",  
"hex": "5221038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e2103789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd063652ae",  
"type": "multisig"  
},  
"bip32_derivs": [  
{  
"pubkey": "03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636",  
"master_fingerprint": "be686772",  
"path": "m"  
},  
{  
"pubkey": "038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e",  
"master_fingerprint": "d6043800",  
"path": "m/0'/0'/26'"  
}  
]  
}  
],  
"outputs": [  
{  
"bip32_derivs": [  
{  
"pubkey": "02fce26085452d07abc63bd389cb7dba9871e79bbecd08039291226be8232a9000",  
"master_fingerprint": "d6043800",  
"path": "m/0'/0'/24'"  
}  
]  
},  
{  
}  
],  
"fee": 0.00000200  
}  
machine1$ bitcoin-cli analyzepsbt $psbt_p1  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": false,  
"next": "signer",  
"missing": {  
"signatures": [  
"be6867729bcc35ed065bb4c937557d371218a8e2"  
]  
}  
}  
],  
"estimated_vsize": 168,  
"estimated_feerate": 0.00001190,  
"fee": 0.00000200,  
"next": "signer"  
}

This demonstrates that the UTXO information has been imported, and that there's a _partial signature_, but that the signing of the single input is still not complete.

Here's the same thing on the other machine:

machine2$ psbt=cHNidP8BAHECAAAAAbU5tQSXtwlf5ZamU+wwrLjHFp1p6WQh7haL/sLFYuxTAAAAAAD/////AnhBDwAAAAAAFgAUzun4goil9JgBkaKNeuCP9YQFDad4QQ8AAAAAABYAFI2GH/borPHKKjs91ZyG8uigq6dcAAAAAAAAAAA=  
machine2$ psbt_p2=$(bitcoin-cli walletprocesspsbt $psbt | jq -r '.psbt')  
machine3$ echo $psbt_p2  
cHNidP8BAHECAAAAAbU5tQSXtwlf5ZamU+wwrLjHFp1p6WQh7haL/sLFYuxTAAAAAAD/////AnhBDwAAAAAAFgAUzun4goil9JgBkaKNeuCP9YQFDad4QQ8AAAAAABYAFI2GH/borPHKKjs91ZyG8uigq6dcAAAAAAABASu4gx4AAAAAACIAICJMtQOn94NXmbnCLuDDx9k9CQNW4w5wAVw+u/pRWjB0IgIDeJ9UNCNnDhaWZ/9+Hy2iqX3xsJEicuFC1YJFGs69BjZHMEQCIDJ71isvR2We6ym1QByLV5SQ+XEJD0SAP76fe1JU5PZ/AiB3V7ejl2H+9LLS6ubqYr/bSKfRfEqrp2FCMISjrWGZ6QEBBUdSIQONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDiEDeJ9UNCNnDhaWZ/9+Hy2iqX3xsJEicuFC1YJFGs69BjZSriIGA3ifVDQjZw4Wlmf/fh8toql98bCRInLhQtWCRRrOvQY2ENPtiCUAAACAAAAAgAYAAIAiBgONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDgRZu4lPAAAiAgNJzEMyT3rZS7QHqb8SvFCv2ee0MKRyVy8bY8tVUDT1KhDT7YglAAAAgAAAAIADAACAAA==

Note again that we managed the signing of this multi-sig by generating a totally unsigned PSBT with the correct UTXO, then allowing each of the users to process that PSBT on their own, adding inputs and signatures. As a result, we have two PSBTs each of which contain one signature and not the other. That wouldn't work in the classic multi-sig scenario, because all the signatures have to be serialized. Here, instead, we can sign in parallel and then make use of the Combiner role to mush those together.

We again go to either machine, and make sure we have both PSBTs in variables, then we combine them:

machine1$ psbt_p2="cHNidP8BAHECAAAAAbU5tQSXtwlf5ZamU+wwrLjHFp1p6WQh7haL/sLFYuxTAAAAAAD/////AnhBDwAAAAAAFgAUzun4goil9JgBkaKNeuCP9YQFDad4QQ8AAAAAABYAFI2GH/borPHKKjs91ZyG8uigq6dcAAAAAAABAIcCAAAAAtu5pTheUzdsTaMCEPj3XKboMAyYzABmIIeOWMhbhTYlAAAAAAD//////uSTLbibcqSd/Z9ieSBWJ2psv+9qvoGrzWEa60rCx9cAAAAAAP////8BuIMeAAAAAAAiACAiTLUDp/eDV5m5wi7gw8fZPQkDVuMOcAFcPrv6UVowdAAAAAAAACICA0nMQzJPetlLtAepvxK8UK/Z57QwpHJXLxtjy1VQNPUqENPtiCUAAACAAAAAgAMAAIAA"  
machine2$ psbt_c=$(bitcoin-cli combinepsbt '''["'$psbt_p1'", "'$psbt_p2'"]''')  
$ bitcoin-cli decodepsbt $psbt_c  
{  
"tx": {  
"txid": "ee82d3e0d225e0fb919130d68c5052b6e3c362c866acc54d89af975330bb4d16",  
"hash": "ee82d3e0d225e0fb919130d68c5052b6e3c362c866acc54d89af975330bb4d16",  
"version": 2,  
"size": 113,  
"vsize": 113,  
"weight": 452,  
"locktime": 0,  
"vin": [  
{  
"txid": "53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00999800,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 cee9f88288a5f4980191a28d7ae08ff584050da7",  
"hex": "0014cee9f88288a5f4980191a28d7ae08ff584050da7",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qem5l3q5g5h6fsqv352xh4cy07kzq2rd8gphqma"  
]  
}  
},  
{  
"value": 0.00999800,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 8d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"hex": "00148d861ff6e8acf1ca2a3b3dd59c86f2e8a0aba75c",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q3krplahg4ncu523m8h2eephjazs2hf6ur8r6zp"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.01999800,  
"scriptPubKey": {  
"asm": "0 224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"hex": "0020224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"type": "witness_v0_scripthash",  
"address": "tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0"  
}  
},  
"partial_signatures": {  
"038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e": "3044022040aae4f2ba37b1526524195f4a325d97d1317227b3c82aea55c5abd66810a7ec0220416e7c03e70a31232044addba454d6b37b6ace39ab163315d3293e343ae9513301",  
"03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636": "30440220327bd62b2f47659eeb29b5401c8b579490f971090f44803fbe9f7b5254e4f67f02207757b7a39761fef4b2d2eae6ea62bfdb48a7d17c4aaba761423084a3ad6199e901"  
},  
"witness_script": {  
"asm": "2 038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e 03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636 2 OP_CHECKMULTISIG",  
"hex": "5221038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e2103789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd063652ae",  
"type": "multisig"  
},  
"bip32_derivs": [  
{  
"pubkey": "03789f543423670e169667ff7e1f2da2a97df1b0912272e142d582451acebd0636",  
"master_fingerprint": "be686772",  
"path": "m"  
},  
{  
"pubkey": "038d73adf2c7ea33f9dc34b77b62b59af433c1de9c763332da79e83e155f96030e",  
"master_fingerprint": "d6043800",  
"path": "m/0'/0'/26'"  
}  
]  
}  
],  
"outputs": [  
{  
"bip32_derivs": [  
{  
"pubkey": "02fce26085452d07abc63bd389cb7dba9871e79bbecd08039291226be8232a9000",  
"master_fingerprint": "d6043800",  
"path": "m/0'/0'/24'"  
}  
]  
},  
{  
"bip32_derivs": [  
{  
"pubkey": "0349cc43324f7ad94bb407a9bf12bc50afd9e7b430a472572f1b63cb555034f52a",  
"master_fingerprint": "d3ed8825",  
"path": "m/0'/0'/3'"  
}  
]  
}  
],  
"fee": 0.00000200  
}  
$ bitcoin-cli analyzepsbt $psbt_c  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": false,  
"next": "finalizer"  
}  
],  
"estimated_vsize": 168,  
"estimated_feerate": 0.00001190,  
"fee": 0.00000200,  
"next": "finalizer"  
}

It worked! We just finalize and send and we're done:

machine2$ psbt_c_hex=$(bitcoin-cli finalizepsbt $psbt_c | jq -r '.hex')  
standup@btctest2:~$ bitcoin-cli -named sendrawtransaction hexstring=$psbt_c_hex  
ee82d3e0d225e0fb919130d68c5052b6e3c362c866acc54d89af975330bb4d16

Obviously, there wasn't a big improvement in using this method over serially signing a transaction for a 2-of-2 multisig when everyone was using bitcoin-cli: we could have passed a raw transaction with partial signatures from one user to the other just as easily as sending that PSBT. But, this was the simplest case. As we delve into more complex multisigs, this methodology becomes better and better.

First of all, it's platform independent. As long as everyone is using a service that supports Bitcoin Core 0.17, they'll all be able to sign this transaction, which isn't true when classic multi-sigs are being passed around among different platforms.

Second, it's a lot more scalable. Consider a 3-of-5 multisig. Under the old methodology it would have to passed from person to person, greatly increasing the problems if any single link in the chain breaks. Here, other users just have to send the PSBTs back to the Creator, and as soon as she has enough, she can generate the final transaction.

## Use a PSBT to Pool Money

Multisigs like the one used in the previous example are often used to receive payments for collaborative work, whether it be royalties for a book or payments made to a company. In that situation, the above example works great: the two participants receive their money which they then split up. But what about the converse case, where two (or more) participants want to set up a joint venture, and they need to seed it with money?

The traditional answer is to create a multisig, then to have the participants individually send their funds to it. The problem is that the first payer has to depend on the good faith of the second, and that doesn't build on the strength of Bitcoin, which is its _trustlessness_. Fortunately, with the advent of PSBTs, we can now make trustless payments that pool funds.

> :book: _**What does trustless mean?**_ Trustless means that no participant has to trust any other participant. They instead expect the software protocols to ensure that everything is enacted fairly in an expected manner. Bitcoin is a trustless protocol because you don't need anyone else to act in good faith; the system manages it. Similarly, PSBTs allow for the trustless creation of transactions that pool or split funds.

The following example shows two users who each have 0.010 BTC that they want to pool to the multisig address tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0, created above.

machine1$ bitcoin-cli listunspent  
[  
{  
"txid": "2536855bc8588e87206600cc980c30e8a65cf7f81002a34d6c37535e38a5b9db",  
"vout": 0,  
"address": "tb1qfg5y4fx979xkv4ezatc5eevufc8vh45553n4ut",  
"label": "",  
"scriptPubKey": "00144a284aa4c5f14d665722eaf14ce59c4e0ecbd694",  
"amount": 0.01000000,  
"confirmations": 2,  
"spendable": true,  
"solvable": true,  
"desc": "wpkh([d6043800/0'/0'/25']02bea222cf9ea1f49b392103058cc7c8741d76a553fe627c1c43fc3ef4404c9d54)#4hnkg9ml",  
"safe": true  
}  
]  
machine2$ bitcoin-cli listunspent  
[  
{  
"txid": "d7c7c24aeb1a61cdab81be6aefbf6c6a27562079629ffd9da4729bb82d93e4fe",  
"vout": 0,  
"address": "tb1qfqyyw6xrghm5kcrpkus3kl2l6dz4tpwrvn5ujs",  
"label": "",  
"scriptPubKey": "001448084768c345f74b6061b7211b7d5fd3455585c3",  
"amount": 0.01000000,  
"confirmations": 5363,  
"spendable": true,  
"solvable": true,  
"desc": "wpkh([d3ed8825/0'/0'/0']03ff6b94c119582a63dbae4fb530efab0ed5635f7c3b2cf171264ca0af3ecef33a)#gtmd2e2k",  
"safe": true  
}  
]

They set up variables to use those transactions:

machine1$ utxo_txid_1=2536855bc8588e87206600cc980c30e8a65cf7f81002a34d6c37535e38a5b9db  
machine1$ utxo_vout_1=0  
machine1$ utxo_txid_2=d7c7c24aeb1a61cdab81be6aefbf6c6a27562079629ffd9da4729bb82d93e4fe  
machine1$ utxo_vout_2=0  
machine1$ multisig=tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0

And create a PSBT:

machine1$ psbt=$(bitcoin-cli -named createpsbt inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' } ]''' outputs='''{ "'$multisig'": 0.019998 }''')

Here's what it looks like:

machine1$ bitcoin-cli decodepsbt $psbt  
{  
"tx": {  
"txid": "53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5",  
"hash": "53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5",  
"version": 2,  
"size": 135,  
"vsize": 135,  
"weight": 540,  
"locktime": 0,  
"vin": [  
{  
"txid": "2536855bc8588e87206600cc980c30e8a65cf7f81002a34d6c37535e38a5b9db",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
},  
{  
"txid": "d7c7c24aeb1a61cdab81be6aefbf6c6a27562079629ffd9da4729bb82d93e4fe",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.01999800,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"hex": "0020224cb503a7f7835799b9c22ee0c3c7d93d090356e30e70015c3ebbfa515a3074",  
"reqSigs": 1,  
"type": "witness_v0_scripthash",  
"addresses": [  
"tb1qyfxt2qa877p40xdecghwps78my7sjq6kuv88qq2u86al5526xp6qfqjud0"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
},  
{  
}  
],  
"outputs": [  
{  
}  
]  
}

It doesn't matter that the transactions are owned by two different people or that their full information appears on two different machines. This funding PSBT will work exactly the same as the multisig PSBT: once all of the controlling parties have signed, then the transaction can be finalized.

Here's the process, this time passing the partially signed PSBT from one user to another rather than having to combine things at the end.

machine1$ bitcoin-cli walletprocesspsbt $psbt  
{  
"psbt": "cHNidP8BAIcCAAAAAtu5pTheUzdsTaMCEPj3XKboMAyYzABmIIeOWMhbhTYlAAAAAAD//////uSTLbibcqSd/Z9ieSBWJ2psv+9qvoGrzWEa60rCx9cAAAAAAP////8BuIMeAAAAAAAiACAiTLUDp/eDV5m5wi7gw8fZPQkDVuMOcAFcPrv6UVowdAAAAAAAAQEfQEIPAAAAAAAWABRKKEqkxfFNZlci6vFM5ZxODsvWlAEIawJHMEQCIGAiKIAWRXiw68o3pw61/cVNP7n2oH73S654XXgQ4kjHAiBtTBqmaF1iIzYGXrG4DadH8y6mTuCRVFDiPl+TLQDBJwEhAr6iIs+eofSbOSEDBYzHyHQddqVT/mJ8HEP8PvRATJ1UAAABAUdSIQONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDiEDeJ9UNCNnDhaWZ/9+Hy2iqX3xsJEicuFC1YJFGs69BjZSriICA3ifVDQjZw4Wlmf/fh8toql98bCRInLhQtWCRRrOvQY2BL5oZ3IiAgONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDhDWBDgAAAAAgAAAAIAaAACAAA==",  
"complete": false  
}

machine2$ psbt_p="cHNidP8BAIcCAAAAAtu5pTheUzdsTaMCEPj3XKboMAyYzABmIIeOWMhbhTYlAAAAAAD//////uSTLbibcqSd/Z9ieSBWJ2psv+9qvoGrzWEa60rCx9cAAAAAAP////8BuIMeAAAAAAAiACAiTLUDp/eDV5m5wi7gw8fZPQkDVuMOcAFcPrv6UVowdAAAAAAAAQEfQEIPAAAAAAAWABRKKEqkxfFNZlci6vFM5ZxODsvWlAEIawJHMEQCIGAiKIAWRXiw68o3pw61/cVNP7n2oH73S654XXgQ4kjHAiBtTBqmaF1iIzYGXrG4DadH8y6mTuCRVFDiPl+TLQDBJwEhAr6iIs+eofSbOSEDBYzHyHQddqVT/mJ8HEP8PvRATJ1UAAABAUdSIQONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDiEDeJ9UNCNnDhaWZ/9+Hy2iqX3xsJEicuFC1YJFGs69BjZSriICA3ifVDQjZw4Wlmf/fh8toql98bCRInLhQtWCRRrOvQY2BL5oZ3IiAgONc63yx+oz+dw0t3titZr0M8HenHYzMtp56D4VX5YDDhDWBDgAAAAAgAAAAIAaAACAAA=="  
machine2$ psbt_f=$(bitcoin-cli walletprocesspsbt $psbt_p | jq -r '.psbt')  
machine2$ bitcoin-cli analyzepsbt $psbt_f  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": true,  
"next": "extractor"  
},  
{  
"has_utxo": true,  
"is_final": true,  
"next": "extractor"  
}  
],  
"estimated_vsize": 189,  
"estimated_feerate": 0.00001058,  
"fee": 0.00000200,  
"next": "extractor"  
}  
machine2$ psbt_hex=$(bitcoin-cli finalizepsbt $psbt_f | jq -r '.hex')  
machine2$ bitcoin-cli -named sendrawtransaction hexstring=$psbt_hex  
53ec62c5c2fe8b16ee2164e9699d16c7b8ac30ec53a696e55f09b79704b539b5

We've used a PSBT to trustlessly gather money into a multisig!

## Use a PSBT to CoinJoin

CoinJoin is another Bitcoin application that requires trustlessness. Here, you have a variety of parties who don't necessarily know each other joining money and getting it back.

The methodology for managing it with PSBTs is exactly the same as you've seen in the above examples, as the following pseudo-code demonstrates:

$ psbt=$(bitcoin-cli -named createpsbt inputs='''[ { "txid": "'$utxo_txid_1'", "vout": '$utxo_vout_1' }, { "txid": "'$utxo_txid_2'", "vout": '$utxo_vout_2' }, { "txid": "'$utxo_txid_3'", "vout": '$utxo_vout_3' } ]''' outputs='''{ "'$split1'": 1.7,"'$split2'": 0.93,"'$split3'": 1.4 }''')

Each user puts in their own UTXO, and each one receives a corresponding output.

The best way to manage a CoinJoin is to send out the base PSBT to all the parties (who could be numerous), and then have them each sign the PSBT and send back to a single party who will combine, finalize, and send.

> :book: _**What is CoinJoin?**_ CoinJoin is a methodology whereby a group of people can mix together their cryptocurrency, helping to reduce fungibility for all the coins. Each person puts in and takes out the same amount of coins (minus transaction fees) in a multi-person transaction that is simultaneously conducted by a _large_ number of people. It's designed to be "trustless" so that the parties don't need to know or trust each other. A CoinJoin ultimately increases anonymity by making the coins hard to trace. The Wasabi Wallet and a number of "mixer" services support CoinJoin at the large-scale necessary for improved anonymity.

## Summary: Using a Partially Signed Bitcoin Transaction

You've now seen the PSBT process that you learned in [§7.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md) in use in three real-life examples: creating a multi-sig, pooling funds, and CoinJoining. These were all theoretically possible in classic Bitcoin by having multiple people sign carefully constructed transactions, but PSBTs make it standardized and simple.

> :fire: _**What's the power of a PSBT?**_ A PSBT allows for the creation of trustless transactions between multiple parties and multiple machines. If more than one party would need to fund a transaction, if more than one party would need to sign a transaction, or if a transaction needs to be created on one machine and signed on another, then a PSBT makes it simple without depending on the non-standardized partial signing mechanisms that used to exist before PSBT.

That last point, on creating a transaction on one machine and signing on another, is an element of PSBTs that we haven't gotten to yet. It's at the heart of hardware wallets, where you often want to create a transaction on a full node, then pass it on to a hardware wallet when a signature is required. That's the topic of the last section (and our fourth real-life example) in this chapter on PSBTs.

## What's Next?

Continue "Expanding Bitcoin Transactions with PSBTs" with [§7.3: Integrating with Hardware Wallets](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_3_Integrating_with_Hardware_Wallets.md).

# 7.3: Integrating with Hardware Wallets

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

One of the greatest powers of PSBTs is the ability to hand transactions off to hardware wallets. This will be a great development tool for you if you continue to program with Bitcoin. However, you can't test it out now if you're using one of the configurations we suggest for this course — a VM on Linode per [§2.1](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md) or an even more farflung option such as AWS per [§2.2](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/02_2_Setting_Up_Bitcoin_Core_Other.md) — because obviously you won't have any way to hook a hardware wallet up to your remote, virtual machine.

> :book: _**What is a Hardware Wallet?**_ A hardware wallet is an electronic device that improves the security of a cryptocurrency by maintaining all the private keys on the device, rather than ever putting them on a computer directly connected to the internet. Hardware wallets have specific protocols for providing online interactions, usually managed by a program talking to the device through a USB port. In this chapter, we'll be managing a hardware wallet with bitcoin-cli and the hwy.py program.

You have three options for moving through this chapter on hardware wallets: (1) read along without testing the code; (2) install Bitcoin on a local machine to fully test these commands; or (3) skip straight ahead to [Chapter 8: Expanding Bitcoin Transactions in Other Ways](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_0_Expanding_Bitcoin_Transactions_Other.md). We suggest option #1, but if you really want to get your hands dirty we'll also give some support for #2 by talking about using a Macintosh (a hardware-platform supported by [Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup)) for testing.

> :warning: **VERSION WARNING:** PSBTs are an innovation from Bitcoin Core v 0.17.0. Earlier versions of Bitcoin Core will not be able to work with the PSBT while it is in progress (though they will still be able to recognize the final transaction). The HWI interface appeared in Bitcoin Core v 0.18.0, but as long as you are using our suggested setup with Bitcoin Standup, it should work.

The methodology described in this chapter for integrating with a hardware wallet depends on the [Bitcoin Hardware Wallet Interface](https://github.com/bitcoin-core/HWI) released through Bitcoin Core and builds on the [installation](https://github.com/bitcoin-core/HWI/blob/master/README.md) and [usage](https://hwi.readthedocs.io/) instructions found there.

> :warning: **FRESHNESS WARNING:** The HWI interface is very new and raw around the edges as of Bitcoin Core v 0.20.0. It may be hard to install correctly, and it may have unintuitive errors. What follows is a description of a working setup, but it took several tries to get it right, and your setup may vary.

## Install Bitcoin Core on a Local Machine

_If you just plan to read over this section and not test out these commands until some future date when you have a local development environment, you can skip this subsection, which is about creating a Bitcoin Core installation on a local machine such as a Mac or Linux machine._

There are alternate versions of the Bitcoin Standup script that you used to create your VM that will install on a MacOS or on a non-Linode Linux machine.

If you have MacOS, you can install [Bitcoin Standup MacOS](https://github.com/BlockchainCommons/Bitcoin-Standup-MacOS/blob/master/README.md).

If you have a local Linux machine, you can install [Bitcoin Standup Linux Scripts](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/README.md).

Once you've gotten Bitcoin Standup running on your local machine, you'll want to sync the "Testnet" blockchain, assuming that you're continuing to follow the standard methodlogy of this course.

We will be using a Macintosh and Testnet for the examples in this section.

### Create an Alias for Bitcoin-CLI

Create an alias that runs bitcoin-cli from the correct directory with any appropriate flags.

Here's an example alias from a Mac:

$ alias bitcoin-cli="~/StandUp/BitcoinCore/bitcoin-0.20.0/bin/bitcoin-cli -testnet"

You'll note it not only gives us the full path, but also ensures that we stay on Testnet.

## Install HWI on a Local Machine

_The following instructions again assume a Mac, and you can again skip this subsection if you're just reading through this chapter._

HWI is a Bitcoin Core program available in python that can be used to interact with hardware wallets.

### Install Python

Because HWI is written in python, you'll need to install that as well as a few auxilliary programs.

If you don't already have the xcode command line tools, you'll need them:

$ xcode-select --install

If you don't already have the Homebrew package manager, you should install that too. Current instructions are available at the [Homebrew site](https://brew.sh/). As of this writing, you simply need to:

$ /bin/bash -c "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/master/install.sh](https://raw.githubusercontent.com/Homebrew/install/master/install.sh))"

For a first-time installation, you should also make sure your /usr/local/Frameworks directory is created correctly:

$ sudo mkdir /usr/local/Frameworks  
$ sudo chown $(whoami):admin /usr/local/Frameworks

If you've got all of that in place, you can finally install Python:

$ brew install python  
$ brew install libusb

### Install HWI

You're now ready to install HWI, which requires cloning a GitHub repo and running an install script.

If you don't have git already installed on your Mac, you can do so just by trying to run it: git --version.

You can then clone the HWI repo:

$ cd ~/StandUp  
$ git clone [https://github.com/bitcoin-core/HWI.git](https://github.com/bitcoin-core/HWI.git)

Afterward, you need to install the package and its dependencies:

$ cd HWI  
HWI$ python3 setup.py install

### Create an Alias for HWI

You'll want to create an alias here too, varied by your actual install location:

$ alias hwi="~/Standup/HWI/hwi.py --chain test"

Again, we've included a reference to testnet in this alias.

## Prepare Your Ledger

_We had to choose a hardware-wallet platform too, for this HWI demonstration. Our choice was the Ledger, which has long been our testbed for hardware wallets. Please see_ [_HWI's device support info_](https://github.com/bitcoin-core/HWI/blob/master/README.md#device-support) _for a list of other supported devices. If you use a device other than a Ledger, you'll need to assess your own solutions for preparing it for usage on the Testnet, but otherwise you should be able to continue with the course as written._

If you are working with Bitcoins on your Ledger, you probably won't need to do anything. (But we don't suggest that for use with this course).

To work with Testnet coins, as suggested by this course, you'll need to make a few updates:

1. Go to Settings on your Ledger Live app (it's the gear), go to the "Experimental Features" tab, and turn on "Developer Mode".
    
2. Go to the "Manager" and install "Bitcoin Test". The current version requires that you have "Bitcoin" installed first.
    
3. Go to the "Manager", scroll to your new "Bitcoin Test", and "Add Account"
    

## Link to a Ledger

In order for a Ledger to be accessible, you must login with your PIN and then call up the app that you want to use, in this case the "Bitcoin Test" app. You may need to repeat this from time to time if your Ledger falls asleep.

Once you've done that, you can ask for HWI to access the Ledger with the enumerate command:

$ hwi enumerate  
[{"type": "ledger", "model": "ledger_nano_s", "path": "IOService:/AppleACPIPlatformExpert/PCI0@0/AppleACPIPCI/XHC1@14/XHC1@14000000/HS05@14100000/Nano S@14100000/Nano S@0/IOUSBHostHIDDevice@14100000,0", "fingerprint": "9a1d520b", "needs_pin_sent": false, "needs_passphrase_sent": false}]

If you receive information on your device, you're set! As you can see, it verifies your hardware-wallet type, provides other identifying information, and tells you how to communicate with the device. The fingerprint (9a1d520b) is what you should pay particular attention to, because all interactions with your hardware wallet will require it.

If you instead got [], then either (1) you didn't get your Ledger device ready by entering your PIN and choosing the correct application, or (2) there's something wrong with your Python setup, probably a missing dependency: you should consider uninstalling it and trying from scratch.

## Import Addresses

Interacting with a hardware wallet usually comes in two parts: watching for funds and spending funds.

You can watch for funds by importing addresses from your hardware wallet to your full node, using HWI and bitcoin-cli.

### Create a Wallet

To use your hardware wallet with bitcoin-cli, you'll want to create a specific named wallet in Bitcoin Core, using the createwallet RPC, which is a command we haven't previously discussed.

$ bitcoin-cli --named createwallet wallet_name="ledger" disable_private_keys="true" descriptors="false"  
{  
"name": "ledger",  
"warning": ""  
}

In this case, you are creating a new wallet ledger without private keys (since those will be over on the Ledger device).

> :book: _**Why Name Wallets?**_ To date, this course has used the default ("") wallet in Bitcoin Core. This is fine for many purposes, but is inadequate if you have a more complex situation, such as when you're watching keys from a hardware wallet. Here, we want to be able to differentiate from the locally owned keys (which are kept in the "" wallet) and the remotely owned keys (which are kept in the "ledger" wallet).

You can now see that the new wallet is in your wallets list:

$ bitcoin-cli listwallets  
[  
"",  
"ledger"  
]

Because you've created a second wallet, some commands will now require a -rpcwallet= flag, to specify which one you're using

### Import the Keys

You now have to import a watch-list of addresses from the hardware wallet. This is done with HWI's getkeypool command:

$ hwi -f 9a1d520b getkeypool 0 1000  
[{"desc": "wpkh([9a1d520b/84h/1h/0h]tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/0/_)#qttxy592", "range": [0, 1000], "timestamp": "now", "internal": false, "keypool": true, "active": true, "watchonly": true}, {"desc": "wpkh([9a1d520b/84h/1h/0h]tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/1/_)#3lw8ep4j", "range": [0, 1000], "timestamp": "now", "internal": true, "keypool": true, "active": true, "watchonly": true}]

We address HWI with the fingerprint and ask for the first 1000 addresses. The WPKH (native Segwit) address type is used as a default. In return, we receive two descriptors for the key pool: one for receiving addresses and one for change addresses.

> :book: _**What is a key pool?**_ A key pool is a group of pregenerated keys. Modern HD wallets create key pools by continuing to determine new hierarchical addresses based on the original seed. The idea of key pools was originally implemented to ease the backup requirements of wallets. This allowed a user to generate a keypool and then backup the wallet immediately, rather than requiring backups after every new address was created. The concept has also proven very useful in the modern day since it allows the importing of a whole set of future addresses from one device to another.

The values returned by getkeypool are the same sorts of descriptors that we learned about in [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md). At the time, we said that they were most useful for moving addresses among different machines. Here's the real-life example: moving addresses from a hardware wallet to Bitcoin Core node, so that our net-connected machine will be able to watch over the keys owned by the offline hardware wallet.

Just as you learned in [§3.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md), you can examine these descriptors with the getdescriptorinfo RPC:

$ bitcoin-cli getdescriptorinfo "wpkh([9a1d520b/84h/1h/0h]tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/0/_)#qttxy592"_  
_{_  
_"descriptor": "wpkh([9a1d520b/84'/1'/0']tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/0/_)#n65e7wjf",  
"checksum": "qttxy592",  
"isrange": true,  
"issolvable": true,  
"hasprivatekeys": false  
}

As you'd expect, we do _not_ have privatekeys, because hardware wallets hold on to those.

With the descriptors in hand, you can import the keys into your new ledger wallet using the importmulti RPC that you also met in [§3.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md). In this case, just put the entire response you got back from HWI in 's.

$ bitcoin-cli -rpcwallet=ledger importmulti '[{"desc": "wpkh([9a1d520b/84h/1h/0h]tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/0/_)#qttxy592", "range": [0, 1000], "timestamp": "now", "internal": false, "keypool": true, "active": true, "watchonly": true}, {"desc": "wpkh([9a1d520b/84h/1h/0h]tpubDD7KTtoGzK9GuWUQcr1uTJazsAkqoXhdrwGXWVix6nPpNZmSbagZWD4QSaMsyK8YohAirGDPrWdRiEpKzTFB7DrTrqfzHCn7yi5EsqeR93S/1/_)#3lw8ep4j", "range": [0, 1000], "timestamp": "now", "internal": true, "keypool": true, "active": true, "watchonly": true}]'  
[  
{  
"success": true  
},  
{  
"success": true  
}  
]

(Note that HWI helpfully output the derivation path with hs to show hardened derivations rather than 's, and calculated its checksum accordingly, so that we don't have to do massive quoting like we did in §3.5.)

You _could_ now list all of the watch-only addresses that you received using the getaddressesbylabel command. All 1000 of the receive addresses are right there, in the ledger wallet!

$ bitcoin-cli -rpcwallet=ledger getaddressesbylabel "" | more  
{  
"tb1qqqvnezljtmc9d7x52udpc0m9zgl9leugd2ur7y": {  
"purpose": "receive"  
},  
"tb1qqzvrm6hujdt93qctuuev5qc4499tq9fdk0prwf": {  
"purpose": "receive"  
},  
...  
}

## Receive a Transaction

Obviously, receiving a transaction is simple. You use getnewaddress to request one of those imported addresses:

$ bitcoin-cli -rpcwallet=ledger getnewaddress  
tb1qqqvnezljtmc9d7x52udpc0m9zgl9leugd2ur7y

Then you send money to it.

The power of HWI is that you can watch the payments from your Bitcoin Core node, rather than having to plug in your hardware wallet and query it.

$ bitcoin-cli -rpcwallet=ledger listunspent  
[  
{  
"txid": "c733533eb1c052242f9ed89cd8927aedb41852156e684634ee7c74028774e595",  
"vout": 1,  
"address": "tb1q948388a23pfsf52kz6skd5k4z4627jja2evztr",  
"label": "",  
"scriptPubKey": "00142d4f139faa885304d15616a166d2d51574af4a5d",  
"amount": 0.01000000,  
"confirmations": 12,  
"spendable": false,  
"solvable": true,  
"desc": "wpkh([9a1d520b/84'/1'/0'/0/0]02a013cf9c4b5f5689d9253036a3e477cf98689626f7814c94f092726f11b741ab)#9za8hlvk",  
"safe": true  
},  
{  
"txid": "5b3c4aeb811f9a119fd633b12a6927415cc61b8654628df58e9141cab804bab8",  
"vout": 0,  
"address": "tb1qqqvnezljtmc9d7x52udpc0m9zgl9leugd2ur7y",  
"label": "",  
"scriptPubKey": "001400193c8bf25ef056f8d4571a1c3f65123e5fe788",  
"amount": 0.01000000,  
"confirmations": 1,  
"spendable": false,  
"solvable": true,  
"desc": "wpkh([9a1d520b/84'/1'/0'/0/569]030168d9482e2b02d7027fb4a89edc54adaa1adf709334f647d0a1b0533828aec5)#sx9haake",  
"safe": true  
}  
]

## Create a Transaction with PSBT

Watching and receiving payments is just half the battle. You may also want to make payments using accounts held by your hardware wallet. This is the fourth real-life example for using PSBTs, per the process outlined in [§7.1: Creating a Partially Signed Bitcoin Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/7_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md).

The commands work exactly the same. In this case, use walletcreatefundedpsbt to form your PSBT because this is a situation where you don't care what UTXOs are used:

$ bitcoin-cli -named -rpcwallet=ledger walletcreatefundedpsbt inputs='''[]''' outputs='''[{"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd":0.015}]'''  
{  
"psbt": "cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giBgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxRiaHVILVAAAgAEAAIAAAACAAAAAADkCAAAAAQEfQEIPAAAAAAAWABQtTxOfqohTBNFWFqFm0tUVdK9KXSIGAqATz5xLX1aJ2SUwNqPkd8+YaJYm94FMlPCScm8Rt0GrGJodUgtUAACAAQAAgAAAAIAAAAAAAAAAAAAAIgID2UK1nupSfXC81nmB65XZ+pYlJp/W6wNk5FLt5ZCSx6kYmh1SC1QAAIABAACAAAAAgAEAAAABAAAAAA==",  
"fee": 0.00000209,  
"changepos": 1  
}

You can take a look at the PSBT and verify that it looks rational:

$ psbt="cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giBgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxRiaHVILVAAAgAEAAIAAAACAAAAAADkCAAAAAQEfQEIPAAAAAAAWABQtTxOfqohTBNFWFqFm0tUVdK9KXSIGAqATz5xLX1aJ2SUwNqPkd8+YaJYm94FMlPCScm8Rt0GrGJodUgtUAACAAQAAgAAAAIAAAAAAAAAAAAAAIgID2UK1nupSfXC81nmB65XZ+pYlJp/W6wNk5FLt5ZCSx6kYmh1SC1QAAIABAACAAAAAgAEAAAABAAAAAA=="

$ bitcoin-cli decodepsbt $psbt  
{  
"tx": {  
"txid": "45f996d4ff8c9e9ab162f611c5b6ad752479ede9780f9903bdc80cd96619676d",  
"hash": "45f996d4ff8c9e9ab162f611c5b6ad752479ede9780f9903bdc80cd96619676d",  
"version": 2,  
"size": 154,  
"vsize": 154,  
"weight": 616,  
"locktime": 0,  
"vin": [  
{  
"txid": "5b3c4aeb811f9a119fd633b12a6927415cc61b8654628df58e9141cab804bab8",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
},  
{  
"txid": "c733533eb1c052242f9ed89cd8927aedb41852156e684634ee7c74028774e595",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01500000,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"hex": "0014c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd"  
]  
}  
},  
{  
"value": 0.00499791,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 f4e8dde5db370898b57c84566e3f76098850817d",  
"hex": "0014f4e8dde5db370898b57c84566e3f76098850817d",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q7n5dmewmxuyf3dtus3txu0mkpxy9pqtacuprak"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.01000000,  
"scriptPubKey": {  
"asm": "0 00193c8bf25ef056f8d4571a1c3f65123e5fe788",  
"hex": "001400193c8bf25ef056f8d4571a1c3f65123e5fe788",  
"type": "witness_v0_keyhash",  
"address": "tb1qqqvnezljtmc9d7x52udpc0m9zgl9leugd2ur7y"  
}  
},  
"bip32_derivs": [  
{  
"pubkey": "030168d9482e2b02d7027fb4a89edc54adaa1adf709334f647d0a1b0533828aec5",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/0/569"  
}  
]  
},  
{  
"witness_utxo": {  
"amount": 0.01000000,  
"scriptPubKey": {  
"asm": "0 2d4f139faa885304d15616a166d2d51574af4a5d",  
"hex": "00142d4f139faa885304d15616a166d2d51574af4a5d",  
"type": "witness_v0_keyhash",  
"address": "tb1q948388a23pfsf52kz6skd5k4z4627jja2evztr"  
}  
},  
"bip32_derivs": [  
{  
"pubkey": "02a013cf9c4b5f5689d9253036a3e477cf98689626f7814c94f092726f11b741ab",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/0/0"  
}  
]  
}  
],  
"outputs": [  
{  
},  
{  
"bip32_derivs": [  
{  
"pubkey": "03d942b59eea527d70bcd67981eb95d9fa9625269fd6eb0364e452ede59092c7a9",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/1/1"  
}  
]  
}  
],  
"fee": 0.00000209  
}

And as usual, analyzepsbt will show how far you've gotten:

$ bitcoin-cli analyzepsbt $psbt  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": false,  
"next": "signer",  
"missing": {  
"signatures": [  
"00193c8bf25ef056f8d4571a1c3f65123e5fe788"  
]  
}  
},  
{  
"has_utxo": true,  
"is_final": false,  
"next": "signer",  
"missing": {  
"signatures": [  
"2d4f139faa885304d15616a166d2d51574af4a5d"  
]  
}  
}  
],  
"estimated_vsize": 208,  
"estimated_feerate": 0.00001004,  
"fee": 0.00000209,  
"next": "signer"  
}

Because you imported that keypool, bitcoin-cli has all the information it needs to fill in the inputs, it just can't sign because the private keys are held on the hardware wallet.

That's where HWI comes in, with the signtx command. You just send along the PSBT:

$ hwi -f 9a1d520b signtx $psbt

Expect to have to do some fiddling with your hardware wallet at this point. The device will probably ask you to confirm the inputs, the outputs, and the fee. When you're done, it should return a new PSBT.

{"psbt": "cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giAgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxUcwRAIgAxkQlk2fqEMxvP54WWyiFhlfSul9sd4GzKDhfGpmlewCIHYej3zXWWMgWI6rixxQw9yzGozDaFPqQNNIvcFPk+lfASIGAwFo2UguKwLXAn+0qJ7cVK2qGt9wkzT2R9ChsFM4KK7FGJodUgtUAACAAQAAgAAAAIAAAAAAOQIAAAABAR9AQg8AAAAAABYAFC1PE5+qiFME0VYWoWbS1RV0r0pdIgICoBPPnEtfVonZJTA2o+R3z5holib3gUyU8JJybxG3QatHMEQCIH5t6T2yufUP7glYZ8YH0/PhDFpotSmjgZUhvj6GbCFIAiBcgXzyYl7IjYuaF3pJ7AgW1rLYkjeCJJ2M9pVUrq5vFwEiBgKgE8+cS19WidklMDaj5HfPmGiWJveBTJTwknJvEbdBqxiaHVILVAAAgAEAAIAAAACAAAAAAAAAAAAAACICA9lCtZ7qUn1wvNZ5geuV2fqWJSaf1usDZORS7eWQksepGJodUgtUAACAAQAAgAAAAIABAAAAAQAAAAA="}  
$ psbt_f="cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giAgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxUcwRAIgAxkQlk2fqEMxvP54WWyiFhlfSul9sd4GzKDhfGpmlewCIHYej3zXWWMgWI6rixxQw9yzGozDaFPqQNNIvcFPk+lfASIGAwFo2UguKwLXAn+0qJ7cVK2qGt9wkzT2R9ChsFM4KK7FGJodUgtUAACAAQAAgAAAAIAAAAAAOQIAAAABAR9AQg8AAAAAABYAFC1PE5+qiFME0VYWoWbS1RV0r0pdIgICoBPPnEtfVonZJTA2o+R3z5holib3gUyU8JJybxG3QatHMEQCIH5t6T2yufUP7glYZ8YH0/PhDFpotSmjgZUhvj6GbCFIAiBcgXzyYl7IjYuaF3pJ7AgW1rLYkjeCJJ2M9pVUrq5vFwEiBgKgE8+cS19WidklMDaj5HfPmGiWJveBTJTwknJvEbdBqxiaHVILVAAAgAEAAIAAAACAAAAAAAAAAAAAACICA9lCtZ7qUn1wvNZ5geuV2fqWJSaf1usDZORS7eWQksepGJodUgtUAACAAQAAgAAAAIABAAAAAQAAAAA="

When you analyze this, you'll see that it's ready to be finalized:

$ bitcoin-cli analyzepsbt $psbt_f  
{  
"inputs": [  
{  
"has_utxo": true,  
"is_final": false,  
"next": "finalizer"  
},  
{  
"has_utxo": true,  
"is_final": false,  
"next": "finalizer"  
}  
],  
"estimated_vsize": 208,  
"estimated_feerate": 0.00001004,  
"fee": 0.00000209,  
"next": "finalizer"  
}

At this point you're back into standard territory:

$ bitcoin-cli finalizepsbt $psbt_f  
{  
"hex": "02000000000102b8ba04b8ca41918ef58d6254861bc65c4127692ab133d69f119a1f81eb4a3c5b0000000000feffffff95e5748702747cee3446686e155218b4ed7a92d89cd89e2f2452c0b13e5333c70100000000feffffff0260e3160000000000160014c772d6f95542e11ef11e8efc7c7a69830ad38a054fa0070000000000160014f4e8dde5db370898b57c84566e3f76098850817d024730440220031910964d9fa84331bcfe78596ca216195f4ae97db1de06cca0e17c6a6695ec0220761e8f7cd7596320588eab8b1c50c3dcb31a8cc36853ea40d348bdc14f93e95f0121030168d9482e2b02d7027fb4a89edc54adaa1adf709334f647d0a1b0533828aec50247304402207e6de93db2b9f50fee095867c607d3f3e10c5a68b529a3819521be3e866c214802205c817cf2625ec88d8b9a177a49ec0816d6b2d8923782249d8cf69554aeae6f17012102a013cf9c4b5f5689d9253036a3e477cf98689626f7814c94f092726f11b741ab00000000",  
"complete": true  
}  
$ hex=02000000000102b8ba04b8ca41918ef58d6254861bc65c4127692ab133d69f119a1f81eb4a3c5b0000000000feffffff95e5748702747cee3446686e155218b4ed7a92d89cd89e2f2452c0b13e5333c70100000000feffffff0260e3160000000000160014c772d6f95542e11ef11e8efc7c7a69830ad38a054fa0070000000000160014f4e8dde5db370898b57c84566e3f76098850817d024730440220031910964d9fa84331bcfe78596ca216195f4ae97db1de06cca0e17c6a6695ec0220761e8f7cd7596320588eab8b1c50c3dcb31a8cc36853ea40d348bdc14f93e95f0121030168d9482e2b02d7027fb4a89edc54adaa1adf709334f647d0a1b0533828aec50247304402207e6de93db2b9f50fee095867c607d3f3e10c5a68b529a3819521be3e866c214802205c817cf2625ec88d8b9a177a49ec0816d6b2d8923782249d8cf69554aeae6f17012102a013cf9c4b5f5689d9253036a3e477cf98689626f7814c94f092726f11b741ab00000000  
$ bitcoin-cli sendrawtransaction $hex  
45f996d4ff8c9e9ab162f611c5b6ad752479ede9780f9903bdc80cd96619676d

You've successfully sent funds using the private keys held on your hardware wallet!

## Learn Other HWI Commands

There are a variety of other commands available for use with HWI. At the time of this writing, they are:

numerate,getmasterxpub,signtx,getxpub,signmessage,getkeypool,getdescriptors,displayaddress,setup,wipe,restore,backup,promptpin,togglepassphrase,sendpin

## Summary: Integrating with Hardware Wallets

Hardware wallets can offer better protection by keeping your private keys offline, protected in the hardware. Fortunately, there's still a way to interact with them using bitcoin-cli. You just install HWI and it will then allow you to (1) import public keys to watch them; and (2) sign transactions using your hardware wallet.

> :fire: _**What's the power of HWI?**_ HWI lets you interact with hardware wallets using all of the commands of bitcoin-cli that you've learned to date. You can make raw transactions of any sort, then send PSBTs to hardware wallets for signing. Thus, you have all of the power of Bitcoin Core, but you also have the security of a hardware device.

## What's Next?

Expand Bitcoin Transactions more with [Chapter Eight: Expanding Bitcoin Transactions in Other Ways](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_0_Expanding_Bitcoin_Transactions_Other.md).

# Chapter Eight: Expanding Bitcoin Transactions in Other Ways

The definition of basic transactions back in [Chapter Six](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_0_Expanding_Bitcoin_Transactions_Multisigs.md) said that they sent _funds_ _immediately_, but those are both elements that can be changed. This final section on Expanding Bitcoin Transactions talks about how to send things other than cash and how to do it at a time other than now.

## Objectives for This Section

After working through this chapter, a developer will be able to:

- Create Transactions with Locktimes
    
- Create Transactions with Data
    

Supporting objectives include the ability to:

- Understand the Different Sorts of Timelocks
    
- Plan for the Power of Locktime
    
- Plan for the Power of OP_RETURN
    

## Table of Contents

- [Section One: Sending a Transaction with a Locktime](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_1_Sending_a_Transaction_with_a_Locktime.md)
    
- [Section Two: Sending a Transaction with Data](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_2_Sending_a_Transaction_with_Data.md)
    

# 8.1: Sending a Transaction with a Locktime

The previous chapters showed two different ways to send funds from multiple machines and to multiple recipients. But there are two other ways to fundamentally change basic transactions. The first of these is to vary time by choosing a locktime. This gives you the ability to send raw transactions at some time in the future.

## Understand How Locktime Works

When you create a locktime transaction, you lock it with a number that represents either a block height (if it's a small number) or a UNIX timestamp (if it's a big number). This tells the Bitcoin network that the transaction may not be put into a block until either the specified time has arrived or the blockchain has reached the specified height.

> :book: _**What is block height?**_ It's the total count of blocks in the chain, going back to the genesis block for Bitcoin.

When a locktime transaction is waiting to go into a block, it can be cancelled. This means that it is far, far from finalized. In fact, the ability to cancel is the whole purpose of a locktime transaction.

> :book: _**What is nLockTime?**_ It's the same thing as locktime. More specifically, it's what locktime is called internal to the Bitcoin Core source code. :book: _**What is Timelock?**_ Locktime is just one way to lock Bitcoin transactions until some point in the future; collectively these methods are called timelocks. Locktime is the most basic timelock method. It locks an entire transaction with an absolute time, and it's available through bitcoin-cli (which is why it's the only timelock covered in this section). A parallel method, which locks a transaction with a relative time, is defined in [BIP 68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki) and covered in [§11.3: Using CSV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md). Bitcoin Script further empowers both sorts of timelocks, allowing for the locking of individual outputs instead of entire transactions. Absolute timelocks (such as Locktime) are linked to the Script opcode OP_CHECKLOCKTIMEVERIFY, which is defined in [BIP 65](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki) and covered in [§11.2: Using CLTV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_2_Using_CLTV_in_Scripts.md), while relative timelocks (such as Timelock) are linked to the Script opcode OP_CHECKSEQUENCEVERIFY, which is defined in [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki) and also covered in [§11.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md).

## Create a Locktime Transaction

In order to create a locktime transaction, you need to first determine what you will set the locktime to.

### Figure Out Your Locktime By UNIX Timestamp

Most frequently you will set the locktime to a UNIX timestamp representing a specific date and time. You can calculate a UNIX timestamp at a web site like [UNIX Time Stamp](http://www.unixtimestamp.com/) or [Epoch Convertor](https://www.epochconverter.com/). However, it would be better to [write your own script](https://www.epochconverter.com/#code) on your local machine, so that you know the UNIX timestamp you receive is accurate. If you don't do that, at least double check on two different sites.

> :book: _**Why Would I Use a UNIX Timestamp?**_ Using a UNIX timestamp makes it easy to definitively link a transaction to a specific time, without worrying about whether the speed of block creation might change at some point. Particularly if you're creating a locktime that's far in the future, it's the safer thing to do. But, beyond that, it's just more intuitive, creating a direct correlation between some calendar date and the time when the transaction can be mined. :warning: **WARNING:** Locktime with UNIX timestamps has a bit of wriggle room: the release of blocks isn't regular and block times can be two hours ahead of real time, so a locktime actually means "within a few hours of this time, plus or minus".

### Figure Out Your Locktime By Block Height

Alternatively, you can set the locktime to a smaller number representing a block height. To calculate your future block height, you need to first know what the current block height is. bitcoin-cli getblockcount will tell you what your local machine thinks the block height is. You may want to double-check with a Bitcoin explorer.

Once you've figured out the current height, you can decide how far in the future to set your locktime to. Remember that on average a new block will be created every 10 minutes. So, for example, if you wanted to set the locktime to a week in the future, you'd choose a block height that is 6 x 24 x 7 = 1,008 blocks in advance of the current one.

> :book: _**Why Would I Use a Blockheight?**_ Unlike with timestamps, there's no fuzziness for blockheights. If you set a blockheight of 120,000 for your locktime, then there's absolutely no way for it to go into block 119,999. This can make it easier to algorithmically control your locktimed transaction. The downside is that you can't be as sure of when precisely the locktime will be. :warning: **WARNING:** If you want to set a block-height locktime, you must set the locktime to less than 500 million. If you set it to 500 million or over, your number will instead be interpreted as a timestamp. Since the UNIX timestamp of 500 million was November 5, 1985, that probably means that your transaction will be put into a block at the miners' first opportunity.

## Write Your Transaction

Once you have figured out your locktime, all you need to do is write up a typical raw transaction, with a third variable for locktime:

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''[{ "'$recipient'": 0.001, "'$changeaddress'": 0.00095 }]''' locktime=1774650)

Note that this usage of locktime is under 500 million, which means that it defines a block height. In this case, it's just a few blocks past the current block height at the time of this writing, meant to exemplify how locktime works without sitting around for a long time to wait and see what happens.

Here's what the created transaction looks like:

$ bitcoin-cli -named decoderawtransaction hexstring=$rawtxhex  
{  
"txid": "ba440b1dd87a7ccb6a200f087d2265992588284eed0ae455d0672aeb918cf71e",  
"hash": "ba440b1dd87a7ccb6a200f087d2265992588284eed0ae455d0672aeb918cf71e",  
"version": 2,  
"size": 113,  
"vsize": 113,  
"weight": 452,  
"locktime": 1774650,  
"vin": [  
{  
"txid": "0ad9fb6992dfe4ea90236b69852b3605c0175633b32996a486dcd0b2e739e385",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.00100000,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 f333554cc0830d03a9c1f26758e2e7e0f155539f",  
"hex": "0014f333554cc0830d03a9c1f26758e2e7e0f155539f",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q7ve42nxqsvxs82wp7fn43ch8urc425ul5um4un"  
]  
}  
},  
{  
"value": 0.00095000,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 a37718a3510958112b6a766e0023ff251b6c2bfb",  
"hex": "0014a37718a3510958112b6a766e0023ff251b6c2bfb",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q5dm33g63p9vpz2m2wehqqglly5dkc2lmtmr98d"  
]  
}  
}  
]  
}

Note that the sequence number (4294967294) is less than 0xffffffff. This is necessary signalling to show that the transaction includes a locktime. It's also done automatically by bitcoin-cli. If the sequence number is instead set to 0xffffffff, your locktime will be ignored.

> :information_source: **NOTE — SEQUENCE:** This is the second use of the nSequence value in Bitcoin. As with RBF, nSequence is again used as an opt-in, this time for the use of locktime. 0xffffffff-1 (4294967294) is the preferred value for signalling locktime because it purposefully disallows the use of both RBF (which requires nSequence < 0xffffffff-1) and relative timelock (which requires nSequence < 0xf0000000), the other two uses of the nSequence value. If you set nSequence lower than 0xf0000000, then you will also relative timelock your transaction, which is probably not what you want. :warning: **WARNING:** If you are creating a locktime raw transaction by some other means than bitcoin-cli, you will have to set the sequence to less than 0xffffffff by hand.

## Send Your Transaction

By now you're probably well familiar with finishing things up:

$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')  
$ bitcoin-cli -named sendrawtransaction hexstring=$signedtx  
error code: -26  
error message:  
non-final

Whoop! What's that error!?

Since 2013, you generally can't place the timelocked transaction into the mempool until its lock has expired. However, you can still hold the transaction, occasionally resending it to the Bitcoin network until it's accepted into the mempool. Alternatively, you could send the signed transaction ($signedtx) to the recipient, so that he could place it in the mempool when the locktime has expired.

Once the locktime is past, anyone can send that signed transaction to the network, and the recipient will receive the money as intended ... provided that the transaction hasn't been cancelled.

## Cancel a Locktime Transaction

Cancelling a locktime transaction is _very_ simple: you send a new transactions using at least one of the same UTXOs.

## Summary: Sending a Transaction with a Locktime

Locktime offers a way to create a transaction that _should_ not be relayable to the network and that _will_ not be accepted into a block until the appropriate time has arrived. In the meantime, it can be cancelled simply by reusing a UTXO.

> :fire: _**What is the Power of Locktime?**_ The power of locktime may not be immediately obvious because of the ability to cancel it so easily. However, it's another of the bases of Smart Contracts: it has a lot of utility in a variety of custodial or contractual applications. For example, consider a situation where a third party is holding your bitcoins. In order to guarantee the return of your bitcoins if the custodian ever disappeared, they could produce a timelock transaction to return the coins to you, then update that every once in a while with a new one, further in the future. If they ever failed to update, then the coins would return to you when the current timelock expired. Locktime could similarly be applied to a payment network, where the network holds coins while they're being exchanged by network participants. Finally, a will offers an example of a more complex contract, where payments are sent out to a number of people. These payments would be built on locktime transactions, and would be continually updated as long as the owner continues to show signs of life. (The unifying factor of all of these applications is, of course, _trust_. Simple locktime transactions only work if the holder of the coins can be trusted to send them out under the appropriate conditions.)

## What's Next?

Continue "Expanding Bitcoin Transactions" with [§8.2: Sending a Transaction with Data](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_2_Sending_a_Transaction_with_Data.md).

# 8.2: Sending a Transaction with Data

The final way to vary how you send a basic transaction is to use the transaction to send data instead of funds (or really, in addition to funds). This gives you the ability to embed information in the blockchain. It is done through a special OP_RETURN command.

The catch? You can only store 80 bytes at a time!

## Create Your Data

The first thing you need to do is create the 80 bytes (or less) of data that you'll be recording in your OP_RETURN. This might be as simple as preparing a message or you might be hashing existing data. For example, sha256sum produces 256 bits of data, which is 32 bytes, well under the limits:

$ sha256sum contract.jpg  
b9f81a8919e5aba39aeb86145c684010e6e559b580a85003ae25d78237a12e75 contract.jpg  
$ op_return_data="b9f81a8919e5aba39aeb86145c684010e6e559b580a85003ae25d78237a12e75"

> :book: _What is an OP_RETURN?_ All Bitcoin transactions are built upon opcode scripts that we'll meet in the next chapter. The OP_RETURN is a simple opcode that defines an OUTPUT as invalid. Convention has resulted in it being used to embed data on the blockchain.

## Prepare Some Money

Your purpose in creating a data transaction isn't to send money to anyone, it's to put data into the blockchain. However, you _must_ send money to do so. You just need to use a change address as your _only_ recipient. Then you can identify a UTXO and send that to your change address, minus a transaction fee, while also using the same transaction to create an OP_RETURN.

Here's the standard setup:

$ bitcoin-cli listunspent  
[  
{  
"txid": "854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42",  
"vout": 0,  
"address": "tb1q6kgsjxuqwj3rwhkenpdfcjccalk06st9z0k0kh",  
"scriptPubKey": "0014d591091b8074a2375ed9985a9c4b18efecfd4165",  
"amount": 0.01463400,  
"confirmations": 1392,  
"spendable": true,  
"solvable": true,  
"desc": "wpkh([d6043800/0'/1'/12']02883bb5463e37d55252d8b3d5c2141b007b37c8a7db6211f75c955acc5ea325eb)#cjr03mru",  
"safe": true  
}  
]

$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ changeaddress=$(bitcoin-cli getrawchangeaddress)

## Write A Raw Transaction

You can now write a new rawtransaction with two outputs: one is your change address to get back (most of) your money, the other is a data address, which is the bitcoin-cli term for an OP_RETURN.

rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "data": "'$op_return_data'", "'$changeaddress'": 0.0146 }''')

Here's what that transaction actually looks like:

{  
"txid": "a600148ac3b05f0c774b8687a71c545077ea5dfb9677e5c6d708215053d892e8",  
"hash": "a600148ac3b05f0c774b8687a71c545077ea5dfb9677e5c6d708215053d892e8",  
"version": 2,  
"size": 125,  
"vsize": 125,  
"weight": 500,  
"locktime": 0,  
"vin": [  
{  
"txid": "854a833b667049ac811b4cf1cad40fa7f8dce8b0f4c1018a58b84559b6e05f42",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00000000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_RETURN b9f81a8919e5aba39aeb86145c684010e6e559b580a85003ae25d78237a12e75",  
"hex": "6a20b9f81a8919e5aba39aeb86145c684010e6e559b580a85003ae25d78237a12e75",  
"type": "nulldata"  
}  
},  
{  
"value": 0.01460000,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 998a9b0ed076bbdec1d88da4f475b9dde75e3620",  
"hex": "0014998a9b0ed076bbdec1d88da4f475b9dde75e3620",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qnx9fkrksw6aaaswc3kj0gademhn4ud3q7cz4fm"  
]  
}  
}  
]  
}

As you can see, this sends the majority of the money straight back to the change address (tb1qnx9fkrksw6aaaswc3kj0gademhn4ud3q7cz4fm) minus a small transaction fee. More importantly, the first output shows an OP_RETURN with the data (b9f81a8919e5aba39aeb86145c684010e6e559b580a85003ae25d78237a12e75) right after it.

## Send A Raw Transaction

Sign your raw transaction and send it, and soon that OP_RETURN will be embedded in the blockchain!

## Check Your OP_RETURN

Again, remember that you can look at this transaction using a blockchain explorer: [https://live.blockcypher.com/btc-testnet/tx/a600148ac3b05f0c774b8687a71c545077ea5dfb9677e5c6d708215053d892e8/](https://live.blockcypher.com/btc-testnet/tx/a600148ac3b05f0c774b8687a71c545077ea5dfb9677e5c6d708215053d892e8/)

You may note a warning about the data being in an "unknown protocol". If you were designing some regular use of OP_RETURN data, you'd probably mark it with a special prefix, to mark that protocol. Then, the actual OP_RETURN data might be something like "CONTRACTS3b110a164aa18d3a5ab064ba93fdce62". This example didn't use a prefix to avoid muddying the data space.

## Summary: Sending a Transaction with Data

You can use an OP_RETURN opcode to store up to 80 bytes of data on the blockchain. You do this with the data codeword for a vout. You still have to send money along too, but you just send it back to a change address, minus a transaction fee.

> :fire: _What is the Power of OP_RETURN?_ The OP_RETURN opens up whole new possibilities for the blockchain, because you can embed data that proves that certain things happened at certain times. Various organizations have used OP_RETURNs for proof of existence, for copyright, for colored coins, and [for other purposes](https://en.bitcoin.it/wiki/OP_RETURN). Though 80 bytes might not seem a lot, it can be quite effective if OP_RETURNs are used to store hashes of the actual data. Then, you can prove the existence of your digital data by demonstrating that the hash of it matches the hash on the blockchain.

Note that there is some controversy over using the Bitcoin blockchain in this way.

## What's Next?

Move on to "Bitcoin Scripting" with [Chapter Nine: Introducing Bitcoin Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_0_Introducing_Bitcoin_Scripts.md).

# Chapter 9: Introducing Bitcoin Scripts

To date, we've been interacting with Bitcoin at a relatively high level of abstraction. The bitcoin-cli program offers access to a variety of RPC commands that support the creation and control of raw Bitcoin transactions that include funds, data, timelocks, and multisigs.

However, Bitcoin offers much more complexity than that. It includes a simple scripting language that can be used to create even more complex redemption conditions. If multisigs and timelocks provided the basis of Smart Contracts, then Bitcoin Script builds high on that foundation. It's the next step in empowering Bitcoin.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Design a Bitcoin Script
    
- Apply a Bitcoin Script
    

Supporting objectives include the ability to:

- Understand the Purpose of Bitcoin Scripts
    
- Understand the P2PKH Script
    
- Understand How P2WPKH Works with Scripting
    
- Understand the Needs for Bitcoin Script Testing
    

## Table of Contents

- [Section One: Understanding the Foundation of Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_1_Understanding_the_Foundation_of_Transactions.md)
    
- [Section Two: Running a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_2_Running_a_Bitcoin_Script.md)
    
- [Section Three: Testing a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_3_Testing_a_Bitcoin_Script.md)
    
- [Section Four: Scripting a P2PKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_4_Scripting_a_P2PKH.md)
    
- [Section Five: Scripting a P2WPKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md)
    

# 9.1: Understanding the Foundation of Transactions

The foundation of Bitcoin is the ability to protect transactions, something that's done with a simple scripting language.

## Know the Parts of the Cryptographic Puzzle

As described in [Chapter 1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/01_0_Introduction.md), the funds in each Bitcoin transaction are locked with a cryptographic puzzle. To be precise, we said that Bitcoin is made up of "a sequence of atomic transactions". We noted that: "Each transaction is authenticated by a sender with the solution to a previous cryptographic puzzle that was stored as a script. The new transaction is locked for the recipient with a new cryptographic puzzle that is also stored as a script." Those scripts, which lock and unlock transactions, are written in Bitcoin Script.

> :book: _**What is Bitcoin Script?**_ Bitcoin Script is a stack-based Forth-like language that purposefully avoids loops and so is not Turing-complete. It's made up of individual opcodes. Every single transaction in Bitcoin is locked with a Bitcoin Script; when the locking transaction for a UTXO is run with the correct inputs, that UTXO can then be spent.

The fact that transactions are locked with scripts means that they can be locked in a variety of different ways, requiring a variety of different keys. In fact, we've met a number of different locking mechanisms to date, each of which used different opcodes:

- OP_CHECKSIG, which checks a public key against a signature, is the basis of the classic P2PKH address, as will be fully detailed in [§9.3: Scripting a P2PKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_4_Scripting_a_P2PKH.md).
    
- OP_CHECKMULTISIG similarly checks multisigs, as will be fully detailed in [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md).
    
- OP_CHECKLOCKTIMEVERIFY and OP_SEQUENCEVERIFY form the basis of more complex Timelocks, as will be fully detailed in [§11.2: Using CLTV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_2_Using_CLTV_in_Scripts.md) and [§11.3: Using CSV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md).
    
- OP_RETURN is the mark of an unspendable transaction, which is why it's used to carry data, as was alluded to in [§8.2: Sending a Transaction with Data](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_2_Sending_a_Transaction_with_Data.md).
    

## Access Scripts In Your Transactions

You may not realize it, but you've already seen these locking and unlocking scripts as part of the raw transactions you've been working with. The best way to look into these scripts in more depth is thus to create a raw transaction, then examine it.

### Create a Test Transaction

To examine real unlocking and locking scripts, create a quick raw transaction by grabbing an unspent Legacy UTXO sitting around, and resending it to a Legacy change address, minus a transaction fee:

$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[1] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[1] | .vout')  
$ recipient=$(bitcoin-cli -named getrawchangeaddress address_type=legacy)  
$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.0009 }''')  
$ signedtx=$(bitcoin-cli -named signrawtransactionwithwallet hexstring=$rawtxhex | jq -r '.hex')

You don't actually need to send it: the goal is simply to produce a complete transaction that you can examine.

> **NOTE:** Why legacy addresses? Because their scripts are more meaningful. However, we'll also offer an example of a native SegWit P2WPKH in [§9.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md).

### Examine Your Test Transaction

You can now examine your transaction in depth by using decoderawtransaction on the $signedtx:

$ bitcoin-cli -named decoderawtransaction hexstring=$signedtx  
{  
"txid": "34151dac704d94a269cd33f80be34c122152edc9bfbb9323852966bf0ce937ed",  
"hash": "34151dac704d94a269cd33f80be34c122152edc9bfbb9323852966bf0ce937ed",  
"version": 2,  
"size": 191,  
"vsize": 191,  
"weight": 764,  
"locktime": 0,  
"vin": [  
{  
"txid": "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa",  
"vout": 0,  
"scriptSig": {  
"asm": "304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c[ALL] 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b",  
"hex": "47304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c01210315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b"  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a91406b5c6ba5330cdf738a2ce91152bfd0e71f9ec3988ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mg8S7F1gY3ivV9M9GrWwe6ziWvK2MFquCf"  
]  
}  
}  
]  
}

The two scripts are found in the two different parts of the transaction.

The scriptSig is located in the vin. This is the _unlocking_ script. It's what's run to access the UTXO being used to fund this transaction. There will be one scriptSig per UTXO in a transaction.

The scriptPubKey is located in the vout. This is the _locking_ script. It's what locks the new output from the transaction. There will be one scriptPubKey per output in a transaction.

> :book: _**How do the scriptSig and scriptPubKey interact?**_ The scriptSig of a transaction unlocks the previous UTXO; this new transaction's output will then be locked with a scriptPubKey, which can in turn be unlocked by the scriptSig of the transaction that reuses that UTXO.

### Read The Scripts in Your Transaction

Look at the two scripts and you'll see that each includes two different representations: the hex is what actually gets stored, but the more readable assembly language (asm) can sort of show you what's going on.

Take a look at the asm of the unlocking script and you'll get your first look at what Bitcoin Scripting looks like:

04402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c[ALL] 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b

As it happens, that mess of numbers is a private-key signature followed by the associated public key. Or at least that's hopefully what it is, because that's what's required to unlock the P2PKH UTXO that this transaction is using.

Read the locking script and you'll see it's a lot more obvious:

OP_DUP OP_HASH160 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 OP_EQUALVERIFY OP_CHECKSIG

That is the standard method in Bitcoin Script for locking a P2PKH transaction.

[§9.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_4_Scripting_a_P2PKH.md) will explain how these two scripts go together, but first you will need to know how Bitcoin Scripts are evaluated.

## Examine a Different Sort of Transaction

Before we leave this foundation behind, we're going to look at a different type of locking script. Here's the scriptPubKey from the multisig transaction that you created in [§6.1: Sending a Transaction with a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md).

  "scriptPubKey": {    
    "asm": "OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL",    
    "hex": "a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387",    
    "reqSigs": 1,    
    "type": "scripthash",    
    "addresses": [    
      "2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr"    
    ]    
  }

Compare that to the scriptPubKey from your new P2PKH transaction:

"scriptPubKey": {    
    "asm": "OP_DUP OP_HASH160 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 OP_EQUALVERIFY OP_CHECKSIG",    
    "hex": "76a91406b5c6ba5330cdf738a2ce91152bfd0e71f9ec3988ac",    
    "reqSigs": 1,    
    "type": "pubkeyhash",    
    "addresses": [    
      "mg8S7F1gY3ivV9M9GrWwe6ziWvK2MFquCf"    
    ]    
  }

These two transactions are _definitely_ locked in different ways. Bitcoin recognises the first as scripthash (P2SH) and the second as pubkeyhash (P2PKH), but you should also be able to see the difference in the different asm code: OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL versus OP_DUP OP_HASH160 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 OP_EQUALVERIFY OP_CHECKSIG. This is the power of scripting: it can very simply produce some of the dramatically different sorts of transactions that you learned about in the previous chapters.

## Summary: Understanding the Foundation of Transactions

Every Bitcoin transaction includes at least one unlocking script (scriptSig), which solves a previous cryptographic puzzle, and at least one locking script (scriptPubKey), which creates a new cryptographic puzzle. There's one scriptSig per input and one scriptPubKey per output. Each of these scripts is written in Bitcoin Script, a Forth-like language that further empowers Bitcoin.

> :fire: _**What is the power of scripts?**_ Scripts unlock the full power of Smart Contracts. With the appropriate opcodes, you can make very precise decisions about who can redeem funds, when they can redeem funds, and how they can redeem funds. More intricate rules for corporate spending, partnership spending, proxy spending, and other methodologies can also be encoded within a Script. It even empowers more complex Bitcoin services such as Lightning and sidechains.

## What's Next?

Continue "Introducing Bitcoin Scripts" with [§9.2: Running a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_2_Running_a_Bitcoin_Script.md).

# 9.2: Running a Bitcoin Script

Bitcoin Scripts may not initially seem that intuitive, but their execution is quite simple, using reverse Polish notation and a stack.

## Understand the Scripting Language

A Bitcoin Script has three parts: it has a line of input; it has a stack for storage; and it has specific commands for execution.

### Understand the Ordering

Bitcoin Scripts are run from left to right. That sounds easy enough, because it's the same way you read. However, it might actually be the most non-intuitive element of Bitcoin Script, because it means that functions don't look like you'd expect. Instead, _the operands go before the operator._

For example, if you were adding together "1" and "2", your Bitcoin Script for that would be 1 2 OP_ADD, _not_ "1 + 2". Since we know that OP_ADD operator takes two inputs, we know that the two inputs before it are its operands.

> :warning: **WARNING:** Technically, everything in Bitcoin Script is an opcode, thus it would be most appropriate to record the above example as OP_1 OP_2 OP_ADD. In our examples, we don't worry about how the constants will be evaluated, as that's a topic of translation, as is explained in [§10.2: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md). Some writers prefer to also leave the "OP" prefix off all operators, but we have opted not to.

### Understand the Stack

It's actually not quite correct to say that an operator applies to the inputs before it. Really, an operator applies to the top inputs in Bitcoin's stack.

> :book: _**What is a stack?**_ A stack is a LIFO (last-in-first-out) data structure. It has two access functions: push and pop. Push places a new object on top of the stack, pushing down everything below it. Pop removes the top object from the stack.

Whenever Bitcoin Script encounters a constant, it pushes it on the stack. So the above example of 1 2 OP_ADD would actually look like this as it was processed:

Script: 1 2 OP_ADD  
Stack: [ ]

Script: 2 OP_ADD  
Stack: [ 1 ]

Script: OP_ADD  
Stack: [ 1 2 ]

_Note that in this and in following examples the top of the stack is to the right and the bottom is to the left._

### Understand the Opcodes

When a Bitcoin Script encounters an operator, it evaluates it. Each operator pops zero or more elements off the stack as inputs, usually one or two. It then processes them in a specific way before pushing zero or more elements back on the stack, usually one or two.

> :book: _**What is an Opcode?**_ Opcode stands for "operation code". It's typically associated with machine-language code, and is a simple function (or "operator").

OP_ADD pops two items off the stack (here: 2 then 1), adds then together, and pushes the result back on the stack (here: 3).

Script:  
Running: 1 2 OP_ADD  
Stack: [ 3 ]

## Build Up Complexity

More complex scripts are created by running more commands in order. They need to be carefully evaluated from left to right, so that you can understand the state of the stack as each new command is run. It will constantly change, as a result of previous operators:

Script: 3 2 OP_ADD 4 OP_SUB  
Stack: [ ]

Script: 2 OP_ADD 4 OP_SUB  
Stack: [ 3 ]

Script: OP_ADD 4 OP_SUB  
Stack: [ 3 2 ]

Script: 4 OP_SUB  
Running: 3 2 OP_ADD  
Stack: [ 5 ]

Script: OP_SUB  
Stack: [ 5 4 ]

Script:  
Running: 5 4 OP_SUB  
Stack: [ 1 ]

## Understand the Usage of Bitcoin Script

That's pretty much Bitcoin Scripting ... other than a few intricacies for how this scripting language interacts with Bitcoin itself.

### Understand scriptSig and scriptPubKey

As we've seen, every input for a Bitcoin transaction contains a scriptSig that is used to unlock the scriptPubKey for the associated UTXO. They are _effectively_ concatenated together, meaning that scriptSig and scriptPubKey are run together, in that order.

So, presume that a UTXO were locked with a scriptPubKey that read OP_ADD 99 OP_EQUAL, requiring as input two numbers that add up to ninety-nine, and presume that the scriptSig of 1 98 were run to unlock it. The two scripts would effectively be run in order as 1 98 OP_ADD 99 OP_EQUAL.

Evaluate the result:

Script: 1 98 OP_ADD 99 OP_EQUAL  
Stack: []

Script: 98 OP_ADD 99 OP_EQUAL  
Stack: [ 1 ]

Script: OP_ADD 99 OP_EQUAL  
Stack: [ 1 98 ]

Script: 99 OP_EQUAL  
Running: 1 98 OP_ADD  
Stack: [ 99 ]

Script: OP_EQUAL  
Stack: [ 99 99 ]

Script:  
Running: 99 99 OP_EQUAL  
Stack: [ True ]

This abstraction isn't quite accurate: for security reasons, the scriptSig is run, then the contents of the stack are transferred for the scriptPubKey to run, but it's accurate enough for understanding how the key of scriptSig fits into the lock of scriptPubKey.

> :warning: **WARNING** The above is a non-standard transaction type. It would not actually be accepted by nodes running Bitcoin Core with the standard settings. [§10.1: Building a Bitcoin Script with P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md) discusses how you actually _could_ run a Bitcoin Script like this, using the power of P2SH.

### Get the Results

Bitcoin will verify a transaction and allow the UTXO to be respent if two criteria are met when running scriptSig and scriptPubKey:

1. The execution did not get marked as invalid at any point, for example with a failed OP_VERIFY or the usage of a disabled opcode.
    
2. The top item in the stack at the end of execution is true (non-zero).
    

In the above example, the transaction would succeed because the stack has a True at its top. But, it would be just as permissible to end with a full stack and the number 42 on top.

## Summary: Running a Bitcoin Script

To process a Bitcoin Script, a scriptSig is run followed by the scriptPubKey that it's unlocking. These commands are run in order, from left to right, with constants being pushed onto a stack and operators popping elements off that stack, then pushing results back onto it. If the Script doesn't halt in the middle and if the item on top of the stack at the end is non-zero, then the UTXO is unlocked.

## What's Next?

Continue "Introducing Bitcoin Scripts" with [§9.3: Testing a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_3_Testing_a_Bitcoin_Script.md).

# 9.3: Testing a Bitcoin Script

Bitcoin Scripting allows for considerable additional control over Bitcoin transactions, but it's also somewhat dangerous. As we'll describe in [§10.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md), the actual Scripts are somewhat isolated from the Bitcoin network, which means that it's possible to write a script and have it accepted by the network even if it's impossible to redeem from that script! So, you need to thoroughly test your Scripts before you put your money into them.

This chapter thus describes a prime method for testing Bitcoin Scripts, which we'll also be using for occasional examples throughout the rest of this section.

## Install btcdeb

The Bitcoin Script Debugger (btcdeb) by @kallewoof is one of the most reliable methods we've found for debugging Bitcoin Scripts. It does, however, require setting up C++ and a few other accessories on your machine, so we'll also offer a few other options toward the end of this chapter.

First, you need to clone the btcdeb GitHub repository, which will also require installing git if you don't yet have it.

$ sudo apt-get install git  
$ git clone [https://github.com/bitcoin-core/btcdeb.git](https://github.com/bitcoin-core/btcdeb.git)

Note that when you run git clone it will copy btcdeb into your current directory. We've chosen to do so in our ~standup directory.

$ ls  
bitcoin-0.20.0-x86_64-linux-gnu.tar.gz btcdeb laanwj-releases.asc SHA256SUMS.asc

Afterward, you must install required C++ and other packages.

$ sudo apt-get install autoconf libtool g++ pkg-config make

You should also install readline, as this makes the debugger a lot easier to use by supporting history using up/down arrows, left-right movement, autocompletion using tab, and other good user interfaces.

$ sudo apt-get install libreadline-dev

You're now ready to compile and install btcdeb:

$ cd btcdeb  
$ ./autogen.sh  
$ ./configure  
$ make  
$ sudo make install

After all of that, you should have a copy of btcdeb:

$ which btcdeb  
/usr/local/bin/btcdeb

## Use btcdeb

btcdeb works like a standard debugger. It takes a script (as well as any number of stack entries) as a startup argument. You then can step through the script.

If you instead start it up with no arguments, you simply get an interpreter where you may issue exec [opcode] commands to perform actions directly.

### Use btcdeb for an Addition Example

The following example shows the use of btcdeb for the addition example from the previous section, 1 2 OP_ADD

$ btcdeb '[1 2 OP_ADD]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
warning: ambiguous input 1 is interpreted as a numeric value; use OP_1 to force into opcode  
warning: ambiguous input 2 is interpreted as a numeric value; use OP_2 to force into opcode  
miniscript failed to parse script; miniscript support disabled  
valid script  
3 op script loaded. type help for usage information  
script | stack  
--------+--------  
1 |  
2 |  
OP_ADD |  
#0000 1

It shows our initial script, running top to bottom, and also shows what will be executed next in the script.

We type step and it advances one step by taking the first item in the script and pushing it onto the stack:

btcdeb> step  
<> PUSH stack 01  
script | stack  
--------+--------  
2 | 01  
OP_ADD |  
#0001 2

And again:

btcdeb> step  
<> PUSH stack 02  
script | stack  
--------+--------  
OP_ADD | 02  
| 01  
#0002 OP_ADD

Now we execute the the OP_ADD and there's great excitement because that opcode pops the first two items off the stack, adds them together, then pushes their sum onto the stack.

btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 03  
script | stack  
--------+--------  
| 03

And that's where our script ends, with nothing more to execute and a 03 sitting on top of our stack as the result of the Script.

> **NOTE:** btcdeb allows you to repeat the previous command by hitting enter. We will be doing this in subsequent examples, so don't be surprised about btcdeb> prompts with nothing as input. It is simply repeating the previous (often step) command.

### Use btcdeb for a Subtraction Example

The previous section also included a slightly more complex subtraction example of Scripting: 3 2 OP_ADD 4 OP_SUB. Here's what that looks like:

$ btcdeb '[3 2 OP_ADD 4 OP_SUB]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
warning: ambiguous input 3 is interpreted as a numeric value; use OP_3 to force into opcode  
warning: ambiguous input 2 is interpreted as a numeric value; use OP_2 to force into opcode  
warning: ambiguous input 4 is interpreted as a numeric value; use OP_4 to force into opcode  
miniscript failed to parse script; miniscript support disabled  
valid script  
5 op script loaded. type help for usage information  
script | stack  
--------+--------  
3 |  
2 |  
OP_ADD |  
4 |  
OP_SUB |  
#0000 3  
btcdeb> step  
<> PUSH stack 03  
script | stack  
--------+--------  
2 | 03  
OP_ADD |  
4 |  
OP_SUB |  
#0001 2  
btcdeb>  
<> PUSH stack 02  
script | stack  
--------+--------  
OP_ADD | 02  
4 | 03  
OP_SUB |  
#0002 OP_ADD  
btcdeb>  
<> POP stack  
<> POP stack  
<> PUSH stack 05  
script | stack  
--------+--------  
4 | 05  
OP_SUB |  
#0003 4  
btcdeb>  
<> PUSH stack 04  
script | stack  
--------+--------  
OP_SUB | 04  
| 05  
#0004 OP_SUB  
btcdeb>  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
script | stack  
--------+--------  
| 01

We'll be returning to btcdeb from time to time, and it will remain an excellent tool for testing your own scripts.

### Use the Power of btcdeb

btcdeb also has a few more powerful functions, such as print and stack, which show you the script and the stack at any time.

For example, in the above script, once you've advanced to the OP_ADD command, you can see the following:

btcdeb> print  
#0000 3  
#0001 2  
-> #0002 OP_ADD  
#0003 4  
#0004 OP_SUB  
btcdeb> stack  
<01> 02 (top)  
<02> 03

Using these commands can make it easier to see what's going on and where you are.

> :warning: **WARNING:** btcdeb is much more complex to use if you are trying to verify signatures. See [Signature Checking with btcdeb](https://github.com/bitcoin-core/btcdeb/blob/master/doc/btcdeb.md#signature-checking). This is true for any script testing, so we don't suggest it if you're trying to verify an OP_CHECKSIG or an OP_CHECKMULTISIG.

## Test a Script Online

There are also a few web simulators that you can use to test scripts online. They can be superior to a command-line tool by offering a more graphical output, but we also find that they tend to have shortcomings.

In the past we've tried to give extensive guidelines on using sites such as the [Script Playground](http://www.crmarsh.com/script-playground/) or the [Bitcoin Online Script Debugger](https://bitcoin-script-debugger.visvirial.com/), but they become out of date and/or disappeared too quickly to keep up with them.

Assume that these debuggers have the nice advantage of showing things visually and explicitly telling you whether a script succeeds (unlocks) or fails (stays locked). Assume that they have disadvantages with signatures, where many of them either always return true for signature tests or else have very cumbersome mechanisms for incorporating them.

## Test a Script with Bitcoin

Even with a great tool like btcdeb or transient resources like the various online script testers, you're not working with the real thing. You can't guarantee that they follow Bitcoin's consensus rules, which means you can't guarantee their results. For example, the Script Playground explicitly says that it ignores a bug that's implicit in Bitcoin multisignatures. This means that any multisig code that you successfully test on the Script Playground will break in the real world.

So the only way to _really_ test Bitcoin Scripts is to try them out on Testnet.

And how do you do that? As it happens that's the topic of [chapter 10](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_0_Embedding_Bitcoin_Scripts_in_P2SH_Transactions.md), which looks into introducing these abstract scripts to the real world of Bitcoin by embedding them in P2SH transactions. (But even then, you will probably need an API to push your P2SH transaction onto the Bitcoin network, so full testing will still be a ways in the future.)

_Whatever_ other testing methods you've used, testing a script on Testnet should be your final test _before_ you put your Script on Mainnet. Don't trust that your code is right; don't just eyeball it. Don't even trust whatever simulators or debuggers you've been using. Doing so is another great way to lose funds on Bitcoin.

## Summary: Testing a Bitcoin Script

You should install btcdeb as a command-line tool to test out your Bitcoin Scripts. As of this writing, it produces accurate results that can step through the entire scripting process. You can also look at some online sites for a more visual representation. When you're all done, you're going to need to go to testnet to make sure things are working accurately, before you deploy more generally.

## What's Next?

Continue "Introducing Bitcoin Scripts" with our first real-life example: [§9.4: Scripting a P2PKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_4_Scripting_a_P2PKH.md).

# 9.4: Scripting a P2PKH

P2PKH addresses are quickly fading in popularity due to the advent of SegWit, but nonetheless they remain a great building block for understanding Bitcoin, and especially for understanding Bitcoin scripts. (We'll take a quick look at how Segwit-native P2WPKH scripts work differently in the next section.)

## Understand the Unlocking Script

We've long said that when funds are sent to a Bitcoin address, they're locked to the private key associated with that address. This is managed through the scriptPubKey of a P2PKH transaction, which is designed such that it requires the recipient to have the private key associated with the the P2PKH Bitcoin address. To be precise, the recipient must supply both the public key linked to the private key and a signature generated by the private key.

Take a look again at the transaction you created in [§9.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_1_Understanding_the_Foundation_of_Transactions.md):

$ bitcoin-cli -named decoderawtransaction hexstring=$signedtx  
{  
"txid": "34151dac704d94a269cd33f80be34c122152edc9bfbb9323852966bf0ce937ed",  
"hash": "34151dac704d94a269cd33f80be34c122152edc9bfbb9323852966bf0ce937ed",  
"version": 2,  
"size": 191,  
"vsize": 191,  
"weight": 764,  
"locktime": 0,  
"vin": [  
{  
"txid": "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa",  
"vout": 0,  
"scriptSig": {  
"asm": "304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c[ALL] 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b",  
"hex": "47304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c01210315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b"  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a91406b5c6ba5330cdf738a2ce91152bfd0e71f9ec3988ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mg8S7F1gY3ivV9M9GrWwe6ziWvK2MFquCf"  
]  
}  
}  
]  
}

You can see that its scriptSig unlocking script has two values. That's a (and an [ALL]) and a :

304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c[ALL] 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b

That's all an unlock script is! (For a P2PKH.)

## Understand the Locking Script

Remember that each unlocking script unlocks a previous UTXO. In the above example, the vin reveals that it's actually unlocking vout 0 of txid bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa.

You can examine that UTXO with gettransaction.

$ bitcoin-cli gettransaction "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa"  
{  
"amount": 0.00095000,  
"confirmations": 12,  
"blockhash": "0000000075a4c1519da5e671b15064734c42784eab723530a6ace83ca1e66d3f",  
"blockheight": 1780789,  
"blockindex": 132,  
"blocktime": 1594841768,  
"txid": "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa",  
"walletconflicts": [  
],  
"time": 1594841108,  
"timereceived": 1594841108,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "mmX7GUoXq2wVcbnrnFJrGKsGR14fXiGbD9",  
"category": "receive",  
"amount": 0.00095000,  
"label": "",  
"vout": 0  
}  
],  
"hex": "020000000001011efcc3bf9950ac2ea08c53b43a0f8cc21e4b5564e205f996f7cadb7d13bb79470000000017160014c4ea10874ae77d957e170bd43f2ee828a8e3bc71feffffff0218730100000000001976a91441d83eaffbf80f82dee4c152de59a38ffd0b602188ac713b10000000000017a914b780fc2e945bea71b9ee2d8d2901f00914a25fbd8702473044022025ee4fd38e6865125f7c315406c0b3a8139d482e3be333727d38868baa656d3d02204b35d9b5812cb85894541da611d5cec14c374ae7a7b8ba14bb44495747b571530121033cae26cb3fa063c95e2c55a94bd04ab9cf173104555efe448b1bfc3a68c8f873342c1b00"  
}

But as you can see, you didn't get the scriptPubKey with gettransaction. You need to take an additional step to retrieve that by examining the raw transaction info (that's the hex) with decoderawtransaction:

$ hex=$(bitcoin-cli gettransaction "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa" | jq -r '.hex')  
$ bitcoin-cli decoderawtransaction $hex  
{  
"txid": "bb4362dec15e67d366088f5493c789f22fb4a604e767dae1f6a631687e2784aa",  
"hash": "6866490b16a92d68179e1cf04380fd08f16ec80bf66469af8d5e78ae624ff202",  
"version": 2,  
"size": 249,  
"vsize": 168,  
"weight": 669,  
"locktime": 1780788,  
"vin": [  
{  
"txid": "4779bb137ddbcaf796f905e264554b1ec28c0f3ab4538ca02eac5099bfc3fc1e",  
"vout": 0,  
"scriptSig": {  
"asm": "0014c4ea10874ae77d957e170bd43f2ee828a8e3bc71",  
"hex": "160014c4ea10874ae77d957e170bd43f2ee828a8e3bc71"  
},  
"txinwitness": [  
"3044022025ee4fd38e6865125f7c315406c0b3a8139d482e3be333727d38868baa656d3d02204b35d9b5812cb85894541da611d5cec14c374ae7a7b8ba14bb44495747b5715301",  
"033cae26cb3fa063c95e2c55a94bd04ab9cf173104555efe448b1bfc3a68c8f873"  
],  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.00095000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_DUP OP_HASH160 41d83eaffbf80f82dee4c152de59a38ffd0b6021 OP_EQUALVERIFY OP_CHECKSIG",  
"hex": "76a91441d83eaffbf80f82dee4c152de59a38ffd0b602188ac",  
"reqSigs": 1,  
"type": "pubkeyhash",  
"addresses": [  
"mmX7GUoXq2wVcbnrnFJrGKsGR14fXiGbD9"  
]  
}  
},  
{  
"value": 0.01063793,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_HASH160 b780fc2e945bea71b9ee2d8d2901f00914a25fbd OP_EQUAL",  
"hex": "a914b780fc2e945bea71b9ee2d8d2901f00914a25fbd87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N9yWARt5E3TQsX2RjsauxSZaEZVhinAS4h"  
]  
}  
}  
]  
}

You can now look at vout 0 and see it was locked with the scriptPubKey of OP_DUP OP_HASH160 41d83eaffbf80f82dee4c152de59a38ffd0b6021 OP_EQUALVERIFY OP_CHECKSIG. That's the standard locking methodology used for an older P2PKH address with the stuck in the middle.

Running it will demonstrate how it works.

## Run a P2PKH Script

When you unlock a P2PKH UTXO, you (effectively) concatenate the unlocking and locking scripts. For a P2PKH address, like the example used in this chapter, that produces:

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG

With that put together, you can examinine how a P2PKH UTXO is unlocked.

First, you put the initial constants on the stack, then make a duplicate of the pubKey with OP_DUP:

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

Script: OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_DUP  
Stack: [ ]

Why the duplicate? Because it's needed to check the two unlocking elements: the public key and the signature.

Next, OP_HASH160 pops the off the stack, hashes it, and puts the result back on the stack.

Script: OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_HASH160  
Stack: [ ]

Then, you place the that was in the locking script on the stack:

Script: OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

OP_EQUALVERIFY is effectively two opcodes: OP_EQUAL, which pops two items from the stack and pushes True or False based on the comparison; and OP_VERIFY which pops that result and immediately marks the transaction as invalid if it's False. (Chapter 12 talks more about the use of OP_VERIFY as a conditional.)

Assuming the two es are equal, you will have the following result:

Script: OP_CHECKSIG  
Running: OP_EQUALVERIFY  
Stack: [ ]

At this point you've proven that the supplied in the scriptSig hashes to the Bitcoin address in question, so you know that the redeemer knew the public key. But, they also need to prove knowledge of the private key, which is done with OP_CHECKSIG, which confirms that the unlocking script's signature matches that public key.

Script:  
Running: OP_CHECKSIG  
Stack: [ True ]

The Script now ends and if it was successful, the transaction is allowed to respend the UTXO in question.

### Use btcdeb for a P2PKH Example

Testing out actual Bitcoin transactions with btcdeb is a bit trickier, because you need to know the public key and a signature to make everything work, and generating the latter is somewhat difficult. However, one way to test things is to let Bitcoin do the work for you in generating a transaction that _would_ unlock a UTXO. That's what you've done above: generating the transaction to spend the UTXO caused bitcoin-cli to calculate the and . You then look at the raw transaction information of the UTXO to learn the locking script including the

You can put together the locking script, the signature, and the pubkey using btcdeb, showing how simple a P2PKH script is.

$ btcdeb '[304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b OP_DUP OP_HASH160 41d83eaffbf80f82dee4c152de59a38ffd0b6021 OP_EQUALVERIFY OP_CHECKSIG]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
unknown key ID 41d83eaffbf80f82dee4c152de59a38ffd0b6021: returning fake key  
valid script  
7 op script loaded. type help for usage information  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b... |  
0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b |  
OP_DUP |  
OP_HASH160 |  
41d83eaffbf80f82dee4c152de59a38ffd0b6021 |  
OP_EQUALVERIFY |  
OP_CHECKSIG |  
|  
|  
#0000 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c

You push the and onto the stack:

btcdeb> step  
<> PUSH stack 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b | 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
OP_DUP |  
OP_HASH160 |  
41d83eaffbf80f82dee4c152de59a38ffd0b6021 |  
OP_EQUALVERIFY |  
OP_CHECKSIG |  
|  
|  
|  
|  
|  
#0001 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
btcdeb> step  
<> PUSH stack 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
OP_DUP | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
OP_HASH160 | 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
41d83eaffbf80f82dee4c152de59a38ffd0b6021 |  
OP_EQUALVERIFY |  
OP_CHECKSIG |  
|  
|  
|  
|  
|  
|  
|

You OP_DUP and OP_HASH the :

#0002 OP_DUP  
btcdeb> step  
<> PUSH stack 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
OP_HASH160 | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
41d83eaffbf80f82dee4c152de59a38ffd0b6021 | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
OP_EQUALVERIFY | 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
OP_CHECKSIG |  
|  
|  
|  
|  
|  
|  
|  
|  
|  
#0003 OP_HASH160  
btcdeb> step  
<> POP stack  
<> PUSH stack 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
41d83eaffbf80f82dee4c152de59a38ffd0b6021 | 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
OP_EQUALVERIFY | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
OP_CHECKSIG | 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
|  
|  
|  
|  
|  
|  
|  
|  
|  
|

You push the from the locking script onto the stack and verify it:

#0004 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
btcdeb> step  
<> PUSH stack 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
OP_EQUALVERIFY | 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
OP_CHECKSIG | 41d83eaffbf80f82dee4c152de59a38ffd0b6021  
| 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
| 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
|  
|  
|  
|  
|  
|  
|  
|  
|  
|  
#0005 OP_EQUALVERIFY  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
<> POP stack  
script | stack  
-------------------------------------------------------------------+-------------------------------------------------------------------  
OP_CHECKSIG | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b  
| 304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b...  
|  
| and_v(  
| sig(304402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c...  
| and_v(  
| pk(0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3...  
| c:pk_h(030500000000000000000000000000000000000000000000...  
| )  
|  
| )  
|

And that point, all that's required is the OP_CHECKSIG:

#0006 OP_CHECKSIG  
btcdeb> step  
error: Signature is found in scriptCode

(Unfortunately this checking may or may not be working at any point due to vagaries of the Bitcoin Core and btcdeb code.)

As is shown, a P2PKH is quite simple: its protection comes about through the strength of its cryptography.

### How to Look Up a Pub Key & Signature by Hand

What if you wanted to generate the and information needed to unlock a UTXO yourself, without leaning on bitcoin-cli to create a transaction?

It turns out that it's pretty easy to get a You just need to use getaddressinfo to examine the address where the UTXO is currently sitting:

$ bitcoin-cli getaddressinfo mmX7GUoXq2wVcbnrnFJrGKsGR14fXiGbD9  
{  
"address": "mmX7GUoXq2wVcbnrnFJrGKsGR14fXiGbD9",  
"scriptPubKey": "76a91441d83eaffbf80f82dee4c152de59a38ffd0b602188ac",  
"ismine": true,  
"solvable": true,  
"desc": "pkh([f004311c/0'/0'/2']0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b)#t3g5mjk9",  
"iswatchonly": false,  
"isscript": false,  
"iswitness": false,  
"pubkey": "0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b",  
"iscompressed": true,  
"ischange": false,  
"timestamp": 1594835792,  
"hdkeypath": "m/0'/0'/2'",  
"hdseedid": "f058372260f71fea37f7ecab9e4c5dc25dc11eac",  
"hdmasterfingerprint": "f004311c",  
"labels": [  
""  
]  
}

Figuring out that signature, however, requires really understanding the nuts and bolts of how Bitcoin transactions are created. So we leave that as advanced study for the reader: creating a bitcoin-cli transaction to "solve" a UTXO is the best solution to that for the moment.

## Summary: Scripting a Pay to Public Key Hash

Sending to a P2PKH address was relatively easy when you were just using bitcoin-cli. Examining the Bitcoin Script underlying it lays bare the cryptographic functions that were implicit in funding that transaction: how the UTXO was unlocked with a signature and a public key.

## What's Next?

Continue "Introducing Bitcoin Scripts" with [§9.5: Scripting a P2WPKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md).

# 9.5: Scripting a P2WPKH

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

P2PKHs are fine for explaining the fundamental way that Bitcoin Scripts work, but what about native SegWit P2WPKH scripts, which are increasingly becoming the majority of Bitcoin transactions? As it turns out, P2WPKH addresses don't use Bitcoin Scripts like traditional Bitcoin addresses do, and so this section is really a digression from the scripting of this chapter — but an important one, because it outlines the _other_ major way in which Bitcoins can be transacted.

## View a P2WPKH Script

It's easy enough to see what a P2WPKH script looks like. The following raw transaction was created by spending a P2WPKH UTXO and then sending the money on to a P2WPKH change address — just as we did with a legacy address in [§9.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_1_Understanding_the_Foundation_of_Transactions.md).

$ bitcoin-cli -named decoderawtransaction hexstring=$signedtx  
{  
"txid": "bdf8f12768a9870d41ac280f8bb4f8ecd9d2fa66fffc75606811f5751c17cb3a",  
"hash": "ec09c84cae48694bec7fd3461b3c5b38a76829c56e9d876037bf2484d443174b",  
"version": 2,  
"size": 191,  
"vsize": 110,  
"weight": 437,  
"locktime": 0,  
"vin": [  
{  
"txid": "3f5417bc7a3a4144d715f3f006d35ea2b405f06091cbb9ce492e04ccefe02b18",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"txinwitness": [  
"3044022064f633ccfc4e937ef9e3edcaa9835ea9a98d31fbea1622c1d8a38d4e7f8f6cb602204bffef45a094de1306f99da055bd5a603a15c277a59a48f40a615aa4f7e5038001",  
"03839e6035b33e37597908c83a2f992ec835b093d65790f43218cb49ffe5538903"  
],  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 92a0db923b3a13eb576a40c4b35515aa30206cba",  
"hex": "001492a0db923b3a13eb576a40c4b35515aa30206cba",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qj2sdhy3m8gf7k4m2grztx4g44gczqm96y6sszv"  
]  
}  
}  
]  
}

There are probably two surprising things here: (1) There's no scriptSig to unlock the previous transaction; and (2) the scriptPubKey to lock the new transaction is just 0 92a0db923b3a13eb576a40c4b35515aa30206cb.

That's, quite simply, because P2WPKH works differently!

## Understand a P2WPKH Transaction

A P2WPKH transaction contains all the same information as a classic P2PKH transaction, but it places it in weird places, not within a traditional Bitcoin Script — and, that's the exact point of SegWit transactions, to pull the "witness" information, which is to say the public keys and signatures, out of the transaction to support a change to block size.

But, if you look carefully, you'll see that the empty scriptSig has been replaced with two entries in a new txinwitness section. If you examine their sizes and formatting, they should seem familiar: they're a signature and public key. Similarly, if you look in the scriptPubKey, you'll see that it's made up of a 0 (actually: OP_0, it's the SegWit version number) and another long number, which is the public-key hash.

Here's a comparison of our two examples: | Type | PubKeyHash | PubKey | Signature | |----------------|----------|-------------|---------| | SegWit | 92a0db923b3a13eb576a40c4b35515aa30206cba | 03839e6035b33e37597908c83a2f992ec835b093d65790f43218cb49ffe5538903 | 3044022064f633ccfc4e937ef9e3edcaa9835ea9a98d31fbea1622c1d8a38d4e7f8f6cb602204bffef45a094de1306f99da055bd5a603a15c277a59a48f40a615aa4f7e5038001 | | non-SegWit | 06b5c6ba5330cdf738a2ce91152bfd0e71f9ec39 | 0315a0aeb37634a71ede72d903acae4c6efa77f3423dcbcd6de3e13d9fd989438b | 04402201cc39005b076cb06534cd084fcc522e7bf937c4c9654c1c9dfba68b92cbab7d1022066f273178febc7a37568e2e9f4dec980a2e9a95441abe838c7ef64c39d85849c |

So how does this work? It depends on old code interpreting this as a valid transaction and new code knowing to check the new "witness" information

### Read a SegWit Script on an Old Machine

If a node has not been upgraded to support SegWit, then it does its usual trick of concatenating the scriptSig and the scriptPubKey. This produces: 0 92a0db923b3a13eb576a40c4b35515aa30206cba (because there's only a scriptPubKey). Running that will produce a stack with everything on it in reverse order:

$ btcdeb '[0 92a0db923b3a13eb576a40c4b35515aa30206cba]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
miniscript failed to parse script; miniscript support disabled  
valid script  
2 op script loaded. type help for usage information  
script | stack  
-----------------------------------------+--------  
0 |  
92a0db923b3a13eb576a40c4b35515aa30206cba |  
#0000 0  
btcdeb> step  
<> PUSH stack  
script | stack  
-----------------------------------------+--------  
92a0db923b3a13eb576a40c4b35515aa30206cba | 0x  
#0001 92a0db923b3a13eb576a40c4b35515aa30206cba  
btcdeb> step  
<> PUSH stack 92a0db923b3a13eb576a40c4b35515aa30206cba  
script | stack  
-----------------------------------------+-----------------------------------------  
| 92a0db923b3a13eb576a40c4b35515aa30206cba  
| 0x

Bitcoin Scripts are considered successful if there's something in the Stack, and it's non-zero, so SegWit scripts automatically succeed on old nodes as long as the scriptPubKey is correctly created with a non-zero pub-key hash. This is called an "anyone-can-spend" transaction, because old nodes verified them as correct without any need for signatures.

> :book: _**Why can't old nodes steal SegWit UTXOs?**_ SegWit was enabled on the Bitcoin network when 95% of miners signalled that they were ready to start using it. That means that only 5% of nodes at that point might have registered anyone-can-spend SegWit transactions as valid without going through the proper work of checking the txinwitness. If they incorrectly incorporated an invalid anyone-can-spend UTXO into a block, the other 95% of nodes would refuse to validate that block, and so it would quickly be orphaned rather than being added to the "main" blockchain. (Certainly, 51% of nodes could choose to stop interpreting SegWit transactions correctly, but 51% of nodes can do anything on a consensus network like a blockchain.)

Because old nodes always see SegWit scripts as correct, they will always verify them, even without understanding their content.

### Read a SegWit Script on a New Machine

A machine that understands how SegWit work does the exact same things that it would with an old P2PKH script, but it doesn't use a script per se: it just knows that it needs to hash the public key in the txinwitness, check that against the hashed key after the version number in the scriptPubKey and then run OP_CHECKSIG on the signature and public key in the txinwitness.

So, it's another way of doing the same thing, but without having the scripts built into the transactions. (The process is built into the node software instead.)

## Summary: Scripting a Pay to Witness Public Key Hash

To a large extent you _don't_ script a P2WPKH. Instead, Bitcoin Core creates the transaction in a different way, placing the witness information in a different place rather than a traditional scriptSig. That means that P2WPKHs are a digression from the Bitcoin Scripts of this part of the book, because they're an expansion of Bitcoin that steps away from traditional Scripting.

However, SegWit was also a clever usage of Bitcoin Scripts. Knowing that there would be nodes that didn't upgrade and needing to stay backward compatible, the developers created the P2WPKH format so that it generated a script that always validated on old nodes (while still having that script provide information to new nodes in the form of a version number and a hashed public key).

When you're programming from the command line, you fundamentally don't have to worry about this, other than knowing that you won't find traditional scripts in raw SegWit transactions (which, again, was the point).

## What's Next?

Continue "Bitcoin Scripting" with [Chapter 10: Embedding Bitcoin Scripts in P2SH Transactions](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_0_Embedding_Bitcoin_Scripts_in_P2SH_Transactions.md).

# Chapter 10: Embedding Bitcoin Scripts in P2SH Transactions

Bitcoin Script moves down several levels of abstraction, allowing you to minutely control the redemption conditions of Bitcoin funds. But, how do you actually incorporate those Bitcoin Scripts into the transactions you've been building to date? The answer is a new sort of Bitcoin transaction, the P2SH.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Design a P2SH Transaction
    
- Apply a P2SH Bitcoin Script
    

Supporting objectives include the ability to:

- Understand the P2SH Script
    
- Understand the Multisig Script
    
- Understand the Various Segwit Variations of Scripts
    
- Understand How to Spend Funds Sent to a P2SH
    

## Table of Contents

- [Section One: Understanding the Foundation of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md)
    
- [Section Two: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md)
    
- [Section Three: Running a Bitcoin Script with P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_3_Running_a_Bitcoin_Script_with_P2SH.md)
    
- [Section Four: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md)
    
- [Section Five: Scripting a Segwit Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_5_Scripting_a_Segwit_Script.md)
    
- [Section Six: Spending a P2SH Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_6_Spending_a_P2SH_Transaction.md)
    

# 10.1: Understanding the Foundation of P2SH

You know that Bitcoin Scripts can be used to control the redemption of UTXOs. The next step is creating Scripts of your own ... but that requires a very specific technique.

## Know the Bitcoin Standards

Here's the gotcha for using Bitcoin Scripts: for security reasons, most Bitcoin nodes will only accept six types of "standard" Bitcoin transactions.

- **Pay to Public Key (P2PK)** — An older, deprecated transaction ( OP_CHECKSIG) that has been replaced by the better security of P2PKH.
    
- **Pay to Public Key Hash (P2PKH)** — A standard transaction (OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG) that pays to the hash of a public key.
    
- **Pay to Witness Public Key hash (P2WPKH)** — The newest sort of public-key transaction. It's just (OP_0 ) because it depends on miner consensus to work, as described in [§9.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md).
    
- **Multisig** — A transaction for a group of keys, as explained more fully in [§10.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md).
    
- **Null Data** — An unspendable transaction (OP_RETURN Data).
    
- **Pay to Script Hash (P2SH)** — A transaction that pays out to a specific script, as explained more fully here.
    

So how do you write a more complex Bitcoin Script? The answer is in that last sort of standard transaction, the P2SH. You can put any sort of long and complex script into a P2SH transaction, and as long as you follow the standard rules for embedding your script and for redeeming the funds, you'll get the full benefits of Bitcoin Scripting.

> :warning: **VERSION WARNING:** Arbitrary P2SH scripts only became standard as of Bitcoin Core 0.10.0. Before that, only P2SH Multisigs were allowed.

## Understand the P2SH Script

You already saw a P2SH transaction when you created a multisig in [§6.1: Sending a Transaction to a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md). Though multisig is one of the standard transaction types, bitcoin-cli simplifies the usage of its multisigs by embedding them into P2SH transactions, as described more fully in [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md).

So, let's look one more time at the scriptPubKey of that P2SH multisig:

  "scriptPubKey": {    
    "asm": "OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL",    
    "hex": "a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387",    
    "reqSigs": 1,    
    "type": "scripthash",    
    "addresses": [    
      "2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr"    
    ]    
  }

The locking script is quite simple looking: OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL. As usual, there's a big chunk of data in the middle. This is a hash of another, hidden locking script (redeemScript) that will only be revealed when the funds are redeemed. In other words, the standard locking script for a P2SH address is: OP_HASH160 OP_EQUAL.

> :book: _**What is a redeemScript?**_ Each P2SH transaction carries the fingerprint of a hidden locking script within it as a 20-byte hash. When a P2SH transaction is redeemed, the full (unhashed) redeemScript is included as part of the scriptSig. Bitcoin will make sure the redeemScript matches the hash; then it actually runs the redeemScript to see if the funds can be spent (or not).

One of the interesting elements of P2SH transactions is that neither the sender nor the Blockchain actually knows what the redeemScript is! A sender just sends to a standardized P2SH address marked with a "2" prefix and they don't worry about how the recipient is going to retrieve the funds at the end.

> :link: **TESTNET vs MAINNET:** on testnet, the prefix for P2SH addresses is 2, while on mainnet, it's 3.

## Understand How to Build a P2SH Script

Since the visible locking script for a P2SH transaction is so simple, creating a transaction of this sort is quite simple too. In theory. All you need to do is create a transaction whose locking script includes a 20-byte hash of the redeemScript. That hashing is done with Bitcoin's standard OP_HASH160.

> :book: _**What is OP_HASH160?**_ The standard hash operation for Bitcoin performs a SHA-256 hash, then a RIPEMD-160 hash.

Overall, four steps are required:

1. Create an arbitrary locking script with Bitcoin Script.
    
2. Create a serialized version of that locking script.
    
3. Perform a SHA-256 hash on those serialized bytes.
    
4. Perform a RIPEMD-160 hash on the results of that SHA-256 hash.
    

Each of those steps of course takes some work on its own, and some of them can be pretty intricate. The good news is that you don't really have to worry about them, because they're sufficiently complex that you'll usually have an API take care of it all for you.

So for now, we'll just provide you with an overview, so that you understand the general methodology. In [§10.2: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md) we'll provide a more in-depth look at script creation, in case you ever want to understand the guts of this process.

## Understand How to Send a P2SH Script Transaction

So how do you actually send your P2SH transaction? Again, the theory is very simple:

1. Embed your hash in a OP_HASH160 OP_EQUAL script.
    
2. Translate that into hexcode.
    
3. Use that hex as your scriptPubKey.
    
4. Create the rest of the transaction.
    

Unfortunately, this is another place where you're going to need to fall back to APIs, in large part because bitcoin-cli doesn't provide any support for creating P2SH transactions. (It can redeem them just fine.)

## Understand How to Unlock a P2SH Script Transaction

The trick to redeeming a P2SH transaction is that the recipient must have saved the secret serialized locking script that was hashed to create the P2SH address. This is called a redeemScript because it's what the recipient needs to redeem his funds.

An unlocking scriptSig for a P2SH transaction is formed as: ... data ... . The data must _solely_ be data that is pushed onto the stack, not operators. ([BIP 16](https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki) calls them signatures, but that's not an actual requirement.)

> :warning: **WARNING:** Though signatures are not a requirement, a P2SH script actually isn't very secure if it doesn't require at least one signature in its inputs. The reasons for this are described in [§13.1: Writing Puzzle Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_1_Writing_Puzzle_Scripts.md).

When a UTXO is redeemed, it runs in two rounds of verification:

1. First, the redeemScript in the scriptSig is hashed and compared to the hashed script in the scriptPubKey.
    
2. If they match, then a second round of verification begins.
    
3. Second, the redeemScript is run using the prior data that was pushed on the stack.
    
4. If that second round of verification _also_ succeeds, the UTXO is unlocked.
    

Whereas you can't easily create a P2SH transaction without an API, you should be able to easily redeem a P2SH transaction with bitcoin-cli. In fact, you already did in [§6.2: Sending a Transaction to a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_2_Spending_a_Transaction_to_a_Multisig.md). The exact process is described in [§10.6: Spending a P2SH Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_6_Spending_a_P2SH_Transaction.md), after we've finished with all the intricacies of P2SH transaction creation.

> :warning: **WARNING:** You can create a perfectly valid transaction with a correcly hashed redeemScript, but if the redeemScript doesn't run, or doesn't run correctly, your funds are lost forever. That's why it is so important to test your Scripts, as discussed in [§9.3: Testing a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_3_Testing_a_Bitcoin_Script.md).

## Summary: Understanding the Foundation of P2SH

Arbitrary Bitcoin Scripts are non-standard in Bitcoin. However, you can incorporate them into standard transactions by using the P2SH address type. You just hash your script as part of the locking script, then you reveal and run it as part of the unlocking script. As long as you can also satisfy the redeemScript, the UTXO can be spent.

> :fire: _**What is the power of P2SH?**_ You already know the power of Bitcoin Script, which allows you to create more complex Smart Contracts of all sorts. P2SH is what actually unleashes that power by letting you include arbitrary Bitcoin Script in standard Bitcoin transactions.

## What's Next?

Continue "Embedding Bitcoin Scripts" with [§10.2: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md).

# 10.2: Building the Structure of P2SH

In the previous section we overviewed the theory of how to create P2SH transactions to hold Bitcoin Scripts. The actual practice of doing so is _much more difficult_, but for the sake of completeness, we're going to look at it here. This is probably not something you'd ever do without an API, so if it gets too intimidating, be aware that we'll be returning to pristine, high-level Scripts in a moment.

## Create a Locking Script

Any P2SH transaction starts with a locking script. This is the subject of chapters 9 and 11-12. You can use any of the Bitcoin Script methods described therein to create any sort of locking script, as long as the resulting serialized redeemScript is 520 bytes or less.

> :book: _**Why are P2SH scripts limited to 520 bytes?**_ As with many things in Bitcoin, the answer is backward compatibility: new functionality has to constantly be built within the old constraints of the system. In this case, 520 bytes is the maximum that can be pushed onto the stack at once. Since the whole redeemScript is pushed onto the stack as part of the redemption process, it hits that limit.

## Serialize a Locking Script the Hard Way

After you create a locking script, you need to serialize it before it can be input into Bitcoin. This is a two-part process. First, you must turn it into hexcode, then you must transform that hex into binary.

### Create the Hex Code

Creating the hexcode that is necessary to serialize a script is both a simple translation and something that is complex enough that it goes beyond any shell script that you're likely to write. This step is one of the main reasons that you need an API to create P2SH transactions.

You create hexcode by stepping through your locking script and turning each element into one-byte hex command, possibly followed by additional data, per the guide at the [Bitcoin Wiki Script page](https://en.bitcoin.it/wiki/Script):

- Operators are translated to the matching byte for that opcode
    
- The constants 1-16 are translated to opcodes 0x51 to 0x61 (OP_1 to OP_16)
    
- The constant -1 is translate to opcode 0x4f (OP_1NEGATE)
    
- Other constants are preceded by opcodes 0x01 to 0x4e (OP_PUSHDATA, with the number specifying how many bytes to push)
    
    - Integers are translated into hex using little-endian signed-magnitude notation
        

### Translate Integers

The integers are the most troublesome part of a locking-script translation.

First, you should verify that your number falls between -2147483647 and 2147483647, the range of four-byte integers when the most significant byte is used for signing.

Second, you need to translate the decimal value into hexadecimal and pad it out to an even number of digits. This can be done with the printf command:

$ integer=1546288031  
$ hex=$(printf '%08x\n' $integer | sed 's/^(00)*//')  
$ echo $hex  
5c2a7b9f

Third, you need to add an additional leading byte of 00 if the top digit is "8" or greater, so that the number is not interpreted as negative.

$ hexfirst=$(echo $hex | cut -c1)  
$ [0x$hexfirst -gt 0x7](https://en.wikipedia.org/wiki/%200x$hexfirst%20-gt%200x7) && hex="00"$hex

Fourth, you need to translate the hex from big-endian (least significant byte last) to little-endian (least significant byte first). You can do this with the tac command:

$ lehex=$(echo $hex | tac -rs .. | echo "$(tr -d '\n')")  
$ echo $lehex  
9f7b2a5c

In addition, you always need to know the size of any data that you put on the stack, so that you can precede it with the proper opcode. You can just remember that every two hexadecimal characters is one byte. Or, you can use echo -n piped to wc -c, and divide that in half:

$ echo -n $lehex | wc -c | awk '{print $1/2}'  
4

With that whole rigamarole, you'd know that you could translate the integer 1546288031 into an 04 opcode (to push four bytes onto the stack) followed by 9f7b2a5c (the little-endian hex representation of 1546288031).

If you instead had a negative number, you would need to (1) do your calculations on the absolute value of the number, then (2) bitwise-or 0x80 to your final, little-endian result. For example, 9f7b2a5c, which is 1546288031, would become 9f7b2adc, which is -1546288031:

$ neglehex=$(printf '%x\n' $((0x$lehex | 0x80)))  
$ echo $neglehex  
9f7b2adc

### Transform the Hex to Binary

To complete your serialization, you translate the hexcode into binary. On the command line, this just requires a simple invocation of xxd -r -p. However, you probably want to do that as part of a a single pipe that will also hash the script ...

## Run The Integer Conversion Script

A complete script for changing an integer between -2147483647 and 2147483647 to a little-endian signed-magnitude representation in hex can be found in the [src code directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/10_2_integer2lehex.sh). You can download it as integer2lehex.sh.

> :warning: **WARNING:** This script has not been robustly checked. If you are going to use it to create real locking scripts you should make sure to double-check and test your results.

Be sure the permissions on the script are right:

$ chmod 755 integer2lehex.sh

You can then run the script as follows:

$ ./integer2lehex.sh 1546288031  
Integer: 1546288031  
LE Hex: 9f7b2a5c  
Length: 4 bytes  
Hexcode: 049f7b2a5c

$ ./integer2lehex.sh -1546288031  
Integer: -1546288031  
LE Hex: 9f7b2adc  
Length: 4 bytes  
Hexcode: 049f7b2adc

## Analyze a P2SH Multisig

To better understand this process, we will reverse-engineer the P2SH multisig that we created in [§6.1: Sending a Transaction to a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md). Take a look at the redeemScript that you used, which you now know is the hex-serialized version of the locking script:

522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae

You can translate this back to Script by hand using the [Bitcoin Wiki Script page](https://en.bitcoin.it/wiki/Script) as a reference. Just look at one byte (two hex characters) of data at a time, unless you're told to look at more by an OP_PUSHDATA command (an opcode in the range of 0x01 to 0x4e).

The whole Script will break apart as follows:

52 / 21 / 02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 / 21 / 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 / 52 / ae

Here's what the individual parts mean:

- 0x52 = OP_2
    
- 0x21 = OP_PUSHDATA 33 bytes (hex: 0x21)
    
- 0x02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 = the next 33 bytes (public key)
    
- 0x21 = OP_PUSHDATA 33 bytes (hex: 0x21)
    
- 0x02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 = the next 33 bytes (public key)
    
- 0x52 = OP_2
    
- 0xae = OP_CHECKMULTISIG
    

In other words, that redeemScript was a translation of of 2 02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 2 OP_CHECKMULTISIG. We'll return to this script in [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md) when we detail exactly how multisigs work within the P2SH paradigm.

If you'd like a mechanical hand with this sort of translation in the future, you can use bitcoin-cli decodescript:

$ bitcoin-cli -named decodescript hexstring=522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae  
{  
"asm": "2 02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 2 OP_CHECKMULTISIG",  
"reqSigs": 2,  
"type": "multisig",  
"addresses": [  
"mmC2x2FoYwBnVHMPRUAzPYg6WDA31F1ot2",  
"mhwZFJUnWqTqy4Y7pXVum88qFtUnVG1keM"  
],  
"p2sh": "2N8MytPW2ih27LctLjn6LfLFZZb1PFSsqBr",  
"segwit": {  
"asm": "0 6fe9f451ccedb8e4090b822dcad973d0388a37b4c89fd1aed485110adecab2a9",  
"hex": "00206fe9f451ccedb8e4090b822dcad973d0388a37b4c89fd1aed485110adecab2a9",  
"reqSigs": 1,  
"type": "witness_v0_scripthash",  
"addresses": [  
"tb1qdl5lg5wvakuwgzgtsgku4ktn6qug5da5ez0artk5s5gs4hk2k25szvjky9"  
],  
"p2sh-segwit": "2NByn92W1vH5oQC1daY69F5sU7PEStKKQBR"  
}  
}

It's especially helpful for checking your work when you're serializing.

## Serialize a Locking Script the Easy Way

When you installed btcdeb in [§9.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_3_Testing_a_Bitcoin_Script.md) you also installed btcc which can be used to serialize Bitcoin scripts:

$ btcc 2 02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 2 OP_CHECKMULTISIG  
warning: ambiguous input 2 is interpreted as a numeric value; use OP_2 to force into opcode  
warning: ambiguous input 2 is interpreted as a numeric value; use OP_2 to force into opcode  
522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae

That's a lot easier than figuring that out by hand!

Also consider the Python [Transaction Script Compiler](https://github.com/Kefkius/txsc), which translates back and forth.

## Hash a Serialized Script

After you've created a locking script and serialized it, the third step in creating a P2SH transaction is to hash the locking script. As previously noted, a 20-byte OP_HASH160 hash is created through a combination of a SHA-256 hash and a RIPEMD-160 hash. Hashing a serialized script thus takes two commands: openssl dgst -sha256 -binary does the SHA-256 hash and outputs a binary to be sent through the pipe, then openssl dgst -rmd160 takes that binary stream, does a RIPEMD-160 hash, and finally outputs a human-readable hexcode.

Here's the whole pipe, including the previous transformation of the hex-serialized script into binary:

$ redeemScript="522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae"  
$ echo -n $redeemScript | xxd -r -p | openssl dgst -sha256 -binary | openssl dgst -rmd160  
(stdin)= a5d106eb8ee51b23cf60d8bd98bc285695f233f3

## Create a P2SH Transaction

Creating your 20-byte hash just gives you the hash at the center of a P2SH locking script. You still need to put it together with the other opcodes that create a standard P2SH transaction: OP_HASH160 a5d106eb8ee51b23cf60d8bd98bc285695f233f3 OP_EQUAL.

Depending on your API, you might be able to enter this as an asm-style scriptPubKey for your transaction, or you might have to translate it to hex code as well. If you have to translate, use the same methods described above for "Creating the Hex Code" (or use btcc), resulting in a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387.

Note that the hex scriptPubKey for P2SH Script transaction will _always_ start with an a914, which is the OP_HASH160 followed by an OP_PUSHDATA of 20 bytes (hex: 0x14); and it will _always_ end with a 87, which is an OP_EQUAL. So all you have to do is put your hashed redeem script in between those numbers.

## Summary: Building the Structure of P2SH

Actually creating the P2SH locking script dives further into the guts of Bitcoin than you've ever gone before. Though it's helpful to know how all of this works at a very low level, it's most likely that you'll have an API taking care of all of the heavy-lifting for you. Your task will simply be to create the Bitcoin Script to do the locking ... which is the main topic of chapters 9 and 11-12.

## What's Next?

Continue "Embedding Bitcoin Scripts" with [§10.3: Running a Bitcoin Script with P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_3_Running_a_Bitcoin_Script_with_P2SH.md).

# 10.3: Running a Bitcoin Script with P2SH

Now that you know the theory and practice behind P2SH addresses, you're ready to turn a non-standard Bitcoin Script into an actual transaction. We'll be reusing the simple locking script from [§9.2: Running a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_2_Running_a_Bitcoin_Script.md), OP_ADD 99 OP_EQUAL.

## Create a P2SH Transaction

To lock a transaction with this Script, do the following:

1. Serialize OP_ADD 99 OP_EQUAL:
    

- OP_ADD = 0x93 — a simple opcode translation
    
- 99 = 0x01, 0x63 — this opcode pushes one byte onto the stack, 99 (hex: 0x63)
    
    - No worries about endian conversion because it's only one byte
        
- OP_EQUAL = 0x87 — a simple opcode translation
    
- = "93016387"
    

$ btcc OP_ADD 99 OP_EQUAL  
93016387

1. Save for future reference as the redeemScript.
    

- = "93016387"
    

1. SHA-256 and RIPEMD-160 hash the serialized script.
    

- = "3f58b4f7b14847a9083694b9b3b52a4cea2569ed"
    

1. Produce a P2SH locking script that includes the .
    

- scriptPubKey = "a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed87"
    

You can then create a transaction using this scriptPubKey, probably via an API.

## Unlock the P2SH Transaction

To unlock this transaction requires that the recipient produce a scriptSig that prepends two constants totalling ninety-nine to the serialized script: 1 98 .

### Run the First Round of Validation

The process of unlocking the P2SH transaction then begins with a first round of validation, which checks that the redeem script matches the hashed value in the locking script.

Concatenate scriptSig and scriptPubKey and execute them, as normal:

Script: 1 98 OP_HASH160 OP_EQUAL  
Stack: []

Script: 98 OP_HASH160 OP_EQUAL  
Stack: [ 1 ]

Script: OP_HASH160 OP_EQUAL  
Stack: [ 1 98 ]

Script: OP_HASH160 OP_EQUAL  
Stack: [ 1 98 ]

Script: OP_EQUAL  
Running: OP_HASH160  
Stack: [ 1 98 ]

Script: OP_EQUAL  
Stack: [ 1 98 ]

Script:  
Running: OP_EQUAL  
Stack: [ 1 98 True ]

The Script ends with a True on top of the stack, and so it succeeds ... even though there's other cruft below it.

However, because this was a P2SH script, the execution isn't done.

### Run the Second Round of Validation

For the second round of validation, verify that the values in the unlocking script satisfy the redeemScript: deserialize the redeemScript ("93016387" = "OP_ADD 99 OP_EQUAL"), then execute it using the items in the scriptSig prior to the serialized script:

Script: 1 98 OP_ADD 99 OP_EQUAL  
Stack: [ ]

Script: 98 OP_ADD 99 OP_EQUAL  
Stack: [ 1 ]

Script: OP_ADD 99 OP_EQUAL  
Stack: [ 1 98 ]

Script: 99 OP_EQUAL  
Running: 1 98 OP_ADD  
Stack: [ 99 ]

Script: OP_EQUAL  
Stack: [ 99 99 ]

Script:  
Running: 99 99 OP_EQUAL  
Stack: [ True ]

With that second validation _also_ true, the UTXO can now be spent!

## Summary: Building a Bitcoin Script with P2SH

Once you know the technique of building P2SHes, any Script can be embedded in a Bitcoin transaction; and once you understand the technique of validating P2SHes, it's easy to run the scripts in two rounds.

## What's Next?

Continue "Embedding Bitcoin Scripts" with [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md).

# 10.4: Scripting a Multisig

Before we close out this intro to P2SH scripting, it's worth examining a more realistic example. Ever since [§6.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md), we've been casually saying that the bitcoin-cli interface wraps its multisig transaction in a P2SH transaction. In fact, this is the standard methodology for creating multisigs on the Blockchain. Here's how that works, in depth.

## Understand the Multisig Code

Multisig transactions are created in Bitcoin using the OP_CHECKMULTISIG code. OP_CHECKMULTISIG expects a long string of arguments that looks like this: 0 ... sigs ... ... public keys ... OP_CHECKMULTISIG. When OP_CHECKMULTISIG is run, it does the following:

1. Pop the first value from the stack ().
    
2. Pop "n" values from the stack as public keys.
    
3. Pop the next value from the stack ().
    
4. Pop "m" values from the stack as potential signatures.
    
5. Pop a 0 from the stack due to a mistake in the original coding.
    
6. Compare the signatures to the public keys.
    
7. Push a True or False depending on the result.
    

The operands of OP_MULTISIG are typically divided, with the 0 and the signatures coming from the unlocking script and the "m", "n", and public keys being detailed by the locking script.

The requirement for that 0 as the first operand for OP_CHECKMULTISIG is a consensus rule. Because the original version of OP_CHECKMULTISIG accidentally popped an extra item off the stack, Bitcoin must forever follow that standard, lest complex redemption scripts from that time period accidentally be broken, rendering old funds unredeemable.

> :book: _**What is a consensus rule?**_ These are the rules that the Bitcoin nodes follow to work together. In large part they're defined by the Bitcoin Core code. These rules include lots of obvious mandates, such as the limit to how many Bitcoins are created for each block and the rules for how transactions may be respent. However, they also include fixes for bugs that have appeared over the years, because once a bug has been introduced into the Bitcoin codebase, it must be continually supported, lest old Bitcoins become unspendable.

## Create a Raw Multisig

As discussed in [§10.1: Understanding the Foundation of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md), multisigs are one of the standard Bitcoin transaction types. A transaction can be created with a locking script that uses the raw OP_CHECKMULTISIG command, and it will be accepted into a block. This is the classic methodology for using multisigs in Bitcoin.

As an example, we will revisit the multisig created in [§6.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md) one final time and build a new locking script for it using this methodology. As you may recall, that was a 2-of-2 multisig built from $pubkey1 and $pubkey2.

As OP_CHECKMULTISIG locking script requires the "m" (2), the public keys, and the "n" (2), you could write the following scriptPubKey:

2 $pubkey1 $pubkey2 2 OP_CHECKMULTISIG

If this looks familiar, that's because it's the multisig that you deserialized in [§10.2: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md).

2 02da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d191 02bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa3 2 OP_CHECKMULTISIG

> **WARNING:** For classic OP_CHECKMULTISIG signatures, "n" must be ≤ 3 for the transaction to be standard.

## Unlock a Raw Multisig

The scriptSig for a standard multisig address must then submit the missing operands for OP_CHECKMULTISIG: a 0 followed by "m" signatures. For example:

0 $signature1 $signature2

### Run a Raw Multisig Script

In order to spend a multisig UTXO, you run the scriptSig and scriptPubKey as follows:

Script: 0 $signature1 $signature2 2 $pubkey1 $pubkey2 2 OP_CHECKMULTISIG  
Stack: [ ]

First, you place all the constants on the stack:

Script: OP_CHECKMULTISIG  
Stack: [ 0 $signature1 $signature2 2 $pubkey1 $pubkey2 2 ]

Then, the OP_CHECKMULTISIG begins to run. First, the "2" is popped:

Running: OP_CHECKMULTISIG  
Stack: [ 0 $signature1 $signature2 2 $pubkey1 $pubkey2 ]

Then, the "2" tells OP_CHECKMULTISIG to pop two public keys:

Running: OP_CHECKMULTISIG  
Stack: [ 0 $signature1 $signature2 2 ]

Then, the next "2" is popped:

Running: OP_CHECKMULTISIG  
Stack: [ 0 $signature1 $signature2 ]

Then, the "2" tells OP_CHECKMULTISIG to pop two signatures:

Running: OP_CHECKMULTISIG  
Stack: [ 0 ]

Then, one more item is mistakenly popped:

Running: OP_CHECKMULTISIG  
Stack: [ ]

Then, OP_CHECKMULTISIG completes its operation by comparing the "m" signatures to the "n" public keys:

Script:  
Stack: [ True ]

## Understand the Limitations of Raw Multisig Scripts

Unfortunately, the technique of embedding a raw multisig into a transaction has some notable drawbacks:

1. Because there's no standard address format for multisigs, each sender has to: enter a long and cumbersome multisig script; have software that allows this; and be trusted not to mess it up.
    
2. Because multisigs can be much longer than typical locking scripts, the blockchain incurs more costs. This requires higher transaction fees from the sender and creates more nuisance for every node.
    

These were generally problems with any sort of complex Bitcoin script, but they quickly became very real problems when applied to multisigs, which were some of the first complex scripts to be widely used on the Bitcoin network. P2SH transactions were created to solve these problems, starting in 2012.

> :book: _**What is a P2SH multisig?**_ P2SH multisigs were the first implementation of P2SH transactions. They simply package up a standard multisig transaction into a standard P2SH transaction. This allows for address standardization; reduces data storage; and increases "m" and "n" counts.

## Create a P2SH Multisig

P2SH multisigs are the modern methodology for creating multisigs on the Blockchain. They can be created very simply, using the same process seen in the previous sections.

### Create the Lock for the P2SH Multisig

To create a P2SH multisig, follow the standard steps for creating a P2SH locking script:

1. Serialize 2 $pubkey1 $pubkey2 2 OP_CHECKMULTISIG.
    

- = "522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae"
    

1. Save for future reference as the redeemScript.
    

- = "522102da2f10746e9778dd57bd0276a4f84101c4e0a711f9cfd9f09cde55acbdd2d1912102bfde48be4aa8f4bf76c570e98a8d287f9be5638412ab38dede8e78df82f33fa352ae"
    

1. SHA-256 and RIPEMD-160 hash the serialized script.
    

- = "a5d106eb8ee51b23cf60d8bd98bc285695f233f3"
    

1. Produce a P2SH Multisig locking script that includes the hashed script (OP_HASH160 OP_EQUAL).
    

- scriptPubKey = "a914a5d106eb8ee51b23cf60d8bd98bc285695f233f387"
    

You can then create a transaction using that scriptPubKey.

## Unlock the P2SH Multisig

To unlock this multisig transaction requires that the recipient produce a scriptSig that includes the two signatures and the redeemScript.

### Run the First Round of P2SH Validation

To unlock the P2SH multisig, first confirm the script:

1. Produce an unlocking script of 0 $signature1 $signature2 .
    
2. Concatenate that with the locking script of OP_HASH160 OP_EQUAL.
    
3. Validate 0 $signature1 $signature2 OP_HASH160 OP_EQUAL.
    
4. Succeed if the matches the .
    

### Run the Second Round of P2SH Validation

Then, run the multisig script:

1. Deserialize to 2 $pubkey1 $pubkey2 2 OP_CHECKMULTISIG.
    
2. Concatenate that with the earlier operands in the unlocking script, 0 $signature1 $signature2.
    
3. Validate 0 $signature1 $signature2 2 $pubkey1 $pubkey2 2 OP_CHECKMULTISIG.
    
4. Succeed if the operands fulfill the deserialized redeemScript.
    

Now you know how the multisig transaction in [§6.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md) was actually created, how it was validated for spending, and why that redeemScript was so important.

## Summary: Creating Multisig Scripts

Multisigs are a standard transaction type, but they're a bit cumbersome to use, so they're regularly incorporated in P2SH transactions, as was the case in [§6.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_1_Sending_a_Transaction_to_a_Multisig.md) when we created our first multisigs. The result is cleaner, smaller, and more standardized — but more importantly, it's a great real-world example of how P2SH scripts really work.

## What's Next?

Continue "Embedding Bitcoin Scripts" with [§10.5: Scripting a Segwit Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_5_Scripting_a_Segwit_Script.md)

# 10.5: Scripting a Segwit Script

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Segwit introduced a number of new options for address (and thus scripting) types. [§9.5: Scripting a P2WPKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md) explained how the new Bech32 address type varied the standard scripts found in most traditional transactions. This chapter looks at the three other sorts of scripts introduced by the Segwit upgrade: the P2SH-Segwit (which was the transitional "nested Segwit" address, as Segwit came into usage), the P2WSH (which is the Segwit equivalent of the P2SH address, just like P2WPKH is the Segwit equivalent of the P2PKH address), and the nested P2WSH address.

This is another situation where you won't really have to worry about these nuances while working with bitcoin-cli, but it's useful to know how it all works.

## Understand a P2SH-Segwit Script

The P2SH-Segwit address is a dying breed. It was basically a stopgap measure while Bitcoin was transitioning to Segwit that allowed a user to create a Segwit address and then have someone with a non-Segwit-enabled exchange or wallet fund that address.

If you ever need to use one, there's an option to create a P2SH-Segwit address using getnewaddress:

$ bitcoin-cli getnewaddress -addresstype p2sh-segwit  
2NEzBvokxh4ME4ahdT18NuSSoYvvhS7EnMU

The address starts with a 2 (or a 3) revealing it as a script

> :book: _**Why can't old nodes send to native Segwit addresses?**_ [§10.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md) noted that there were a set number of "standard" Bitcoin transactions. You can't actually lock a transaction with a script that isn't one of those standard types. Segwit is now recognized as one of those standards, but an old node won't know that, and so it will refuse to send on such a transaction for the protection of the sender. Wrapping a Segwit address inside a standard script hash resolves the problem.

When you look at a UTXO sent to that address, you can see the desc is different, revealing a WPKH address wrapped in a script:

$ bitcoin-cli listunspent  
{  
"txid": "ed752673bfd4338ccf0995983086da846ad652ae0f28280baf87f9fd44b3c45f",  
"vout": 1,  
"address": "2NEzBvokxh4ME4ahdT18NuSSoYvvhS7EnMU",  
"redeemScript": "001443ab2a09a1a5f2feb6c799b5ab345069a96e1a0a",  
"scriptPubKey": "a914ee7aceea0865a05a29a28d379cf438ac5b6cd9c687",  
"amount": 0.00095000,  
"confirmations": 1,  
"spendable": true,  
"solvable": true,  
"desc": "sh(wpkh([f004311c/0'/0'/3']03bb469e961e9a9cd4c23db8442d640d9b0b11702dc0126462ac9eb88b64a4dd48))#p29e839h",  
"safe": true  
}

More importantly, there's a redeemScript, which decodes to OP_0 OP_PUSHDATA (20 bytes) 3ab2a09a1a5f2feb6c799b5ab345069a96e1a0a. This should look familiar, because it's an OP_0 followed by 20-byte hexcode of a public key hash. In other words, a P2SH-SegWit is just a SegWit scriptPubKey jammed into a script. That's all there is to it. It precisely matches how modern multisigs are a multsig placed inside a P2SH, as discussed in [§10.4: Scripting a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_4_Scripting_a_Multisig.md).

Conversely, when we spend this transaction, it looks exactly like a P2SH:

$ bitcoin-cli getrawtransaction ed752673bfd4338ccf0995983086da846ad652ae0f28280baf87f9fd44b3c45f 1  
{  
"txid": "ed752673bfd4338ccf0995983086da846ad652ae0f28280baf87f9fd44b3c45f",  
"hash": "aa4b1c2bde86ea446c9a9db2f77e27421316f26a8d88869f5b195f03b1ac4f23",  
"version": 2,  
"size": 247,  
"vsize": 166,  
"weight": 661,  
"locktime": 1781316,  
"vin": [  
{  
"txid": "59178b02cfcbdee51742a4b2658df35b63b51115a53cf802bc6674fd94fa593a",  
"vout": 1,  
"scriptSig": {  
"asm": "00149ef51fb1f5adb44e20eff758d34ae64fa781fa4f",  
"hex": "1600149ef51fb1f5adb44e20eff758d34ae64fa781fa4f"  
},  
"txinwitness": [  
"3044022069a23fcfc421b44c622d93b7639a2152f941dbfd031970b8cef69e6f8e97bd46022026cb801f38a1313cf32a8685749546a5825b1c332ee4409db82f9dc85d99086401",  
"030aec1384ae0ef264718b8efc1ef4318c513403d849ea8466ef2e4acb3c5ccce6"  
],  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 8.49029534,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 b4b656f4c4b14ee0d098299d1d6eb42d2e22adcd OP_EQUAL",  
"hex": "a914b4b656f4c4b14ee0d098299d1d6eb42d2e22adcd87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2N9ik3zihJ91VGNF55sZFe9GiCAXh2cVKKW"  
]  
}  
},  
{  
"value": 0.00095000,  
"n": 1,  
"scriptPubKey": {  
"asm": "OP_HASH160 ee7aceea0865a05a29a28d379cf438ac5b6cd9c6 OP_EQUAL",  
"hex": "a914ee7aceea0865a05a29a28d379cf438ac5b6cd9c687",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2NEzBvokxh4ME4ahdT18NuSSoYvvhS7EnMU"  
]  
}  
}  
],  
"hex": "020000000001013a59fa94fd7466bc02f83ca51511b5635bf38d65b2a44217e5decbcf028b175901000000171600149ef51fb1f5adb44e20eff758d34ae64fa781fa4ffeffffff029e299b320000000017a914b4b656f4c4b14ee0d098299d1d6eb42d2e22adcd87187301000000000017a914ee7aceea0865a05a29a28d379cf438ac5b6cd9c68702473044022069a23fcfc421b44c622d93b7639a2152f941dbfd031970b8cef69e6f8e97bd46022026cb801f38a1313cf32a8685749546a5825b1c332ee4409db82f9dc85d9908640121030aec1384ae0ef264718b8efc1ef4318c513403d849ea8466ef2e4acb3c5ccce6442e1b00",  
"blockhash": "0000000069cbe44925fab2d472870608c7e1e241a1590fd78be10c63388ed6ee",  
"confirmations": 282952,  
"time": 1595360859,  
"blocktime": 1595360859  
}

Each vout is of the form OP_HASH160 OP_EQUAL. That's a normal P2SH per [§10.2](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/82ca897286aac612804ae849b260750229fa3a52/10_2_Building_the_Structure_of_P2SH.md), which means that it's only when the redeem script is run that the magic occurs. Just as with a P2WPKH, an old node wil see OP_0 OP_PUSHDATA (20 bytes) 3ab2a09a1a5f2feb6c799b5ab345069a96e1a0a in the redeem script and verify it automatically, while a new node will see that, know it's a P2WPKH, and so go out to the witnesses. See [§9.5: Scripting a P2WPKH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_5_Scripting_a_P2WPKH.md).

> :book: _**What are the disadvantages of nested Segwit transactions?**_ They're bigger than native Segwit transactions, so you get some of advantages of Segwit, but not all of them.

## Understand a P2WSH Script

Contrariwise, the P2WSH transactions should be ever-increasing in usage, since they're the native Segwit replacement for P2SH, offering all the same advantages of blocksize that were created with native Segwit P2WPKH transactions.

This is example of P2WSH address: [https://blockstream.info/testnet/address/tb1qrp33g0q5c5txsp9arysrx4k6zdkfs4nce4xj0gdcccefvpysxf3q0sl5k7](https://blockstream.info/testnet/address/tb1qrp33g0q5c5txsp9arysrx4k6zdkfs4nce4xj0gdcccefvpysxf3q0sl5k7)

The details show that a UTXO sent to this address is locked with a scriptPubKey like this:

OP_0 OP_PUSHDATA (32 bytes) 1863143c14c5166804bd19203356da136c985678cd4d27a1b8c6329604903262

This works just like a P2WPKH address, the only difference being that instead of a 20-byte public-key-hash, the UTXO includes a 32-byte script-hash. Just as with a P2WPKH, old nodes just verify this, while new nodes recognize this is a P2WSH and so internally verify the script as described in previous sections, but using the witness data, which now includes the redeem script.

There is also one more variant, a P2WSH script embedded in a P2SH script, which works much like the P2SH-Segwit described above, but for nested P2WSH scripts. (Whew!)

## Summary: Scripting a Segwit Script

There are two sorts of P2SH scripts that relate to Segwit.

The P2SH-Segwit address is a nested Segwit address that embed the simple Segwit scriptPubkey inside a Script, just like multisigs are embedded in scripts nowadays: the Segwit-style key is unwound, and then parsed like normal on a machine that understands Segwit. The purpose is backward compatibility to old nodes that might not otherwise be able to send to native Segwit addresses.

The P2WSH address is a Segwit variant of P2SH, just as P2WPKH is a Segwit variant of P2WSH. It works with the same logic, and is identified by having a 32-byte hash instead of a 20-byte hash. The purpose is to extend the advantages of Segwit to other sorts of scripts.

## What's Next?

Continue "Embedding Bitcoin Scripts" with [§10.6: Spending a P2SH Transaction](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_6_Spending_a_P2SH_Transaction.md).

# 10.6: Spending a P2SH Transaction

Before we close out this overview of P2SH transactions, we're going to touch upon how to spend them. This section is mainly an overview, referring back to a previous section where we _already_ spent a P2SH transaction.

## Use the Redeem Script

As we saw in [§6.2: Spending a Transaction with a Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_2_Spending_a_Transaction_to_a_Multisig.md), spending a P2SH transaction is all about having that serialized version of the locking script, the so-called _redeemScript_. So, the first step in being able to spend a P2SH transaction is making sure that you save the _redeemScript_ before you give out the P2SH address to everyone.

### Collect Your Variables

Because P2SH addresses other than the special multisig and nested Segwit addresses aren't integrated into bitcoin-cli there will be no short-cuts for P2SH spending like you saw in [§6.3: Sending an Automated Multisig](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/06_3_Sending_an_Automated_Multisig.md). You're going to need to collect all the more complex variables on your own!

This means that you need to collect:

- The hex of the scriptPubKey for the transaction you're spending
    
- The serialized redeemScript
    
- Any private keys, since you'll be signing by hand
    
- All of the regular txids, vouts, and addresses that you'd need
    

## Create the Transaction

As we saw in §6.2, the creation of a transaction is pretty standard:

$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.00005}''')  
$ echo $rawtxhex  
020000000121654fa95d5a268abf96427e3292baed6c9f6d16ed9e80511070f954883864b10000000000ffffffff0188130000000000001600142c48d3401f6abed74f52df3f795c644b4398844600000000

However, signing requires entering extra information for the (1) scriptPubKey; (2) the redeemScript; and (3) any required private keys.

Here's the example of doing so for that P2SH-embedded multisig in §6.2:

$ bitcoin-cli -named signrawtransactionwithkey hexstring=$rawtxhex prevtxs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout', "scriptPubKey": "'$utxo_spk'", "redeemScript": "'$redeem_script'" } ]''' privkeys='["cNPhhGjatADfhLD5gLfrR2JZKDE99Mn26NCbERsvnr24B3PcSbtR"]'

With any other sort of P2SH you're going to be including a different redeemscript, but otherwise the practice is exactly the same. The only difference is that after two chapters of work on Scripts you now understand what the scriptPubKey is and what the redeemScript is, so hopefully what were mysterious elements four chapters ago are now old hat.

## Summary: Spending a P2SH Transaction

You already spent a P2SH back in Chapter 6, when you resent a multsig transaction the hard way, which required lining up the scriptPubKey and redeemScript information. Now you know that the scriptPubKey is a standardized P2SH locking script, while the redeemScript matches a hash in that locking script and that you need to be able to run it with the proper variables to receive a True result. But other than knowing more, there's nothing new in spending a P2SH transaction, because you already did it!

## What's Next?

Advance through "Bitcoin Scripting" with [Chapter Eleven: Empowering Timelock with Bitcoin Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_0_Empowering_Timelock_with_Bitcoin_Scripts.md).

# Chapter 11: Empowering Timelock with Bitcoin Scripts

The nLockTime feature from [§8.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_1_Sending_a_Transaction_with_a_Locktime.md) was just the beginning of Timelocks. When you start writing Bitcoin Scripts, two timelocking opcodes become available.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Decide which Timelock to Use
    
- Create Scripts with CLTV
    
- Create Scripts with CSV
    

Supporting objectives include the ability to:

- Understand the Differences Between the Different Timelocks
    
- Generate Relative Times
    

## Table of Contents

- [Section One: Understanding Timelock Options](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_1_Understanding_Timelock_Options.md)
    
- [Section Two: Using CLTV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_2_Using_CLTV_in_Scripts.md)
    
- [Section Three: Using CSV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md)
    

# 11.1: Understanding Timelock Options

In [§8.1: Sending a Transaction with a Locktime](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_1_Sending_a_Transaction_with_a_Locktime.md), nLocktime offered a great first option for locking transactions so that they couldn't be spent until some point in the future — based either on time or blockheight. But, that's not the only way to put a timelock on a transaction.

## Understand the Limitations of nLockTime

nLockTime is a simple and powerful way to lock a transaction, but it has some limitations:

1. **No Divisions.** nLocktime locks the entire transaction.
    
2. **No Networking.** Most modern nodes won't accept a nLockTime into the mempool until it's almost ready to finalize.
    
3. **No Scripts.** The original, simple use of nLockTime didn't allow it to be used in Scripts.
    
4. **No Protection.** nLockTime allows the funds to be spent with a different, non-locked transaction.
    

The last item was often the dealbreaker for nLockTime. It prevented a transaction from being spent, but it didn't prevent the funds from being used in a different transaction. So, it had uses, but they all depended on trust.

## Understand the Possibilities of Timelock Scripts

In more recent years, Bitcoin Core has expanded to allow the manipulation of timelocks at the opcode level with _OP_CHECKLOCKTIMEVERIFY_ (CLTV) and _OP_CHECKSEQUENCEVERIFY_ (CSV). These both work under a new methodology that further empowers Bitcoin.

_They Are Opcodes._ Because they're opcodes, CLTV and CSV can be used as part of more complex redemption conditions. Most often they're linked with the conditionals described in the next chapter.

_They Lock Outputs._ Because they're opcodes that are included in transactions as part of a scriptPubKey, they just lock that single output. That means that the transactions are accepted onto the Bitcoin network and that the UTXOs used to fund those transactions are spent. There's no going back on a transaction timelocked with CLTV or CSV like there is with a bare nLockTime. Respending the resultant UTXO then requires that the timelock conditions be met.

Here's one catch for using timelocks: _They're one-way locks._ Timelocks are designed so that they unlock funds at a certain time. They cannot then relock a fund: once a timelocked fund is available to spend, it remains available to spend.

### Understand the Possibilities of CLTV

_OP_CHECKLOCKTIMEVERIFY_ or CLTV is a match for the classic nLockTime feature, but in the new opcode-based paradigm. It allows a UTXO to become accessible at a certain time or at a certain blockheight.

CLTV was first detailed in [BIP 65](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki).

### Understand the Possibilities of CSV

_OP_CHECKSEQUENCEVERIFY_ or CSV depends on a new sort of "relative locktime", which is set in the transaction's _nSequence_ field. As usual, it can be set as either a time or a blockheight. If it's set as a time, "n", then a relative-timelocked transaction is spendable "n x 512" seconds after its UTXO was mined, and if it's set as a block, "n", then a relative-timelocked transaction is spendable "n" blocks after its UTXO was mined.

The use of nSequence for a relative timelock was first detailed in [BIP 68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki), then the CSV opcode was added in [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki).

## Summary: Understanding Timelock Options

You now have four options for Timelock:

- nLockTime to keep a transaction off the blockchain until a specific time.
    
- nSequence to keep a transaction off the blockchain until a relative time.
    
- CLTV to make a UTXO unspendable until a specific time.
    
- CSV to make a UTXO unspendable until a relative time.
    

## What's Next?

Continue "Empowering Timelock" with [§11.2: Using CLTV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_2_Using_CLTV_in_Scripts.md).

# 11.2: Using CLTV in Scripts

OP_CHECKLOCKTIMEVERIFY (or CLTV) is the natural complement to nLockTime. It moves the idea of locking transactions by an absolute time or blockheight into the realm of opcodes, allowing for the locking of individual UTXOs.

> :warning: **VERSION WARNING:** CLTV became available with Bitcoin Core 0.11.2, but should be fairly widely deployed at this time.

## Remember nLockTime

Before digging into CLTV, we should first recall how nLockTime works.

As detailed in [§8.1: Sending a Transaction with a Locktime](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_1_Sending_a_Transaction_with_a_Locktime.md), locktime is enabled by setting two variables, nLockTime and the nSequence. The nSequence must be set to less than 0xffffffff (usually: 0xffffffff-1), then the nLockTime is interpreted as follows:

- If the nLockTime is less than 500 million, it is interpreted as a blockheight.
    
- If the nLockTime is 500 million or more, it is interpreted as a UNIX timestamp.
    

A transaction with nLockTime set cannot be spent (or even put on the block chain) until either the blockheight or time is reached. In the meantime, the transaction can be cancelled by respending any of the UTXOs that make up the transaction.

## Understand the CLTV Opcode

OP_CHECKLOCKTIMEVERIFY works within the same paradigm of absolute blockheights or absolute UNIX times, but it runs as part of a Bitcoin Script. It reads one argument, which can be a blockheight or an absolute UNIX time. Through a somewhat convoluted methodology, it compares that argument to the current time. If it's too early, the script fails; if the time condition has been met, the script carries on.

Because CLTV is just part of a script (and presumably part of a P2SH transaction), a CLTV transaction is not kept out of the mempool like an nLockTime transaction is; as soon as it's verified, it goes onto the blockchain, and the funds are considered spent. The trick is that all the outputs that were locked with the CLTV aren't available for _respending_ until the CLTV allows it.

### Understand a CLTV Absolute Time

This is how OP_CHECKLOCKTIMEVERIFY would be used to check against May 24, 2017:

1495652013 OP_CHECKLOCKTIMEVERIFY

But we'll usually depict this in an abstraction like this:

OP_CHECKLOCKTIMEVERIFY

Or this:

OP_CHECKLOCKTIMEVERIFY

### Understand a CLTV Absolute Block Height

This is how OP_CHECKLOCKTIMEVERIFY would check against a blockheight that was reached on May 24, 2017:

467951 OP_CHECKLOCKTIMEVERIFY

But we'll usually abtract it like this:

OP_CHECKLOCKTIMEVERIFY

### Understand How CLTV Really Works

The above explanation is sufficient to use and understand CLTV. However, [BIP 65](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki) lays out all the details.

A locking script will only allow a transaction to respend a UTXO locked with a CLTV if OP_CHECKLOCKTIMEVERIFY verifies all of the following:

- The nSequence field must be set to less than 0xffffffff, usually 0xffffffff-1 to avoid confilcts with relative timelocks.
    
- CLTV must pop an operand off the stack and it must be 0 or greater.
    
- Both the stack operand and nLockTime must either be above or below 500 million, to depict the same sort of absolute timelock.
    
- The nLockTime value must be greater than or equal to the stack operand.
    

So the first thing to note here is that nLockTime is still used with CLTV. To be precise, it's required in the transaction that tries to _respend_ a CLTV-timelocked UTXO. That means that it's not a part of the script's requirements. It's just the timer that's used to release the funds, _as defined in the script_.

This is managed through a clever understanding of how nLockTime works: a value for nLockTime must always be chosen that is less than or equal to the present time (or blockheight), so that the respending transaction can be put on the blockchain. However, due to CLTV's requirements, a value must also be chosen that is greater than or equal to CLTV's operand. The union of these two sets is NULL until the present time matches the CLTV operand. Afterward, any value can be chosen between CLTV's operand and the present time. Usually, you'd just set it to the present time (or block).

## Write a CLTV Script

OP_CHECKLOCKTIMEVERIFY includes an OP_VERIFY, which means that it will immediately halt the script if its verification does not succeed. It has one other quirk: unlike most "verify" commands, it leaves what it's testing on the stack (just in case you want to make any other checks against the time). This means that an OP_CHECKLOCKTIMEVERIFY is usually followed by an OP_DROP to clear the stack.

The following simple locking script could be used to transform a P2PKH output to a timelocked-P2PKH transaction:

OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG

### Encode a CLTV Script

Of course, as with any complex Bitcoin Scripts, this CLTV script would actually be encoded in a P2SH script, as explained in [§10.1: Understanding the Foundation of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_1_Understanding_the_Foundation_of_P2SH.md) and [§10.2: Building the Structure of P2SH](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md).

Assuming that were the integer "1546288031" (little-endian hex: 0x9f7b2a5c) and were "371c20fb2e9899338ce5e99908e64fd30b789313", this redeemScript would be built as:

OP_PUSHDATA (4 bytes) 0x9f7b2a5c OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 OP_PUSHDATA (20 bytes) 0x371c20fb2e9899338ce5e99908e64fd30b789313 OP_EQUALVERIFY OP_CHECKSIG

Which translates into hex as:

04 9f7b2a5c b1 75 76 a9 14 371c20fb2e9899338ce5e99908e64fd30b789313 88 ac

Or if you prefer:

$ btcc 0x9f7b2a5c OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 0x371c20fb2e9899338ce5e99908e64fd30b789313 OP_EQUALVERIFY OP_CHECKSIG  
049f7b2a5cb17576a914371c20fb2e9899338ce5e99908e64fd30b78931388ac

The decodescript RPC can verify that we got it right:

{  
"asm": "1546288031 OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 371c20fb2e9899338ce5e99908e64fd30b789313 OP_EQUALVERIFY OP_CHECKSIG",  
"type": "nonstandard",  
"p2sh": "2MxANZMPo1b2jGaeKTv9rwcBEiXcXYCc3x9",  
"segwit": {  
"asm": "0 07e55bf1eaedf43ec52af57b77ad7330506c209a70d17fa2e1853304aa8e4e5b",  
"hex": "002007e55bf1eaedf43ec52af57b77ad7330506c209a70d17fa2e1853304aa8e4e5b",  
"reqSigs": 1,  
"type": "witness_v0_scripthash",  
"addresses": [  
"tb1qqlj4hu02ah6ra3f274ah0ttnxpgxcgy6wrghlghps5esf25wfedse4yw4w"  
],  
"p2sh-segwit": "2N4HTwMjVdm38bdaQ5h3X3VktLY74D2qBoK"  
}  
}

We're not going to continuously show how all Bitcoin Scripts are encoded into P2SH transactions, but will instead offer these shorthands: when we describe a script, it will be a redeemScript, which would normally be serialized and hashed in a locking script and serialized in the unlocking script; when we show an unlocking procedure, it will be the second round of validation, following the confirmation of the locking script hash.

## Spend a CLTV UTXO

In order to spend a UTXO that is locked with a CLTV, you must set nLockTime on your new transaction. Usually, you just want to set it to the present time or the present block, as appropriate. As long the CLTV time or blockheight is in the past, and as long as you supply any other data required by the unlocking script, you'll be able to process the UTXO.

In the case of the above example, the following unlocking script would suffice, provided that nLockTime was set to somewhere in advance of the date, and provided it was indeed at least :

### Run a CLTV Script

To run the Script, you would first concatenate the unlocking and locking scripts:

Script: OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

The three constants would be pushed onto the stack:

Script: OP_CHECKLOCKTIMEVERIFY OP_DROP OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

Then, OP_CHECKLOCKTIMEVERIFY runs. It finds something on the stack and verifies that nSequence isn't 0xffffffff. Finally, it compares with nLockTime. If they are both the same sort of representation and if nLockTime ≥ , then it successfully processes (else, it ends the script):

Script: OP_DROP OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_CHECKLOCKTIMEVERIFY  
Stack: [ ]

Then, OP_DROP gets rid of that left around:

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_DROP  
Stack: [ ]

Finally, the remainder of the script runs, which is a normal check of a signature and public key.

## Summary: Using CLTV in Scripts

OP_CHECKLOCKTIMEVERIFY is a simple opcode that looks at a single argument, interprets it as a blockheight or UNIX timestamp, and only allows its UTXO to be unlocked if that blockheight or UNIX timestamp is in the past. Setting nLockTime on the spending transaction is what allows Bitcoin to make this calculation.

> :fire: _**What is the Power of CLTV?**_ You've already seem that simple locktimes were one of the bases of Smart Contracts. CLTV takes the next step. Now you can both guarantee that a UTXO can't be spent before a certain time _and_ guarantee that it won't be spent either. In its simplest form, this could be used to create a trust that someone could only access when they reached 18 or a retirement fund that they could only access when they turned 50. However its true power comes when combined with conditionals, where the CLTV only activates in certain situations.

## What's Next?

Continue "Empowering Timelock" with [§11.3: Using CSV in Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/11_3_Using_CSV_in_Scripts.md).

# 11.3: Using CSV in Scripts

nLockTime and OP_CHECKLOCKTIMEVERIFY (or CLTV) are just one side of the timelock equation. On the other side are nSequence and OP_CHECKSEQUENCEVERIFY, which can be used to check against relative times rather than absolute times.

> :warning: **VERSION WARNING:** CSV became available with Bitcoin Core 0.12.1, in spring 2016.

## Understand nSequence

Every input into a transaction has an nSequence (or if you prefer sequence) value. It's been a prime tool for Bitcoin expansions as discussed previously in [§5.2: Resending a Transaction with RBF](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/05_2_Resending_a_Transaction_with_RBF.md) and [§8.1 Sending a Transaction with a Locktime](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/08_1_Sending_a_Transaction_with_a_Locktime.md), where it was used to signal RBF and nLockTime, respectively. However, there's one more use for nSequence, described by [BIP 68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki): you can use it to create a relative timelock on a transaction.

A relative timelock is a lock that's placed on a specific input of a transaction and that's calculated in relation to the mining date of the UTXO being used in the input. For example, if a UTXO was mined at block #468260 and a transaction was created where the input for that UTXO was given an nSequence of 100, then the new transaction could not be mined until at least block #468360.

Easy!

> :information_source: **NOTE — SEQUENCE:** This is the third use of the nSequence value in Bitcoin. Any nSequence value without the 32nd bit set (1<<31), so 0x00 00 00 01 to 0x7f ff ff ff, will be interpreted as a relative timelock if nVersion ≥ 2 (which is the default starting in Bitcoin Core 0.14.0). You should be careful to ensure that relative timelocks don't conflict with the other two uses of nSequence, for signalling nLockTime and RBF. nLockTime usually sets a value of 0xff ff ff ff-1, where a relative timelock is disallowed; and RBF usually sets a value of "1", where a relative timelock is irrelevent, because it defines a timelock of 1 block. In general, remember: with a nVersion value of 2, a nSequence value of 0x00000001 to 0x7ffffff allows relative timelock, RBF, and nTimeLock; a nSequence value of 0x7fffffff to 0xffffffff-2 allows RBF and nTimeLock; a nSequence value of 0xffffffff-1 allows only nTimeLock; a nSequence value of 0xffffffff allows none; and nVersion can be set to 1 to disallow relative timelocks for any value of nSequence. Whew!

### Create a CSV Relative Block Time

The format for using nSequence to represent relative time locks is defined in [BIP 68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki) and is slightly more complex than just inputting a number, like you did for nLockTime. Instead, the BIP specifications breaks up the four byte number into three parts:

- The first two bytes are used to specify a relative locktime.
    
- The 23rd bit is used to positively signal if the lock refers to a time rather than a blockheight.
    
- The 32nd bit is used to positively signal if relative timelocks are deactivated.
    

With that said, the construction of a block-based relative timelock is still quite easy, because the two flagged bits are set to 0, so you just set nSequence to a value between 1 and 0xff ff (65535). The new transaction can be mined that number of blocks after the associated UTXO was mined.

### Create a CSV Relative Time

You can instead set nSequence as a relative time, where the lock lasts for 512 seconds times the value of nSequence.

In order to do that:

1. Decide how far in the future to set your relative timelock.
    
2. Convert that to seconds.
    
3. Divide by 512.
    
4. Round that value up or down and set it as nSequence.
    
5. Set the 23rd bit to true.
    

To set a time 6 months n the future, you must first calculate as follows:

$ seconds=$((6_30_24_60_60))  
$ nvalue=$(($seconds/512))

Then, turn it into hex:

$ hexvalue=$(printf '%x\n' $nvalue)

Finally, bitwise-or the 23rd bit into the hex value you created:

$ relativevalue=$(printf '%x\n' $((0x$hexvalue | 0x400000)))  
$ echo $relativevalue  
4076a7  
$ printf "%d\n" "0x$relativevalue"  
4224679

If you convert that back you'll see that 4224679 = 10000000111011010100111. The 23rd digit is set to a "1"; meanwhile the first 2 bytes, 0111011010100111, convert to 76A7 in hex or 30375 in decimal. Multiply that by 512 and you get 15.55 million seconds, which indeed is 180 days.

## Create a Transaction with a Relative Timelock

So you want to create a simple transaction with a relative timelock? All you have to do is issue a transaction where the nSequence in an input is set as shown above: with the nSequence for that input set such that the first two bytes define the timelock, the 23rd bit defines the type of timelock, and the 32nd bit is set to false.

Issue the transaction and you'll see that it can't legally be mined until enough blocks or enough time has passed beyond the time that the UTXO was mined.

Except pretty much no one does this. The [BIP 68](https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki) definitions for nSequence were incorporated into Bitcoin Core at the same time as [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki). which describes the CSV opcode, the nSequence equivalent to the CLTV opcode. Just like CLTV, CSV offers increased capabilities. So, almost all usage of relative timelocks has been with the CSV opcode, not with the raw nSequence value on its own.

  
|Absolute Timelock|Relative Timelock||
|---|---|---|
|**Lock Transaction**|nLockTime|nSequence|
|**Lock Output**|OP_CHECKLOCKTIMEVERIFY|OP_CHECKSEQUENCEVERIFY|

  
  

## Understand the CSV Opcode

OP_SEQUENCEVERIFY in Bitcoin Scripts works pretty much like OP_LOCKTIMEVERIFY.

You might require a UTXO be held for a hundred blocks past its mining:

100 OP_CHECKSEQUENCEVERIFY

Or your might make a more complex calculation to require that a UTXO be held for six months, in which case you'll end up with a more complex number:

4224679 OP_CHECKSEQUENCEVERIFY

In this case we'll use a shorthand:

<+6Months> OP_CHECKSEQUENCEVERIFY

> :warning: **WARNING:** Remember that a relative timelock is a time span since the mining of the UTXO used as an input. It is _not_ a timespan after you create the transaction. If you use a UTXO that's already been confirmed a hundred times, and you place a relative timelock of 100 blocks on it, it will be eligible for mining immediately. Relative timelocks have some very specific uses, but they probably don't apply if your only goal is to determine some set time in the future.

### Understand How CSV Really Works

CSV has many of the same subtleties in usage as CLTV:

- The nVersion field must be set to 2 or more.
    
- The nSequence field must be set to less than 0x80000000.
    
- When CSV is run, there must be an operand on the stack that's between 0 and 0xf0 00 00 00-1.
    
- Both the stack operand and nSequence must have the same value on the 23rd bit.
    
- The nSequence must be greater than or equal to the stack operand.
    

Just as with CLTV, when you are respending a UTXO with a CSV in its locking conditions, you must set the nSequence to enable the transaction. You'll usually set it to the exact value in the locking script.

## Write a CSV Script

Just like OP_CHECKLOCKTIMEVERIFY, OP_CHECKSEQUENCEVERIFY includes an implicit OP_VERIFY and leaves its arguments on the stack, requiring an OP_DROP when you're all done.

A script that would lock funds until six months had passed following the mining of the input, and that would then require a standard P2PKH-style signature would look as follows:

<+6Months> OP_CHECKSEQUENCEVERIFY OP_DROP OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG

### Encode a CSV Script

When you encode a CSV script, be careful how you encode the integer value for the relative locktime. It should be passed as a 3-byte integer, which means that you're ignoring the top byte, which could inactivate the relative locktime. Since it's an integer, be sure you convert it to little-endian.

This can be done with the integer2lehex.sh shell script from the previous chapter.

For a relative time of 100 blocks:

$ ./integer2lehex.sh 100  
Integer: 100  
LE Hex: 64  
Length: 1 bytes  
Hexcode: 0164

Though that should be padded out to 000064, requiring a code of 03000064.

For a relative time of 6 months:

$ ./integer2lehex.sh 4224679  
Integer: 4224679  
LE Hex: a77640  
Length: 3 bytes  
Hexcode: 03a77640

## Spend a CSV UTXO

To spend a UTXO locked with a CSV script, you must set the nSequence of that input to a value greater than the requirement in the script, but less than the time between the UTXO and the present block. Yes, this means that you need to know the exact requirement in the locking script ... but you have a copy of the redeemScript, so if you don't know the requirements, you deserialize it, and then set the nSequence to the number that's shown there.

## Summary: Using CSV in Scripts

nSequence and CSV offer an alternative to nLockTime and CLTV where you lock a transaction based on a relative time since the input was mined, rather than basing the lock on a set time in the future. They work almost identically, other than the fact that the nSequence value is encoded slightly differently than the nLockTime value, with specific bits meaning specific things.

> :fire: _**What is the power of CSV?**_ CSV isn't just a lazy way to lock, when you don't want to calculate a time in the future. Instead, it's a totally different paradigm, a lock that you would use if it was important to create a specific minimum duration between when a transaction is mined and when its funds can be respent. The most obvious usage is (once more) for an escrow, when you want a precise time between the input of funds and their output. However, it has much more powerful possibilities in off-chain transactions, including payment channels. These applications are by definition built on transactions that are not actually put onto the blockchain, which means that if they are later put on the blockchain an enforced time-lapse can be very helpful. [Hashed Timelock Contracts](https://en.bitcoin.it/wiki/Hashed_Timelock_Contracts) have been one such implementation, empowering the Lightning payment network. They're discussed in [§13.3: Empowering Bitcoin with Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_3_Empowering_Bitcoin_with_Scripts.md).

## What's Next?

Advance through "Bitcoin Scripting" with [Chapter Twelve: Expanding Bitcoin Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/12_0_Expanding_Bitcoin_Scripts.md).

# Chapter 12: Expanding Bitcoin Scripts

There's still a little more to Bitcoin Scripts. Conditionals give you full access to flow control, while a variety of other opcodes can expand your possibilities.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Decide How to Use Script Conditionals
    
- Decide How to Use Other Script Opcodes
    

Supporting objectives include the ability to:

- Understand the Full Range of Scripting Possibilities
    
- Identify How to Learn More about Opcodes
    

## Table of Contents

- [Section One: Using Script Conditionals](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/12_1_Using_Script_Conditionals.md)
    
- [Section Two: Using Other Script Commands](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/12_2_Using_Other_Script_Commands.md)
    

# 12.1: Using Script Conditionals

There's one final aspect of Bitcoin Scripting that's crucial to unlocking its true power: conditionals allow you create various paths of execution.

## Understand Verify

You've already seen one conditional in scripts: OP_VERIFY (0x69). It pops the top item on the stack and sees if it's true; if not _it ends execution of the script_.

Verify is usually incorporated into other opcodes. You've already seen OP_EQUALVERIFY (0xad), OP_CHECKLOCKTIMEVERIFY (0xb1), and OP_CHECKSEQUENCEVERIFY (0xb2). Each of these opcodes does its core action (equal, checklocktime, or checksequence) and then does a verify afterward. The other verify opcodes that you haven't seen are: OP_NUMEQUALVERIFY (0x9d), OP_CHECKSIGVERIFY (0xad), and OP_CHECKMULTISIGVERIFY (0xaf).

So how is OP_VERIFY a conditional? It's the most powerful sort of conditional. Using OP_VERIFY, _if_ a condition is true, the Script continues executing, _else_ the Script exits. This is how you check conditions that are absolutely required for a Script to succeed. For example, the P2PKH script (OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG) has two required conditions: (1) that the supplied public key match the public-key hash; and (2) that the supplied signature match that public key. An OP_EQUALVERIFY is used for the comparison of the hashed public key and the public-key hash because it's an absolutely required condition. You don't _want_ the script to continue on if that fails.

You may notice there's no OP_VERIFY at the end of this (or most any) script, despite the final condition being required as well. That's because Bitcoin effectively does an OP_VERIFY at the very end of each Script, to ensure that the final stack result is true. You don't _want_ to do an OP_VERIFY before the end of the script, because you need to leave something on the stack to be tested!

## Understand If/Then

The other major conditional in Bitcoin Script is the classic OP_IF (0x63) / OP_ELSE (0x67) / OP_ENDIF (0x68). This is typical flow control: if OP_IF detects a true statement, it executes the block under it; otherwise, if there's an OP_ELSE, it executes that; and OP_ENDIF marks the end of the final block.

> :warning: **WARNING:** These conditionals are technically opcodes too, but as with small numbers, we're going to leave the OP_ prefix off for brevity and clarity. Thus we'll write IF, ELSE, and ENDIF instead of OP_IF, OP_ELSE, and OP_ENDIF.

### Understand If/Then Ordering

There are two big catches to conditionals. They make it harder to read and assess scripts if you're not careful.

First, the IF conditional checks the truth of what's _before it_ (which is to say what's in the stack), not what's after it.

Second, the IF conditional tends to be in the locking script and what it's checking tends to be in the unlocking script.

Of course, you might say, that's how Bitcoin Script works. Conditionals use reverse Polish notation and they adopt the standard unlocking/locking paradigm, just like _everything else_ in Bitcoin Scripting. That's all true, but it also goes contrary to the standard way we read IF/ELSE conditionals in other programming languages; thus, it's easy to unconsciously read Bitcoin conditionals wrong.

Consider the following code: IF OP_DUP OP_HASH160 ELSE OP_DUP OP_HASH160 ENDIF OP_EQUALVERIFY OP_CHECKSIG .

Looking at conditionals in prefix notation might lead you to read this as:

IF (OP_DUP) THEN

OP_HASH160     
OP_PUSHDATA <pubKeyHashA>   

ELSE

OP_DUP     
OP_HASH160     
OP_PUSHDATA <pubKeyHashB>   

ENDIF

OP_EQUALVERIFY  
OP_CHECKSIG

So, you might think, if the OP_DUP is successful, then we get to do the first block, else the second. But that doesn't make any sense! Why wouldn't the OP_DUP succeed?!

And, indeed, it doesn't make any sense, because we accidentally read the statement using the wrong notation. The correct reading of this is:

IF

OP_DUP    
OP_HASH160     
OP_PUSHDATA <pubKeyHashA>   

ELSE

OP_DUP     
OP_HASH160     
OP_PUSHDATA <pubKeyHashB>   

ENDIF

OP_EQUALVERIFY  
OP_CHECKSIG

The statement that will evaluate to True or False is placed on the stack _prior_ to running the IF, then the correct block of code is run based on that result.

This particular example code is intended as a poor man's 1-of-2 multisignature. The owner of would put True in his unlocking script, while the owner of would put False in her unlocking script. That trailing True or False is what's checked by the IF/ELSE statement. It tells the script which public-key hash to check against, then the OP_EQUALVERIFY and the OP_CHECKSIG at the end do the real work.

### Run an If/Then Multisig

With a core understanding of Bitcoin conditionals in hand, we're now ready to run through a script. We're going to do so by creating a slight variant of our poor man's 1-of-2 multisignature where our users don't have to remember if they're True or False. Instead, if need be, the script checks both public-key hashes, just requiring one success:

OP_DUP OP_HASH160 OP_EQUAL  
IF

OP_CHECKSIG  

ELSE

OP_DUP OP_HASH160 <pubKeyHashB> OP_EQUALVERIFY OP_CHECKSIG  

ENDIF

Remember your reverse Polish notation! That IF statement is referring to the OP_EQUAL before it, not the OP_CHECKSIG after it!

#### Run the True Branch

Here's how it actally runs if unlocked with :

Script: OP_DUP OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

First, we put constants on the stack:

Script: OP_DUP OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

Then we run the first few, obvious commands, OP_DUP and OP_HASH160 and push another constant:

Script: OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_DUP  
Stack: [ ]

Script: OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_HASH160  
Stack: [ ]

Script: OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

Next we run the OP_EQUAL, which is what's going to feed the IF:

Script: IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_EQUAL  
Stack: [ True ]

Now the IF runs, and since there's a True, it only runs the first block, eliminating all the rest:

Script: OP_CHECKSIG  
Running: True IF  
Stack: [ ]

And the OP_CHECKSIG will end up True as well:

Script:  
Running: OP_CHECKSIG  
Stack: [ True ]

#### Run the False Branch

Here's how it actually runs if unlocked with :

Script: OP_DUP OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

First, we put constants on the stack:

Script: OP_DUP OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

Then we run the first few, obvious commands, OP_DUP and OP_HASH160 and push another constant:

Script: OP_HASH160 OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_DUP  
Stack: [ ]

Script: OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_HASH160  
Stack: [ ]

Script: OP_EQUAL IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Stack: [ ]

Next we run the OP_EQUAL, which is what's going to feed the IF:

Script: IF OP_CHECKSIG ELSE OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG ENDIF  
Running: OP_EQUAL  
Stack: [ False ]

Whoop! The result was False because does not equal . Now when the IF runs, it collapses down to just the ELSE statement:

Script: OP_DUP OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Running: False IF  
Stack: [ ]

Afterward, we go through the whole rigamarole again, starting with another OP_DUP, but eventually testing against the other pubKeyHash:

Script: OP_HASH160 OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_DUP  
Stack: [ ]

Script: OP_EQUALVERIFY OP_CHECKSIG  
Running: OP_HASH160  
Stack: [ ]

Script: OP_EQUALVERIFY OP_CHECKSIG  
Stack: [ ]

Script:OP_CHECKSIG  
Running: OP_EQUALVERIFY  
Stack: [ ]

Script:  
Running: OP_CHECKSIG  
Stack: [ True ]

This probably isn't nearly as efficient as a true Bitcoin multisig, but it's a good example of how results pushed onto the stack by previous tests can be used to feed future conditionals. In this case, it's the failure of the first signature which tells the conditional that it should go check the second one.

## Understand Other Conditionals

There are a few other conditionals of note. The big one is OP_NOTIF (0x64), which is the opposite of OP_IF: it executes the following block if the top item is False. An ELSE can be placed with it, which as usual is executed if the first block is not executed. You still end with OP_ENDIF.

There's also an OP_IFDUP (0x73), which duplicates the top stack item only if it's not 0.

These options are used much less often than the main IF/ELSE/ENDIF construction.

## Summary: Using Script Conditionals

Conditionals in Bitcoin Script allow you to halt the script (using OP_VERIFY) or to choose different branches of execution (using OP_IF). However, reading OP_IF can be a bit tricky. Remember that it's the item pushed onto the stack _before_ the OP_IF is run that controls its execution; that item will typically be part of the unlocking script (or else a direct result of items in the unlocking script).

> :fire: _**What is the power of conditionals?**_ Script Conditionals are the final major building block in Bitcoin Script. They're what are required to turn simple, static Bitcoin Scripts into complex, dynamic Bitcoin Scripts that can evaluate differently based on different times, different circumstances, or different user inputs. In other words, they're the final basis of smart contracts.

## What's Next?

Continue "Expanding Bitcoin Scripts" with [§12.2: Using Other Script Commands](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/12_2_Using_Other_Script_Commands.md).

# 12.2: Using Other Script Commands

You may already have in hand most of the Bitcoin Script opcodes that you'll be using in most scripts. However, Bitcoin Script offers a lot more options, which might be exactly what you need to create the financial instrument of your dreams.

You should consult the [Bitcoin Script page](https://en.bitcoin.it/wiki/Script) for a more thorough look at all of these and many other commands. This section only highlights the most notable opcodes.

## Understand Arithmetic Opcodes

Arithmetic opcodes manipulate or test numbers.

Manipulate one number:

- OP_1ADD (0x8b) — Increment by one
    
- OP_1SUB (0x8c) — Decrement by one
    
- OP_NEGATE (0x8f) — Flip the sign of the number
    
- OP_ABS (0x90) — Make the number positive
    
- OP_NOT (0x91) — Flips 1 and 0, else 0
    

Also see: OP_0NOTEQUAL (0x92)

Manipulate two numbers mathematically:

- OP_ADD (0x93) — Add two numbers
    
- OP_SUB (0x94) — Subtract two numbers
    
- OP_MIN (0xa3) — Return the smaller of two numbers
    
- OP_MAX (0xa4) — Return the larger of two numbers
    

Manipulate two numbers logically:

- OP_BOOLAND (0x9a) — 1 if both numbers are not 0, else 0
    
- OP_BOOLOR (0x9b) — 1 if either number is not 0, else 0
    

Test two numbers:

- OP_NUMEQUAL (0x9c) — 1 if both numbers are equal, else 0
    
- OP_LESSTHAN (0x9f) — 1 if first number is less than second, else 0
    
- OP_GREATERTHAN (0xa0) — 1 if first number is greater than second, else 0
    
- OP_LESSTHANOREQUAL (0xa1) — 1 if first number is less than or equal to second, else 0
    
- OP_GREATERTHANOREQUAL (0xa2) — 1 if first number is greater than or equal to second, else 0
    

Also see: OP_NUMEQUALVERIFY (0x9d), OP_NUMNOTEQUAL (0x9e)

Test three numbers:

- OP_WITHIN (0xa5) — 1 if a number is in the range of two other numbers
    

## Understand Stack Opcodes

There are a shocking number of stack opcodes, but other than OP_DROP, OP_DUP, and sometimes OP_SWAP they're generally not necessary if you're careful about stack ordering. Nonetheless, here are a few of the more interesting ones:

- OP_DEPTH (0x74) — Pushes the size of the stack
    
- OP_DROP (0x75) — Pops the top stack item
    
- OP_DUP (0x76) — Duplicates the top stack item
    
- OP_PICK (0x79) — Duplicates the nth stack item as the top of the stack
    
- OP_ROLL (0x7a) — Moves the nth stack item to the top of the stack
    
- OP_SWAP (0x7c) — Swaps the top two stack items
    

Also see: OP_TOALTSTACK (0x6b), OP_FROMALTSTACK (0x6c), OP_2DROP (0x6d), OP_2DUP (0x6e), OP_3DUP (0x6f), OP_2OVER (0x70), OP_2ROT (0x71), OP_2SWAP (0x72), OP_IFDUP (0x73), OP_NIP (0x77), OP_OVER (0x78), OP_ROT (0x7b), and OP_TUCK (0x7d).

## Understand Cryptographic Opcodes

Finally, a variety of opcodes support hashing and signature checking:

Hash:

- OP_RIPEMD160 (0xa6) — RIPEMD-160
    
- OP_SHA1 (0xa7) — SHA-1
    
- OP_SHA256 (0xa8) - SHA-256
    
- OP_HASH160 (0xa9) — SHA-256 + RIPEMD-160
    
- OP_HASH256 (0xaa) — SHA-256 + SHA-256
    

Check Signatures:

- OP_CHECKSIG (0xac) — Check a signature
    
- OP_CHECKMULTISIG (0xae) — Check a m-of-n multisig
    

Also see: OP_CODESEPARATOR (0xab), OP_CHECKSIGVERIFY (0xad), and OP_CHECKMULTISIGVERIFY (0xaf).

## Summary: Using Other Script Commands

Bitcoin Script includes a wide array of arithmetic, stack, and cryptographic opcodes. Most of these additional opcodes are probably not as common as the ones discussed in previous sections, but nonetheless they're available if they're just what you need to write your Script!

## What's Next?

Advance through "Bitcoin Scripting" with [Chapter Thirteen: Designing Real Bitcoin Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_0_Designing_Real_Bitcoin_Scripts.md).

# Chapter 13: Designing Real Bitcoin Scripts

Our Bitcoin Scripts to date have been largely theoretical examples, because we've still been putting together the puzzle pieces. Now, with the full Bitcoin Script repertoire in hand, we're ready to dig into several real-world Bitcoin Scripts and see how they work.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Assess Real-World Bitcoin Scripts
    
- Create Real-World Bitcoin Scripts
    

Supporting objectives include the ability to:

- Understand Existing Bitcoin Scripts
    
- Understand the Importance of Signatures
    

## Table of Contents

- [Section One: Writing Puzzles Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_1_Writing_Puzzle_Scripts.md)
    
- [Section Two: Writing Complex Multisig Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_2_Writing_Complex_Multisig_Scripts.md)
    
- [Section Three: Empowering Bitcoin with Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_3_Empowering_Bitcoin_with_Scripts.md)
    

# 13.1: Writing Puzzle Scripts

Bitcoin Scripts _don't_ actually have to depend on the knowledge of a secret key. They can instead be puzzles of any sort.

## Write Simple Algebra Scripts

Our first real Script, from [§9.2: Running a Bitcoin Script](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/09_2_Running_a_Bitcoin_Script.md) was an alegbraic puzzle. That Bitcoin Script, OP_ADD 99 OP_EQUAL, could have been alternatively described as x + y = 99.

This sort of Script doesn't have a lot of applicability in the real world, as it's too easy to claim the funds. But, a puzzle-solving contest giving out Bitcoin dust might offer it as a fun entertainment.

More notably, creating alegebraic puzzles gives you a nice understanding of how the arithmetic functions in Bitcoin Script work.

### Write a Multiplier Script

Bitcoin Script has a number of opcodes that were disabled to maintain the security of the system. One of the is OP_MUL, which would have allowed multiplication ... but is instead disabled.

So, how would you write an algebraic function like 3x + 7 = 13?

The most obvious answer is to OP_DUP the number input from the locking script twice. Then you can push the 7 and keep adding until you get your total. The full locking script would look like this: OP_DUP OP_DUP 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL.

Here's how it would run if executed with the correct unlocking script of 2:

Script: 2 OP_DUP OP_DUP 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL  
Stack: [ ]

Script: OP_DUP OP_DUP 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL  
Stack: [ 2 ]

Script: OP_DUP 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL  
Running: 2 OP_DUP  
Stack: [ 2 2 ]

Script: 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL  
Running: 2 OP_DUP  
Stack: [ 2 2 2 ]

Script: OP_ADD OP_ADD OP_ADD 13 OP_EQUAL  
Stack: [ 2 2 2 7 ]

Script: OP_ADD OP_ADD 13 OP_EQUAL  
Running: 2 7 OP_ADD  
Stack: [ 2 2 9 ]

Script: OP_ADD 13 OP_EQUAL  
Running: 2 9 OP_ADD  
Stack: [ 2 11 ]

Script: 13 OP_EQUAL  
Running: 2 11 OP_ADD  
Stack: [ 13 ]

Script: OP_EQUAL  
Stack: [ 13 13 ]

Script:  
Running: 13 13 OP_EQUAL  
Stack: [ True ]

Or if you prefer btcdeb:

$ btcdeb '[2 OP_DUP OP_DUP 7 OP_ADD OP_ADD OP_ADD 13 OP_EQUAL]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
valid script  
9 op script loaded. type help for usage information  
script | stack  
---------+--------  
2 |  
OP_DUP |  
OP_DUP |  
7 |  
OP_ADD |  
OP_ADD |  
OP_ADD |  
13 |  
OP_EQUAL |

#0000 2  
btcdeb> step  
<> PUSH stack 02  
script | stack  
---------+--------  
OP_DUP | 02  
OP_DUP |  
7 |  
OP_ADD |  
OP_ADD |  
OP_ADD |  
13 |  
OP_EQUAL |

#0001 OP_DUP  
btcdeb> step  
<> PUSH stack 02  
script | stack  
---------+--------  
OP_DUP | 02  
7 | 02  
OP_ADD |  
OP_ADD |  
OP_ADD |  
13 |  
OP_EQUAL |

#0002 OP_DUP  
btcdeb> step  
<> PUSH stack 02  
script | stack  
---------+--------  
7 | 02  
OP_ADD | 02  
OP_ADD | 02  
OP_ADD |  
13 |  
OP_EQUAL |

#0003 7  
btcdeb> step  
<> PUSH stack 07  
script | stack  
---------+--------  
OP_ADD | 07  
OP_ADD | 02  
OP_ADD | 02  
13 | 02  
OP_EQUAL |

#0004 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 09  
script | stack  
---------+--------  
OP_ADD | 09  
OP_ADD | 02  
13 | 02  
OP_EQUAL |

#0005 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 0b  
script | stack  
---------+--------  
OP_ADD | 0b  
13 | 02  
OP_EQUAL |

#0006 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 0d  
script | stack  
---------+--------  
13 | 0d  
OP_EQUAL |  
#0007 13  
btcdeb> step  
<> PUSH stack 0d  
script | stack  
---------+--------  
OP_EQUAL | 0d  
| 0d

#0008 OP_EQUAL  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
script | stack  
---------+--------  
| 01

### Write an Equation System

What if you wanted to instead write an equation system, such as x + y = 3, y + z = 5, and x + z = 4? A bit of algebra tells you that the answers come out to x = 1, y = 2, and z = 3. But, how do you script it?

Most obviously, after the redeemer inputs the three numbers, you're going to need two copies of each number, since each number goes into two different equations. OP_3DUP takes care of that and results in x y z x y z being on the stack. Popping off two items at a time will give you y z, z x, and x y. Voila! That's the three equations, so you just need to add them up and test them in the right order! Here's the full script: OP_3DUP OP_ADD 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL.

Here's how it runs with the correct unlocking script of 1 2 3:

Script: 1 2 3 OP_3DUP OP_ADD 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Stack: [ ]

Script: OP_3DUP OP_ADD 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Stack: [ 1 2 3 ]

Script: OP_ADD 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Running: 1 2 3 OP_3DUP  
Stack: [ 1 2 3 1 2 3 ]

Script: 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Running: 2 3 OP_ADD  
Stack: [ 1 2 3 1 5 ]

Script: OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Stack: [ 1 2 3 1 5 5 ]

Script: OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Running: 5 5 OP_EQUALVERIFY  
Stack: [ 1 2 3 1 ] — Does Not Exit

Script: 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Running: 3 1 OP_ADD  
Stack: [ 1 2 4 ]

Script: OP_EQUALVERIFY OP_ADD 3 OP_EQUAL  
Stack: [ 1 2 4 4 ]

Script: OP_ADD 3 OP_EQUAL  
Running: 4 4 OP_EQUALVERIFY  
Stack: [ 1 2 ] — Does Not Exit

Script: 3 OP_EQUAL  
Running: 1 2 OP_ADD  
Stack: [ 3 ]

Script: OP_EQUAL  
Stack: [ 3 3 ]

Script:  
Running: 3 3 OP_EQUAL  
Stack: [ True ]

Here it is in btcdeb:

$ btcdeb '[1 2 3 OP_3DUP OP_ADD 5 OP_EQUALVERIFY OP_ADD 4 OP_EQUALVERIFY OP_ADD 3 OP_EQUAL]'  
btcdeb 0.2.19 -- type btcdeb -h for start up options  
valid script  
13 op script loaded. type help for usage information  
script | stack  
---------------+--------  
1 |  
2 |  
3 |  
OP_3DUP |  
OP_ADD |  
5 |  
OP_EQUALVERIFY |  
OP_ADD |  
4 |  
OP_EQUALVERIFY |  
OP_ADD |  
3 |  
OP_EQUAL |

#0000 1  
btcdeb> step  
<> PUSH stack 01  
script | stack  
---------------+--------  
2 | 01  
3 |  
OP_3DUP |  
OP_ADD |  
5 |  
OP_EQUALVERIFY |  
OP_ADD |  
4 |  
OP_EQUALVERIFY |  
OP_ADD |  
3 |  
OP_EQUAL |

#0001 2  
btcdeb> step  
<> PUSH stack 02  
script | stack  
---------------+--------  
3 | 02  
OP_3DUP | 01  
OP_ADD |  
5 |  
OP_EQUALVERIFY |  
OP_ADD |  
4 |  
OP_EQUALVERIFY |  
OP_ADD |  
3 |  
OP_EQUAL |

#0002 3  
btcdeb> step  
<> PUSH stack 03  
script | stack  
---------------+--------  
OP_3DUP | 03  
OP_ADD | 02  
5 | 01  
OP_EQUALVERIFY |  
OP_ADD |  
4 |  
OP_EQUALVERIFY |  
OP_ADD |  
3 |  
OP_EQUAL |

#0003 OP_3DUP  
btcdeb> step  
<> PUSH stack 01  
<> PUSH stack 02  
<> PUSH stack 03  
script | stack  
---------------+--------  
OP_ADD | 03  
5 | 02  
OP_EQUALVERIFY | 01  
OP_ADD | 03  
4 | 02  
OP_EQUALVERIFY | 01  
OP_ADD |  
3 |  
OP_EQUAL |

#0004 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 05  
script | stack  
---------------+--------  
5 | 05  
OP_EQUALVERIFY | 01  
OP_ADD | 03  
4 | 02  
OP_EQUALVERIFY | 01  
OP_ADD |  
3 |  
OP_EQUAL |

#0005 5  
btcdeb> step  
<> PUSH stack 05  
script | stack  
---------------+--------  
OP_EQUALVERIFY | 05  
OP_ADD | 05  
4 | 01  
OP_EQUALVERIFY | 03  
OP_ADD | 02  
3 | 01  
OP_EQUAL |

#0006 OP_EQUALVERIFY  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
<> POP stack  
script | stack  
---------------+--------  
OP_ADD | 01  
4 | 03  
OP_EQUALVERIFY | 02  
OP_ADD | 01  
3 |  
OP_EQUAL |

#0007 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 04  
script | stack  
---------------+--------  
4 | 04  
OP_EQUALVERIFY | 02  
OP_ADD | 01  
3 |  
OP_EQUAL |

#0008 4  
btcdeb> step  
<> PUSH stack 04  
script | stack  
---------------+--------  
OP_EQUALVERIFY | 04  
OP_ADD | 04  
3 | 02  
OP_EQUAL | 01

#0009 OP_EQUALVERIFY  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
<> POP stack  
script | stack  
---------------+--------  
OP_ADD | 02  
3 | 01  
OP_EQUAL |

#0010 OP_ADD  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 03  
script | stack  
---------------+--------  
3 | 03  
OP_EQUAL |

#0011 3  
btcdeb> step  
<> PUSH stack 03  
script | stack  
---------------+--------  
OP_EQUAL | 03  
| 03

#0012 OP_EQUAL  
btcdeb> step  
<> POP stack  
<> POP stack  
<> PUSH stack 01  
script | stack  
---------------+--------  
| 01

> :warning: **WARNING** btcdeb isn't just useful for providing visualization of these scripts, but to also double-check the results. Sure enough, we got this one wrong the first time, testing the equations in the wrong order. That's how easy it is to make a financially fatal mistake in a Bitcoin Script, and that's why every script must be tested.

## Write Simple Computational Scripts

Though puzzle scripts are trivial, they can actually have real-world usefulness if you want to crowdsource a computation. You simply create a script that requires the answer to the computation and you send funds to the P2SH address as a reward. It'll stay there until someone comes up with the answer.

For example, Peter Todd [offered rewards](https://bitcointalk.org/index.php?topic=293382.0) for solving equations that demonstrate collisions for standard cryptographic algorithms. Here was his script for confirming a SHA1 collision: OP_2DUP OP_EQUAL OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL. It requires two inputs, which will be the two numbers that collide.

Here's how it runs with correct answers.

First, we fill in our stack:

Script: OP_2DUP OP_EQUAL OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Stack: [ ]

Script: OP_2DUP OP_EQUAL OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Stack: [ ]

Script: OP_EQUAL OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Running: OP_2DUP  
Stack: [ ]

Then, we make sure the two numbers aren't equal, exiting if they are:

Script: OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Running: OP_EQUAL  
Stack: [ False ]

Script: OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Running: False OP_NOT  
Stack: [ True ]

Script: OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL  
Running: True OP_VERIFY  
Stack: [ ] — Does Not Exit

We now create two SHAs:

Script: OP_SWAP OP_SHA1 OP_EQUAL  
Running: OP_SHA1  
Stack: [ ]

Script: OP_SHA1 OP_EQUAL  
Running: OP_SWAP  
Stack: [ ]

Script: OP_EQUAL  
Running: OP_SHA1  
Stack: [ ]

Finally, we see if they match.

Script:  
Running: OP_EQUAL  
Stack: [ True ]

This is a nice script because it shows careful use of logic (with the OP_NOT and the OP_VERIFY) and good use of stack functions (with the OP_SWAP). It's all around a great example of a real-world function. And it is very real-world. When [SHA-1 was broken](https://shattered.io/), 2.48 BTC were quickly liberated from the address, with a total value of about $3,000 at the time.

btcdeb can be run to prove the collision (and the script):

$ btcdeb '[255044462d312e330a25e2e3cfd30a0a0a312030206f626a0a3c3c2f57696474682032203020522f4865696768742033203020522f547970652034203020522f537562747970652035203020522f46696c7465722036203020522f436f6c6f7253706163652037203020522f4c656e6774682038203020522f42697473506572436f6d706f6e656e7420383e3e0a73747265616d0affd8fffe00245348412d3120697320646561642121212121852fec092339759c39b1a1c63c4c97e1fffe017f46dc93a6b67e013b029aaa1db2560b45ca67d688c7f84b8c4c791fe02b3df614f86db1690901c56b45c1530afedfb76038e972722fe7ad728f0e4904e046c230570fe9d41398abe12ef5bc942be33542a4802d98b5d70f2a332ec37fac3514e74ddc0f2cc1a874cd0c78305a21566461309789606bd0bf3f98cda8044629a1 255044462d312e330a25e2e3cfd30a0a0a312030206f626a0a3c3c2f57696474682032203020522f4865696768742033203020522f547970652034203020522f537562747970652035203020522f46696c7465722036203020522f436f6c6f7253706163652037203020522f4c656e6774682038203020522f42697473506572436f6d706f6e656e7420383e3e0a73747265616d0affd8fffe00245348412d3120697320646561642121212121852fec092339759c39b1a1c63c4c97e1fffe017346dc9166b67e118f029ab621b2560ff9ca67cca8c7f85ba84c79030c2b3de218f86db3a90901d5df45c14f26fedfb3dc38e96ac22fe7bd728f0e45bce046d23c570feb141398bb552ef5a0a82be331fea48037b8b5d71f0e332edf93ac3500eb4ddc0decc1a864790c782c76215660dd309791d06bd0af3f98cda4bc4629b1 OP_2DUP OP_EQUAL OP_NOT OP_VERIFY OP_SHA1 OP_SWAP OP_SHA1 OP_EQUAL]'

Peter Todd's other [bounties](https://bitcointalk.org/index.php?topic=293382.0) remain unclaimed at the time of this writing. They're all written in the same manner as the SHA-1 example above.

## Understand the Limitations of Puzzle Scripts

Puzzle scripts are great to further examine Bitcoin Scripting, but you'll only see them in real-world use if they're holding small amounts of funds or if they're intended for redemption by very skilled users. There's a reason for this: they aren't secure.

Here's where the security falls down:

First, anyone can redeem them without knowing much of a secret. They do have to have the redeemScript, which offers some protection, but once they do, that's probably the only secret that's necessary — unless your puzzle is _really_ tough, such as a computational puzzle.

Second, the actual redemption isn't secure. Normally, a Bitcoin transaction is protected by the signature. Because the signature covers the transaction, no one on the network can rewrite that transaction to instead send to their address without invalidating the signature (and thus the transaction). That isn't true with a transactions whose inputs are just numbers. Anyone could grab the transaction and rewrite it to allow them to steal the funds. If they can get their transaction into a block before yours, they win, and you don't get the puzzle money. There are solutions for this, but they involve mining the block yourself or having a trusted pool mine it, and neither of those options is rational for an average Bitcoin user.

Yet, Peter Todd's cryptographic bounties prove that puzzle scripts do have some real-world application.

## Summary: Writing Puzzle Scripts

Puzzles scripts are a great introduction to more realistic and complex Bitcoin Scripts. They demonstrate the power of the mathematical and stack functions in Bitcoin Script and how they can be carefully combined to create questions that require very specific answers. However, their real-world usage is also limited by the security issues inherent in non-signed Bitcoin transactions.

> :fire: _**What is the power of puzzle script?**_ Despite their limitations, puzzles scripts have been used in the real world as the prizes for computational bounties. Anyone who can figure out a complex puzzle, whose solution presumably has some real-world impact, can win the bounty. Whether they get to actually keep it is another question.

## What's Next?

Continue "Designing Real Bitcoin Scripts" with [§13.2: Writing Complex Multisig Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_2_Writing_Complex_Multisig_Scripts.md).

# 13.2: Writing Complex Multisig Scripts

To date, the multisigs described in these documents have been entirely simple, of the m-of-n or n-of-n form. However, you might desire more complex multisigs, where cosigners vary or where different options might become available over time.

## Write a Variable Multisig

A variable multisig requires different numbers of people to sign depending on who is signing.

### Write a Multisig with a Single Signer or Co-Signers

Imagine a corporation where either the president or two-out-of-three vice presidents could agree to the usage of funds.

You can write this by creating an IF/ELSE/ENDIF statement that has two blocks, one for the president and his one-of-one signature and one for the vice-presidents and their two-of-three signatures. You can then determine which block to use based on how many signatures are in the unlocking script. Using OP_DEPTH 1 OP_EQUAL will tell you if there is one item on the stack, and you then go from there.

The full locking script would be OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF

If run by the president, it would look like this:

Script: OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ ]

Script: OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ ]

Script: 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Running: OP_DEPTH  
Stack: [ 1 ]

Script: OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ 1 1 ]

Script: IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Running: 1 1 OP_EQUAL  
Stack: [ True ]

Because the result is True, the Script now collapses to the IF statement:

Script: OP_CHECKSIGNATURE  
Running: True IF  
Stack: [ ]

Script: OP_CHECKSIGNATURE  
Stack: [ ]

Script:  
Running: OP_CHECKSIGNATURE  
Stack: [ True ]

If run by two vice-presidents, it would look like this:

Script: 0 OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ ]

Script: OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ 0 ]

Script: 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Running: 0 OP_DEPTH  
Stack: [ 0 3 ]

Script: OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Stack: [ 0 3 1 ]

Script: IF OP_CHECKSIGNATURE ELSE 2 3 OP_CHECKMULTISIG ENDIF  
Running: 3 1 OP_EQUAL  
Stack: [ 0 False ]

Because the result is False, the Script now collapses to the ELSE statement:

Script: 2 3 OP_CHECKMULTISIG  
Running: False IF  
Stack: [ 0 ]

Script: OP_CHECKMULTISIG  
Stack: [ 0 2 3 ]

Script:  
Running: 0 2 3 OP_CHECKMULTISIG  
Stack: [ ]

You might notice that the President's signature just uses a simple OP_CHECKSIGNATURE rather than the more complex code usually required for a P2PKH. We can get away with including the public key in the locking script, obviating the usual rigamarole, because it's hashed and won't be revealed (through the redeemScript) until the transaction is unlocked. This also allows for all of the possible signers to sign using the same methodology.

The only possible problem is if the President is absent-minded and accidentally signs a transaction with one of his VPs, because he remembers this being a 2-of-3 multisig. One option is to decide that's an acceptable failure condition, because the President is using the multsig incorrectly. Another option is to turn the 2-of-3 multisig into a 2-of-4 multisig, just in case the President doesn't tolerate failure: OP_DEPTH 1 OP_EQUAL IF OP_CHECKSIGNATURE ELSE 2 4 OP_CHECKMULTISIG ENDIF. This would allow the President to mistakenly sign with any Vice President, but wouldn't impact things if two Vice Presidents wanted to (correctly) sign.

### Write a Multisig with a Required Signer

Another multisig possibility involves have a m-of-n multisig where one of the signers is required. This can usually be managed by breaking the multisig down into multiple m of n-1 multisigs. For example, a 2-of-3 multisig where one of the signers is required would actually be two 2-of-2 multisigs, each including the required signer.

Here's a simple way to script that:

OP_3DUP  
2 2 OP_CHECKMULTISIG  
NOTIF

2 2 OP_CHECKMULTISIG

ENDIF

The unlocking script would be either 0 or 0 .

First the Script would check the signatures against . If that fails, it would check against .

The result of the final OP_CHECKMULTISIG that was run will be left on the top of the stack (though there will be cruft below it if the first one succeeded).

## Write an Escrow Multisig

We've talked a lot about escrows. Complex multisigs combined with timelocks offer an automated way to create them in a robust manner.

Imagine home buyer Alice and home seller Bob who are working with an escrow agent. The easy way to script this would be as a multisig where any two of the three parties could release the money: either the seller and buyer agree or the escrow agent takes over and agrees with one of the parties: 2 3 OP_CHECKMULTISG.

However, this weakens the power of the escrow agent and allows the seller and buyer to accidentally make a bad decision between themselves — which is one of the things an escrow system is designed to avoid. So it could be that what we really want is the system that we just laid out, where the escrow agent is a required party in the 2-of-3 multisig: OP_3DUP 2 2 OP_CHECKMULTISIG NOTIF 2 2 OP_CHECKMULTISIG ENDIF.

However, this doesn't pass the walk-in-front-of-a-bus test. If the escrow agent dies or flees to the Bahamas during the escrow, the buyer and seller are out a lot of money. This is where a timelock comes in. You can create an additional test that will only be run if we've passed the end of our escrow period. In this situation, you allow the buyer and seller to sign together:

OP_3DUP  
2 2 OP_CHECKMULTISIG  
NOTIF

OP_3DUP  
2 2 OP_CHECKMULTISIG  
NOTIF

<+30Days> OP_CHECKSEQUENCEVERIFY OP_DROP    
2 <pubKeyA> <pubKeyB> 2 OP_CHECKMULTISIG  

ENDIF  
ENDIF

First, you test a signature for the buyer and the escrow agent, then a signature for the seller and the escrow agent. If both of those fail and 30 days have passed, then you also allow a signature for the buyer and seller.

### Write a Buyer-Centric Escrow Multisig

[BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki#Escrow_with_Timeout) offers a different example of this sort of escrow that doesn't have the extra protections to prevent going around the escrow agent, but which does give Alice total control if the escrow fails.

IF

2 <pubKeyA> <pubKeyB> <pubKeyEscrow> 3 OP_CHECKMULTISIG   

ELSE

<+30Days> OP_CHECKSEQUENCEVERIFY OP_DROP    
<pubKeyA> OP_CHECKSIGNATURE  

ENDIF

Here, any two of the three signers can release the money at any time, but after 30 days Alice can retrieve her money on her own.

Note that this Script requires a True or False to be passed in to identify which branch is being used. This is a simpler, less computationally intensive way to support branches in a Bitcoin Script; it's fairly common.

Early on, the following sigScript would be allowed: 0 True. After 30 days, Alice could produce a sigScript like this: False.

## Summary: Writing Complex Multisig Scripts

More complex multisignatures can typically be created by combining signatures or multisignatures with conditionals and tests. The resulting multisigs can be variable, requiring different numbers of signers based on who they are and when they're signing.

> :fire: _**What is the power of complex multisig scripts?**_ More than anything we've seen to date, complex multisig scripts are truly smart contracts. They can be very precise in who is allowed to sign and when. Multi-level corporations, partnerships, and escrows alike can be supported. Using other powerful features like timelocks can further protect these funds, allowing them to be released or even returned at certain times.

## What's Next?

Continue "Designing Real Bitcoin Scripts" with [§13.3: Empowering Bitcoin with Scripts](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/13_3_Empowering_Bitcoin_with_Scripts.md).

# 13.3: Empowering Bitcoin with Scripts

Bitcoin Scripts can go far beyond the relatively simple financial instruments detailed to date. They're also the foundation of most complex usages of the Bitcoin network, as demonstrated by these real-world examples of off-chain functionality, drawn from the Lightning Network examples in [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki).

## Lock for the Lightning Network

The [Lightning Network](https://rusty.ozlabs.org/?p=450) is a payment channel that allows users to take funds off-chain and engage in numerous microtransactions before finalizing the payment channel and bringing the funds back into Bitcoin. Benefits include lower fees and faster transaction speeds. It's discussed in more detail, with examples of how to use it from the command line, starting [Chapter 19](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md).

[BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki) contains a few examples of how these off-chain transactions could be generated, using Bitcoin locking scripts.

### Lock with Revocable Commitment Transactions

The trick with Lightning is the fact that it's off-chain. To use Lightning, participants jointly lock funds on the Bitcoin blockchain with an n-of-n multisignature. Then, they engage in a number of transactions between themselves. Each new "commitment transaction" splits those joint funds in a different way; these transactions are partially signed but _they aren't put on the blockchain_.

If you have a mass of unpublished transactions, any of which _could_ be placed on the Blockchain, how do you keep one of the participants from reverting back to an old transaction that's more beneficial to them? The answer is _revocation_. A simplified example in BIP 112, which offers one of the stepping stones to Lightning, shows how: you give the participant who would be harmed by reversion to a revoked transaction the ability to reclaim the funds himself if the the other participant illegitimately tries to use the revoked transaction.

For example, presume that Alice and Bob update the commitment transaction to give more of the funds to Bob (effectively: Alice sent funds to Bob via the Lightning network). They partially sign new transactions, but they also each offer up their own revokeCode for previous transactions. This effectively guarantees that they won't publish previous transactions, because doing so would allow their counterparty to claim those previous funds.

So what does the old transaction look like? It was a commitment transaction showing funds intended for Alice, before she gave them to Bob. It had a locking script as follows:

OP_HASH160  
  
OP_EQUAL

IF

<pubKeyBob>  

ELSE

<+24Hours>     
OP_CHECKSEQUENCEVERIFY     
OP_DROP    
<pubKeyAlice>  

ENDIF  
OP_CHECKSIG

The ELSE block is where Alice got her funds, after a 24-hour delay. However now it's been superceded; that's the whole point of a Lightning-style payment channel, after all. In this situation, this transaction should never be published. Bob has no incentive to because he has a newer transaction, which benefits him more because he's been sent some of Alice's funds. Alice has no incentive either, because she loses the funds if she tries because of that revokeCode. So no one puts the transaction onto the blockchain, and the off-chain transactions continue.

It's worth exploring how this script would work in a variety of situations, most of which involve Alice trying to cheat by reverting to this older transaction, which describes the funds _before_ Alice sent some of them to Bob.

#### Run the Lock Script for Cheating Alice, with Revocation Code

Alice could try to use revocation code that she gave to Bob to immediately claim the funds. She writes a locking script of :

Script: OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: OP_HASH160  
Stack: [ ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: OP_EQUAL  
Stack: [ True ]

The OP_EQUAL feeds the IF statement. Because Alice uses the revokeCode, she gets into the branch that allows her to redeem the funds immediately, collapsing the rest of the script down to (within the conditional) and OP_CHECKSIG (afterward).

Script: OP_CHECKSIG  
Running: True IF  
Stack: [ ]

Curses! Only Bob can sign immediately using the redeemCode!

Script: OP_CHECKSIG  
Stack: [ ]

Script:  
Running: OP_CHECKSIG  
Stack: [ False ]

#### Run the Lock Script for Cheating Alice, without Revocation Code

So what if Alice instead tries to use her own signature, without the revokeCode? She uses an unlocking script of .

Script: 0 OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ 0 ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: 0 OP_HASH160  
Stack: [ <0Hash> ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ <0Hash> ]

Script: IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: <0Hash> OP_EQUAL  
Stack: [ False ]

We now collapse down to the ELSE statement and what comes after the conditional:

Script: <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP OP_CHECKSIG  
Running: False IF  
Stack: [ ]

Script: OP_CHECKSEQUENCEVERIFY OP_DROP OP_CHECKSIG  
Stack: [ <+24Hours> ]

And then Alice is foiled again because 24 hours haven't gone by!

Script: OP_DROP OP_CHECKSIG  
Running: <+24Hours> OP_CHECKSEQUENCEVERIFY  
Stack: [ <+24Hours> ] — Script EXITS

#### Run the Lock Script for Victimized Bob

What this means is that Bob has 24 hours to reclaim his funds if Alice ever tries to cheat, using the and his signature as his unlocking script:

Script: OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: OP_HASH160 OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: OP_HASH160  
Stack: [ ]

Script: OP_EQUAL IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Stack: [ ]

Script: IF ELSE <+24Hours> OP_CHECKSEQUENCEVERIFY OP_DROP ENDIF OP_CHECKSIG  
Running: OP_EQUAL  
Stack: [ True ]

Script: OP_CHECKSIG  
Running: True IF  
Stack: [ ]

Script: OP_CHECKSIG  
Stack: [ ]

Script:  
Running: OP_CHECKSIG  
Stack: [ True ]

#### Run the Lock Script for Virtuous Alice

All of Alice's commitment transactions are locked with this same locking script, whether they've been revoked or not. That means that the newest commitment transaction, which is the currently valid one, is locked with it as well. Alice has never sent a newer transaction to Bob and thus never sent him the previous revokeCode.

In this situation, she could virtuously publish the transaction, closing down the proto-Lightning channel. She puts the transaction on the chain and she waits 24 hours. Bob can't do anything about it because he doesn't have the recovation code. Then, after the wait, Alice reclaims her funds. (Bob does the same thing with his own final commtiment transaction.)

### Lock with Hashed Time-Lock Contracts

The Revocable Commitment Transactions were just a stepping stone to Lightning. The actual Lightning Network uses a more complex mechanism called a [hashed timelock contract](https://en.bitcoin.it/wiki/Hashed_Timelock_Contracts), or HTLC.

The main purpose of HTLCs is to create a comprehensive network of participants. Transactions are no longer just between a pair of participants who have entered the network together, but can now be between previously unassociated people. When funds are sent, a string of transactions are created, each of them locked with a secretHash. When the corresponding secretCode is revealed, the entire string of transactions can be spent. This is what allows singular transactions to actually become a network.

There's also a bit more complexity in Lightning Network locking scripts. There are separate locks for the sender and the recipient of each transaction that are more widely divergent than the differing commitment transactions alluded to in the previous section. We're going to show both of them, to demonstrate the power of these locking scripts, but we're not going to dwell on how they interact with each other.

#### Lock the Recipient's Transaction

Once more, we're going to start looking at Alice's commitment transaction, which shows funds that she's received:

OP_HASH160  
OP_DUP  
  
OP_EQUAL

IF

<+24Hours>    
OP_CHECKSEQUENCEVERIFY    
OP_2DROP    
<pubKeyAlice>  

ELSE

<revokeHash>     
OP_EQUAL    
        
OP_NOTIF    
            
    <Date>     
    OP_CHECKLOCKTIMEVERIFY     
    OP_DROP    
        
ENDIF    
        
<pubKeyBob>  

ENDIF

OP_CHECKSIG

The key to these new HTLCs is the secretHash, which we said is what allows a transaction to span the network. When the transaction has spanned from its originator to its intended recipient, the secretCode is revealed, which allows all the participants to create a secretHash and unlock the whole network of payments.

After the secretCode has been revealed, the IF branch opens up: Alice can claim the funds 24 hours after the transaction is put on the Bitcoin network.

However, there's also the opportunity for Bob to reclaim his funds, which appears in the ELSE branch. He can do so if the transaction has been revoked (but Alice puts it on the blockchain anyway), _or if_ an absolute timeout has occurred.

#### Lock the Sender's Transaction

Here's the alternative commitment transaction locking script used by the sender:

OP_HASH160  
OP_DUP  
  
OP_EQUAL  
OP_SWAP  
  
OP_EQUAL  
OP_ADD

IF

<pubKeyAlice>  

ELSE

<Date>    
OP_CHECKLOCKTIMEVERIFY    
<+24Hours>    
OP_CHECKSEQUENCEVERIFY    
OP_2DROP    
<pubKeyBob>  

ENDIF  
OP_CHECKSIG

The initial part of their Script is quite clever and so worth running:

Initial Script: OP_HASH160 OP_DUP OP_EQUAL OP_SWAP OP_EQUAL OP_ADD  
Stack: [ ]

Initial Script: OP_HASH160 OP_DUP OP_EQUAL OP_SWAP OP_EQUAL OP_ADD  
Stack: [ ]

Initial Script: OP_DUP OP_EQUAL OP_SWAP OP_EQUAL OP_ADD  
Running: OP_HASH160  
Stack: [ ]

Initial Script: OP_EQUAL OP_SWAP OP_EQUAL OP_ADD  
Running: OP_DUP  
Stack: [ ]

Initial Script: OP_EQUAL OP_SWAP OP_EQUAL OP_ADD  
Stack: [ ]

Initial Script: OP_SWAP OP_EQUAL OP_ADD  
Running: OP_EQUAL  
Stack: [ <wasItSecretHash?> ]

Initial Script: OP_EQUAL OP_ADD  
Running: <wasItSecretHash?> OP_SWAP  
Stack: [ <wasItSecretHash?> ]

Initial Script: OP_EQUAL OP_ADD  
Stack: [ <wasItSecretHash?> ]

Initial Script: OP_ADD  
Running: OP_EQUAL  
Stack: [ <wasItSecretHash?> <wasItRevokeHash?> ]

Initial Script:  
Running: <wasItSecretHash?> <wasItRevokeHash?> OP_ADD  
Stack: [ <wasItSecretOrRevokeHash?> ]

Running through the script reveals that the initial checks, above the IF/ELSE/ENDIF, determine if the hash was _either_ the secretCode _or_ the revokeCode. If so, Alice can take the funds in the first block. If not, Bob can take the funds, but only after Alice has had her chance and after both the 24 hour timeout and the absolute timeout have passed.

#### Understand HTLCs

HTLCs are quite complex, and this overview doesn't try to explain all of their intricacies. Rusty Russell's [overview](https://rusty.ozlabs.org/?p=462) explains more, and there's even more detail in his [Deployable Lightning](https://github.com/ElementsProject/lightning/blob/master/doc/deployable-lightning.pdf) paper. But don't worry if some of the intricacies still escape you, particularly the interrelations of the two scripts.

For the purposes of this tutorial, there are two important lessons for HTLCs:

- Understand that a very complex structure like an HTLC can be created with Bitcoin Script.
    
- Analyze how to run each of the HTLC scripts.
    

It's worth your time running each of the two HTLC scripts through each of its permutations, one stack item at a time.

## Summary: Empowering Bitcoin with Scripts

We're closing our examination of Bitcoin Scripts with a look at how truly powerful they can be. In 20 opcodes or less, a Bitcoin Script can form the basis of an entire off-chain payment channel. Similarly, two-way pegged sidechains are the product of less than twenty opcodes, as also briefly noted in [BIP 112](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki).

If you've ever seen complex Bitcoin functionality or Bitcoin-adjacent systems, they were probably built on Bitcoin Scripts. And now you have all the tools to do the same yourself.

## What's Next?

Move on to "Using Tor" with [Chapter Fourteen: Using Tor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_0_Using_Tor.md).

Or, if you prefer, there are two alternate paths:

If you want to stay focused on Bitcoin, move on to "Programming with RPC" with [Chapter Sixteen: Talking to Bitcoind with C](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_0_Talking_to_Bitcoind.md).

Or, if you want to stay focused on the command-line because you're not a programmer, you can skip to [Chapter Nineteen: Understanding Your Lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md) to continue your command-line education with the Lightning Network.

# Chapter 14: Using Tor

Tor is one of the standard programs installed by [Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). It will help to keep your server secure, which is critically important when you're dealing with cryptocurrency. This chapter digresses momentarily from Bitcoin to help you understand this core security infrastructure.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Use a Tor Setup
    
- Perform Tor Maintenance
    

Supporting objectives include the ability to:

- Understand the Tor Network
    
- Understand Bitcoin's Various Ports
    

## Table of Contents

- [Section One: Verifying Your Tor Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_1_Verifying_Your_Tor_Setup.md)
    
- [Section Two: Changing Your Bitcoin Hidden Services](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_2_Changing_Your_Bitcoin_Hidden_Services.md)
    
- [Section Three: Adding SSH Hidden Services](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_3_Adding_SSH_Hidden_Services.md)
    

# 14.1: Verifying Your Tor Setup

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

If you did a standard installation with [Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup) then you should have Tor set up as part of your Bitcoin node: Tor is installed and has created hidden services for the Bitcoin RPC ports; while an onion address has also been created for bitcoind. This section talks about what all of that is and what to do with it.

> :book: _**What is Tor?**_ Tor is a low-latency anonymity and overlay network based on onion routing and path-building design for enabling anonymous communication. It's free and open-source software with the name derived from the acronym for the original software project name: "The Onion Router". :book: _**Why Use Tor for Bitcoin?**_ The Bitcoin network is a peer-to-peer network that listens for transactions and propagates them using a public IP address. When connecting to the network not using Tor, you would share your IP address, which could expose your location, your uptime, and others details to third parties — which is an undesirable privacy practice. To protect yourself online you should use tools like Tor to hide your connection details. Tor allows you to improve your privacy online as your data is cryptographically encoded and goes through different nodes, each one decoding a single layer (hence the onion metaphor).

## Understand Tor

So how does Tor work?

When a user wants to connect to an Internet server, Tor tries to build a path formed by at least three Tor relay nodes, called Guard, Middle, and Exit. While building this path, symmetric encryption keys are negotiated; when a message moves along the path, each relay then strips off its layer of encryption. In this way, the message arrives at the final destination in its original form, and each party only knows the previous and the next hop and cannot determine origin or destination.

Here's what a connection looks like without Tor:

20:58:03.804787 IP bitcoin.36300 > lb-140-82-114-25-iad.github.com.443: Flags [P.], seq 1:30, ack 25, win 501, options [nop,nop,TS val 3087919981 ecr 802303366], length 29

Contrariwise, with Tor much less information about the actual machines is transmitted:

21:06:52.744602 IP bitcoin.58776 > 195-xxx-xxx-x.rev.pxxxxxm.eu.9999: Flags [P.], seq 264139:265189, ack 3519373, win 3410, options [nop,nop,TS val 209009853 ecr 3018177498], length 1050  
21:06:52.776968 IP 195-xxx-xxx-x.rev.pxxxxxm.eu.9999 > bitcoin.58776: Flags [.], ack 265189, win 501, options [nop,nop,TS val 3018177533 ecr 209009853], length 0

Bottom line: Tor encrypts your data in such a way that it hides your origin, your destination, and what services you're using, whereas a standard encryption protocol like TLS _only_ protects what your data contains.

### Understand the Tor Network Architecture

The basic architecture of the Tor network is made up of the following components:

- **Tor Client (OP or Onion Proxy).** A Tor client installs local software that acts as an onion proxy. It packages application data into cells that are all the same size (512 bytes), which it then sends to the Tor network. A cell is the basic unit of Tor transmission.
    
- **Onion Node (OR or Onion Router).** An onion node transmits cells coming from the Tor client and from online servers. There are three types of onion nodes: input (Guard), intermediate nodes (Middle), and output nodes (Exit).
    
- **Directory Server.** A Directory server stores information about onion routers and onion servers (hidden services), such as their public keys.
    
- **Onion Server (hidden server).** An onion server supports TCP applications such as web pages or IRC as services.
    

### Understand the Limitations of Tor

Tor isn't a perfect tool. Because information from the Tor network is decrypted at the exit nodes before being sent to its final destinations, theoretically an observer could collect sufficient metadata to compromise anonymity and potentially identify users.

There are also studies that suggest that possible exploits of Bitcoin's anti-DoS protection could allow an attacker to force other users who use Tor to connect exclusively through his Tor Exit nodes or to his Bitcoin peers, isolating the client from the rest of the Bitcoin network and exposing them to censorship, correlation, and other attacks.

Similarly, Bitcoin Tor users could be fingerprint-attacked by setting an address cookie on their nodes. This would also allow correlation and thus deanonymization.

Meanwhile, even over Tor, Bitcoin is only a pseudoanonymous service due to the many dangers of correlation that stem from the permanent ledger itself. This means that Bitcoin usage over Tor is actually more likely to be _deanonymized_ than other services (and could lead to the deanonymization of other activities).

With that said, Tor is generally considered safer than the alternative, which is non-anonymous browsing.

## Verify Your Tor Setup

So how do you verify that you've enabled Tor? If you installed with Bitcoin Standup, the following will verify that Tor is running on your system

$ sudo -u debian-tor tor --verify-config

If Tor is installed correctly you should output like this:

Jun 26 21:52:09.230 [notice] Tor 0.4.3.5 running on Linux with Libevent 2.0.21-stable, OpenSSL 1.0.2n, Zlib 1.2.11, Liblzma 5.2.2, and Libzstd N/A.  
Jun 26 21:52:09.230 [notice] Tor can't help you if you use it wrong! Learn how to be safe at [https://www.torproject.org/download/download#warning](https://www.torproject.org/download/download#warning)  
Jun 26 21:52:09.230 [notice] Read configuration file "/etc/tor/torrc".  
Configuration was valid

> :warning: **WARNING:** This just means that Tor is running, not that its being used for all (or any) connections.

### Verify Your Tor Setup for RPC

The most important purpose of Tor, as installed by Bitcoin Standup, is to offer hidden services for the RPC ports that are used to send command-line style commands to bitcoind.

> :book: _**What is a Tor Hidden Service?**_ A hidden service (aka "an onion service") is a service that is accessible via Tor. Connection made to that service _using the Onion Network_ will be anonymized.

The Tor config file is found at /etc/tor/torrc. If you look at it, you should see the following services to protect your RPC ports:

HiddenServiceDir /var/lib/tor/standup/  
HiddenServiceVersion 3  
HiddenServicePort 1309 127.0.0.1:18332  
HiddenServicePort 1309 127.0.0.1:18443  
HiddenServicePort 1309 127.0.0.1:8332

> :link: **TESTNET vs MAINNET:** Mainnet RPC is run on port 8332, testnet on port 18332. :information_source: **NOTE:** The HiddenServiceDir is where all the files are kept for this particular service. If you need to lookup your onion address, access keys, or add authorized clients, this is where to do so!

The easy way to test your RPC Hidden Service is to use the [QuickConnect API](https://github.com/BlockchainCommons/Bitcoin-Standup/blob/master/Docs/Quick-Connect-API.md) built into Bitcoin Standup. Just download the QR code found at /qrcode.png and scan it using a wallet or node that support QuickConnect, such as [The Gordian Wallet](https://github.com/BlockchainCommons/FullyNoded-2). When you scan the QR, you should see the wallet sync up with your node; it's doing so using the RPC hidden services.

The hard way to test your RPC Hidden Service is to send a bitcoin-cli command with torify, which allows you to translate a normal UNIX command to a Tor-protected command. It's difficult because you need to grab three pieces of information.

1. **Your Hidden Service Port.** This comes from /etc/tor/torrc/. By default, it's port 1309.
    
2. **Your Tor Address.** This is in the hostname file in the HiddenServiceDir directory defined in /etc/tor/torrc. By default the file is thus /var/lib/tor/standup/hostname. It's protected, so you'll need to sudo to access it:
    

$ sudo more /var/lib/tor/standup/hostname  
mgcym6je63k44b3i5uachhsndayzx7xi4ldmwrm7in7yvc766rykz6yd.onion

1. **Your RPC Password.** This is in ~/.bitcoin/bitcoin.conf
    

When you have all of that information you can issue a bitcoin-cli command using torify and specifying the -rpcconnect as your onion address, the -rpcport as your hidden service port, and the -rpcpassword as your password:

$ torify bitcoin-cli -rpcconnect=mgcym6je63k44b3i5uachhsndayzx7xi4ldmwrm7in7yvc766rykz6yd.onion -rpcport=1309 -rpcuser=StandUp -rpcpassword=685316cc239c24ba71fd0969fa55634f getblockcount

### Verify Your Tor Setup for Bitcoind

Bitcoin Standup also ensures that your bitcoind is set up to optionally communicate on an onion address.

You can verify the initial setup of Tor for bitcoind by grepping for "tor" in the debug.log in your data directory:

$ grep "tor:" ~/.bitcoin/testnet3/debug.log  
2021-06-09T14:07:04Z tor: ADD_ONION successful  
2021-06-09T14:07:04Z tor: Got service ID vazr3k6bgnfafmdpcmbegoe5ju5kqyz4tk7hhntgaqscam2qupdtk2yd, advertising service vazr3k6bgnfafmdpcmbegoe5ju5kqyz4tk7hhntgaqscam2qupdtk2yd.onion:18333  
2021-06-09T14:07:04Z tor: Cached service private key to /home/standup/.bitcoin/testnet3/onion_v3_private_key

> :information_source: **NOTE:** Bitcoin Core does not support v2 addresses anymore. Tor v2 support was removed in [#22050](https://github.com/bitcoin/bitcoin/pull/22050) **TESTNET vs MAINNET:** Mainnet bitcoind responds on port 8333, testnet on port 18333.

You can verify that a Tor hidden service has been created for Bitcoin with the getnetworkinfo RPC call:

$ bitcoin-cli getnetworkinfo  
...  
"localaddresses": [  
{  
"address": "173.255.245.83",  
"port": 18333,  
"score": 1  
},  
{  
"address": "2600:3c01::f03c:92ff:fe86:f26",  
"port": 18333,  
"score": 1  
},  
{  
"address": "vazr3k6bgnfafmdpcmbegoe5ju5kqyz4tk7hhntgaqscam2qupdtk2yd.onion",  
"port": 18333,  
"score": 4  
}  
],  
...

This shows three addresses to access your Bitcoin server, an IPv4 address (173.255.245.83), an IPv6 address (2600:3c01::f03c:92ff:fe86:f26), and a Tor address (vazr3k6bgnfafmdpcmbegoe5ju5kqyz4tk7hhntgaqscam2qupdtk2yd.onion).

> :warning: **WARNING:** Obviously: never reveal your Tor address in a way that's associated with your name or other PII!

You can see similar information with getnetworkinfo.

bitcoin-cli getnetworkinfo  
{  
"version": 200000,  
"subversion": "/Satoshi:0.20.0/",  
"protocolversion": 70015,  
"localservices": "0000000000000408",  
"localservicesnames": [  
"WITNESS",  
"NETWORK_LIMITED"  
],  
"localrelay": true,  
"timeoffset": 0,  
"networkactive": true,  
"connections": 10,  
"networks": [  
{  
"name": "ipv4",  
"limited": false,  
"reachable": true,  
"proxy": "",  
"proxy_randomize_credentials": false  
},  
{  
"name": "ipv6",  
"limited": false,  
"reachable": true,  
"proxy": "",  
"proxy_randomize_credentials": false  
},  
{  
"name": "onion",  
"limited": false,  
"reachable": true,  
"proxy": "127.0.0.1:9050",  
"proxy_randomize_credentials": true  
}  
],  
"relayfee": 0.00001000,  
"incrementalfee": 0.00001000,  
"localaddresses": [  
{  
"address": "173.255.245.83",  
"port": 18333,  
"score": 1  
},  
{  
"address": "2600:3c01::f03c:92ff:fe86:f26",  
"port": 18333,  
"score": 1  
},  
{  
"address": "vazr3k6bgnfafmdpcmbegoe5ju5kqyz4tk7hhntgaqscam2qupdtk2yd.onion",  
"port": 18333,  
"score": 4  
}  
],  
"warnings": ""  
}

This hidden service will allow anonymous connections to your bitcoind over the Bitcoin Network.

> :warning: **WARNING:** Running Tor and having a Tor hidden service doesn't force either you or your peers to use Tor.

### Verify Your Tor Setup for Peers

Using the RPC command getpeerinfo, you can see what nodes are connected to your node and check whether they are connected with Tor.

$ bitcoin-cli getpeerinfo

Some might be connected via Tor:

...  
{  
"id": 9,  
"addr": "nkv.......xxx.onion:8333",  
"addrbind": "127.0.0.1:51716",  
"services": "000000000000040d",  
"servicesnames": [  
"NETWORK",  
"BLOOM",  
"WITNESS",  
"NETWORK_LIMITED"  
],  
"relaytxes": true,  
"lastsend": 1593981053,  
"lastrecv": 1593981057,  
"bytessent": 1748,  
"bytesrecv": 41376,  
"conntime": 1593980917,  
"timeoffset": -38,  
"pingwait": 81.649295,  
"version": 70015,  
"subver": "/Satoshi:0.20.0/",  
"inbound": false,  
"addnode": false,  
"startingheight": 637875,  
"banscore": 0,  
"synced_headers": -1,  
"synced_blocks": -1,  
"inflight": [  
],  
"whitelisted": false,  
"permissions": [  
],  
"minfeefilter": 0.00000000,  
"bytessent_per_msg": {  
"addr": 55,  
"feefilter": 32,  
"getaddr": 24,  
"getheaders": 1053,  
"inv": 280,  
"ping": 32,  
"pong": 32,  
"sendcmpct": 66,  
"sendheaders": 24,  
"verack": 24,  
"version": 126  
},  
"bytesrecv_per_msg": {  
"addr": 30082,  
"feefilter": 32,  
"getdata": 280,  
"getheaders": 1053,  
"headers": 106,  
"inv": 9519,  
"ping": 32,  
"pong": 32,  
"sendcmpct": 66,  
"sendheaders": 24,  
"verack": 24,  
"version": 126  
}  
}  
...

Some might not, such as this IPv6 connection:

...  
{  
"id": 17,  
"addr": "[2001:638:a000:4140::ffff:191]:18333",  
"addrlocal": "[2600:3c01::f03c:92ff:fe86:f26]:36344",  
"addrbind": "[2600:3c01::f03c:92ff:fe86:f26]:36344",  
"services": "0000000000000409",  
"servicesnames": [  
"NETWORK",  
"WITNESS",  
"NETWORK_LIMITED"  
],  
"relaytxes": true,  
"lastsend": 1595447081,  
"lastrecv": 1595447067,  
"bytessent": 12250453,  
"bytesrecv": 2298711417,  
"conntime": 1594836414,  
"timeoffset": -1,  
"pingtime": 0.165518,  
"minping": 0.156638,  
"version": 70015,  
"subver": "/Satoshi:0.20.0/",  
"inbound": false,  
"addnode": false,  
"startingheight": 1780784,  
"banscore": 0,  
"synced_headers": 1781391,  
"synced_blocks": 1781391,  
"inflight": [  
],  
"whitelisted": false,  
"permissions": [  
],  
"minfeefilter": 0.00001000,  
"bytessent_per_msg": {  
"addr": 4760,  
"feefilter": 32,  
"getaddr": 24,  
"getdata": 8151183,  
"getheaders": 1085,  
"headers": 62858,  
"inv": 3559475,  
"ping": 162816,  
"pong": 162816,  
"sendcmpct": 132,  
"sendheaders": 24,  
"tx": 145098,  
"verack": 24,  
"version": 126  
},  
"bytesrecv_per_msg": {  
"addr": 33877,  
"block": 2291124374,  
"feefilter": 32,  
"getdata": 9430,  
"getheaders": 1085,  
"headers": 60950,  
"inv": 2019175,  
"ping": 162816,  
"pong": 162816,  
"sendcmpct": 66,  
"sendheaders": 24,  
"tx": 5136622,  
"verack": 24,  
"version": 126  
}  
}  
...

Having a Tor address for your bitcoind is probably somewhat less useful than having a Tor address for your RPC connections. That's in part because it's not recommended to try and send all your Bitcoin connections via Tor, and in part because protecting your RPC commands is really what's important: you're much more likely to be doing that remotely, from a software wallet like The Gordian Wallet, while your server itself is more likely to be sitting in your office, basement, or bunker.

Nonetheless, there are ways to make bitcoind use Tor more, as discussed in the next section.

## Summary: Verifying Your Tor Setup

Tor is a software package installed at part of Bitcoin Standup that allows you to exchange communications anonymously. It will protect both your RPC ports (8332 or 18332) and your bitcoind ports (8333 or 18333) — but you have to actively connect to the onion address to use them! Tor is a building stone of privacy and security for your Bitcoin setup, and you can verify it's available and linked to Bitcoin with a few simple commands.

> :fire: _**What is the power of Tor?**_ Many attacks on Bitcoin users depend on knowing who the victim is and that they're transacting Bitcoins. Tor can protect you from that by hiding both where you are and what you're doing. It's particularly important if you want to connect to your own node remotely via a software wallet, and can be crucial if you do so in some country where you might not feel that your Bitcoin usage is appreciated or protected. If you must take your Bitcoin services on the road, make sure that your wallet fully supports Tor and exchanges all RPC commands with your server using that protocol.

## What's Next?

Continue "Understanding Tor" with [§14.2: Changing Your Bitcoin Hidden Services](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_2_Changing_Your_Bitcoin_Hidden_Services.md).

# Chapter 14.2: Changing Your Bitcoin Hidden Services

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

You've got a working Tor service, but over time you may wish to reset or otherwise adjust it.

## Secure Your Hidden Services

Tor allows you to limit which clients talk to your hidden services. If you did not already authorize your client during your server setup, at the earliest opportunity you should do the following:

1. Request your Tor V3 Authentication Public Key from your client. (In [GordianWallet](https://github.com/BlockchainCommons/GordianWallet-iOS), it's available under the settings menu.)
    
2. Go to the appropriate subdirectory for your Bitcoin hidden service, which if you used Bitcoin Standup is /var/lib/tor/standup/.
    
3. Go to the authorized_clients subdirectory.
    
4. Add a file called [anything].auth. The [anything] can really be anything.
    
5. Place the public key (and nothing else) in the file.
    

Once you've added an .auth file to the authorized_client subdirectory, then only authorized clients will be able to communicate with that hidden service. You can add ~330 different public keys to enable different clients.

## Reset Your bitcoind Onion Address

If you ever want to reset your onion address for bitcoind, just remove the onion_private_key in your data directory, such as ~/.bitcoin/testnet:

$ cd ~/.bitcoin/testnet  
$ rm onion_private_key

When you restart, a new onion address will be generated:

2020-07-22T23:52:27Z tor: Got service ID pyrtqyiqbwb3rhe7, advertising service pyrtqyiqbwb3rhe7.onion:18333  
2020-07-22T23:52:27Z tor: Cached service private key to /home/standup/.bitcoin/testnet3/onion_private_key

## Reset Your RPC Onion Address

If you want to reset your onion address for RPC access, you similarly delete the appropriate HiddenServiceDirectory and restart Tor:

$ sudo rm -rf /var/lib/tor/standup/  
$ sudo /etc/init.d/tor restart

> :warning: **WARNING:** Reseting your RPC onion address will disconnect any mobile wallets or other services that you've connected using the Quicklink API. Do this with extreme caution.

## Force bitcoind to Use Tor

Finally, you can force bitcoind to use onion by adding the following to your bitcoin.conf:

proxy=127.0.0.1:9050  
listen=1  
bind=127.0.0.1  
onlynet=onion

You will then need to add onion-based seed nodes or other nodes to your setup, once more by editing the bitcoin.conf:

seednode=address.onion  
seednode=address.onion  
seednode=address.onion  
seednode=address.onion  
addnode=address.onion  
addnode=address.onion  
addnode=address.onion  
addnode=address.onion

See [Bitcoin Onion Nodes](https://github.com/emmanuelrosa/bitcoin-onion-nodes) for a listing and an example of how to add them.

Afterward, restart tor and bitcoind.

You should now be communicating exclusively on Tor. But, unless you are in a hostile state, this level of anonymity is probably not required. It also is not particularly recommended: you might greatly decrease your number of potential peers, inviting problems of censorship or even correlation. You may also see lag. And, this setup may give you a false sense of anonymity that really doesn't exist on the Bitcoin network.

> :warning: **WARNING:** This setup is untested! Use at your own risk!

## Summary: Changing Your Bitcoin Hidden Services

You probably won't need to fool with your Onion services once you've verified them, but in case you do, here's how to reset a Tor address that has become compromised or to move over to exclusive-Tor use for your bitcoind.

## What's Next?

Continue "Understanding Tor" with [14.3: Adding SSH Hidden Services](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_3_Adding_SSH_Hidden_Services.md).

# Chapter 14.3: Adding SSH Hidden Services

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

To date, you've used Tor with your Bitcoin services, but you can also use it to protect other services on your machine, improving their security and privacy. This section demonstrates how by introducing an ssh hidden service to login remotely using Tor.

## Create SSH Hidden Services

New services are created by adding them to the /etc/tor/torrc file:

$ su

# cat >> /etc/tor/torrc << EOF

HiddenServiceDir /var/lib/tor/hidden-service-ssh/  
HiddenServicePort 22 127.0.0.1:22  
EOF

# exit

Here's what that means:

- HiddenServiceDir: Indicates that you have a hidden service directory with the necessary configuration at this path.
    
- HiddenServicePort: Indicates the tor port to be used; in the case of SSH, this is usually 22.
    

After you add the appropriate lines to your torrc file, you will need to restart Tor:

$ sudo /etc/init.d/tor restart

After the restart, your HiddenServiceDir should have new files as follows:

$ sudo ls -l /var/lib/tor/hidden-service-ssh  
total 16  
drwx--S--- 2 debian-tor debian-tor 4096 Jul 22 14:55 authorized_clients  
-rw------- 1 debian-tor debian-tor 63 Jul 22 14:56 hostname  
-rw------- 1 debian-tor debian-tor 64 Jul 22 14:55 hs_ed25519_public_key  
-rw------- 1 debian-tor debian-tor 96 Jul 22 14:55 hs_ed25519_secret_key

The file hostname in this directory contains your new onion ID:

$ sudo cat /var/lib/tor/hidden-service-ssh/hostname  
qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion

You can connect to the ssh hidden service using torify and that address:

$ torify ssh [standup@qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion](mailto:standup@qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion)  
The authenticity of host 'qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion (127.42.42.0)' can't be established.  
ECDSA key fingerprint is SHA256:LQiWMtM8qD4Nv7eYT1XwBPDq8fztQafEJ5nfpNdDtCU.  
Are you sure you want to continue connecting (yes/no)? yes  
Warning: Permanently added 'qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion' (ECDSA) to the list of known hosts.  
standup@qwkemc3vusd73glx22t3sglf7izs75hqodxsgjqgqlujemv73j73qpid.onion's password:

## Summary: Adding SSH Hidden Services

Now that you've got Tor installed and know how to use it, you can add other services to Tor. You just add lines to your torrc (on your server), then connect with torify (on your client).

> :fire: _**What's the power of Other Hidden Services?**_ Every time you access a service on your server remotely, you leave footprints on the network. Even if the data is encrypted by something like SSH (or TLS), lurkers on the network can see where you're connecting from, where you're connecting to, and what service you're using. Does this matter? This is the question you have to ask. But if the answer is "Yes", you can protect the connection with a hidden service.

## What's Next?

For a different sort of privacy, move on to "Using i2p" with [Chapter Fifteen: Using i2p](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_0_Using_i2p.md).

# Chapter 15: Using I2P

There are alternatives to Tor. One is the Invisible Internet Project (I2P), a fully encrypted private network layer. It uses a distributed [network database](https://geti2p.net/en/docs/how/network-database) and encrypted unidirectional tunnels between peers. The biggest difference between Tor and I2P is that Tor is fundamentally a proxy network that offers internet services in a private form, while I2P is fundamentally a sequestered network that offers I2P services only to the I2P network, creating a "network within a network". However, you might just want it as an alternative, so that you're not dependent solely on Tor.

I2P is not currently installed by [Bitcoin Standup](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts), as I2P support was recently added in Bitcoin Core. However, this chapter explains how to manually install it.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Run Bitcoin Core as an I2P (Invisible Internet Project) service
    

Supporting objectives include the ability to:

- Understand the I2P Network
    
- Learn the difference between Tor and I2P
    

## Table of Contents

- [Section One: Bitcoin Core as an I2P (Invisible Internet Project) service](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_1_i2p_service.md)
    

# 15.1: Bitcoin Core as an I2P (Invisible Internet Project) service

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Rather than using the proxy-based Tor service to ensure the privacy of your Bitcoin communications, you may instead wish to use I2P, which is designed to act as a private network within the internet, rather than simply offering private access to internet services.

## Understand the Differences

Tor and I2P both offer private access to online services, but with different routing and databases, and with different architectures for relays. Since hidden services (such as Bitcoin access) are core to the design of I2P, they have also been better optimized:

  
|Tor|I2P||
|---|---|---|
|Routing|[Onion](https://www.onion-router.net/)|[Garlic](https://geti2p.net/en/docs/how/garlic-routing)|
|Network Database|Trusted [Directory Servers](https://blog.torproject.org/possible-upcoming-attempts-disable-tor-network)|[Distributed network database](https://geti2p.net/en/docs/how/network-database)|
|Relay|**Two-way** encrypted connections between each Relay|**One-way** connections between every server in its tunnels|
|Hidden services|Slow|Fast|

  
  

A more detailed comparison may be found at [geti2p.net](https://geti2p.net/en/comparison/tor).

### Understand Tradeoffs for Limiting Outgoing Connections

There are [tradeoffs](https://bitcoin.stackexchange.com/questions/107060/tor-and-i2p-tradeoffs-in-bitcoin-core) if you choose to support only I2P, only Tor, or both. These configurations, which limit outgoing clearnet connections, are made in Bitcoin Core using the onlynet argument in your bitcoin.conf.

- onlynet=onion, which limits outgoing connections to Tor, can expose a node to Sybil attacks and can create network partitioning, because of limited connections between Tornet and the clearnet.
    
- onlynet=onion and onlynet=i2p in conjunction, which runs Onion service with I2P service is experimental for now.
    

## Install I2P

To install I2P, you should make sure your ports are correctly set up and then you can continue with your setup process.

### Prepare Ports

To use I2P, you will need to open the following ports, which are required by I2P:

1. **Outbound (Internet facing):** a random port between 9000 and 31000 is selected. It is best if all these ports are open for outbound connections, which doesn't affect your security.
    

- You can check firewall status using sudo ufw status verbose, which shouldn't deny outgoing connections by default.
    

1. Inbound (Internet facing): optional. A variety of inbound ports are listed in the [I2P docs](https://geti2p.net/en/faq#ports).
    

- For maximum privacy, it is preferable to disable accepting incoming connections.
    

### Run I2P

The following will run Bitcoin Core I2P services:

1. Install i2pd on Ubuntu:
    
    sudo add-apt-repository ppa:purplei2p/i2pd  
    sudo apt-get update  
    sudo apt-get install i2pd
    
    For installing on other OSes, see [these docs](https://i2pd.readthedocs.io/en/latest/user-guide/install/)
    
2. [Run](https://i2pd.readthedocs.io/en/latest/user-guide/run/) the I2P service:
    
    $ sudo systemctl start i2pd.service
    
3. Check that I2P is running. You should see it on port 7656:
    
    $ ss -nlt
    
    State Recv-Q Send-Q Local Address:Port Peer Address:Port Process
    
    LISTEN 0 4096 127.0.0.1:7656 0.0.0.0:*
    
4. Add the following lines in bitcoin.conf:
    
    i2psam=127.0.0.1:7656  
    debug=i2p
    
    The logging option, debug=i2p, is used to record additional information in the debug log about your I2P configuration and connections. The default location for this debugging file on Linux is: ~/.bitcoin/debug.log:
    
5. Restart bitcoind
    
    $ bitcoind
    
6. Check debug.log to see if I2P was setup correctly, or if any errors appeared in the logs.
    
    2021-06-15T20:36:16Z i2paccept thread start  
    2021-06-15T20:36:16Z I2P: Creating SAM session with 127.0.0.1:7656
    
    2021-06-15T20:36:56Z I2P: SAM session created: session id=3e0f35228b, my address=bmwyyuzyqdc5dcx27s4baltbu6zw7rbqfl2nmclt45i7ng3ul4pa.b32.i2p:18333  
    2021-06-15T20:36:56Z AddLocal(bmwyyuzyqdc5dcx27s4baltbu6zw7rbqfl2nmclt45i7ng3ul4pa.b32.i2p:18333,4)
    
    The I2P address is mentioned in the logs, ending with _b32.i2p_. For example bmwyyuzyqdc5dcx27s4baltbu6zw7rbqfl2nmclt45i7ng3ul4pa.b32.i2p:18333.
    
7. Confirm i2p_private_key was created in the Bitcoin Core data directory. The first time Bitcoin Core connects to the I2P router, its I2P address (and corresponding private key) will be automatically generated and saved in a file named _i2p_private_key_:
    
    ~/.bitcoin/testnet3$ ls
    
    anchors.dat chainstate i2p_private_key settings.json  
    banlist.dat debug.log mempool.dat wallets  
    blocks fee_estimates.dat peers.dat
    
8. Check that bitcoin-cli -netinfo or bitcoin-cli getnetworkinforeturns the I2P address:
    
    Local addresses  
    bmwyyuzyqdc5dcx27s4baltbu6zw7rbqfl2nmclt45i7ng3ul4pa.b32.i2p port 18333 score 4
    

You now have your Bitcoin server accessible through the I2P network at your new local address.

## Summary: Bitcoin Core as an I2P (Invisible Internet Project) service

It is always good to have alternatives for privacy and not depend solely on Tor for running Bitcoin Core as a hidden service. Since I2P was recently added in Bitcoin Core, not many people use it. Experiment with it and report bugs if you find any issues.

> :information_source: **NOTE:** For the official i2prouter implementation in Java, visit the [I2P download page](https://geti2p.net/en/download) and follow the instructions for your Operating System. Once installed, open a terminal window and type i2prouter start. Then visit 127.0.0.1:7657 in your browser to enable SAM. To do so, select: "Configure Homepage", then "Clients", and finally select the "Play Button" next to SAM application Bridge. On the left side of the page, there should be a green light next to "Shared Clients".

Move on to "Programming with RPC" with [Chapter Sixteen: Talking to Bitcoind with C](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_0_Talking_to_Bitcoind.md).

Or, if you're not a programmer, you can skip to [Chapter Nineteen: Understanding Your Lightning Setup](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/19_0_Understanding_Your_Lightning_Setup.md) to continue your command-line education with the Lightning Network.

# Chapter 16: Talking to Bitcoind with C

While working with Bitcoin Scripts, we hit the boundaries of what's possible with bitcoin-cli: it can't currently be used to generate transactions containing unusual scripts. Shell scripts also aren't great for some things, such as creating listener programs that are constantly polling. Fortunately, there are other ways to access the Bitcoin network: programming APIs.

This section focuses on three different libraries that can be used as the foundation of sophisticated C programming: an RPC library and a JSON library together allow you to recreate a lot of what you did in shell scripts, but now using C; while a ZMQ library links you in to notifications, something you haven't been able to previously access. (The next chapter will cover an even more sophisticated library called Libwally, to finish out this introductory look at programming Bitcoin with C.)

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Create C Programs that use RPC to Talk to the Bitcoind
    
- Create C Programs that use ZMQ to Talk to the Bitcoind
    

Supporting objectives include the ability to:

- Understand how to use an RPC library
    
- Understand how to use a JSON library
    
- Understand the capabilities of ZMQ
    
- Understand how to use a ZMQ library
    

## Table of Contents

- [Section One: Accessing Bitcoind in C with RPC Libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_1_Accessing_Bitcoind_with_C.md)
    
- [Section Two: Programming Bitcoind in C with RPC Libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_2_Programming_Bitcoind_with_C.md)
    
- [Section Three: Receiving Notifications in C with ZMQ Libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_3_Receiving_Bitcoind_Notifications_with_C.md)
    

# 16.1: Accessing Bitcoind in C with RPC Libraries

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

You've already seen one alternative way to access the Bitcoind's RPC ports: curl, which was covered in a [Chapter 4 Interlude](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md). Interacting with bitcoind through an RPC library in C is no different than that, you just need some good libraries to help you out. This section introduces a package called libbitcoinrpc, which allows you to access JSON-RPC bitcoind port. It uses a curl library for accessing the data and it uses the jansson library for encoding and decoding the JSON.

## Set Up libbitcoinrpc

To use libbitcoinrpc, you need to install a basic C setup and the dependent packages libcurl, libjansson, and libuuid. The following will do so on your Bitcoin Standup server (or any other Ubuntu server).

$ sudo apt-get install make gcc libcurl4-openssl-dev libjansson-dev uuid-dev  
Suggested packages:  
libcurl4-doc libidn11-dev libkrb5-dev libldap2-dev librtmp-dev libssh2-1-dev  
The following NEW packages will be installed:  
libcurl4-openssl-dev libjansson-dev uuid-dev  
0 upgraded, 3 newly installed, 0 to remove and 4 not upgraded.  
Need to get 358 kB of archives.  
After this operation, 1.696 kB of additional disk space will be used.  
Do you want to continue? [Y/n] y

You can then download [libbitcoinrpc from Github](https://github.com/BlockchainCommons/libbitcoinrpc/blob/master/README.md). Clone it or grab a zip file, as you prefer.

$ sudo apt-get install git  
$ git clone [https://github.com/BlockchainCommons/libbitcoinrpc.git](https://github.com/BlockchainCommons/libbitcoinrpc.git)

### Compiling libbitcoinrpc

Before you can compile and install the package, you'll probably need to adjust your $PATH, so that you can access /sbin/ldconfig:

$ PATH="/sbin:$PATH"

For an Ubuntu system, you'll also want to adjust the INSTALL_LIBPATH in the libbitcoinrpc Makefile to install to /usr/lib instead of /usr/local/lib:

$ emacs ~/libbitcoinrpc/Makefile  
...  
INSTALL_LIBPATH := $(INSTALL_PREFIX)/usr/lib

(If you prefer not to sully your /usr/lib, the alternative is to change your etc/ld.so.conf or its dependent files appropriately ... but for a test setup on a test machine, this is probably fine.)

Likewise, you'll also want to adjust the INSTALL_HEADERPATH in the libbitcoinrpc Makefile to install to /usr/include instead of /usr/local/include:

...  
INSTALL_HEADERPATH := $(INSTALL_PREFIX)/usr/include

Then you can compile:

$ cd libbitcoinrpc  
~/libbitcoinrpc$ make

gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc_err.o -c src/bitcoinrpc_err.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc_global.o -c src/bitcoinrpc_global.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc.o -c src/bitcoinrpc.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc_resp.o -c src/bitcoinrpc_resp.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc_cl.o -c src/bitcoinrpc_cl.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -o src/bitcoinrpc_method.o -c src/bitcoinrpc_method.c  
gcc -fPIC -O3 -g -Wall -Werror -Wextra -std=c99 -D VERSION="0.2" -shared -Wl,-soname,libbitcoinrpc.so.0 \  
src/bitcoinrpc_err.o src/bitcoinrpc_global.o src/bitcoinrpc.o src/bitcoinrpc_resp.o src/bitcoinrpc_cl.o src/bitcoinrpc_method.o \  
-o .lib/libbitcoinrpc.so.0.2 \  
-Wl,--copy-dt-needed-entries -luuid -ljansson -lcurl  
ldconfig -v -n .lib  
.lib:  
libbitcoinrpc.so.0 -> libbitcoinrpc.so.0.2 (changed)  
ln -fs libbitcoinrpc.so.0 .lib/libbitcoinrpc.so

If that works, you can install the package:

$ sudo make install  
Installing to  
install .lib/libbitcoinrpc.so.0.2 /usr/local/lib  
ldconfig -n /usr/local/lib  
ln -fs libbitcoinrpc.so.0 /usr/local/lib/libbitcoinrpc.so  
install -m 644 src/bitcoinrpc.h /usr/local/include  
Installing docs to /usr/share/doc/bitcoinrpc  
mkdir -p /usr/share/doc/bitcoinrpc  
install -m 644 doc/_.md /usr/share/doc/bitcoinrpc_  
_install -m 644 CREDITS /usr/share/doc/bitcoinrpc_  
_install -m 644 LICENSE /usr/share/doc/bitcoinrpc_  
_install -m 644 Changelog.md /usr/share/doc/bitcoinrpc_  
_Installing man pages_  
_install -m 644 doc/man3/bitcoinrpc_.gz /usr/local/man/man3

## Prepare Your Code

libbitcoinrpc has well-structured and simple methods for connecting to your bitcoind, executing RPC calls, and decoding the response.

To use libbitcoinrpc, make sure that your code files include the appropriate headers:

#include <jansson.h>  
#include <bitcoinrpc.h>

You'll also need to link in the appropriate libraries whenever you compile:

$ cc yourcode.c -lbitcoinrpc -ljansson -o yourcode

## Build Your Connection

Building the connection to your bitcoind server takes a few simple steps.

First, initialize the library:

bitcoinrpc_global_init();

Then connect to your bitcoind with bitcoinrpc_cl_init_params. The four arguments for bitcoinrpc_cl_init_params are username, password, IP address, and port. You should already know all of this information from your work with [Curl](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md). As you'll recall, the IP address 127.0.0.1 and port 18332 should be correct for the standard testnet setup described in these documents, while you can extract the user and password from ~/.bitcoin/bitcoin.conf.

$ cat bitcoin.conf  
server=1  
dbcache=1536  
par=1  
maxuploadtarget=137  
maxconnections=16  
rpcuser=StandUp  
rpcpassword=6305f1b2dbb3bc5a16cd0f4aac7e1eba  
rpcallowip=127.0.0.1  
debug=tor  
prune=550  
testnet=1  
[test]  
rpcbind=127.0.0.1  
rpcport=18332  
[main]  
rpcbind=127.0.0.1  
rpcport=8332  
[regtest]  
rpcbind=127.0.0.1  
rpcport=18443

Which you then place in the bitcoinrpc_cl_init_params:

bitcoinrpc_cl_t *rpc_client;  
rpc_client = bitcoinrpc_cl_init_params("StandUp", "6305f1b2dbb3bc5a16cd0f4aac7e1eba", "127.0.0.1", 18332);

> **MAINNET VS TESTNET:** The port would be 8332 for a mainnet setup.

If rpc_client is successfully initialized, you'll be able to send off RPC commands.

Later, when you're all done with your bitcoind connection, you should close it:

bitcoinrpc_global_cleanup();

### Test the Test Code

Test code can be found at [16_1_testbitcoin.c in the src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/16_1_testbitcoin.c). Download it to your testnet machine, then insert the correct RPC password (and change the RPC user if you didn't create your server with StandUp).

You can compile and run this as follows:

$ cc testbitcoin.c -lbitcoinrpc -ljansson -o testbitcoin  
$ ./testbitcoin  
Successfully connected to server!

> :warning: **WARNING:** If you forget to enter your RPC password in this or any other code samples that depend on RPC, you will receive a mysterious ERROR CODE 5.

## Make an RPC Call

In order to use an RPC method using libbitcoinrpc, you must initialize a variable of type bitcoinrpc_method_t. You do so with the appropriate value for the method you want to use, all of which are listed in the [bitcoinrpc Reference](https://github.com/BlockchainCommons/libbitcoinrpc/blob/master/doc/reference.md).

bitcoinrpc_method_t *getmininginfo = NULL;  
getmininginfo = bitcoinrpc_method_init(BITCOINRPC_METHOD_GETMININGINFO);

Usually you would set parameters next, but getmininginfo requires no parameters, so you can skip that for now.

You must also create two other objects, a "response object" and an "error object". They can be initialized as follows:

bitcoinrpc_resp_t *btcresponse = NULL;  
btcresponse = bitcoinrpc_resp_init();

bitcoinrpc_err_t btcerror;

You use the rpc_client variable that you already learned about in the previous test, and add on your getmininginfo method and the two other objects:

bitcoinrpc_call(rpc_client, getmininginfo, btcresponse, &btcerror);

### Output Your Response

You'll want to know what the RPC call returned. To do so, retrieve the output of your call as a JSON object with bitcoinrpc_resp_get and save it into a standard jansson object, of type json_t:

json_t *jsonresponse = NULL;  
jsonresponse = bitcoinrpc_resp_get(btcresponse);

If you want to output the complete JSON results of the RPC call, you can do so with a simple invocation of json_dumps, also from the jansson library:

printf ("%s\n", json_dumps(j, JSON_INDENT(2)));

However, since you're now writing complete programs, you probably want to do more subtle work, such as pulling out individual JSON values for specific usage. The [jansson Reference](https://jansson.readthedocs.io/en/2.10/apiref.html) details how to do so.

Just as when you were using [Curl](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md), you'll find that RPC returns a JSON object containing an id, an error, and most importantly a JSON object of the result.

The json_object_get function will let you retrieve a value (such as the result) from a JSON object by key:

json_t *jsonresult = NULL;  
jsonresult = json_object_get(jsonresponse,"result");  
printf ("%s\n", json_dumps (jsonresult, JSON_INDENT(2)));

However, you probably want to drill down further, to get a specific variable. Once you've retrieved the appropriate value, you will need to convert it to a standard C object by using the appropriate json_*_value function. For example, accessing an integer uses json_integer_value:

json_t *jsonblocks = NULL;  
jsonblocks = json_object_get(jsonresult,"blocks");

int blocks;  
blocks = json_integer_value(jsonblocks);  
printf("Block Count: %d\n",blocks);

> :warning: **WARNING:** It's extremely easy to segfault your C code when working with jansson objects if you get confused with what type of object you're retrieving. Make careful use of bitcoin-cli help to know what you should expect, and if you experience a segmentation fault, first look at your JSON retrieval functions.

### Test the Info Code

Retrieve the test code from [the src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/16_1_getmininginfo.c).

$ cc getmininginfo.c -lbitcoinrpc -ljansson -o getmininginfo  
$ ./getmininginfo  
Full Response: {  
"result": {  
"blocks": 1804406,  
"difficulty": 4194304,  
"networkhashps": 54842097951591.781,  
"pooledtx": 127,  
"chain": "test",  
"warnings": "Warning: unknown new rules activated (versionbit 28)"  
},  
"error": null,  
"id": "474ccddd-ef8c-4e3f-93f7-fde72fc08154"  
}

Just the Result: {  
"blocks": 1804406,  
"difficulty": 4194304,  
"networkhashps": 54842097951591.781,  
"pooledtx": 127,  
"chain": "test",  
"warnings": "Warning: unknown new rules activated (versionbit 28)"  
}

Block Count: 1804406

## Make an RPC Call with Arguments

But what if your RPC call _did_ have arguments?

### Create a JSON Array

To send parameters to your RPC call using libbitcoinrpc you have to wrap them in a JSON array. Since an array is just a simple listing of values, all you have to do is encode the parameters as ordered elements in the array.

Create the JSON array using the json_array function from jansson:

json_t *params = NULL;  
params = json_array();

You'll then reverse the procedure that you followed to access JSON values: you'll convert C-typed objects to JSON-typed objects using the json_* functions. Afterward, you'll append them to the array:

json_array_append_new(params,json_string(tx_rawhex));

Note that there are two variants to the append command: json_array_append_new, which appends a newly created variable, and json_array_append, which appends an existing variable.

This simple json_array_append_new methodology will serve for the majority of RPC commands with parameters, but some RPC commands require more complex inputs. In these cases you may need to create subsidiary JSON objects or JSON arrays, which you will then append to the parameters array as usual. The next section contains an example of doing so using createrawtransaction, which contains a JSON array of JSON objects for the inputs, a JSON object for the outputs, and the locktime parameter.

### Assign the Parameters

When you've created your parameters JSON array, you simply assign it after you've initialized your RPC method, as follows:

bitcoinrpc_method_set_params(rpc_method, params)

This section doesn't include a full example of this more complex methodology, but we'll see it in action multiple times in our first comprehensive RPC-based C program, in the next section.

## Summary: Accessing Bitcoind with C

By linking to the bitcoinrpc RPC and jansson JSON libraries, you can easily access bitcoind via RPC calls from a C library. To do so, you create an RPC connection, then make individual RPC calls, some of them with parameters. jansson then allows you to decode the JSON responses. The next section will demonstrate how this can be used for a pragmatic, real-world program.

- :fire: _**What is the power of C?**_ C allows you to take the next step beyond shell-scripting, permitting the creation of more comprehensive and robust programs.
    

## What's Next?

Learn more about "Talking to Bitcoind with C" in [16.2: Programming Bitcoind in C with RPC Libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_2_Programming_Bitcoind_with_C.md).

# 16.2: Programming Bitcoind in C with RPC Libraries

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

[§16.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_1_Accessing_Bitcoind_with_C.md) laid out the methodology for creating C programs using RPC and JSON libraries. We're now going to show the potential of those C libraries by laying out a simplistic, first cut of an actual Bitcoin program.

## Plan for Your Code

This section will create a simplistic first cut version of sendtoaddress, which will allow a user to send money to an address as long as he has a big enough UTXO. Here's what we need to do:

1. Request an address and an amount
    
2. Set an arbitrary fee
    
3. Prepare Your RPC
    
4. Find a UTXO that's large enough for the amount + the fee
    
5. Create a change address
    
6. Create a raw transaction that sends from the UTXO to the address and the change address
    
7. Sign the transaction
    
8. Send the transaction
    

### Plan for Your Future

Since this is your first functional C program, we're going to try and keep it simple (KISS). If we were producing an actual production program, we'd at least want to do the following:

1. Test and/or sanitize the inputs
    
2. Calculate a fee automatically
    
3. Think logically about which valid UTXO to use
    
4. Combine multiple UTXOs if necessary
    
5. Watch for more errors in the libbitcoinrpc or jansson commands
    
6. Watch for errors in the RPC responses
    

If you want to continue to expand this example, addressing the inadequacies of this example program would be a great place to start.

## Write Your Transaction Software

Your now ready to undertake that plan step by step

### Step 1: Request an Address and an Amount

Inputting the information is easy enough via command line arguments:

if (argc != 3) {

printf("ERROR: Only %i arguments! Correct usage is '%s [recipient] [amount]'\n",argc-1,argv[0]);  
exit(-1);

}

char *tx_recipient = argv[1];  
float tx_amount = atof(argv[2]);

printf("Sending %4.8f BTC to %s\n",tx_amount,tx_recipient);

> :warning: **WARNING:** A real program would need much better sanitization of these variables.

### Step 2: Set an Arbitrary Fee

This example just an arbitrary 0.0005 BTC fee to ensure that the test transactions goes through quickly:

float tx_fee = 0.0005;  
float tx_total = tx_amount + tx_fee;

> :warning: **WARNING:** A real program would calculate a fee that minimized cost while ensuring the speed was sufficient for the sender.

### Step 3: Prepare Your RPC

Obviously, you're going to need to get all of your variables ready again, as discussed in [§16.1: Accessing Bitcoind with C](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_1_Accessing_Bitcoind_with_C.md). You also need to initialize your library, connect your RPC client, and prepare your response object:

bitcoinrpc_global_init();  
rpc_client = bitcoinrpc_cl_init_params ("bitcoinrpc", "YOUR-RPC-PASSWD", "127.0.0.1", 18332);  
btcresponse = bitcoinrpc_resp_init();

### Step 4: Find a UTXO

To find a UTXO you must call the listunspent RPC:

rpc_method = bitcoinrpc_method_init(BITCOINRPC_METHOD_LISTUNSPENT);  
bitcoinrpc_call(rpc_client, rpc_method, btcresponse, &btcerror);

However, the real work comes in decoding the response. The previous section noted that the jansson library was "somewhat clunky" and this is why: you have to create (and clear) a very large set of json_t objects in order to dig down to what you want.

First, you must retrieve the result field from JSON:

json_t *lu_response = NULL;  
json_t *lu_result = NULL;

lu_response = bitcoinrpc_resp_get (btcresponse);  
lu_result = json_object_get(lu_response,"result");

> :warning: **WARNING:** You only get a result if there wasn't an error. Here's another place for better error checking for production code.

Then, you go into a loop, examining each unspent transaction, which appears as an element in your JSON result array:

int i;

const char *tx_id = 0;  
int tx_vout = 0;  
double tx_value = 0.0;

for (i = 0 ; i < json_array_size(lu_result) ; i++) {

json_t *lu_data = NULL;  
lu_data = json_array_get(lu_result, i);

json_t *lu_value = NULL;  
lu_value = json_object_get(lu_data,"amount");  
tx_value = json_real_value(lu_value);

Is the UTXO large enough to pay out your transaction? If so, grab it!

> :warning: **WARNING:** A real-world program would think more carefully about which UTXO to grab, based on size and other factors. It probably wouldn't just grab the first thing it saw that worked.

if (tx_value > tx_total) {

json_t *lu_txid = NULL;    
lu_txid = json_object_get(lu_data,"txid");    
tx_id = strdup(json_string_value(lu_txid));    
  
json_t *lu_vout = NULL;    
lu_vout = json_object_get(lu_data,"vout");    
tx_vout = json_integer_value(lu_vout);    
  
json_decref(lu_value);    
json_decref(lu_txid);    
json_decref(lu_vout);    
json_decref(lu_data);    
break;  

}

You should clear your main JSON elements as well:

}

json_decref(lu_result);  
json_decref(lu_response);

> :warning: **WARNING:** A real-world program would also make sure the UTXOs were spendable.

If you didn't find any large-enough UTXOs, you'll have to report that sad fact to the user ... and perhaps suggest that they should use a better program that will correctly merge UTXOs.

if (!tx_id) {

printf("Very Sad: You don't have any UTXOs larger than %f\n",tx_total);  
exit(-1);  
}

> **WARNING:** A real program would use subroutines for this sort of lookup, so that you could confidentally call various RPCs from a library of C functions. We're just going to blob it all into main as part of our KISS philosophy of simple examples.

### Step 5: Create a Change Address

Repeat the standard RPC-lookup methodology to get a change address:

rpc_method = bitcoinrpc_method_init(BITCOINRPC_METHOD_GETRAWCHANGEADDRESS);

if (!rpc_method) {

printf("ERROR: Unable to initialize listunspent method!\n");  
exit(-1);

}

bitcoinrpc_call(rpc_client, rpc_method, btcresponse, &btcerror);

if (btcerror.code != BITCOINRPCE_OK) {

printf("Error: listunspent error code %d [%s]\n", btcerror.code,btcerror.msg);

exit(-1);

}

lu_response = bitcoinrpc_resp_get (btcresponse);  
lu_result = json_object_get(lu_response,"result");  
char *changeaddress = strdup(json_string_value(lu_result));

The only difference is in what particular information is extracted from the JSON object.

> :warning: **WARNING:** Here's a place that a subroutine would be really nice: to abstract out the whole RPC method initialization and call.

### Step 6: Create a Raw Transaction

Creating the actual raw transaction is the other tricky part of programming your sendtoaddress replacement. That's because it requires the creation of a complex JSON object as a paramter.

To correctly create these parameters, you'll need to review what the createrawtransaction RPC expects. Fortunately, this is easy to determine using the bitcoin-cli help functionality:

$ bitcoin-cli help createrawtransaction  
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,"data":"hex",...} ( locktime )

To review, your inputs will be a JSON array containing one JSON object for each UTXO. Then the outputs will all be in one JSON object. It's easiest to create these JSON elements from the inside out, using jansson commands.

#### Step 6.1: Create the Input Parameters

To create the input object for your UTXO, use json_object, then fill it with key-values using either json_object_set_new (for newly created references) or json_object_set (for existing references):

json_t *inputtxid = NULL;  
inputtxid = json_object();

json_object_set_new(inputtxid,"txid",json_string(tx_id));  
json_object_set_new(inputtxid,"vout",json_integer(tx_vout));

You'll note that you again have to translate each C variable type into a JSON variable type using the appropriate function, such as json_string or json_integer.

To create the overall input array for all your UTXOs, use json_array, then fill it up with objects using json_array_append:

json_t *inputparams = NULL;  
inputparams = json_array();  
json_array_append(inputparams,inputtxid);

#### Step 6.2: Create the Output Parameters

To create the output array for your transaction, follow the same format, creating a JSON object with json_object, then filling it with json_object_set:

json_t *outputparams = NULL;  
outputparams = json_object();

char tx_amount_string[32];  
sprintf(tx_amount_string,"%.8f",tx_amount);  
char tx_change_string[32];  
sprintf(tx_change_string,"%.8f",tx_value - tx_total);

json_object_set(outputparams, tx_recipient, json_string(tx_amount_string));  
json_object_set(outputparams, changeaddress, json_string(tx_change_string));

> :warning: **WARNING:** You might expect to input your Bitcoin values as numbers, using json_real. Unfortunately, this exposes one of the major problems with integrating the jansson library and Bitcoin. Bitcoin is only valid to eight significant digits past the decimal point. You might recall that .00000001 BTC is a satoshi, and that's the smallest possible division of a Bitcoin. Doubles in C offer more significant digits than that, though they're often imprecise out past eight decimals. If you try to convert straight from your double value in C (or a float value, for that matter) to a Bitcoin value, the imprecision will often create a Bitcoin value with more than eight significant digits. Before Bitcoin Core 0.12 this appears to work, and you could use json_real. But as of Bitcoin Core 0.12, if you try to give createrawtransaction a Bitcoin value with too many significant digits, you'll instead get an error and the transaction will not be created. As a result, if the Bitcoin value has _ever_ become a double or float, you must reformat it to eight significant digits past the digit before feeding it in as a string. This is obviously a kludge, so you should make sure it continues to work in future versions of Bitcoin Core.

#### Step 6.3: Create the Parameter Array

To finish creating your parameters, simply bundle them all up in a JSON array:

json_t *params = NULL;  
params = json_array();  
json_array_append(params,inputparams);  
json_array_append(params,outputparams);

#### Step 6.4 Make the RPC Call

Use the normal method to create your RPC call:

rpc_method = bitcoinrpc_method_init(BITCOINRPC_METHOD_CREATERAWTRANSACTION);

However, now you must feed it your parameters. This simply done with bitcoinrpc_method_set_params:

if (bitcoinrpc_method_set_params(rpc_method, params) != BITCOINRPCE_OK) {

fprintf (stderr, "Error: Could not set params for createrawtransaction");

}

Afterward, run the RPC and get the results as usual:

bitcoinrpc_call(rpc_client, rpc_method, btcresponse, &btcerror);

lu_response = bitcoinrpc_resp_get(btcresponse);  
lu_result = json_object_get(lu_response,"result");

char *tx_rawhex = strdup(json_string_value(lu_result));

### Step 7. Sign the Transaction

It's a lot easier to assign a simple parameter to a function. You just create a JSON array, then assign the parameter to the array:

params = json_array();  
json_array_append_new(params,json_string(tx_rawhex));

Sign the transaction by following the typical rigamarole for creating an RPC call:

rpc_method = bitcoinrpc_method_init(BITCOINRPC_METHOD_SIGNRAWTRANSACTION);  
if (bitcoinrpc_method_set_params(rpc_method, params) != BITCOINRPCE_OK) {

fprintf (stderr, "Error: Could not set params for signrawtransaction");

}

json_decref(params);

bitcoinrpc_call(rpc_client, rpc_method, btcresponse, &btcerror);  
lu_response = bitcoinrpc_resp_get(btcresponse);

Again, using jansson to access the output can be a little tricky. Here you have to remember that hex is part of a JSON object, not a standalone result, as was the case when you created the raw transaction. Of course, you can always access this information from command line help: bitcoin-cli help signrawtransaction:

lu_result = json_object_get(lu_response,"result");  
json_t *lu_signature = json_object_get(lu_result,"hex");  
char *tx_signrawhex = strdup(json_string_value(lu_signature));  
json_decref(lu_signature);

> :warning: _**WARNING:**_ A real-world program would obviously carefully test the response of every RPC command to make sure there were no errors. That's especially true for signrawtransaction, because you might end up with a partially signed transaction. Worse, if you don't check the errors in the JSON object, you'll just see the hex and not realize that it's either unsigned or partially signed.

### Step 8. Send the Transaction

You can now send your transaction, using all of the previous techniques:

params = json_array();  
json_array_append_new(params,json_string(tx_signrawhex));

rpc_method = bitcoinrpc_method_init(BITCOINRPC_METHOD_SENDRAWTRANSACTION);

if (bitcoinrpc_method_set_params(rpc_method, params) != BITCOINRPCE_OK) {

fprintf (stderr, "Error: Could not set params for sendrawtransaction");

}

json_decref(params);

bitcoinrpc_call(rpc_client, rpc_method, btcresponse, &btcerror);  
lu_response = bitcoinrpc_resp_get(btcresponse);  
lu_result = json_object_get(lu_response,"result");

char *tx_newid = strdup(json_string_value(lu_result));

printf("Txid: %s\n",tx_newid);

The entire code, with a _little_ more error-checking appears in the Appendix.

## Test Your Code

The complete code can be found in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/16_2_sendtoaddress.c).

Compile this as usual:

$ cc sendtoaddress.c -lbitcoinrpc -ljansson -o sendtoaddress

You can then use it to send funds to an address:

./sendtoaddress tb1qynx7f8ulv4sxj3zw5gqpe56wxleh5dp9kts7ns .001  
Txid: b93b19396f8baa37f5f701c7ca59d3128144c943af5294aeb48e3eb4c30fa9d2

You can see information on this transaction that we sent [here](https://live.blockcypher.com/btc-testnet/tx/b93b19396f8baa37f5f701c7ca59d3128144c943af5294aeb48e3eb4c30fa9d2/).

## Summary: Programming Bitcoind with C

With access to a C library, you can create much more fully featured programs than it was reasonable to do so with shell scripts. But, it can take a lot of work! Even at 316 lines of code, sendtoaddress.c doesn't cover nearly all of the intricacies requires to safely and intelligently transact bitcoins.

## What's Next?

Learn more about "Talking to Bitcoind with C" in [16.3: Receiving Notifications in C with ZMQ Libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_3_Receiving_Bitcoind_Notifications_with_C.md).

# 16.3 Receiving Notifications in C with ZMQ Libraries

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

[§16.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_1_Accessing_Bitcoind_with_C.md) and [§16.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_2_Programming_Bitcoind_with_C.md) introduced RPC and JSON libraries for C, and in doing so showed one of the advantages of accessing Bitcoin's RPC commands through a programming language: the ability to reasonably create much more complex programs. This chapter introduces a third library, for [ZMQ](http://zeromq.org/), and in doing so reveals another advantage: the ability to monitor for notifications. It will use that for coding a blockchain listener.

> :book: _**What is ZMQ?**_ ZeroMQ (ZMQ)is a high-performance asynchronous messaging library that provides a message queue. ZeroMQ supports common messaging patterns (pub/sub, request/reply, client/server, and others) over a variety of transports (TCP, in-process, inter-process, multicast, WebSocket, and more), making inter-process messaging as simple as inter-thread messaging. You can find more details about ZMQ notifications and others kind of messages in [this repo](https://github.com/Actinium-project/ChainTools/blob/master/docs/chainlistener.md).

## Set Up ZMQ

Before you can create a blockchain listener, you will need to configure bitcoind to allow ZMQ notifications, and then you'll need to install a ZMQ library to take advantage of those notifications.

### Configure bitcoind for ZMQ

Bitcoin Core is ZMQ-ready, but you must specify ZMQ endpoints. ZeroMQ publish-sockets prepend each data item with an arbitrary topic prefix that allows subscriber clients to request only those items with a matching prefix. There are currently four topics supported by bitcoind:

$ bitcoind --help | grep zmq | grep address  
-zmqpubhashblock=  
-zmqpubhashtx=  
-zmqpubrawblock=  
-zmqpubrawtx=

You can run bitcoind with command-line arguments for ZMQ endpoints, as shown above, but you can also make an endpoint accessible by adding appropriate lines to your ~/.bitcoin/bitcoin.conf file and restarting your daemon.

zmqpubrawblock=tcp://127.0.0.1:28332  
zmqpubrawtx=tcp://127.0.0.1:28333

You can then test your endpoints are working using the getzmqnotifications RPC:

$ bitcoin-cli getzmqnotifications  
[  
{  
"type": "pubrawblock",  
"address": "tcp://127.0.0.1:28332",  
"hwm": 1000  
},  
{  
"type": "pubrawtx",  
"address": "tcp://127.0.0.1:28333",  
"hwm": 1000  
}  
]

Your bitcoind will now issue ZMQ notifications

### Install ZMQ

To take advantage of those notifications, you need a ZMQ library to go with C; we'll thus be using a new ZMQ library instead of the libbitcoinrpc library in this section, but when you're experimenting in the future, you'll of course be able to combine them.

Fortunately, ZMQ libraries are available through standard Debian packages:

$ sudo apt-get install libzmq3-dev  
$ sudo apt-get install libczmq-dev

You're now ready to code!

## Write Your Notification Program

The following C program is a simple client that subscribes to a ZMQ connection point served by bitcoind and reads incoming messages.

The program requires two parameters: the first parameter is the "server", which is the TCP connection point exposed by bitcoind; and the second is the "topic", which is currently zmqpubhashblock, zmqpubhashtx, zmqpubrawblock, or zmqpubrawtx. The topic must be supported through the bitcoin.conf and the server's IP address and port must match what's defined there.

#include <czmq.h>  
int main(int argc, char ** argv) {

char *zmqserver;  
char *topic;

if (argc < 3) {  
printf("\nUSAGE:\nchainlistener [tcp://localhost:port](tcp://localhost:port) \n\n");  
return 0;  
} else {  
zmqserver = argv[1];  
topic = argv[2];  
}

You will open a ZMQ socket to the defined server for the defined topic:

zsock_t *socket = zsock_new_sub(zmqserver, topic);  
assert(socket);

After that, you wait:

while(1) {  
zmsg_t *msg;  
int rc = zsock_recv(socket, "m", &msg);  
assert(rc == 0);

char *header = zmsg_popstr(msg);    
zframe_t *zdata = zmsg_pop(msg);    
unsigned int *no = (unsigned int*)zmsg_popstr(msg);    
  
char *data = zframe_strhex(zdata);    
int len = zframe_size(zdata);    
printf("Size: %d\n", len);    
printf("Data: %s", data);    
printf("\nNo: %d\n", *no);    
  
free(header);    
free(data);    
free(no);    
free(zdata);    
zmsg_destroy(&msg);    
sleep(1);  

}

While, waiting, you watch for messages on the ZMQ socket. Whenever you receive a message, you will pop it off the stack and report out its number, its length, and most importantly the data.

That's it!

Of course when you're done, you should clean up:

zsock_destroy(&socket);  
return 0;  
}

### Test the Notification Code

The source code is in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/16_3_chainlistener.c) as usual. You should compile it:

$ cc -o chainlistener chainlistener.c -I/usr/local/include -L/usr/local/lib -lzmq -lczmq

Afterward, you can run it with the topics and addresses that you defined in your bitcoin.conf:

$ ./chainlistener tcp://127.0.0.1:28333 rawtx  
Size: 250  
Data: 02000000000101F5BD2032E5A9E6650D4E411AD272E391F26AFC3C9102B7C0C7444F8F74AE86010000000017160014AE9D51ADEEE8F46ED2017F41CD631D210F2ED9C5FEFFFFFF0203A732000000000017A9147231060F1CDF34B522E9DB650F44EDC6C0714E4C8710270000000000001976A914262437B129CF8592AB2EDC59C07D19C57729F72888AC02483045022100AE316D5F21657E3525271DE39EB285D8A0E89A20AB6413824E88CE47DCD0EFE702202F61E10C2A8F4A7125D5EB63AEF883D8E3584A0ECED0D349283AABB6CA5E066D0121035A77FE575A9005E3D3FF0682E189E753E82FA8BFF0A20F8C45F06DC6EBE3421079111B00  
No: 67  
Size: 249  
Data: 0200000000010165C986992F7DAD22BBCE3FCF0BF546EDBC3C599618B04CFA22D9E64EF0CE4C030000000017160014B58E0A5CD68B249F1C407E9AAE9CD0332AAA3067FEFFFFFF02637932000000000017A914CCC47261489036CB6B9AA610857793FF5752E5378710270000000000001976A914262437B129CF8592AB2EDC59C07D19C57729F72888AC0247304402206CCC3F3B4BE01D4E532A01C2DC6BC3B53E4FFB6B494C8B87DD603EFC648A159902201653841E8B16A814DC375129189BB7CF01CFF7D269E91178645B6A97F5C7F4F10121030E20F3D2F172281B8DC747F007DF24B352248AC09E48CA64016942A8F01D317079111B00  
No: 68  
Size: 250  
Data: 02000000000101E889CFC1FFE127BA49F6C1011388606A194109AE1EDAAB9BEE215E123C14A7920000000017160014577B0B3C2BF91B33B5BD70AE9E8BD8144F4B87E7FEFFFFFF02C34B32000000000017A914A9F1440402B46235822639C4FD2F78A31E8D269E8710270000000000001976A914262437B129CF8592AB2EDC59C07D19C57729F72888AC02483045022100B46318F53E1DCE63E7109DB4FA54AF40AADFC2FEB0E08263756BC3B7A6A744CB02200851982AF87DBABDC3DFC3362016ECE96AECFF50E24D9DCF264AE8966A5646FE0121039C90FCB46AEA1530E5667F8FF15CB36169D2AD81247472F236E3A3022F39917079111B00  
No: 69  
Size: 250  
Data: 0200000000010137527957C9AD6CFF0C9A74597E6EFCD7E1EBD53E942AB2FA34A831046CA11488000000001716001429BFF05B3CD79E9CCEFDB5AE82139F72EB3E9DB0FEFFFFFF0210270000000000001976A914262437B129CF8592AB2EDC59C07D19C57729F72888AC231E32000000000017A9146C8D5FE29BFDDABCED0D6F4D8E82DCBFD9D34A8B8702483045022100F259846BAE29EB2C7A4AD711A3BC6109DE69AE91E35B14CA2742157894DD9760022021464E09C00ABA486AEAA0C49FEE12D2850DC03F57F04A1A9E2CC4D0F4F1459C012102899F24A9D60132F4DD1A5BA6DCD1E4E4B6C728927BA482C2C4E511679F60CA5779111B00  
No: 70  
.......

### Summary Receiving Bitcoind Notifications with C.md

By using the ZMQ framework, you can easily receive notifications by subscribing to a connection point exposed by bitcoind through its configuration file.

> :fire: _**What is the Power of Notifications?**_ With notifications, you're no longer entirely dependent upon users to issue commands. Instead, you can create programs that monitor the Bitcoin blockchain and take appropriate actions when certain things occur. This in turn could be merged with the RPC commands that you programmed in previous sections. This is also a big step beyond what you could do with shell scripts: certainly, you can create infinite-loop listener shell scripts, but programming languages tend to be a better tool for that task.

## What's Next?

Learn more about "Programming with RPC" in [Chapter 17: Programming Bitcoin with Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_0_Programming_with_Libwally.md).

# Chapter 17: Programming with Libwally

The previous chapter presented three C Libraries, for RPC, JSON, and ZMQ, all of which are intended to interact directly with bitcoind, just like you've been doing since the start. But, sometimes you might want to code without direct access to a bitcoind. This might be due to an offline client, or just because you want to keep some functionality internal to your C program. You also might want to get into deeper wallet functionality, like mnemonic word creation or address derivation. That's where Libwally comes in: it's a wallet library for C, C++, Java, NodeJS, or Python, with wrappers also available for other languages, such as Swift.

This chapter touches upon the functionality possible within Libwally, most of which complements the work you've done through RPC access to bitcoind, but some of which replicates it. It also shows how to integrate that work with the RPC clients that you're more familiar with. However, note that this is just the barest introduction to Libwally. Several of its more important function sets are highlighted, but we never do more than stick our toes in. If you find its functions useful or intriguing, then you'll need to dig in much more deeply than this course can cover.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Use Wallet Functions with Libwally
    
- Perform Manipulations of PSBTs and Transactions with Libwally
    
- Implement Designs that Mix Libwally and RPC Work
    

Supporting objectives include the ability to:

- Understand BIP39 Mnemonic Words
    
- Understand More about BIP32 Hierarchical Wallets
    
- Summarize the Functional Depth of Libwally
    

## Table of Contents

- [Section One: Setting Up Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_1_Setting_Up_Libwally.md)
    
- [Section Two: Using BIP39 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_2_Using_BIP39_in_Libwally.md)
    
- [Section Three: Using BIP32 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_3_Using_BIP32_in_Libwally.md)
    
- [Section Four: Using PSBTs in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_4_Using_PSBTs_in_Libwally.md)
    
- [Section Five: Using Scripts in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_5_Using_Scripts_in_Libwally.md)
    
- [Section Six: Using Other Functions in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_6_Using_Other_Functions_in_Libwally.md)
    
- [Section Seven: Integrating Libwally and Bitcoin-CLI](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_7_Integrating_Libwally_and_Bitcoin-CLI.md)
    

# 17.1: Setting Up Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This first section will explain how to download the Libwally C Library and get it working.

> :book: _**What is Libwally?**_ Libwally is a library of primitives helpful for the creation of wallets that is cross-platform and cross-language, so that the same functions can be used everywhere. There are [online docs](https://wally.readthedocs.io/en/latest/). Libwally is made available as part of Blockstream's [Elements Project](https://github.com/ElementsProject).

## Install Libwally

As usual, you'll need some packages on your system:

$ sudo apt-get install git  
$ sudo apt-get install dh-autoreconf

You can then download Libwally from its Git repo:

$ git clone [https://github.com/ElementsProject/libwally-core](https://github.com/ElementsProject/libwally-core)

Afterward, you can begin the configuration process:

$ ./tools/autogen.sh

As with libbitcoinrpc, you may wish to install this in /usr/include and /usr/lib for ease of usage. Just modify the appropriate line in the configure program:

## < ac_default_prefix=/usr

> ac_default_prefix=/usr/local

Afterward you can finish your prep:

$ ./configure  
$ make

You can then verify that tests are working:

# $ make check  
Making check in src  
make[1]: Entering directory '/home/standup/libwally-core/src'  
Making check in secp256k1  
make[2]: Entering directory '/home/standup/libwally-core/src/secp256k1'  
make check-TESTS  
make[3]: Entering directory '/home/standup/libwally-core/src/secp256k1'  
make[4]: Entering directory '/home/standup/libwally-core/src/secp256k1'

# Testsuite summary for libsecp256k1 0.1

# TOTAL: 0

# PASS: 0

# SKIP: 0

# XFAIL: 0

# FAIL: 0

# XPASS: 0

# ERROR: 0

# ============================================================================  
make[4]: Leaving directory '/home/standup/libwally-core/src/secp256k1'  
make[3]: Leaving directory '/home/standup/libwally-core/src/secp256k1'  
make[2]: Leaving directory '/home/standup/libwally-core/src/secp256k1'  
make[2]: Entering directory '/home/standup/libwally-core/src'  
make check-TESTS check-local  
make[3]: Entering directory '/home/standup/libwally-core/src'  
make[4]: Entering directory '/home/standup/libwally-core/src'  
PASS: test_bech32  
PASS: test_psbt  
PASS: test_psbt_limits  
PASS: test_tx

# Testsuite summary for libwallycore 0.7.8

# TOTAL: 4

# PASS: 4

# SKIP: 0

# XFAIL: 0

# FAIL: 0

# XPASS: 0

# ERROR: 0

============================================================================  
make[4]: Leaving directory '/home/standup/libwally-core/src'  
make[3]: Nothing to be done for 'check-local'.  
make[3]: Leaving directory '/home/standup/libwally-core/src'  
make[2]: Leaving directory '/home/standup/libwally-core/src'  
make[1]: Leaving directory '/home/standup/libwally-core/src'  
make[1]: Entering directory '/home/standup/libwally-core'  
make[1]: Nothing to be done for 'check-am'.  
make[1]: Leaving directory '/home/standup/libwally-core'

Finally, you can install:

$ sudo make install

## Prepare for Libwally

So how do you use Libwally in a program? As usual, you'll need to include appropriate files and link appropriate libraries for your code.

### Include the Files

There are a considerable number of possible include files:

$ ls /usr/include/wally*  
/usr/include/wally_address.h /usr/include/wally_bip39.h /usr/include/wally_elements.h /usr/include/wally_script.h  
/usr/include/wally_bip32.h /usr/include/wally_core.h /usr/include/wally.hpp /usr/include/wally_symmetric.h  
/usr/include/wally_bip38.h /usr/include/wally_crypto.h /usr/include/wally_psbt.h /usr/include/wally_transaction.h

Fortunately, the file names largely match the sections in the [docs](https://wally.readthedocs.io/en/latest/), so you should be able to include the correct files based on what you're doing, after including the ubiquitous wally_core.h.

### Link the Libraries

You also will need to link appropriate libraries:

$ ls /usr/lib/libsecp* /usr/lib/libwally*  
/usr/lib/libsecp256k1.a /usr/lib/libwallycore.la /usr/lib/libwallycore.so.0  
/usr/lib/libsecp256k1.la /usr/lib/libwallycore.so /usr/lib/libwallycore.so.0.0.0

Mostly, you'll be using libwallycore.

## Set Up a Libwally Program

Compared to some of the previous libraries, Libwally is ridiculously easy to initialize:

lw_response = wally_init(0);

And then when you're done, there's a handy function to clean up any allocated memory:

wally_cleanup(0);

In both cases, the argument is for flags, but is currently set to 0.

## Test a Test Libwally Program

The src directory contains [testwally.c](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_1_testwally.c), which just shows how the initialize and cleanup functions work.

You can compile it as follows:

$ cc testwally.c -lwallycore -o testwally

Afterward you can run it:

$ ./testwally  
Startup: 0

The "Startup" value is the return from wally_init. The 0 value may initially appear discouraging, but it's's what you want to see:

include/wally_core.h:#define WALLY_OK 0 /** Success */

## Install Libsodium

You should also install Libsodium to get access to a high quality random number generator for testing purposes.

> :warning: **WARNING:** The generation of random numbers can be one of the greatest points of vulnerability in any Bitcoin software. If you do it wrong, you expose your users to attacks because they end up with insecure Bitcoin keys, and this isn't a [theoretical problem](https://github.com/BlockchainCommons/SmartCustodyBook/blob/master/manuscript/03-adversaries.md#adversary-systemic-key-compromise). BlockchainInfo once incorrectly generated 0.0002% of their keys, which resulted in the temporary loss of 250 Bitcoins. Bottom line: make sure you're totally comfortable with your random number generation. It might be Libsodium, or it might be an even more robust TRNG method.

You can download a [Libsodium tarball](https://download.libsodium.org/libsodium/releases/) and then follow the instructions at [Libsodium installation](https://doc.libsodium.org/installation) to install.

First, untar:

$ tar xzfv /tmp/libsodium-1.0.18-stable.tar.gz

Then, adjust the configure file exactly as you have the other libraries to date:

## < ac_default_prefix=/usr

> ac_default_prefix=/usr/local

Finally, make, check, and install:

# $ make  
$ make check  
...

# Testsuite summary for libsodium 1.0.18

# TOTAL: 77

# PASS: 77

# SKIP: 0

# XFAIL: 0

# FAIL: 0

# XPASS: 0

# ERROR: 0

============================================================================  
...  
$ sudo make install

This course will only use libsodium for one small (but crucial!) bit of entropy generation, but watch for it in the next section.

## Summary: Setting Up Libwally

By installing the Libwally (and Libsodium) includes and libraries, you gain access to a number of cryptographic and wallet functions, which can complement your RPC and ZMQ libraries (or your command-line bitcoin-cli).

So what precisely can you do now? That's what the rest of this chapter is about.

## What's Next?

Learn more about "Programming Bitcoin with Libwally" in [17.2: Using BIP39 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_2_Using_BIP39_in_Libwally.md).

# 17.2: Using BIP39 in Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

One of Libwally's greatest powers is that it can lay bare the underlying work of generating seeds, private keys, and ultimately addresses. To start with, it supports [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), which is the BIP that defines mnemonic codes for Bitcoin — something that's entirely unsupported, to date, by Bitcoin Core.

> :book: _**What is a Mnemonic Code?**_ Bitcoin addresses (and their corresponding private keys and underlying seeds) are long, unintelligible lists of characters and numbers, which are not only impossible to remember, but also easy to mistype. Mnemonic codes are a solution for this that allow users to record 12 (or 24) words in their language — something that's much less prone to mistakes. These codes can then be used to fully restore a BIP32 seed that's the basis of an HD wallet. :book: _**What is a Seed?**_ We briefly touched on seeds in [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md). It's the random number that's used to generate a whole sequence of private keys (and thus addresses) in an HD wallet. We'll return to seeds in the next section, which is all about HD wallets and Libwally. For now, just know that a BIP39 mnemonic code corresponds to the seed for a BIP32 hierarchical deterministic wallet.

## Create Mnemonic Codes

All Bitcoin keys start with entropy. This first use of Libwally, and its BIP39 mnemonics, thus shows how to generate entropy and to get a mnemonic code from that.

> :book: _**What is Entropy?**_ Entropy is a fancy way of saying randomness, but it's a carefully measured randomness that's used as the foundation of a true-random-number generated (TRG). Its measured in "bits", with more bits of entropy resulting in more randomness (and thus more protection for what's being generated). For Bitcoin, entropy is the foundation of your seed, which in an HD wallet generates all of your addresses.

You'll always start work with Libwally by initializing the library and testing the results, as first demonstrated in [§17.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_1_Setting_Up_Libwally.md):

int lw_response;

lw_response = wally_init(0);

if (lw_response) {

printf("Error: Wally_init failed: %d\n",lw_response);    
exit(-1);  

}

Now you're ready to entropize.

### Create Entropy

Using libsodium, you can create entropy with the randombytes_buf command:

unsigned char entropy[16];  
randombytes_buf(entropy, 16);

This example, which will be the only way we use the libsodium library, creates 16 bytes of entropy. Generally, to create a secure mnemonic code, you should use between 128 and 256 bits of entropy, which is 16 to 32 bytes.

> :warning: **WARNING:** Again, be very certain that you're very comfortable with your method for entropy generation before you use it in a real-world program.

### Translate into a Mnemonic

16 bytes of entropy is sufficient to create a 12-character Mnemonic code, which is done with Libwally's bip39_mnemonic_from_bytes function:

char *mnem = NULL;  
lw_response = bip39_mnemonic_from_bytes(NULL,entropy,16,&mnem);

Note that you have to pass along the byte size, so if you were to increase the size of your entropy, to generate a longer mnemonic phrase, you'd also need to increase the value in this function.

> **NOTE:** There are mnemonic word lists for different languages! The default is to use the English-language list, which is the NULL variable in these Libwally mnemonic commands, but you can alternatively request a different language!

That's it! You've created a mnemonic phrase!

> :book: _**How is the Mnemonic Phrase Created?**_ You can learn about that in [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), but if you prefer, Greg Walker has an [excellent example](https://learnmeabitcoin.com/technical/mnemonic): basically, you add a checksum, then you covert each set of 11 bits into a word from the word list. You can do this with the commands bip39_get_wordlist and bip39_get_word if you don't trust the bip39_mnemonic_from_bytes command.

### Translate into a Seed

There are some functions, such as bip32_key_from_seed (which we'll meet in the next section) that require you to have the seed rather than the Mnemonic. The two things are functionally identical: if you have the seed, you can generate the mnemonic, and vice-versa.

If you need to generate the seed from your mnemonic, you just use the bip39_mnemonic_to_seed command:

unsigned char seed[BIP39_SEED_LEN_512];  
size_t seed_len;

lw_response = bip39_mnemonic_to_seed(mnem,NULL,seed,BIP39_SEED_LEN_512,&seed_len);

Note that all BIP39 seeds are current 512 bytes; nonetheless you have to set the size of your variable appropriately, and pass along that size to bip39_mnemonic_to_seed.

### Print Your Seed

If you want to see what your seed looks like in hex, you can use the wally_hex_from_bytes function to turn your seed into a readable (but not-great-for-people) hex code:

char *seed_hex;  
wally_hex_from_bytes(seed,sizeof(seed),&seed_hex);  
printf("Seed: %s\n",seed_hex);

If you've done everything right, you should get back a 64-byte seed. (That's the BIP39_SEED_LEN_512 variable you've been throwing around, which defines a default seed length as 512 bits or 64 bytes.)

> :warning: **WARNING:** You definitely should test that your seed length is 64 bytes in some way, because it's easy to mess up, for example by using the wrong variable type when you run bip39_mnemonic_to_seed.

## Test Mnemonic Code

The full code for generating entropy, generating a BIP39 mnemonic, validating the mnemonic, and generating a seed can be found in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_2_genmnemonic.c). Download it and compile:

$ cc genmnemonic.c -lwallycore -lsodium -o genmnemonic

Then you can run the test:

Mnemonic: parent wasp flight sweet miracle inject lemon matter label column canyon trend  
Mnemonic validated!  
Seed: 47b04cfb5d8fd43d371497f8555a27a25ca0a04aafeb6859dd4cbf37f6664b0600c4685c1efac29c082b1df29081f7a46f94a26f618fc6fd38d8bc7b6cd344c7

## Summary: Using BIP39 in Libwally

BIP39 allows you generate a set of 12-24 Mnemonic words from a seed (and the Libwally library also allows you to validate it!).

> :fire: _**What is the power of BIP39?**_ Bitcoin seeds and private keys are prone to all sorts of lossage. You mistype a single digit, and your money is gone forever. Mnemonic Words are a much more user-friendly way of representing the same data, but because they're words in the language of the user's choice, they're less prone to mistakes. The power of BIP39 is thus to improve the accessibility, usability, and safety of Bitcoin. :fire: _**What is the power of BIP39 in Libwally?**_ Bitcoind doesn't currently support mnemonic words, so using Libwally can allow you to generate mnemonic words in conjunction with addresses held by bitcoind (though as we'll see in §17.7, it requires a bit of a work-around at present to import your keys into Bitcoin Core).

## What's Next?

Learn more about "Programming Bitcoin with Libwally" in [17.3: Using BIP32 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_3_Using_BIP32_in_Libwally.md).

# 17.3: Using BIP32 in Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

In [§17.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_2_Using_BIP39_in_Libwally.md), you were able to use entropy to generate a seed and its related mnemonic. As you may recall from [§3.5: Understanding the Descriptor](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md), a seed is the basis of a Hierchical Deterministic (HD) Wallet, where that single seed can be used to generate many addresses. So how do you get from the seed to actual addresses? That's where [BIP32](https://en.bitcoin.it/wiki/BIP_0032) comes in.

## Create an HD Root

To create a HD address requires starting with a seed, and then walking down the hierarchy until the point that you create addresses.

That starts off easily enough, you just generate a seed, which you already did in the previous section:

unsigned char entropy[16];  
randombytes_buf(entropy, 16);

char *mnem = NULL;  
lw_response = bip39_mnemonic_from_bytes(NULL,entropy,16,&mnem);

unsigned char seed[BIP39_SEED_LEN_512];  
size_t seed_len;  
lw_response = bip39_mnemonic_to_seed(mnem,NULL,seed,BIP39_SEED_LEN_512,&seed_len);

### Generate a Root Key

With a seed in hand, you can then generate a master extended key with the bip32_key_from_seed_alloc function (or alternatively the bip32_key_from_seed, which doesn't do the alloc):

struct ext_key *key_root;  
lw_response = bip32_key_from_seed_alloc(seed,sizeof(seed),BIP32_VER_TEST_PRIVATE,0,&key_root);

As you can see, you'll need to tell it what version of the key to return, in this case BIP32_VER_TEST_PRIVATE, a private testnet key.

> :link: **TESTNET vs MAINNET:** On mainnet, you'd instead ask for BIP32_VER_MAIN_PRIVATE.

### Generate xpub & xprv

Whenever you have a key in hand, you can turn it into xpub or xprv keys for distribution with the bip32_key_to_base58 command. You just tell it whether you want a PRIVATE (xprv) or PUBLIC (xpub) key:

char *xprv;  
lw_response = bip32_key_to_base58(key_root, BIP32_FLAG_KEY_PRIVATE, &xprv);

char *xpub;  
lw_response = bip32_key_to_base58(key_root, BIP32_FLAG_KEY_PUBLIC, &xpub);

## Understand the Hierarchy

Before going further, you need to understand how the hierarchy of an HD wallet works. As discussed in [§3.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md), a derivation path describes the tree that you follow to get to a hierarchical key, so [0/1/0] is the 0th child of the 1st child of the 0th child of a root key. Sometimes part of that derivation are marked with 's or hs to show hardened derivations, which increase security: [0'/1'/0'].

However, for HD wallets, each of those levels of the hierachy is used in a very specific way. This was originally defined in [BIP44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki) and was later updated for Segwit in [BIP84].

Altogether, a BIP32 derivation path is defined to have five levels:

1. **Purpose.** This is usually set to 44' or 84', depending on the BIP that is being followed.
    
2. **Coin.** For Mainnet bitcoins, this is 0', for testnet it's 1'.
    
3. **Account.** A wallet can contain multiple, discrete accounts, starting with 0'.
    
4. **Change.** External addresses (for distribution) are set to 0, while internal addresses (for change) are set to 1.
    
5. **Index.** The nth address for the hierarchy, starting with 0.
    

So on testnet, the zeroth adddress for an external address for the zeroth account for testnet coins using the BIP84 standards is [m/84'/1'/0'/0/0]. That's the address you'll be creating momentarily.

> :link: **TESTNET vs MAINNET:** For mainnet, that'd be [m/84'/0'/0'/0/0]

### Understand the Hierarchary in Bitcoin Core

We'll be using the above hierarchy for all HD keys in Libwally, but note that this standard isn't used by Bitcoin Core's bitcoin-cli, which instead uses [m/0'/0'/0'] for the 0th external address and [m/0'/1'/0'] for the 0th change address.

## Generate an Address

To generate an address, you thus have to dig down through the whole hierarchy.

### Generate an Account Key

One way to do this is to use the bip32_key_from_parent_path_alloc function to drop down several levels of a hierarchy. You embed the levels in an array:

uint32_t path_account[] = {BIP32_INITIAL_HARDENED_CHILD+84, BIP32_INITIAL_HARDENED_CHILD+1, BIP32_INITIAL_HARDENED_CHILD};

Here we'll be looking at the zeroth hardened child (that's the account) or the first hardened child (that's testnet coins) of the 84th hardened child (that's the BIP84 standard): [m/84'/1'/0'].

You can then use that path to generate a new key from your old key:

struct ext_key *key_account;  
lw_response = bip32_key_from_parent_path_alloc(key_root,path_account,sizeof(path_account),BIP32_FLAG_KEY_PRIVATE,&key_account);

Every time you have a new key, you can use that to generate new xprv and xpub keys, if you desire:

lw_response = bip32_key_to_base58(key_account, BIP32_FLAG_KEY_PRIVATE, &a_xprv);  
lw_response = bip32_key_to_base58(key_account, BIP32_FLAG_KEY_PUBLIC, &a_xpub);

### Generate an Address Key

Alternatively, you can use the bip32_key_from_parent_alloc function, which just drops down one level of the hierarchy at a time. The following example drops down to the 0th child of the account key (which is the external address) and then the 0th child of that. This would be useful because then you could continue generating the 1st address, the 2nd address, and so on from that external key:

struct ext_key *key_external;  
lw_response = bip32_key_from_parent_alloc(key_account,0,BIP32_FLAG_KEY_PRIVATE,&key_external);

struct ext_key *key_address;  
lw_response = bip32_key_from_parent_alloc(key_external,0,BIP32_FLAG_KEY_PRIVATE,&key_address);

> :warning: **WARNING:** At some point in this hierarchy, you might decide to generate BIP32_FLAG_KEY_PUBLIC instead of BIP32_FLAG_KEY_PRIVATE. Obviously this decision will be based on your security and your needs, but remember that you only need a public key to generate the actual address.

### Generate an Address

Finally, you're ready to generate an address from your final key. All you do is run wally_bip32_to_addr_segwit using your final key and a description of what sort of address this is.

char *segwit;  
lw_response = wally_bip32_key_to_addr_segwit(key_address,"tb",0,&segwit);

printf("[m/84'/1'/0'/0/0]: %s\n",segwit);

> :link: **TESTNET vs MAINNET:** The tb argument defines a testnet address. For mainnet instead use bc.

There is also a wally_bip32_key_to_address function, which can be used to generate a legacy address or a nested Segwit address.

## Test HD Code

The code for these HD example can, as usual, be found in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_3_genhd.c).

You can compile and test it:

$ cc genhd.c -lwallycore -lsodium -o genhd  
$ ./genhd  
Mnemonic: behind mirror pond finish borrow wood park foam guess mail regular reflect  
Root xprv key: tprv8ZgxMBicQKsPdLFXmZ6VegTxcmeieNpRUq8J2ahXxSaK2aF7CGqAc14ZADLjdHJdCr8oR2Zng9YH1x1A7EBaajQLVGNtxc4YpFejdE3wyj8  
Root xpub key: tpubD6NzVbkrYhZ4WoHKfCm64685BoAeoi1L48j5K6jqNiNhs4VspfeknVgRLLiQJ3RkXiA9VxguUjmEwobtmrXNbhXsPHfm9W5HJR9DKRGaGJ2  
Account xprv key: tprv8yZN7h6SPvJXrhAk56z6cwHQE6qZBRreB9fqqZJ1Xd1nLci3Rw8HTmqNkpFNgf3eZx8hYzhFWafUhHSt3HgF13aHvCE6kveS7gZAyfQwMDi  
Account xpub key: tpubDWFQG78gYHzCkACXxkeh2LwWo8MVLm3YkTGd85LJwtpBB6xp4KwseGTEvxjeZNhnCNPdfZqRcgcZZAka4tD3xGS2J53WKHPMRhG357VKsqT  
[m/84'/1'/0'/0/0]: tb1q0knqq26ek59pfl7nukzqr28m2zl5wn2f0ldvwu

## Summary: Using BIP32 in Libwally

An HD wallet allows you to generate a vast number of keys from a single seed. You now know how those keys are organized under BIP44, BIP84, and Bitcoin Core and how to derive them, starting with either a seed or mnemonic words.

> :fire: _**What is the power of BIP32?**_ Keys are the most difficult (and most dangerous) element of most cryptographic operations. If you lose them, you lose whatever the key protected. BIP32 ensures that you just need to know one key, the seed, rather than a huge number of different keys for different addresses. :fire: _**What is the power of BIP32 in Libwally?**_ Bitcoind already does HD-based address creation for you, which means you don't usually have to worry about deriving addresses in this way. However, using the BIP32 functions of Libwally can be very useful if you have an offline machine where you need to derive addresses, possibly based on a seed passed out of bitcoind to your offline device (or vice-versa).

## What's Next?

Learn more about "Programming Bitcoin with Libwally" in [17.4: Using PSBTs in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_4_Using_PSBTs_in_Libwally.md).

# 17.4: Using PSBTs in Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

You learned all about Partially Signed Bitcoin Transactions (PSBTs) in [§7.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md) and [§7.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_2_Using_a_Partially_Signed_Bitcoin_Transaction.md), and as you saw in [§7.3: Integrating with Hardware Wallets](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/blob/master/07_3_Integrating_with_Hardware_Wallets.md), one of their prime advantages is being able to integrate with offline nodes, such as Hardware Wallets. HWI allowed you to pass commands to a Hardware Wallet, but what does the wallet itself use to manage the PSBTs? As it happens, it can use something like Libwally, as this section demonstrates.

Basically, Libwally has all of the PSBT functionality, so if there's something you could do with bitcoind, you could also do it using Libwally, even if your device is offline. What follows is the barest introduction to what's a very complex topic.

## Convert a PSBT

Converting a PSBT into Libwally's internal structure is incredibly easy, you just run wally_psbt_from_base64 with a base64 PSBT — which are the outputs produced by bitcoin-cli, such as:

cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giBgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxRiaHVILVAAAgAEAAIAAAACAAAAAADkCAAAAAQEfQEIPAAAAAAAWABQtTxOfqohTBNFWFqFm0tUVdK9KXSIGAqATz5xLX1aJ2SUwNqPkd8+YaJYm94FMlPCScm8Rt0GrGJodUgtUAACAAQAAgAAAAIAAAAAAAAAAAAAAIgID2UK1nupSfXC81nmB65XZ+pYlJp/W6wNk5FLt5ZCSx6kYmh1SC1QAAIABAACAAAAAgAEAAAABAAAAAA==

However, it's a bit harder to deal with the result, because Libwally converts it into a very complex wally_psbt structure.

Here's how it's defined in /usr/include/wally_psbt.h:

struct wally_psbt {  
unsigned char magic[5];  
struct wally_tx *tx;  
struct wally_psbt_input *inputs;  
size_t num_inputs;  
size_t inputs_allocation_len;  
struct wally_psbt_output *outputs;  
size_t num_outputs;  
size_t outputs_allocation_len;  
struct wally_unknowns_map *unknowns;  
uint32_t version;  
};

struct wally_psbt_input {  
struct wally_tx *non_witness_utxo;  
struct wally_tx_output *witness_utxo;  
unsigned char *redeem_script;  
size_t redeem_script_len;  
unsigned char *witness_script;  
size_t witness_script_len;  
unsigned char *final_script_sig;  
size_t final_script_sig_len;  
struct wally_tx_witness_stack *final_witness;  
struct wally_keypath_map *keypaths;  
struct wally_partial_sigs_map *partial_sigs;  
struct wally_unknowns_map *unknowns;  
uint32_t sighash_type;  
};

struct wally_psbt_output {  
unsigned char *redeem_script;  
size_t redeem_script_len;  
unsigned char *witness_script;  
size_t witness_script_len;  
struct wally_keypath_map *keypaths;  
struct wally_unknowns_map *unknowns;  
};

These in turn use some transaction structures defined in /usr/include/wally_transaction.h:

struct wally_tx {  
uint32_t version;  
uint32_t locktime;  
struct wally_tx_input *inputs;  
size_t num_inputs;  
size_t inputs_allocation_len;  
struct wally_tx_output *outputs;  
size_t num_outputs;  
size_t outputs_allocation_len;  
};

struct wally_tx_output {  
uint64_t satoshi;  
unsigned char *script;  
size_t script_len;  
uint8_t features;  
};

There's a lot there! Though much of this should be familiar from pervious chapters, it's a bit overwhelming to see it all laid out in C structures.

## Read a Converted PSBT

Obviously, you can read anything out of a PSBT structure by calling up the individual elements from the various substructures. The following is a brief overview showing how to grab a few of the elements.

Here's an example of retrieving the values and scriptPubKeys of the inputs:

int inputs = psbt->num_inputs;  
printf("TOTAL INPUTS: %i\n",inputs);

for (int i = 0 ; i < inputs ; i++) {  
printf("\nINPUT #%i: %i satoshis\n",i, psbt->inputs[i].witness_utxo->satoshi);

char *script_hex;    
wally_hex_from_bytes(psbt->inputs[i].witness_utxo->script,psbt->inputs[i].witness_utxo->script_len,&script_hex);    
printf("scriptPubKey: %s\n",script_hex);    
wally_free_string(script_hex);  

}

This programming pattern will be used on many parts of the PSBT. You look at the size of the inputs array, then you step through it, retrieving what you want to see (in this case, satoshis and scripts).

Here's a similar example for the outputs:

int outputs = psbt->num_outputs;  
printf("\nTOTAL OUTPUTS: %i\n",outputs);  
for (int i = 0 ; i < outputs ; i++) {

char *pubkey_hex;    
wally_hex_from_bytes(psbt->tx->outputs[i].script,psbt->tx->outputs[i].script_len,&pubkey_hex);    
printf("\nINPUT #%i\n",i);    
printf("scriptPubKey: %s\n",pubkey_hex);    
wally_free_string(pubkey_hex);      

}

Obviously, there's a lot more you could look at in the PSBTs. In fact, looking is the main point of a PSBT: you can verify inputs and outputs from an offline computer.

> :warning: **WARNING:** These reading functions are _very_ rudimentary and will not work properly for extremly normal situations like an input or output that's still empty or that includes a non_witness_utxo. They will segfault if they aren't delivered a precisely expected PSBT. A real reader would need to be considerably more robust, to cover all possible situations, but that's left as an exercise for the reader.

### Test Your PSBT Reader

Again, the code for this (extremely rudimentary and specific) PSBT reader is in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_4_examinepsbt.c).

You can compile it as normal:

$ cc examinepsbt.c -lwallycore -o examinepsbt

The following PSBT from [§7.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_3_Integrating_with_Hardware_Wallets.md) can be used for testing, as it matches the very narrow criteria required by this limited implementation:

psbt=cHNidP8BAJoCAAAAAri6BLjKQZGO9Y1iVIYbxlxBJ2kqsTPWnxGaH4HrSjxbAAAAAAD+////leV0hwJ0fO40RmhuFVIYtO16ktic2J4vJFLAsT5TM8cBAAAAAP7///8CYOMWAAAAAAAWABTHctb5VULhHvEejvx8emmDCtOKBU+gBwAAAAAAFgAU9Ojd5ds3CJi1fIRWbj92CYhQgX0AAAAAAAEBH0BCDwAAAAAAFgAUABk8i/Je8Fb41FcaHD9lEj5f54giBgMBaNlILisC1wJ/tKie3FStqhrfcJM09kfQobBTOCiuxRiaHVILVAAAgAEAAIAAAACAAAAAADkCAAAAAQEfQEIPAAAAAAAWABQtTxOfqohTBNFWFqFm0tUVdK9KXSIGAqATz5xLX1aJ2SUwNqPkd8+YaJYm94FMlPCScm8Rt0GrGJodUgtUAACAAQAAgAAAAIAAAAAAAAAAAAAAIgID2UK1nupSfXC81nmB65XZ+pYlJp/W6wNk5FLt5ZCSx6kYmh1SC1QAAIABAACAAAAAgAEAAAABAAAAAA==

Run examinepsbt with that PSBT, and you should see the scripts on the inputs and the outputs:

$ ./examinepsbt $psbt  
TOTAL INPUTS: 2

INPUT #0: 1000000 satoshis  
scriptPubKey: 001400193c8bf25ef056f8d4571a1c3f65123e5fe788

INPUT #1: 1000000 satoshis  
scriptPubKey: 00142d4f139faa885304d15616a166d2d51574af4a5d

TOTAL OUTPUTS: 2

INPUT #0  
scriptPubKey: 0014c772d6f95542e11ef11e8efc7c7a69830ad38a05

INPUT #1  
scriptPubKey: 0014f4e8dde5db370898b57c84566e3f76098850817d

And of course, you can check this with the decodepsbt RPC command for bitcoin-cli:

$ bitcoin-cli decodepsbt $psbt  
{  
"tx": {  
"txid": "45f996d4ff8c9e9ab162f611c5b6ad752479ede9780f9903bdc80cd96619676d",  
"hash": "45f996d4ff8c9e9ab162f611c5b6ad752479ede9780f9903bdc80cd96619676d",  
"version": 2,  
"size": 154,  
"vsize": 154,  
"weight": 616,  
"locktime": 0,  
"vin": [  
{  
"txid": "5b3c4aeb811f9a119fd633b12a6927415cc61b8654628df58e9141cab804bab8",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
},  
{  
"txid": "c733533eb1c052242f9ed89cd8927aedb41852156e684634ee7c74028774e595",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967294  
}  
],  
"vout": [  
{  
"value": 0.01500000,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"hex": "0014c772d6f95542e11ef11e8efc7c7a69830ad38a05",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qcaedd724gts3aug73m78c7nfsv9d8zs9q6h2kd"  
]  
}  
},  
{  
"value": 0.00499791,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 f4e8dde5db370898b57c84566e3f76098850817d",  
"hex": "0014f4e8dde5db370898b57c84566e3f76098850817d",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q7n5dmewmxuyf3dtus3txu0mkpxy9pqtacuprak"  
]  
}  
}  
]  
},  
"unknown": {  
},  
"inputs": [  
{  
"witness_utxo": {  
"amount": 0.01000000,  
"scriptPubKey": {  
"asm": "0 00193c8bf25ef056f8d4571a1c3f65123e5fe788",  
"hex": "001400193c8bf25ef056f8d4571a1c3f65123e5fe788",  
"type": "witness_v0_keyhash",  
"address": "tb1qqqvnezljtmc9d7x52udpc0m9zgl9leugd2ur7y"  
}  
},  
"bip32_derivs": [  
{  
"pubkey": "030168d9482e2b02d7027fb4a89edc54adaa1adf709334f647d0a1b0533828aec5",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/0/569"  
}  
]  
},  
{  
"witness_utxo": {  
"amount": 0.01000000,  
"scriptPubKey": {  
"asm": "0 2d4f139faa885304d15616a166d2d51574af4a5d",  
"hex": "00142d4f139faa885304d15616a166d2d51574af4a5d",  
"type": "witness_v0_keyhash",  
"address": "tb1q948388a23pfsf52kz6skd5k4z4627jja2evztr"  
}  
},  
"bip32_derivs": [  
{  
"pubkey": "02a013cf9c4b5f5689d9253036a3e477cf98689626f7814c94f092726f11b741ab",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/0/0"  
}  
]  
}  
],  
"outputs": [  
{  
},  
{  
"bip32_derivs": [  
{  
"pubkey": "03d942b59eea527d70bcd67981eb95d9fa9625269fd6eb0364e452ede59092c7a9",  
"master_fingerprint": "9a1d520b",  
"path": "m/84'/1'/0'/1/1"  
}  
]  
}  
],  
"fee": 0.00000209  
}

You can see the input satoshis and scriptPubKey clearly listed in the inputs and the new scriptPubKeys in the tx's vout.

So, it's all there for your gathering!

## Create a PSBT

As noted at the head of this section, all of the functions needed to create and process PSBTs are available in Libwally. Actually running through the process of doing so is complex enough that it's beyond the scope of this section, but here's a quick run-down of the functions required. Note that the [documents](https://wally.readthedocs.io/en/latest/psbt/) are out of date for PSBTs, so you'll need to consult /usr/include/wally_psbt.h for full information.

As discussed in [§7.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_1_Creating_a_Partially_Signed_Bitcoin_Transaction.md) there are several roles involved in creating PSBTs

### Take the Creator Role

The creator role is tasked with creating a PSBT with at least one input.

A PSBT is created with a simple use of wally_psbt_init_alloc, telling it how many inputs and outputs you will eventually add:

struct wally_psbt *psbt;  
lw_response = wally_psbt_init_alloc(0,1,1,0,0,&psbt);

But what you have is not yet a legal PSBT, because of the lack of inputs. You can create those by creating a transaction and setting it as the global transaction in the PSBT, which updates all the inputs and outputs:

struct wally_tx *gtx;  
lw_response = wally_tx_init_alloc(0,0,1,1,&gtx);  
lw_response = wally_psbt_set_global_tx(psbt,gtx);

### Test Your PSBT Creation

At this point, you should have an empty, but working PSBT, which you can see by compiling and running [the program](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_4_createemptypsbt.c).

$ cc createemptypsbt.c -lwallycore -o createemptypsbt  
$ ./createemptypsbt  
cHNidP8BAAoAAAAAAAAAAAAAAA==

You can even use bitcoin-cli to test the result:

$ psbt=$(./createpsbt)  
$ bitcoin-cli decodepsbt $psbt  
{  
"tx": {  
"txid": "f702453dd03b0f055e5437d76128141803984fb10acb85fc3b2184fae2f3fa78",  
"hash": "f702453dd03b0f055e5437d76128141803984fb10acb85fc3b2184fae2f3fa78",  
"version": 0,  
"size": 10,  
"vsize": 10,  
"weight": 40,  
"locktime": 0,  
"vin": [  
],  
"vout": [  
]  
},  
"unknown": {  
},  
"inputs": [  
],  
"outputs": [  
],  
"fee": 0.00000000  
}

## Take the Rest of the Roles

As with PSBT reading, we are introducing the concept of PSBT creation, and then leaving the rest as an exercise for the reader.

Following is a rough listing of functions for every roles; more functions will be needed to create some of the elements that are added to PSBTs.

**Creator:**

- wally_psbt_init_alloc
    
- wally_psbt_set_global_tx
    

**Updater:**

- wally_psbt_input_set_non_witness_utxo
    
- wally_psbt_input_set_witness_utxo
    
- wally_psbt_input_set_redeem_script
    
- wally_psbt_input_set_witness_script
    
- wally_psbt_input_set_keypaths
    
- wally_psbt_input_set_unknowns
    
- wally_psbt_output_set_redeem_script
    
- wally_psbt_output_set_witness_script
    
- wally_psbt_output_set_keypaths
    
- wally_psbt_output_set_unknowns
    

**Signer:**

- wally_psbt_input_set_partial_sigs
    
- wally_psbt_input_set_sighash_type
    
- wally_psbt_sign
    

**Combiner:**

- wally_psbt_combine
    

**Finalizer:**

- wally_psbt_finalize
    
- wally_psbt_input_set_final_script_sig
    
- wally_psbt_input_set_final_witness
    

**Extracter:**

- wally_psbt_extract
    

## Summary: Using PSBTs in Libwally

This section could be an entire chapter, as working with PSBTs at a low level is very intensive work that requires much more intensive manipulating of inputs and outputs than was the case in [Chapter 7](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_0_Expanding_Bitcoin_Transactions_PSBTs.md). Instead this section shows the basics: how to extract information from a PSBT, and how to begin creating one.

> :fire: _**What is the Power of PSBTs in Libwally?**_ Obviously, you can already do all of this in bitcoin-cli, and it's simpler because Bitcoin Core manages a lot of the drudgery. The advantage of using Libwally is that it can be run offline, so it could be Libwally that's sitting on the other side of a hardware device that your bitcoin-cli is communicating to with HWI. This is, in fact, one of the major points of PSBTs: to be able to manipulate partially signed transactions without needing a full node. Libwally enables it.

## What's Next?

Learn more about "Programming Bitcoin with Libwally" in [17.5: Using Scripts in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_5_Using_Scripts_in_Libwally.md).

# 17.5: Using Scripts in Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Way back in Part 3, while introducing Scripts, we said that you were likely to actually create transactions using scripts with an API, and marked it as a topic for the future. Well, the future has now arrived.

## Create the Script

Creating the script is the _easiest_ thing to do in Libwally. Take the following example, a simple [Puzzle Script](file:///../13_1_Writing_Puzzle_Scripts.md) that we've returned to from time to time:

OP_ADD 99 OP_EQUAL

Using btcc, we can serialize that.

$ btcc OP_ADD 99 OP_EQUAL  
warning: ambiguous input 99 is interpreted as a numeric value; use 0x99 to force into hexadecimal interpretation  
93016387

Previously we built the standard P2SH script by hand, but Libwally can actually do that for you.

First, Libwally has to convert the hex into bytes, since bytes are most of what it works with:

int script_length = strlen(script)/2;  
unsigned char bscript[script_length];

lw_response = wally_hex_to_bytes(script,bscript,script_length,&written);

Then, you run wally_scriptpubkey_p2sh_from_bytes with your bytes, telling Libwally to also HASH160 it for you:

unsigned char p2sh[WALLY_SCRIPTPUBKEY_P2SH_LEN];

lw_response = wally_scriptpubkey_p2sh_from_bytes(bscript,sizeof(bscript),WALLY_SCRIPT_HASH160,p2sh,WALLY_SCRIPTPUBKEY_P2SH_LEN,&written);

If you looked at the results of p2sh, you'd see it was:

a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed87

Which [you may recall](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md) breaks apart to:

a9 / 14 / 3f58b4f7b14847a9083694b9b3b52a4cea2569ed / 87

That's our old friend OP_HASH160 3f58b4f7b14847a9083694b9b3b52a4cea2569ed OP_EQUAL.

Basically, Libwally took your serialized redeem script, hashed it for you with SHA-256 and RIPEMD-160, and then applied the standard framing to turn it into a proper P2SH; You did similar work in [§10.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/10_2_Building_the_Structure_of_P2SH.md), but with an excess of shell commands.

In fact, you can double-check your work using the same commands from §10.2:

$ redeemScript="93016387"  
$ echo -n $redeemScript | xxd -r -p | openssl dgst -sha256 -binary | openssl dgst -rmd160  
(stdin)= 3f58b4f7b14847a9083694b9b3b52a4cea2569ed

## Create a Transaction

In order to make use of that pubScriptKey that you just created, you need to create a transaction and embed the pubScriptKey within (and this is the big change from bitcoin-cli: you can actually hand create a transaction with a P2SH script).

The process of creating a transaction in Libwally is very intensive, just like the process for creating a PSBT, and so we're just going to outline it, taking one major shortcut, and then leave a method without shortcuts for future investigation.

Creating a transaction itself is easy enough: you just need to tell wally_tx_init_alloc your version number, your locktime, and your number of inputs and outputs:

struct wally_tx *tx;  
lw_response = wally_tx_init_alloc(2,0,1,1,&tx);

Filling in those inputs and outputs is where things get tricky!

### Create a Transaction Output

To create an output, you tell wally_tx_output_init_alloc how many satoshis you're spending and you hand it the locking script:

struct wally_tx_output *tx_output;  
lw_response = wally_tx_output_init_alloc(95000,p2sh,sizeof(p2sh),&tx_output);

That part actually wasn't hard at all, and it allowed you to at long-last embed a P2SH in a vout.

One more command adds it to your transaction:

lw_response = wally_tx_add_output(tx,tx_output);

### Create a Transaction Input

Creating the input is much harder because you have to pile information into the creation routines, not all of which is intuitively accessible when you're using Libwally. So, rather than going that deep into the weeds, here's where we take our shortcut. We write our code so that it's passed the hex code for a transaction that's already been created, and then we just reuse the input.

The conversion from the hex code is done with wally_tx_from_hex:

struct wally_tx *utxo;  
lw_response = wally_tx_from_hex(utxo_hex,0,&utxo);

Then you can plunder the inputs from your hexcode to create an input with Libwally:

struct wally_tx_input *tx_input;  
lw_response = wally_tx_input_init_alloc(utxo->inputs[0].txhash,sizeof(utxo->inputs[0].txhash),utxo->inputs[0].index,0,utxo->inputs[0].script,utxo->inputs[0].script_len,utxo->inputs[0].witness,&tx_input);  
assert(lw_response == WALLY_OK);

As you might expect, you then add that input to your transaction:

lw_response = wally_tx_add_input(tx,tx_input);

> **NOTE** Obviously, you'll want to be able to create your own inputs if you're using Libwally for real applications, but this is intended as a first step. And, it can actually be useful for integrating with bitcoin-cli, as we'll see in [§16.7](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_7_Integrating_Libwally_and_Bitcoin-CLI.md).

### Print a Transaction

You theoretically could sign and send this transaction from your C program built on Libwally, but in keeping with the idea that we're just using a simple C program to substitute in a P2SH, we're going to print out the new hex. This is done with the help of wally_tx_to_hex:

char *tx_hex;  
lw_response = wally_tx_to_hex(tx,0, &tx_hex);

printf("%s\n",tx_hex);

We'll show how to make use of that in §16.7.

## Test Your Replacement Script

You can grab the test code from the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_5_replacewithscript.c) and compile it:

$ cc replacewithscript.c -lwallycore -o replacewithscript

Afterward, prepare a hex transaction and a serialized hex script:

hex=020000000001019527cebb072524a7961b1ba1e58fc18dd7c6fc58cd6c1c45d7e1d8fc690b006e0000000017160014cc6e8522f0287b87b7d0a83629049c2f2b0e972dfeffffff026f8460000000000017a914ba421212a629a840492acb2324b497ab95da7d1e87306f0100000000001976a914a2a68c5f9b8e25fdd1213c38d952ab2be2e271be88ac02463043021f757054fa61cfb75b64b17230b041b6d73f25ff9c018457cf95c9490d173fb4022075970f786f24502290e8a5ed0f0a85a9a6776d3730287935fb23aa817791c01701210293fef93f52e6ce8be581db62229baf116714fcb24419042ffccc762acc958294e6921b00

script=93016387

You can then run the replacement program:

$ ./replacewithscript $hex $script  
02000000019527cebb072524a7961b1ba1e58fc18dd7c6fc58cd6c1c45d7e1d8fc690b006e0000000017160014cc6e8522f0287b87b7d0a83629049c2f2b0e972d0000000001187301000000000017a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed8700000000

You can then see the results with bitcoin-cli:

$ bitcoin-cli decoderawtransaction $newhex  
{  
"txid": "f4e7dbab45e759a7ac6e2fb0f10720cd29d047efad89fe1b569f5f4ba61fd8e6",  
"hash": "f4e7dbab45e759a7ac6e2fb0f10720cd29d047efad89fe1b569f5f4ba61fd8e6",  
"version": 2,  
"size": 106,  
"vsize": 106,  
"weight": 424,  
"locktime": 0,  
"vin": [  
{  
"txid": "6e000b69fcd8e1d7451c6ccd58fcc6d78dc18fe5a11b1b96a7242507bbce2795",  
"vout": 0,  
"scriptSig": {  
"asm": "0014cc6e8522f0287b87b7d0a83629049c2f2b0e972d",  
"hex": "160014cc6e8522f0287b87b7d0a83629049c2f2b0e972d"  
},  
"sequence": 0  
}  
],  
"vout": [  
{  
"value": 0.00095000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 3f58b4f7b14847a9083694b9b3b52a4cea2569ed OP_EQUAL",  
"hex": "a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2My2ApqGcoNXYceZC4d7fipBu4GodkbefHD"  
]  
}  
}  
]  
}

The vin should just match the input you substituted in, but it's the vout that's exciting: you've created a transaction with a scripthash!

## Summary: Using Scripts in Libwally

Creating transactions in Libwally is another topic that could take up a whole chapter, but the great thing is that once you make this leap, you can introduce a P2SH scriptPubKey, and that part alone is pretty easy. Though the methodology detailed in this chapter requires you to have a transaction hex already in hand (probably created with bitcoin-cli) if you dig further into Libwally, you can do it all yourself.

> :fire: _**What is the Power of Scripts in Libwally?**_ Quite simply, you can do something you couldn't before: create a transaction locked with an arbitrary P2SH.

## What's Next?

Learn more about "Programming Bitcoin with Libwally" in [§17.6: Using Other Functions in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_6_Using_Other_Functions_in_Libwally.md).

# 17.6: Using Other Functions in Libwally

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Libwally is an extensive library that provides a considerable amount of wallet-related functionality, much of it not available through bitcoin-cli. Following is an overview of some functionality not previously covered in this chapter.

## Use Cryptographic Functions

A number of cryptographic functions can be directly accessed from Libwally:

- wally_aes — Use AES encryption or decryption
    
- wally_aes_cbc — Use AES encryption or decryption in CBC mode
    
- wally_hash160 — Use RIPEMD-160(SHA-256) hash
    
- wally_scrypt — Use Scrypt key derivation
    
- wally_sha256 — Use SHA256 hash
    
- wally_sha256_midstate — Use SHA256 to hash only the first chunk of data
    
- wally_sha256d — Conduct a SHA256 double-hash
    
- wally_sha512 — Use SHA512 hash
    

There are also HMAC functions for the two SHA hashes, which are used generate message-authentication-codes based on the hashes. They're used in [BIP32](https://en.bitcoin.it/wiki/BIP_0032), among other places.

- wally_hmac_sha256
    
- wally_hmac_sha512
    

Additional functions cover PBKDF2 key derivation and elliptic-curve math.

## Use Address Functions

Libwally contains a number of functions that can be used to import, export, and translate Bitcoin addresses.

Some convert back and forth between addresses and scriptPubKey bytes:

- wally_addr_segwit_from_bytes — Convert a witness program (in bytes) into a Segwit address
    
- wally_addr_segwit_to_bytes — Convert a Segwit address into a scriptPubKey (in bytes)
    
- wally_address_to_scriptpubkey — Convert a legacy address into a scriptPubKey(in bytes)
    
- wally_scriptpubkey_to_address — Convert a scriptPubKey (in bytes) into a legacy address
    

Some relate to the wallet import format (WIF):

- wally_wif_from_bytes — Convert a private key (in bytes) to a WIF
    
- wally_wif_is_uncompressed — Determines if a WIF is uncompressed
    
- wally_wif_to_address — Derive a P2PKH address from a WIF
    
- wally_wif_to_bytes — Convert a WIF to a private key (in bytes)
    
- wally_wif_to_public_key — Derive a public key (in bytes) from a WIF
    

## Use BIP32 Functions

There are additional BIP32 HD-wallet functions, beyond what was covered in [§17.3: Using BIP32 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_3_Using_BIP32_in_Libwally.md).

- bip32_key_get_fingerprint — Generate a BIP32 fingerprint for an extended key
    
- bip32_key_serialize — Transform an extended key into serialized bytes
    
- bip32_key_strip_private_key — Convert an extended private key to an extended public key
    
- bip32_key_unserialize — Transform serialized bytes into an extended key
    

There are also numerous various depending on whether you want to allocate memory or have Libwally do the _alloc for you.

## Use BIP38 Functions

[BIP38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki) allows for the creation of password-protected private key. We do not teach it because we consider inserting this sort of human factor into key management dangerous. See [#SmartCustody](https://www.smartcustody.com/index.html).

The main functions are:

- bip38_from_private_key — Encode a private key using BIP38
    
- bip38_to_private_key — Decode a private key using BIP38
    

## Use BIP39 Functions

A few BIP39 mnemonic-word functions were just overviewed in [§17.2: Using BIP39 in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_2_Using_BIP39_in_Libwally.md):

- bip39_get_languages — See a list of supported languages
    
- bit39_get_word — Retrieve a specific word from a language's word list
    
- bip39_get_wordlist — See a list of words for a language
    

## Use PSBT Functions

Listings of most PSBT functions can be found in [17.4: Using PSBTs in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_4_Using_PSBTs_in_Libwally.md).

## Use Script Functions

[§17.5: Using Scripts in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_5_Using_Scripts_in_Libwally.md) just barely touched upon Libwally's Scripts functions.

There's another function that lets you determine the sort of script found in a transaction:

- wally_scriptpubkey_get_type — Determine a transaction's script type.
    

Then there are a slew of functions that create scriptPubKey from bytes, scriptSig from signatures, and Witnesses from bytes or signatures.

- wally_script_push_from_bytes
    
- wally_scriptpubkey_csv_2of2_then_1_from_bytes
    
- wally_scriptpubkey_csv_2of3_then_2_from_bytes
    
- wally_scriptpubkey_multisig_from_bytes
    
- wally_scriptpubkey_op_return_from_bytes
    
- wally_scriptpubkey_p2pkh_from_bytes
    
- wally_scriptpubkey_p2sh_from_bytes
    
- wally_scriptsig_multisig_from_bytes
    
- wally_scriptsig_p2pkh_from_der
    
- wally_scriptsig_p2pkh_from_sig
    
- wally_witness_multisig_from_bytes
    
- wally_witness_p2wpkh_from_der
    
- wally_witness_p2wpkh_from_sig
    
- wally_witness_program_from_bytes
    

## Use Transaction Functions

We also just barely touched upon the functions that can be used to create and convert functions in [§17.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_5_Using_Scripts_in_Libwally.md).

There are numerous informational functions, some of the more interesting of which are:

- wally_tx_get_length
    
- wally_tx_get_total_output_satoshi
    
- wally_tx_get_weight
    

There also are functions that affect a wally_tx, a wally_tx_input, a wally_tx_output, or a wally_tx_witness_stack and that create signatures.

## Use Elements Functions

Libwally can be compiled to be used with Blockstream's Elements, which includes access to its assets functions.

## Summary: Using Other Functions in Libwally

There is much more that you can do with Libwally, more than can be covered in this chapter or even listed in this section. Notably, you can perform cryptographic functions, encode private keys, build complete transactions, and use Elements. The [Libwally docs](https://wally.readthedocs.io/en/latest/) are the place to go for more information, though as of this writing they are both limited and out-of-date. The Libwally header files are a backup if the docs are incomplete or wrong.

## What's Next?

Finish learning about "Programming Bitcoin with Libwally" in [§17.7: Integrating Libwally and Bitcoin-CLI](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_7_Integrating_Libwally_and_Bitcoin-CLI.md).

# 17.7: Integrating Libwally and Bitcoin-CLI

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Libwally is limited. It's about manipulating seeds, keys, addresses, and other elements of wallets, with some additional functions related to transactions and PSBTs that might be useful for services that are not connected to full nodes on the internet. Ultimately, however, you're going to need full node services to take advantage of Libwally.

This final section will offer some examples of using Libwally programs to complement a bitcoin-cli environment. Though these examples imply that these services are all on the same machine, they may become even more powerful if the bitcoin-cli service is directly connected to the internet and the Libwally service is not.

## Share a Transaction

[§17.5: Using Scripts in Libwally](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_5_Using_Scripts_in_Libwally.md) detailed how Libwally could be used to rewrite an existing transaction, to do something that bitcoin-cli can't: produce a transaction that contains a unique P2SH. Obviously, this is a building block; if you decide to dig further into Libwally you'll create entire transactions on your own. But, this abbreviated methodology also has its own usage: it shows how transactions can be passed back and forth between bitcoin-cli and Libwally, demonstrating a first example of using them in a complementary fashion.

To fully demonstrate this methodology, you'll create a transaction with bitcoin-cli, using this UTXO:

{  
"txid": "c0a110a7a84399b98052c6545018873b13ee3128fa74f7a697779174a36ea33a",  
"vout": 1,  
"address": "mvLyH7Rs45c16FG2dfV7uuTKV6pL92kWxo",  
"label": "",  
"scriptPubKey": "76a914a2a68c5f9b8e25fdd1213c38d952ab2be2e271be88ac",  
"amount": 0.00094000,  
"confirmations": 17375,  
"spendable": true,  
"solvable": true,  
"desc": "pkh([ce0c7e14/0'/0'/5']0368d0fffa651783524f8b934d24d03b32bf8ff2c0808943a556b3d74b2e5c7d65)#qldtsl65",  
"safe": true  
}

By now, you know how to set up a transaction with bitcoin-cli:

$ utxo_txid=$(bitcoin-cli listunspent | jq -r '.[0] | .txid')  
$ utxo_vout=$(bitcoin-cli listunspent | jq -r '.[0] | .vout')  
$ recipient=tb1qycsmq3jas5wkhf8xrfn8k7438cm5pc8h9ae2k0  
$ rawtxhex=$(bitcoin-cli -named createrawtransaction inputs='''[ { "txid": "'$utxo_txid'", "vout": '$utxo_vout' } ]''' outputs='''{ "'$recipient'": 0.0009 }''')

Though you placed a recipient and an amount in the output, it's irrelevent, because you'll be rewriting those. A fancier bit of code could read the existing vout info before rewriting, but we're keeping things very close to our [original code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_5_replacewithscript.c).

Here's the one change necessary, to allow you to specify the satoshi vout, without having to hardcode it, as in the original:

...  
int satoshis = atoi(argv[3]);  
...  
lw_response = wally_tx_output_init_alloc(satoshis,p2sh,sizeof(p2sh),&tx_output);  
...

Then you just run things like before:

$ newtxhex=$(./replacewithscript $rawtxhex $script 9000)

Here's what the original transaction looked like:

$ bitcoin-cli decoderawtransaction $rawtxhex  
{  
"txid": "438d50edd7abeaf656c5abe856a00a20af5ff08939df8fdb9f8bfbfb96234fcb",  
"hash": "438d50edd7abeaf656c5abe856a00a20af5ff08939df8fdb9f8bfbfb96234fcb",  
"version": 2,  
"size": 82,  
"vsize": 82,  
"weight": 328,  
"locktime": 0,  
"vin": [  
{  
"txid": "c0a110a7a84399b98052c6545018873b13ee3128fa74f7a697779174a36ea33a",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 2621b0465d851d6ba4e61a667b7ab13e3740e0f7",  
"hex": "00142621b0465d851d6ba4e61a667b7ab13e3740e0f7",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1qycsmq3jas5wkhf8xrfn8k7438cm5pc8h9ae2k0"  
]  
}  
}  
]  
}

And here's the transaction rewritten by Libwally to use a P2SH:

standup@btctest:~/c$ bitcoin-cli decoderawtransaction $newtxhex  
{  
"txid": "badb57622ab5fe029fc1a71ace9f7b76c695f933bceb0d38a155c2e5c984f4e9",  
"hash": "badb57622ab5fe029fc1a71ace9f7b76c695f933bceb0d38a155c2e5c984f4e9",  
"version": 2,  
"size": 83,  
"vsize": 83,  
"weight": 332,  
"locktime": 0,  
"vin": [  
{  
"txid": "c0a110a7a84399b98052c6545018873b13ee3128fa74f7a697779174a36ea33a",  
"vout": 1,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"sequence": 0  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 3f58b4f7b14847a9083694b9b3b52a4cea2569ed OP_EQUAL",  
"hex": "a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2My2ApqGcoNXYceZC4d7fipBu4GodkbefHD"  
]  
}  
}  
]  
}

Afterward you can sign it as usual with bitcoin-cli:

$ signedtx=$(bitcoin-cli signrawtransactionwithwallet $newtxhex | jq -r '.hex')

And as you can see, the result is a legitimate transaction ready to go out to the Bitcoin network:

$ bitcoin-cli decoderawtransaction $signedtx  
{  
"txid": "3061ca8c01d029c0086adbf8b7d4280280c8aee151500bab7c4f783bbc8e75e6",  
"hash": "3061ca8c01d029c0086adbf8b7d4280280c8aee151500bab7c4f783bbc8e75e6",  
"version": 2,  
"size": 189,  
"vsize": 189,  
"weight": 756,  
"locktime": 0,  
"vin": [  
{  
"txid": "c0a110a7a84399b98052c6545018873b13ee3128fa74f7a697779174a36ea33a",  
"vout": 1,  
"scriptSig": {  
"asm": "3044022026c81b6ff4a15135d10c7f4b1ae6e44ac4fdb25c4a3c03161b17b8ab8d04850502200b448d070f418de1ca07e76943d23d447bc95c7c5e0322bcc153cadb5d9befe0[ALL] 0368d0fffa651783524f8b934d24d03b32bf8ff2c0808943a556b3d74b2e5c7d65",  
"hex": "473044022026c81b6ff4a15135d10c7f4b1ae6e44ac4fdb25c4a3c03161b17b8ab8d04850502200b448d070f418de1ca07e76943d23d447bc95c7c5e0322bcc153cadb5d9befe001210368d0fffa651783524f8b934d24d03b32bf8ff2c0808943a556b3d74b2e5c7d65"  
},  
"sequence": 0  
}  
],  
"vout": [  
{  
"value": 0.00090000,  
"n": 0,  
"scriptPubKey": {  
"asm": "OP_HASH160 3f58b4f7b14847a9083694b9b3b52a4cea2569ed OP_EQUAL",  
"hex": "a9143f58b4f7b14847a9083694b9b3b52a4cea2569ed87",  
"reqSigs": 1,  
"type": "scripthash",  
"addresses": [  
"2My2ApqGcoNXYceZC4d7fipBu4GodkbefHD"  
]  
}  
}  
]  
}

Voila! That's the power of Libwally with bitcoin-cli.

Obviously, you can also pass around a PSBT using the functions described in [§17.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_4_Using_PSBTs_in_Libwally.md) and that's a more up-to-date methodology for the modern-day usage of Bitcoin, but in either example, the concept of passing transactions from bitcoin-cli to Libwally code and back should be similar.

## Import & Export BIP39 Seeds

Unfortunately, not all interactions between Libwally and bitcoin-cli go as smoothly. For example, it would be nice if you could either export an HD seed from bitcoin-cli, to generate the mnemonic phrase with Libwally, or generate a seed from a mneomnic phrase using Libwally, and then import it into bitcoin-cli. Unfortunately, neither of these is possible at this time. A mneomnic phrase is translated into a seed using HMAC-SHA512, which means the result is 512 bits. However, bitcoin-cli exports HD seeds (using dumpwallet) and imports HD seeds (using sethdseed) with a length of 256 bits. Until that is changed, never the twain shall meet.

> :book: _**What's the Difference Between Entropy & a Seed?**_ Libwally says that it creates its mnemonic phrases from entropy. That's essentially the same thing as a seed: they're both large, randomized numbers. So, if bitcoin-cli was compatible with 512-bit mnemonic-phrase seeds, you could use one to generate the mneomnic phrases, and get the results that you'd expect. :book: _**What's the difference between Entropy & Raw Entropy?**_ Not all entropy is the same. When you input entropy into a command that creates a mnemonic seed, it has to a specific, well-understood length. Changing raw entropy into entropy requires massaging the raw entropy until it's the right length and format, and at that point you could reuse that (non-raw) entropy to always recreate the same mnemonics (which is why entropy is effectively the same thing as a seed at that point, but raw entropy isn't).

## Import Private Keys

Fortunately, you can do much the same thing by importing a private key generated in Libwally. Take a look at [genhd-for-import.c](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/17_7_genhd_for_import.c), a simplified version of the genhd program from [§17.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_3_Using_BIP32_in_Libwally.md) that also uses the jansson library from [§16.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_1_Accessing_Bitcoind_with_C.md) for regularized output.

The updated code also contains one change of note: it requests a fingerprint from Libwally so that it can properly create a derivation path:

char account_fingerprint[BIP32_KEY_FINGERPRINT_LEN];  
lw_response = bip32_key_get_fingerprint(key_account,account_fingerprint,BIP32_KEY_FINGERPRINT_LEN);

char *fp_hex;  
lw_response = wally_hex_from_bytes(account_fingerprint,BIP32_KEY_FINGERPRINT_LEN,&fp_hex);

> :warning: **WARNING:** Remember that the fingerprint in derivation paths is arbitrary. Because Libwally provides one, we're using it, but if you didn't have one, you could add an arbitrary 4-byte hexcode as a fingerprint to your derivation path.

Be sure to compile the new code with the jansson library, after installing it (if necessary) per [§16.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_1_Accessing_Bitcoind_with_C.md).

$ cc genhd-for-import.c -lwallycore -lsodium -ljansson -o genhd-for-import

When you run the new program, it'll give you a nicely output list of everything:

$ ./genhd-for-import  
{  
"mnemonic": "physical renew say quit enjoy eager topic remind riot concert refuse chair",  
"account-xprv": "tprv8yxn8iFNgsLktEPkWKQpMqb7bcx5ViFQEbJMtqrGi8LEgvy8es6YeJvyJKrbYEPKMw8JbU3RFhNRQ4F2pataAtTNokS1JXBZVg62xfd5HCn",  
"address": "tb1q9lhru6k0ymwrtr5w98w35n3lz22upml23h753n",  
"derivation": "[d1280779/84h/1h/0h]"  
}

You have the mnemonic that you can recover from, an account-xprv that you can import, a derivation to use for the import, and a sample address, that you can use for testing the import.

You can now fall back on lessons learned from [§3.5](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_5_Understanding_the_Descriptor.md) on how to turn that xprv into a descriptor and import it.

First, you need to figure out the checksum:

$ xprv=tprv8yxn8iFNgsLktEPkWKQpMqb7bcx5ViFQEbJMtqrGi8LEgvy8es6YeJvyJKrbYEPKMw8JbU3RFhNRQ4F2pataAtTNokS1JXBZVg62xfd5HCn  
$ dp=[d1280779/84h/1h/0h]  
$ bitcoin-cli getdescriptorinfo "wpkh($dp$xprv/0/_)"_  
_{_  
_"descriptor": "wpkh([d1280779/84'/1'/0']tpubDWepH8HcqF2RmhRYPy5QmFFEAeU1f3SJotu9BMta8Q8dXRDuHFv8poYqUUtEiWftBjtKn1aNhi9Qg2P4NdzF66dShYvB92z78WJbYeHTLTz/0/_)#f8rmqc0z",  
"checksum": "46c00dk5",  
"isrange": true,  
"issolvable": true,  
"hasprivatekeys": true  
}

There are three things to note here:

1. We use wpkh as the function in our derivation path. That's because we want to generate modern Segwit addresses, not legacy addresses. That matches our usage in Libwally of the wally_bip32_key_to_addr_segwit function. The most important thing, however, is to have the same expectations with Libwally and bitcoin-cli (and your descriptor) of what sort of address you're generating, so that everything matches!
    
2. We use the path /0/* because we wanted the external addresses for this account. If we instead wanted the change addresses, we'd use /1/*.
    
3. We are not going to use the returned descriptor line, as it's for a xpub address. Instead we'll apply the returned checksum to the xprv that we already have.
    

$ cs=$(bitcoin-cli getdescriptorinfo "wpkh($dp$xprv/0/*)" | jq -r ' .checksum')

You then plug that into importmulti to import this key into bitcoin-cli:

$ bitcoin-cli importmulti '''[{ "desc": "wpkh('$dp''$xprv'/0/*)#'$cs'", "timestamp": "now", "range": 10, "watchonly": false, "label": "LibwallyImports", "keypool": false, "rescan": false }]'''  
[  
{  
"success": true  
}  
]

Here, you imported/generated the first ten addresses for the private key.

Examining the new LibwallyImported label shows them:

$ bitcoin-cli getaddressesbylabel "LibwallyImports"  
{  
"tb1qzeqrrt77xhvazq5g8sc9th0lzjwstknan8gzq7": {  
"purpose": "receive"  
},  
"tb1q9lhru6k0ymwrtr5w98w35n3lz22upml23h753n": {  
"purpose": "receive"  
},  
"tb1q8fsgxt0z9r9hfl5mst5ylxka2yljjxlxlvaf8j": {  
"purpose": "receive"  
},  
"tb1qg6dayhdk4qc6guutxvdweh6pctc9dpguu6awqc": {  
"purpose": "receive"  
},  
"tb1qdphaj0exvemxhgfpyh4p99wn84e2533u7p96l6": {  
"purpose": "receive"  
},  
"tb1qwv9mdqkpx6trtmvgw3l95npq8gk9pgllucvata": {  
"purpose": "receive"  
},  
"tb1qwh92pkrv6sps62udnmez65vfxe9n5ceuya56xz": {  
"purpose": "receive"  
},  
"tb1q4e98ln8xlym64qjzy3k8zyfyt5q60dgcn39d90": {  
"purpose": "receive"  
},  
"tb1qhzje887fyl65j4mulqv9ysmntwn95zpgmgvtqd": {  
"purpose": "receive"  
},  
"tb1q62xf9ec8zcfkh2qy5qnq4qcxrx8l0jm27dd8ru": {  
"purpose": "receive"  
},  
"tb1qlw85usfk446ssxejm9dmxsfn40kzsqce77aq20": {  
"purpose": "receive"  
}  
}

The second one on your list indeed matches your sample (tb1q9lhru6k0ymwrtr5w98w35n3lz22upml23h753n). The import of this private key and the derivation of ten addresses was successful.

If you now look back at [§7.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/07_3_Integrating_with_Hardware_Wallets.md), you'll see this was the same methodology we used to import addresses from a Hardware Wallet (though this time we also imported the private key as proof of concept). The biggest difference is that previously the information was created by a black box (literally: it was a Ledger device), and this time you created the information yourself using Libwally, showing how you can do this sort of work on airgapped or other more remote devices, then bring it over to bitcoin-cli.

## Import Addresses

Obviously, if you can import private keys, you can import addresses too — which usually means importing watch-only addresses _without_ the private keys.

One way to do so is to use the importmulti methodology above, but to use the supplied xpub address (wpkh([d1280779/84'/1'/0']tpubDWepH8HcqF2RmhRYPy5QmFFEAeU1f3SJotu9BMta8Q8dXRDuHFv8poYqUUtEiWftBjtKn1aNhi9Qg2P4NdzF66dShYvB92z78WJbYeHTLTz/0/*)#f8rmqc0z) rather than original xprv. That's the best way to import a whole sequence of watch-only addresses.

Alternatively, you can import individual addresses. For example, consider the single sample address currently returned by the genhd-for-import program:

$ ./genhd-for-import  
{  
"mnemonic": "finish lady crucial walk illegal ride hamster strategy desert file twin nature",  
"account-xprv": "tprv8xRujYeVN7CwBHxLoTHRdmzwdW7dKUzDfruSo56GqqfRW9QXtnxnaRG8ke7j65uNjxmCVfcagz5uuaMi2vVJ8jpiGZvLwahmNB8F3SHUSyv",  
"address": "tb1qtvcchgyklp6cyleth85c7pfr4j72z2vyuwuj3d",  
"derivation": "[6214ecff/84h/1h/0h]"  
}

You can import that as a watch-only address with importaddress:

$ bitcoin-cli -named importaddress address=tb1qtvcchgyklp6cyleth85c7pfr4j72z2vyuwuj3d label=LibwallyWO rescan=false  
$ bitcoin-cli getaddressesbylabel "LibwallyWO"  
{  
"tb1qtvcchgyklp6cyleth85c7pfr4j72z2vyuwuj3d": {  
"purpose": "receive"  
}  
}

## Summary: Integrating Libwally and Bitcoin-CLI

With a foundational knowledge of Libwally, you can now complement all of the work of your previous lessons. Transferring addresses, keys, transactions, and PSBTs are just some of the ways in which you might make use these two powerful Bitcoin programming methods together. There's also much more potential depth if you want to dig deeper into Libwally's extensive library of functions.

> :fire: _**What is the Power of Integrating Libwally and Bitcoin-CLI?**_ One of the biggest advantages of Libwally is that it has lots of functions that can be used offline. In comparison, Bitcoin Core is a networked program. This can help you increase security by having bitcoin-cli pass off keys, addresses, transactions, or PSBTs to an offline source (which would be running Libwally programs). Besides that, Libwally can do things that Bitcoin Core currently can't, such as generating a seed from a BIP39 mnemonic (and even if you can't currently import the seed to Bitcoin Core, you _can_ still import the master key for the account, as shown here).

## What's Next?

Learn about other sorts of programming in [Chapter 18: Talking to Bitcoind with Other Languages](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_0_Talking_to_Bitcoind_Other.md).

# Chapter 18: Talking to Bitcoind with Other Languages

You should now have a solid foundation for working with Bitcoin in C, not only using RPC, JSON, and ZMQ libraries to directly interact with bitcoind, but also utilizing the Libwally libraries to complement that work. And C is a great language for prototyping and abstraction — but it's probably not what you're programming in. This chapter thus takes a whirlwind tour of six other programming languages, demonstrating the barest Bitcoin functionality in each and allowing you to expand the lessons of the command line and C to the programming language of your choice.

Each of the sections contains approximately the same information, focused on: creating an RPC connection; examining the wallet; creating a new address, and creating a transaction. However, there's some variety among the languages, showing off different aspects of Bitcoin's RPC commands in different examples. In particular, some languages use the easy methodology of sendtoaddress while others use the hard methodology of creating a raw transaction from scratch.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Prepare Bitcoin Development Environments for a Variety of Languages
    
- Use Wallet Functions in a Variety of Languages
    
- Use Transaction Functions in a Variety of Languages
    

Supporting objectives include the ability to:

- Understand More about Bitcoin RPC through Interactions with a Variety of Languages
    

## Table of Contents

- [Section One: Accessing Bitcoind with Go](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_1_Accessing_Bitcoind_with_Go.md)
    
- [Section Two: Accessing Bitcoind with Java](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_2_Accessing_Bitcoind_with_Java.md)
    
- [Section Three: Accessing Bitcoind with NodeJS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_3_Accessing_Bitcoind_with_NodeJS.md)
    
- [Section Four: Accessing Bitcoind with Python](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_4_Accessing_Bitcoind_with_Python.md)
    
- [Section Five: Accessing Bitcoind with Rust](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_5_Accessing_Bitcoind_with_Rust.md)
    
- [Section Six: Accessing Bitcoind with Swift](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_6_Accessing_Bitcoind_with_Swift.md)
    

# 18.1: Accessing Bitcoind with Go

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the Go programming language and the [btcd rpcclient](https://github.com/btcsuite/btcd/tree/master/rpcclient). Note that it has some quirks and some limitations.

## Set Up Go

To prepare for Go usage on your UNIX machine, first install curl if you haven't already:

$ sudo apt install curl

Then, look at the [Go downloads page](https://golang.org/dl/), get the link for the latest download, and download it using curl. For a Debian setup, you will want to use the linux-amd64 version:

$ curl -O [https://dl.google.com/go/go1.15.1.linux-amd64.tar.gz](https://dl.google.com/go/go1.15.1.linux-amd64.tar.gz)

Once it finishes downloading, compare the hash of the download to the hash on the [Go downloads page](https://golang.org/dl/):

$ sha256sum go1.15.1.linux-amd64.tar.gz  
70ac0dbf60a8ee9236f337ed0daa7a4c3b98f6186d4497826f68e97c0c0413f6 go1.15.1.linux-amd64.tar.gz

The hashes should match. If so, extract the tarball and install Go on your system:

$ tar xfv go1.15.1.linux-amd64.tar.gz  
$ sudo chown -R root:root ./go  
$ sudo mv go /usr/local

Now you need to create a Go path to specify your environment. Open the ~/.profile file with an editor of your choice and add the following to the end of it:

export GOPATH=$HOME/work  
export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

Then, refresh your profile:

$ source ~/.profile

Lastly, create the directory for your Go workspace:

$ mkdir $HOME/work

### Set Up btcd rpcclient

You'll be using the rpcclient that comes with btcd, a Bitcoin implementation written in Go. Although rpcclient was originally designed to work with the btcd Bitcoin full node, it also works with Bitcoin Core. It has some quirks which we will be looking at.

You can use go get to download it:

$ go get github.com/btcsuite/btcd/rpcclient

To test that it works, navigate to the directory with the Bitcoin Core examples:

$ cd $GOPATH/src/github.com/btcsuite/btcd/rpcclient/examples/bitcoincorehttp

Modify the main.go file and enter the details associated with your Bitcoin core setup, which can be found in ~/.bitcoin/bitcoin.conf:

    Host:         "localhost:18332",    
    User:         "StandUp",    
    Pass:         "6305f1b2dbb3bc5a16cd0f4aac7e1eba",

> **MAINNET VS TESTNET:** The port would be 8332 for a mainnet setup.

You can now run a test:

$ go run main.go

You should see the block count printed:

2020/09/01 11:41:24 Block count: 1830861

### Create a rpcclient Project

You will typically be creating projects in your ~/work/src/myproject/bitcoin directory:

$ mkdir -p ~/work/src/myproject/bitcoin  
$ cd ~/work/src/myproject/bitcoin

Each project should have the following imports:

import (  
"log"  
"fmt"  
"github.com/btcsuite/btcd/rpcclient"  
)

This import declaration allows you to import relevant libraries. For every example here, you will need to import "log", "fmt" and "github.com/btcsuite/btcd/rpcclient". You may need to import additional libraries for some examples.

- log is used for printing out error messages. After each time the Bitcoin node is called, an if statement will check if there are any errors. If there are errors, log is used to print them out.
    
- fmt is used for printing out output.
    
- rpcclient is obviously the rpcclient library
    

## Build Your Connection

Every bitcoind function in Go begins with creating the RPC connection, using the ConnConfig function:

connCfg := &rpcclient.ConnConfig{    
    Host:         "localhost:18332",    
    User:         "StandUp",    
    Pass:         "431451790e3eee1913115b9dd2fbf0ac",    
    HTTPPostMode: true,    
    DisableTLS:   true,    
}    
client, err := rpcclient.New(connCfg, nil)    
if err != nil {    
    log.Fatal(err)    
}    
defer client.Shutdown()

The connCfg parameters allow you to choose the Bitcoin RPC port, username, password and whether you are on testnet or mainnet.

> **NOTE:** Again, be sure to substitute the User and Pass with the one found in your ~/.bitcoin/bitcon.conf.

Therpcclient.New(connCfg, nil) function then configures client to connect to your Bitcoin node.

The defer client.Shutdown() line is for disconnecting from your Bitcoin node, once the main() function finishes executing. After the defer client.Shutdown() line is where the exciting stuff goes — and it will be pretty easy to use. That's's because rpcclient helpfully turns the bitcoin-cli commands into functions using PascalCase. For example, bitcoin-cli getblockcount will be client.GetBlockCount in Go.

### Make an RPC Call

All that's required now is to make an informational call like GetBlockCount or GetBlockHash using your client:

blockCount, err := client.GetBlockCount()    
if err != nil {    
    log.Fatal(err)    
}    
blockHash, err := client.GetBlockHash(blockCount)    
if err != nil {    
    log.Fatal(err)    
}    
  
fmt.Printf("%d\n", blockCount)    
fmt.Printf("%s\n", blockHash.String())

### Make an RPC Call with Arguments

The rpcclient functions can take inputs as well; for example client.GetBlockHash(blockCount) takes the block count as an input. The client.GetBlockHash(blockCount) from above would look like this as a bitcoin-cli command:

$ bitcoin-cli getblockhash 1830868  
00000000000002d53b6b9bba4d4e7dc44a79cebd1024d1bcfb9b3cc07d6cad9c

However, a quirk with hashes in rpcclient is that they will typically print in a different encoding if you were to print then normally with blockHash. In order to print them as a string, you need to use blockHash.String().

### Run Your Code

You can download the complete code from the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_1_blockinfo.go).

You can then run:

$ go run blockinfo.go  
1830868  
00000000000002d53b6b9bba4d4e7dc44a79cebd1024d1bcfb9b3cc07d6cad9c

The latest block number along with its hash should be printed out.

## Look up Funds

Due to limitations of the btcd rpcclient, you can't make a use of the getwalletinfo function. However, you can make use of the getbalance RPC:

wallet, err := client.GetBalance("*")    
if err != nil {    
    log.Fatal(err)    
}    
  
fmt.Println(wallet)

client.GetBalance("_") requires the "_" input, due to a quirk with btcd. The asterisk signifies that you want to get the balance of all of your wallets.

If you run [the src code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_1_getbalance.go), you should get an output similar to this:

$ go run getbalance.go  
0.000689 BTC

## Create an Address

You can generate addresses in Go, but you can't specify the address type:

This requires the use of a special chaincfg function, to specify which network the addresses are being created for. This specification is only required during address generation, which is why it is only used in this example. You can include this in other examples as well, but it isn't necessary.

Be sure to import "github.com/btcsuite/btcd/chaincfg":

import (  
"log"  
"fmt"  
"github.com/btcsuite/btcd/rpcclient"  
"github.com/btcsuite/btcd/chaincfg"  
)

Then call connCfG with the chaincfg.TestNet3Params.Name parameter:

connCfg := &rpcclient.ConnConfig{    
    Host:         "localhost:18332",    
    User:         "bitcoinrpc",    
    Pass:         "431451790e3eee1913115b9dd2fbf0ac",    
    HTTPPostMode: true,    
    DisableTLS:   true,    
    Params: chaincfg.TestNet3Params.Name,    
}    
client, err := rpcclient.New(connCfg, nil)    
if err != nil {    
    log.Fatal(err)    
}    
defer client.Shutdown()

> **MAINNET VS TESTNET:** Params: chaincfg.TestNet3Params.Name, should be Params: chaincfg.MainNetParams.Name, on mainnet.

You can then create your address:

address, err := client.GetNewAddress("")    
if err != nil {    
    log.Fatal(err)    
}    
fmt.Println(address)

A quirk with client.GetNewAddress("") is that an empty string needs to be included for it to work.

Running [the source](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_1_getaddress.go) produces the following results:

$ go run getaddress.go  
tb1qutkcj34pw0aq7n9wgp3ktmz780szlycwddfmza

### Decode an Address

Creating an address took a little extra work, in specifying the appropriate chain. Using an address also will because you'll have to decode it prior to use.

The means that you'll have to import both the "github.com/btcsuite/btcutil" and "github.com/btcsuite/btcd/chaincfg" libraries.

- btcutil allows for a Bitcoin address to be decoded in a way that therpcclient can understand. This is necessary when working with addresses in rpcclient.
    
- chaincfg is (again) used to configure your chain as the Testnet chain. This is necessary for address decoding since the addresses used on Mainnet and Testnet are different.
    

import (  
"log"  
"fmt"  
"github.com/btcsuite/btcd/rpcclient"  
"github.com/btcsuite/btcutil"  
"github.com/btcsuite/btcd/chaincfg"  
)

The defaultNet variable is now used to specify whether your Bitcoin node is on testnet or on mainnet. That information (and the btcutil object) is then used to decode the address.

> **MAINNET VS TESTNET:** &chaincfg.TestNet3Params should be &chaincfg.MainNetParams on mainnet.

defaultNet := &chaincfg.TestNet3Params    
addr, err := btcutil.DecodeAddress("mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha", defaultNet)    
if err != nil {    
    log.Fatal(err)    
}

> **NOTE:** Change the address (mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha) for one actually your wallet; you can use bitcoin-cli listunspent to find some addresses with funds for this test. If you want to be really fancy, modify the Go code to take an argument, then write a script that runs listunspent, saves the info to a variable, and runs the Go code on that.

Only afterward do you use the getreceivedbyaddress RPC, on your decoded address:

wallet, err := client.GetReceivedByAddress(addr)    
if err != nil {    
    log.Fatal(err)    
}    
  
fmt.Println(wallet)

When you run [the code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_1_getamountreceived.go), you should get output similar to:

$ go run getamountreceived.go  
0.0085 BTC

## Send a Transaction

You've now got all the puzzle pieces in place to send a transaction. You're going to want to:

1. Import the correct libraries, including chaincfg to specify a network and btcutil to decode an address.
    
2. Choose an address to send to.
    
3. Decode that address.
    
4. Run sendtoaddress to send funds the easy way.
    

package main

import (  
"log"  
"fmt"  
"github.com/btcsuite/btcd/rpcclient"  
"github.com/btcsuite/btcutil"  
"github.com/btcsuite/btcd/chaincfg"  
)

func main() {  
connCfg := &rpcclient.ConnConfig{  
Host: "localhost:18332",  
User: "StandUp",  
Pass: "431451790e3eee1913115b9dd2fbf0ac",  
HTTPPostMode: true,  
DisableTLS: true,  
}  
client, err := rpcclient.New(connCfg, nil)  
if err != nil {  
log.Fatal(err)  
}  
defer client.Shutdown()

defaultNet := &chaincfg.TestNet3Params    
addr, err := btcutil.DecodeAddress("n2eMqTT929pb1RDNuqEnxdaLau1rxy3efi", defaultNet)    
if err != nil {    
    log.Fatal(err)    
}    
sent, err := client.SendToAddress(addr, btcutil.Amount(1e4))    
if err != nil {    
    log.Fatal(err)    
}    
  
fmt.Println(sent)  

}

When you run [the code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_1_sendtransaction.go), the txid of the transaction is outputted:

$ go run sendtransaction.go  
9aa4cd6559e0d69059eae142c35bfe78b71a8084e1fcc2c74e2a9675e9e7489d

### Look Up a Transaction

To lookup a transaction, such as the one you just sent, you'll need to once again do some conversions, this time of txid. "github.com/btcsuite/btcd/chaincfg/chainhash" is imported in order to allow hashes to be stored in the Go code. chainhash.NewHashFromStr("hash") converts a hash in a string to a format that works with rpcclient.

package main

import (  
"log"  
"fmt"  
"github.com/btcsuite/btcd/rpcclient"  
"github.com/btcsuite/btcd/chaincfg/chainhash"  
)

func main() {  
connCfg := &rpcclient.ConnConfig{  
Host: "localhost:18332",  
User: "StandUp",  
Pass: "431451790e3eee1913115b9dd2fbf0ac",  
HTTPPostMode: true,  
DisableTLS: true,  
}  
client, err := rpcclient.New(connCfg, nil)  
if err != nil {  
log.Fatal(err)  
}  
defer client.Shutdown()

chash, err := chainhash.NewHashFromStr("1661ce322c128e053b8ea8fcc22d17df680d2052983980e2281d692b9b4ab7df")    
if err != nil {    
    log.Fatal(err)    
}    
transactions, err := client.GetTransaction(chash)    
if err != nil {    
    log.Fatal(err)    
}    
  
fmt.Println(transactions)  

}

> **NOTE:** Again, you'll want to change out the txid for one actually recognized by your system.

When you run [the code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_1_lookuptransaction.go) it will print out the details associated with a transaction, such as its amount and how many times it has been confirmed:

$ go run lookuptransaction.go  
{  
"amount": 0.00100000,  
"confirmations": 4817,  
"blockhash": "000000006628870b0a8a66abea9cf0d4e815c491f079e3fa9e658a87b5dc863a",  
"blockindex": 117,  
"blocktime": 1591857418,  
"txid": "1661ce322c128e053b8ea8fcc22d17df680d2052983980e2281d692b9b4ab7df",  
"walletconflicts": [  
],  
"time": 1591857343,  
"timereceived": 1591857343,  
"bip125-replaceable": "no",  
"details": [  
{  
"address": "mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha",  
"category": "receive",  
"amount": 0.00100000,  
"label": "",  
"vout": 0  
}  
],  
"hex": "02000000000101e9e8c3bd057d54e73baadc60c166860163b0e7aa60cab33a03e89fb44321f8d5010000001716001435c2aa3fc09ea53c3e23925c5b2e93b9119b2568feffffff02a0860100000000001976a914600c8c6a4abb0a502ea4de01681fe4fa1ca7800688ac65ec1c000000000017a91425b920efb2fde1a0277d3df11d0fd7249e17cf8587024730440220403a863d312946aae3f3ef0a57206197bc67f71536fb5f4b9ca71a7e226b6dc50220329646cf786cfef79d60de3ef54f702ab1073694022f0618731902d926918c3e012103e6feac9d7a8ad1ac6b36fb4c91c1c9f7fff1e7f63f0340e5253a0e4478b7b13f41fd1a00"  
}

## Summary: Accessing Bitcoind with Go

Although the btcd rpcclient has some limits, you can still perform the main RPC commands in Go. The documentation for rpcclient is available on [Godoc](https://godoc.org/github.com/btcsuite/btcd/rpcclient). If the documentation doesn't have what you're looking for, also consult the [btcd repository](https://github.com/btcsuite/btcd). It is generally well documented and easy to read. Based on these examples you should be able to incorporate Bitcoin in a Go project and do things like send and receive coins.

## What's Next?

Learn more about "Talking to Bitcoin in Other Languages" in [18.2: Accessing Bitcoin with Java](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_2_Accessing_Bitcoind_with_Java.md).

# 18.2: Accessing Bitcoind with Java

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the Java programming language and the [JavaBitcoindRpcClient](https://github.com/Polve/JavaBitcoindRpcClient).

## Set Up Java

You can install Java on your server, using the apt-get command. You will also install [Apache Maven](http://maven.apache.org/) to manage the dependencies.

$ sudo apt-get install openjdk-11-jre-headless maven

You can verify your Java installation:

$ java -version  
openjdk version "11.0.8" 2020-07-14  
OpenJDK Runtime Environment (build 11.0.8+10-post-Debian-1deb10u1)  
OpenJDK 64-Bit Server VM (build 11.0.8+10-post-Debian-1deb10u1, mixed mode, sharing)

### Create a Maven Project

In order to program with Bitcoin using java, you will create a Maven project:

$ mvn archetype:generate -DgroupId=com.blockchaincommons.lbtc -DartifactId=java-project -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

This will download some dependencies

Downloading: [https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom](https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom)  
Downloaded: [https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom](https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-clean-plugin/2.5/maven-clean-plugin-2.5.pom) (4 KB at 4.2 KB/sec)  
Downloading: [https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom](https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom)  
Downloaded: [https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom](https://repo.maven.apache.org/maven2/org/apache/maven/plugins/maven-plugins/22/maven-plugins-22.pom) (13 KB at 385.9 KB/sec)  
Downloading: [https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom](https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom)  
Downloaded: [https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom](https://repo.maven.apache.org/maven2/org/apache/maven/maven-parent/21/maven-parent-21.pom) (26 KB at 559.6 KB/sec)  
Downloading: [https://repo.maven.apache.org/maven2/org/apache/apache/10/apache-10.pom](https://repo.maven.apache.org/maven2/org/apache/apache/10/apache-10.pom)  
..............

It will also create a configuration file pom.xml:

$ cd java-project  
$ ls -lagh  
total 16K  
drwxr-xr-x 3 sudo 4.0K Sep 1 13:58 .  
drwxr-xr-x 15 sudo 4.0K Sep 1 13:58 ..  
-rw-r--r-- 1 sudo 663 Sep 1 13:58 pom.xml  
drwxr-xr-x 4 sudo 4.0K Sep 1 13:58 src

In order to include JavaBitcoindRpcClient, you must add its dependency to in the pom.xml file

  <dependency>    
    <groupId>wf.bitcoin</groupId>    
    <artifactId>bitcoin-rpc-client</artifactId>    
    <version>1.2.1</version>    
  </dependency>

You also need to add compiler properties to indicate what JDK version will compile the source code.

Whenever you add source code to your classes, you'll be able to test it with:

$ mvn compile

You can also execute with exec:java

$ mvn exec:java -Dexec.mainClass=com.blockchaincommons.lbtc.App

### Create Alternative Projects

If you use [Gradle](([https://gradle.org/releases/](https://gradle.org/releases/)), you can instead run:

compile 'wf.bitcoin:JavaBitcoindRpcClient:1.2.1'

If you want a sample project and some instructions on how to run it on the server that you just created, you can refer to the [Bitcoind Java Sample Project](https://github.com/brunocvcunha/bitcoind-java-client-sample/). You can also browse all souce code for bitcoin-rpc-client ([https://github.com/Polve/bitcoin-rpc-client](https://github.com/Polve/bitcoin-rpc-client)).

## Build Your Connection

To use JavaBitcoindRpcClient, you need to create a BitcoindRpcClient instance. You do this by creating a URL with arguments of username, password, IP address and port. As you'll recall, the IP address 127.0.0.1 and port 18332 should be correct for the standard testnet setup described in this course, while you can extract the user and password from ~/.bitcoin/bitcoin.conf.

   BitcoindRpcClient rpcClient = new BitcoinJSONRPCClient("http://StandUp:6305f1b2dbb3bc5a16cd0f4aac7e1eba@localhost:18332");

Note that you'll also need to import the appropriate information:

import wf.bitcoin.javabitcoindrpcclient.BitcoinJSONRPCClient;  
import wf.bitcoin.javabitcoindrpcclient.BitcoindRpcClient;

> **MAINNET VS TESTNET:** The port would be 8332 for a mainnet setup.

If rpcClient is successfully initialized, you'll be able to send RPC commands.

Later, when you're all done with your bitcoind connection, you should close it:

rpcClient.stop();

### Make an RPC Call

You'll find that the BitcoindRpcClient provides most of the functionality that can be accessed through bitcoin-cli or other RPC methods, using the same method names, but in camelCase.

For example, to execute the getmininginfo command to get the block information and the difficulty on the network, you should use the getMiningInfo() method:

MiningInfo info = rpcClient.getMiningInfo();  
System.out.println("Mining Information");  
System.out.println("------------------");  
System.out.println("Chain......: " + info.chain());  
System.out.println("Blocks.....: " + info.blocks());  
System.out.println("Difficulty.: " + info.difficulty());  
System.out.println("Hash Power.: " + info.networkHashps());

The output for this line should be similar to this:

## Mining Information

Chain......: test  
Blocks.....: 1830905  
Difficulty.: 4194304  
Hash Power.: 40367401348837.41

### Make an RPC Call with Arguments

You can look up addresses on your wallet by passing the address as an argument to getAddressInfo:

String addr1 = "mvLyH7Rs45c16FG2dfV7uuTKV6pL92kWxo";    
  
AddressInfo addr1Info = rpcClient.getAddressInfo(addr1);    
System.out.println("Address: " + addr1Info.address());    
System.out.println("MasterFingerPrint: " + addr1Info.hdMasterFingerprint());    
System.out.println("HdKeyPath: " + addr1Info.hdKeyPath());    
System.out.println("PubKey: " + addr1Info.pubKey());

The output will look something like this:

Address: mvLyH7Rs45c16FG2dfV7uuTKV6pL92kWxo  
MasterFingerPrint: ce0c7e14  
HdKeyPath: m/0'/0'/5'  
PubKey: 0368d0fffa651783524f8b934d24d03b32bf8ff2c0808943a556b3d74b2e5c7d65

### Run Your Code

The code for these examples can be found in [the src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_2_App-getinfo.java) and should be installed into the standard directory structure created here as ~/java-project/src/main/java/com/blockchaincommons/lbtc/App.java. It can then be compiled and run.

$ mvn compile  
$ mvn exec:java -Dexec.mainClass=com.blockchaincommons.lbtc.App  
Chain......: test  
Blocks.....: 1831079  
Difficulty.: 4194304  
Hash Power.: 38112849943221.16  
Address: mvLyH7Rs45c16FG2dfV7uuTKV6pL92kWxo  
MasterFingerPrint: ce0c7e14  
HdKeyPath: m/0'/0'/5'  
PubKey: 0368d0fffa651783524f8b934d24d03b32bf8ff2c0808943a556b3d74b2e5c7d65

(You'll also see lots more information about the compilation, of course.)

## Look up Funds

Retrieving the balance for a whole account is equally easy:

    System.out.println("Balance: " + rpcClient.getBalance());

## Create an Address

You can create a new address on your wallet, attach a specific label to it, and even dump its private key.

String address = rpcClient.getNewAddress("Learning-Bitcoin-from-the-Command-Line");  
System.out.println("New Address: " + address);

String privKey = rpcClient.dumpPrivKey(address);  
System.out.println("Priv Key: " + privKey);

Output:

New Address: mpsFtZ8qTJPRGZy1gaaUw37fHeUSPLkzzs  
Priv Key: cTy2AnmAALsHokYzJzTdsUBSqBtypmWfmSNYgG6qQH43euUZgqic

## Send a Transaction

The JavaBitcoindRpcClient library has some good tools that make it easy to create a transaction from scratch.

### Create a Transaction

You can create a raw transaction using the createRawTransaction method, passing as arguments two ArrayList objects containing inputs and outputs to be used.

First you set up your new addresses, here an existing address on your system and a new address on your system.

    String addr1 = "tb1qdqkc3430rexxlgnma6p7clly33s6jjgay5q8np";    
    System.out.println("Used address addr1: " + addr1);    
  
    String addr2 = rpcClient.getNewAddress();    
    System.out.println("Created address addr2: " + addr2);

Then, you can use the listUnspent RPC to find UTXOs for the existing address.

    List<Unspent> utxos = rpcClient.listUnspent(0, Integer.MAX_VALUE, addr1);    
    System.out.println("Found " + utxos.size() + " UTXOs (unspent transaction outputs) belonging to addr1");

Here's an output of all the information:

System.out.println("Created address addr1: " + addr1);  
String addr2 = rpcClient.getNewAddress();  
System.out.println("Created address addr2: " + addr2);  
List generatedBlocksHashes = rpcClient.generateToAddress(110, addr1);  
System.out.println("Generated " + generatedBlocksHashes.size() + " blocks for addr1");  
List utxos = rpcClient.listUnspent(0, Integer.MAX_VALUE, addr1);  
System.out.println("Found " + utxos.size() + " UTXOs (unspent transaction outputs) belonging to addr1");

Transactions are built with BitcoinRawTxBuilder:

    BitcoinRawTxBuilder txb = new BitcoinRawTxBuilder(rpcClient);

First you fill the inputs with the UTXOs you're spending:

    TxInput in = utxos.get(0);    
    txb.in(in);

> :warning: **WARNING:** Obviously in a real program you'd intelligently select a UTXO; here, we just grab the 0th one, a tactic that we'll use throughout this chapter.

Second, you fill the ouputs each with an amount and an address:

BigDecimal estimatedFee = BigDecimal.valueOf(0.00000200);    
    BigDecimal txToAddr2Amount = utxos.get(0).amount().subtract(estimatedFee);    
txb.out(addr2, txToAddr2Amount);    
  
System.out.println("unsignedRawTx in amount: " + utxos.get(0).amount());    
    System.out.println("unsignedRawTx out amount: " + txToAddr2Amount);

You're now ready to actually create the transaction:

String unsignedRawTxHex = txb.create();    
System.out.println("Created unsignedRawTx from addr1 to addr2: " + unsignedRawTxHex);

### Sign a Transactions

You now can sign transaction with the method signRawTransactionWithKey. This method receives as parameters an unsigned raw string transaction, the private key of the sending address, and the TxInput object.

SignedRawTransaction srTx = rpcClient.signRawTransactionWithKey(    
                unsignedRawTxHex,    
                Arrays.asList(rpcClient.dumpPrivKey(addr1)), //    
                Arrays.asList(in),    
                null);    
System.out.println("signedRawTx hex: " + srTx.hex());    
System.out.println("signedRawTx complete: " + srTx.complete());

### Send a Transactiong

Finally, sending requires the sendRawTransaction command:

String sentRawTransactionID = rpcClient.sendRawTransaction(srTx.hex());  
System.out.println("Sent signedRawTx (txID): " + sentRawTransactionID);

### Run Your Code

You can now run [the transaction code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_2_App-sendtx.java) as ~/java-project/src/main/java/com/blockchaincommons/lbtc/App.java.

$ mvn compile  
$ mvn exec:java -Dexec.mainClass=com.blockchaincommons.lbtc.App  
Used address addr1: tb1qdqkc3430rexxlgnma6p7clly33s6jjgay5q8np  
Created address addr2: tb1q04q2wzlhfqlrnz95ynfj7gp4t3yynrj0542smv  
Found 1 UTXOs (unspent transaction outputs) belonging to addr1  
unsignedRawTx in amount: 0.00850000  
unsignedRawTx out amount: 0.00849800  
Created unsignedRawTx from addr1 to addr2: 0200000001d2a90fc3b43e8eb4ae9452af43c9448112d359cac701f7f537aa8b6f39193bb90100000000ffffffff0188f70c00000000001600147d40a70bf7483e3988b424d32f20355c48498e4f00000000  
signedRawTx hex: 02000000000101d2a90fc3b43e8eb4ae9452af43c9448112d359cac701f7f537aa8b6f39193bb90100000000ffffffff0188f70c00000000001600147d40a70bf7483e3988b424d32f20355c48498e4f024730440220495fb64d8cf9dee9daa8535b8867709ac8d3763d693fd8c9111ce610645c76c90220286f39a626a940c3d9f8614524d67dd6594d9ee93818927df4698c1c8b8f622d01210333877967ac52c0d0ec96aca446ceb3f51863de906e702584cc4da2780d360aae00000000  
signedRawTx complete: true  
Sent signedRawTx (txID): 82032c07e0ed91780c3369a1943ea8abf49c9e11855ffedd935374ecbc789c45

## Listen to Transactions or Blocks

As with [C and its ZMQ libraries](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/15_3_Receiving_Bitcoind_Notifications_with_C.md), there are easy ways to use Java to listen to the blockchain — and to execute specific code when something happens, such as a transaction that involves an address in your wallet, or even the generation of a new block in the network.

To do this, use JavaBitcoindRpcClient's BitcoinAcceptor class, which allows you to attach listeners in the network.

    String blockHash = rpcClient.getBestBlockHash();    
BitcoinAcceptor acceptor = new BitcoinAcceptor(rpcClient, blockHash, 6, new BitcoinPaymentListener() {    
  
      @Override    
      public void transaction(Transaction tx) {    
        System.out.println("Transaction: " + tx);    
      }    
  
      @Override    
      public void block(String block) {    
        System.out.println("Block: " + block);    
      }    
});  

acceptor.run();

See [the src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_2_App-listen.java) for the complete code. Every time a transaction is sent or a new block is generated, you should see output on your console:

Transaction: {account=Tests, address=mhopuJzgmTwhGfpNLCJ9CRknugY691oXp1, category=receive, amount=5.0E-4, label=Tests, vout=1, confirmations=0, trusted=false, txid=361e8fcff243b74ebf396e595a007636654f67c3c7b55fd2860a3d37772155eb, walletconflicts=[], time=1513132887, timereceived=1513132887, bip125-replaceable=unknown}

Block: 000000004564adfee3738314549f7ca35d96c4da0afc6b232183917086b6d971

### Summary Accessing Bitcoind with Java

By using the javabitcoinrpc library, you can easily access bitcoind via RPC calls from Java. You'll also have access to nice additional features, like the bitcoinAcceptor listening service.

## What's Next?

Learn more about "Talking to Bitcoin in Other Languages" in [18.3: Accessing Bitcoin with NodeJS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_3_Accessing_Bitcoind_with_NodeJS.md).

# 18.3: Accessing Bitcoind with NodeJS

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the NodeJS programming language and the [BCRPC package](https://github.com/dgarage/bcrpc).

## Set Up Node.js

BCRPC is built on node.js. Thus, you'll first need to install the node.js and npm (the node package manager) packages for your system.

If you're using a Ubuntu machine, you can run the following commands to get a new version of node.js (as opposed to the horribly out-of-date version in the Ubuntu package system).

$ curl -sL [https://deb.nodesource.com/setup_14.x](https://deb.nodesource.com/setup_14.x) | sudo bash -  
$ sudo apt-get install -y nodejs  
$ sudo npm install mocha -g

### Set Up BCRPC

You can now clone the BCRPC package from GitHub and install its dependencies.

$ git clone [https://github.com/dgarage/bcrpc.git](https://github.com/dgarage/bcrpc.git)  
$ cd bcrpc  
$ npm install

To test the BCRPC package, you must first set environmental variables for your rpcuser and rpcpassword. As usual, these come from ~/.bitcoin/bitcoin.conf. You must also set the RPC port to 18332 which should be correct for the standard testnet setup described in these documents.

$ export BITCOIND_USER=StandUp  
$ export BITCOIND_PASS=d8340efbcd34e312044c8431c59c792c  
$ export BITCOIND_PORT=18332

> :warning: **WARNING:** Obviously, you'd never put your password in an environmental variable in a production environment. :link: **MAINNET VS TESTNET:** The port would be 8332 for a mainnet setup.

You can now verify everything is working correctly:

$ npm test

> [bcrpc@0.2.2](mailto:bcrpc@0.2.2) test /home/user1/bcrpc  
> mocha tests.js

BitcoinD  
✓ is running

bcrpc  
✓ can get info

2 passing (36ms)

Congratulations, you now have a Bitcoin-ready RPC wrapper for Node.js that is working with your Bitcoin setup.

### Create a BCRPC Project

You can now create a new Node.js project and install BCRPC via npm.

$ cd ~  
$ mkdir myproject  
$ cd myproject  
$ npm init  
[continue with default options]  
$ npm install bcrpc

## Build Your Connection

In your myproject directory, create a .js file where you JavaScript code will be executed.

You can initiate an RPC connection by creating an RpcAgent:

const RpcAgent = require('bcrpc');  
agent = new RpcAgent({port: 18332, user: 'StandUp', pass: 'd8340efbcd34e312044c8431c59c792c'});

Obviously, your user and pass should again match what's in your ~/.bitcoin/bitcoin.conf, and you use port 18332 if you're on testnet.

### Make an RPC Call

Using BCRPC, you can use the same RPC commands you would usually use via bitcoin-cli with your RpcAgent, except they need to be in camelCase. For example, getblockhash would be getBlockHash instead.

To print the newest block number, you just call getBlockCount through your RpcAgent:

agent.getBlockCount(function (err, blockCount) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(blockCount.result);  
});

### Make an RPC Call with Arguments

The BCRPC functions can accept arguments. For example, getBlockHash takes blockCount.result as an input.

agent.getBlockHash(blockCount.result, function (err, hash) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(hash.result);  
})

The result of the BCRPC functions is a JSON object containing information about any errors and the id of the request. When accessing your result, you add .result to the end of it to specify that you are interested in the actual result, not information about errors.

### Run Your Code

You can find the getinfo code in [the src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_3_getinfo.js).

$ node getinfo.js  
1831094  
00000000000002bf8b522a830180ad3a93b8eed33121f54b3842d8838580a53c

This is what output of the above example would look like if you replaced console.log(blockCount.result); and console.log(hash.result); with console.log(blockCount); and console.log(hash);, respectively:

{ result: 1774686, error: null, id: null }  
{  
result: '00000000000000d980c495a2b7addf09bb0a9c78b5b199c8e965ee54753fa5da',  
error: null,  
id: null  
}

## Look Up Funds

It's useful when accepting Bitcoin to check the received Bitcoin on a specific address in your wallet. For example, if you were running an online store accepting Bitcoin, for each payment from a customer, you would generate a new address, show that address to the customer, then check the balance of the address after some time, to make sure the correct amount has been received:

agent.getReceivedByAddress('mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha', function (err, addressInfo) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(addressInfo.result);  
});

> :information_source: **NOTE:** Obviously, you'll need to enter an address recognized by your machine.

By default this functions checks the transactions that have been confirmed once, however you can increase this to a higher number such as 6:

agent.getReceivedByAddress('mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha', 6, function (err, addressInfo) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(addressInfo.result);  
});

### Look Up Wallet Information

You can also look up additional information about your wallet and view your balance, transaction count, et cetera:

agent.getWalletInfo(function (err, walletInfo) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(walletInfo.result);  
});

The source is available as [walletinfo.js](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_3_walletinfo.js).

$ node walletinfo.js  
0.008498  
{  
walletname: '',  
walletversion: 169900,  
balance: 0.010438,  
unconfirmed_balance: 0,  
immature_balance: 0,  
txcount: 4,  
keypoololdest: 1596567843,  
keypoolsize: 999,  
hdseedid: 'da5a1b058deb9e51ecffef1b0ddc069a5dfb2c5f',  
keypoolsize_hd_internal: 1000,  
paytxfee: 0,  
private_keys_enabled: true,  
avoid_reuse: false,  
scanning: false  
}

Instead of printing all the details associated with your wallet, you can print specific information, such as your balance. Since a JSON object is being accessed, this can be done by changing the line console.log(walletInfo.result); to console.log(walletInfo.result.balance);:

## Create an Address

You can also pass additional arguments to RPC commands. For example, the following generates a new legacy address, with the -addresstype flag.

agent.getNewAddress('-addresstype', 'legacy', function (err, newAddress) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(newAddress.result);  
});

This is the same as running the following from the command line:

$ bitcoin-cli getnewaddress -addresstype legacy  
mtGPcBvRPZFEHo2YX8un9qqPBydhG82uuZ

In BCRPC, you can generally use the same flags as in bitcoin-cli in BCRPC. Though you use camelCase (getNewAddress) for the methods, the flags, which are normally separated by spaces on the command line, are instead placed in strings and separated by commas.

## Send a Transaction

You can send coins to an address most easily using the sendToAddress function:

agent.sendToAddress(newAddress.result, 0.00001, function(err, txid) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(txid.result);  
});

This should print the txid of the transaction:

1679bee019c61608340b79810377be2798efd4d2ec3ace0f00a1967af70666b9

### Look Up a Transaction

You may now wish to view a transaction, such as the one you just sent.

agent.getTransaction(txid.result, function (err, transaction) {  
if (err)  
throw Error(JSON.stringify(err));  
console.log(transaction.result);  
});

You should get an output similar to this:

{  
amount: 0.001,  
confirmations: 4776,  
blockhash: '000000006628870b0a8a66abea9cf0d4e815c491f079e3fa9e658a87b5dc863a',  
blockindex: 117,  
blocktime: 1591857418,  
txid: '1661ce322c128e053b8ea8fcc22d17df680d2052983980e2281d692b9b4ab7df',  
walletconflicts: [],  
time: 1591857343,  
timereceived: 1591857343,  
'bip125-replaceable': 'no',  
details: [  
{  
address: 'mpGpCMX6SuUimDZKiVViuhd7EGyVxkNnha',  
category: 'receive',  
amount: 0.001,  
label: '',  
vout: 0  
}  
],  
hex: '02000000000101e9e8c3bd057d54e73baadc60c166860163b0e7aa60cab33a03e89fb44321f8d5010000001716001435c2aa3fc09ea53c3e23925c5b2e93b9119b2568feffffff02a0860100000000001976a914600c8c6a4abb0a502ea4de01681fe4fa1ca7800688ac65ec1c000000000017a91425b920efb2fde1a0277d3df11d0fd7249e17cf8587024730440220403a863d312946aae3f3ef0a57206197bc67f71536fb5f4b9ca71a7e226b6dc50220329646cf786cfef79d60de3ef54f702ab1073694022f0618731902d926918c3e012103e6feac9d7a8ad1ac6b36fb4c91c1c9f7fff1e7f63f0340e5253a0e4478b7b13f41fd1a00'  
}

The full code is available as [sendtx.js](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_3_sendtx.js).

## Summary: Accessing Bitcoind with Node

With BCRPC you can access all the RPC commands available through bitcoin-cli, in JavaScript. The [BCRPC README](https://github.com/dgarage/bcrpc) has some examples which use promises (the examples in this document use callbacks). The [JavaScript behind it](https://github.com/dgarage/bcrpc/blob/master/index.js) is short and readable.

Based on these examples you should be able to incorporate Bitcoin in a Node.js project and do things like sending and receiving coins.

## What's Next?

Learn more about "Talking to Bitcoin in Other Languages" in [18.4: Accessing Bitcoin with Python](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_4_Accessing_Bitcoind_with_Python.md).

# 18.4: Accessing Bitcoind with Python

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the Python programming language and the [Python-BitcoinRPC](https://github.com/jgarzik/python-bitcoinrpc).

## Set Up Python

If you already have Bitcoin Core installed, you should have Python 3 available as well. You can check this by running:

$ python3 --version

If it returns a version number (e.g., 3.7.3 or 3.8.3) then you have python3 installed.

However, if you somehow do not have Python installed, you'll need build it from source as follows. Please see the ["Building Python from Source"](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/17_4_Accessing_Bitcoind_with_Python.md#variant-build-python-from-source) variant before continuing.

### Set Up BitcoinRPC

Whether you used an existing Python or built it from source, you're now ready to install the python-bitcoinrpc library:

$ pip3 install python-bitcoinrpc

If you don't have pip installed, you'll need to run the following:

$ sudo apt install python3-pip

(Then repeat the pip3 install python-bitcoinrpc instructions.)

### Create a BitcoinRPC Project

You'll generally need to include appropriate declarations from bitcoinrpc in your Bitcoin projects in Python. The following will give you access to the RPC based commands:

from bitcoinrpc.authproxy import AuthServiceProxy, JSONRPCException

You may also find the following useful:

from pprint import pprint  
import logging

pprint will pretty print the json response from bitcoind.

logging will print out the call you make to bitcoind and bitcoind's response, which is useful when you make a bunch of calls together. If you don't want the excessive output in the terminal just comment out the logging block.

## Build Your Connection

You are now ready to start interacting with bitcoind by establishing a connection. Create a file called btcrpc.py and type the following:

logging.basicConfig()  
logging.getLogger("BitcoinRPC").setLevel(logging.DEBUG)

# rpc_user and rpc_password are set in the bitcoin.conf file

rpc_user = "StandUp"  
rpc_pass = "6305f1b2dbb3bc5a16cd0f4aac7e1eba"  
rpc_host = "127.0.0.1"  
rpc_client = AuthServiceProxy(f"http://{rpc_user}:{rpc_pass}@{rpc_host}:18332", timeout=120)

The arguments in the URL are <rpc_username>:<rpc_password>@<host_IP_address>:. As usual, the user and pass are found in your ~/.bitcoin/bitcoin.conf, while the host is your localhost, and the port is 18332 for testnet. The timeout argument is specified since sockets timeout under heavy load on the mainnet. If you get socket.timeout: timed out response, be patient and increase the timeout.

> :link: **MAINNET VS TESTNET:** The port would be 8332 for a mainnet setup.

### Make an RPC Call

If rpc_client is successfully initialized, you'll be able to send off RPC commands to your bitcoin node.

In order to use an RPC method from python-bitcoinrpc, you'll use rpc_client object that you created, which provides most of the functionality that can be accessed through bitcoin-cli, using the same method names.

For example, the following will retrieve the blockcount of your node:

block_count = rpc_client.getblockcount()  
print("---------------------------------------------------------------")  
print("Block Count:", block_count)  
print("---------------------------------------------------------------\n")

You should see the following output with logging enabled :

## DEBUG:BitcoinRPC:-3-> getblockcount []  
DEBUG:BitcoinRPC:<-3- 1773020

## Block Count: 1773020

### Make an RPC Call with Arguments

You can use that blockcount as an argument to retrieve the blockhash of a block and also to retrieve details of that block.

This is done by send your rpc_client object commands with an argument:

blockhash = rpc_client.getblockhash(block_count)  
block = rpc_client.getblock(blockhash)

The getblockhash will return a single value, while the getblock will return an associative array of information about the block, which includes an array under block['tx'] providing details on each transaction within the block:

nTx = block['nTx']  
if nTx > 10:  
it_txs = 10  
list_tx_heading = "First 10 transactions: "  
else:  
it_txs = nTx  
list_tx_heading = f"All the {it_txs} transactions: "  
print("---------------------------------------------------------------")  
print("BLOCK: ", block_count)  
print("-------------")  
print("Block Hash...: ", blockhash)  
print("Merkle Root..: ", block['merkleroot'])  
print("Block Size...: ", block['size'])  
print("Block Weight.: ", block['weight'])  
print("Nonce........: ", block['nonce'])  
print("Difficulty...: ", block['difficulty'])  
print("Number of Tx.: ", nTx)  
print(list_tx_heading)  
print("---------------------")  
i = 0  
while i < it_txs:  
print(i, ":", block['tx'][i])  
i += 1  
print("---------------------------------------------------------------\n")

### Run Your Code

You can retrieve [the src code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_4_getinfo.py) and run it with python3:

## $ python3 getinfo.py

## Block Count: 1831106

---

## BLOCK: 1831106

## Block Hash...: 00000000000003b2ea7c2cdfffd86156ad1f5606ab58e128940a2534d1348b04  
Merkle Root..: 056a547fe59208167eef86fa694263728fb684119254b340c1f86bdd423a8082  
Block Size...: 52079  
Block Weight.: 128594  
Nonce........: 1775583700  
Difficulty...: 4194304  
Number of Tx.: 155  
First 10 transactions:

## 0 : d228d55112e3aa26265b0118cfdc98345c229d20fe074b9afb87107c03ce11b5  
1 : 92822e8e34fafb472b87c99ea3f3e16440452b3f361ed86c6fa62175173fb750  
2 : fa7c67600c14d4aa350a9674688f1429577954f4a6c5e4639d06c8964824f647  
3 : 3a91d1527e308e5603dafde7ab17824f441a73a779d2571d073466dc9e8451b2  
4 : 30fd0e5527b1522e7b26a4818b9edac80fe47c0c39fc34705478a49e684708d0  
5 : 24c5372b38c78cbaf5b0b305925502a491bc0c1b5758f50c0bd335abb6ae85f5  
6 : be70e125a5793efc5e32051fecba0668df971bdf371138c8261201c2a46b2d38  
7 : 41ebf52c847a59ba0aeb4425c74e89a01e91defa86a82785ff53ed4668054561  
8 : dc8211b4ce122f87692e7c203672e3eb1ffc44c0a307eafcc560323fcc5fae78  
9 : 59e2d8e11cad287eacf3207e64a373f65059286b803ef0981510193ae29cbc8c

## Look Up Funds

You can similarly retrieve your wallet's information with the getwalletinfo RPC:

wallet_info = rpc_client.getwalletinfo()  
print("---------------------------------------------------------------")  
print("Wallet Info:")  
print("-----------")  
pprint(wallet_info)  
print("---------------------------------------------------------------\n")

You should have an output similar to the following with logging disabled:

---

## Wallet Info:

## {'avoid_reuse': False,  
'balance': Decimal('0.07160443'),  
'hdseedid': '6dko666b1cc0d69b7eb0539l89eba7b6390kdj02',  
'immature_balance': Decimal('0E-8'),  
'keypoololdest': 1542245729,  
'keypoolsize': 999,  
'keypoolsize_hd_internal': 1000,  
'paytxfee': Decimal('0E-8'),  
'private_keys_enabled': True,  
'scanning': False,  
'txcount': 9,  
'unconfirmed_balance': Decimal('0E-8'),  
'walletname': '',  
'walletversion': 169900}

Other informational commands such as getblockchaininfo, getnetworkinfo, getpeerinfo, and getblockchaininfo will work similarly.

Other commands can give you specific information on select elements within your wallet.

### Retrieve an Array

The listtransactions RPC allows you to look at the most recent 10 transactions on your system (or some arbitrary set of transactions using the count and skip arguments). It shows how an RPC command can return an easy-to-manipulate array:

tx_list = rpc_client.listtransactions()  
pprint(tx_list)

### Explore a UTXO

You can similarly use listunspent to get an array of UTXOs on your system:

print("Exploring UTXOs")

## List UTXOs

utxos = rpc_client.listunspent()  
print("Utxos: ")  
print("-----")  
pprint(utxos)  
print("------------------------------------------\n")

In order to manipulate an array like the one returned from listtransactions or listunspent, you just grab the appropriate item from the appropriate element of the array:

## Select a UTXO - first one selected here

utxo_txid = utxos[0]['txid']

For listunspent, you get a txid. You can retrieve information about it with gettransaction, then decode that with decoderawtransaction:

utxo_hex = rpc_client.gettransaction(utxo_txid)['hex']

utxo_tx_details = rpc_client.decoderawtransaction(utxo_hex)

print("Details of Utxo with txid:", utxo_txid)  
print("---------------------------------------------------------------")  
print("UTXO Details:")  
print("------------")  
pprint(utxo_tx_details)  
print("---------------------------------------------------------------\n")

This code is available at [walletinfo.py](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_4_walletinfo.py).

## $ python3 walletinfo.py

## Wallet Info:

## {'avoid_reuse': False,  
'balance': Decimal('0.01031734'),  
'hdseedid': 'da5a1b058deb9e51ecffef1b0ddc069a5dfb2c5f',  
'immature_balance': Decimal('0E-8'),  
'keypoololdest': 1596567843,  
'keypoolsize': 1000,  
'keypoolsize_hd_internal': 999,  
'paytxfee': Decimal('0E-8'),  
'private_keys_enabled': True,  
'scanning': False,  
'txcount': 6,  
'unconfirmed_balance': Decimal('0E-8'),  
'walletname': '',  
'walletversion': 169900}

## Utxos:

## [{'address': 'mv9cjEnS2o1EygBMdrz99LzhM8KeEMoXDg',  
'amount': Decimal('0.00001000'),  
'confirmations': 1180,  
'desc': "pkh([ce0c7e14/0'/0'/25']02d0541b9211aecd25913f7fdecfc1b469215fa326d52067b1b3f7efbd12316472)#n06pq9q5",  
'label': '-addresstype',  
'safe': True,  
'scriptPubKey': '76a914a080d1a10f5e7a02d0a291f118982ed19e8cfcd788ac',  
'solvable': True,  
'spendable': True,  
'txid': '84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e',  
'vout': 0},  
{'address': 'tb1qrcf8c29966tvqxhwrtd2se3rj6jeqtll3r46a4',  
'amount': Decimal('0.01029734'),  
'confirmations': 1180,  
'desc': "wpkh([ce0c7e14/0'/1'/26']02c581259ba7e6aef6d7ea23adb08f7c7f10c4c678f2e097a4074639e7685d4805)#j3pctfhf",  
'safe': True,  
'scriptPubKey': '00141e127c28a5d696c01aee1adaa8662396a5902fff',  
'solvable': True,  
'spendable': True,  
'txid': '84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e',  
'vout': 1},  
{'address': 'mzDxbtYY3LBBBJ6HhaBAtnHv6c51BRBTLE',  
'amount': Decimal('0.00001000'),  
'confirmations': 1181,  
'desc': "pkh([ce0c7e14/0'/0'/23']0377bdd176f985b4af2f6bdbb22c2925b6007b6c07ba171f75e65990c002615e98)#3y6ef6vu",  
'label': '-addresstype',  
'safe': True,  
'scriptPubKey': '76a914cd339342b06042bb986a45e73d56db46acc1e01488ac',  
'solvable': True,  
'spendable': True,  
'txid': '1679bee019c61608340b79810377be2798efd4d2ec3ace0f00a1967af70666b9',  
'vout': 1}]

## Details of Utxo with txid: 84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e

## UTXO Details:

## {'hash': '0c6c27f58f122329bbc53a91f290b35ce23bd2708706b21a04cdc387dc8e2fd9',  
'locktime': 1831103,  
'size': 225,  
'txid': '84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e',  
'version': 2,  
'vin': [{'scriptSig': {'asm': '', 'hex': ''},  
'sequence': 4294967294,  
'txid': '1679bee019c61608340b79810377be2798efd4d2ec3ace0f00a1967af70666b9',  
'txinwitness': ['3044022014b3e2359fb46d8cbc4cd30fa991b455edfa4b419a4c64a53fcdfc79e3ca89db022010cefc3268bc252d55f1982c426328b709b47d02332def9e2efb3b12de2cf0d301',  
'0351b470e87b44e8e9607acf09b8d4543c51c93c17dc741176319e60202091f2be'],  
'vout': 0}],  
'vout': [{'n': 0,  
'scriptPubKey': {'addresses': ['mv9cjEnS2o1EygBMdrz99LzhM8KeEMoXDg'],  
'asm': 'OP_DUP OP_HASH160 '  
'a080d1a10f5e7a02d0a291f118982ed19e8cfcd7 '  
'OP_EQUALVERIFY OP_CHECKSIG',  
'hex': '76a914a080d1a10f5e7a02d0a291f118982ed19e8cfcd788ac',  
'reqSigs': 1,  
'type': 'pubkeyhash'},  
'value': Decimal('0.00001000')},  
{'n': 1,  
'scriptPubKey': {'addresses': ['tb1qrcf8c29966tvqxhwrtd2se3rj6jeqtll3r46a4'],  
'asm': '0 1e127c28a5d696c01aee1adaa8662396a5902fff',  
'hex': '00141e127c28a5d696c01aee1adaa8662396a5902fff',  
'reqSigs': 1,  
'type': 'witness_v0_keyhash'},  
'value': Decimal('0.01029734')}],  
'vsize': 144,  
'weight': 573}

## Create an Address

Creating a new address with Python 3 just requires the use of an RPC like getnewaddress or getrawchangeaddress.

new_address = rpc_client.getnewaddress("Learning-Bitcoin-from-the-Command-Line")  
new_change_address = rpc_client.getrawchangeaddress()

In this example, you give the getnewaddress command an argument: the Learning-Bitcoin-from-the-Command-Line label.

## Send a Transaction

Creating a transaction in Python 3 requires combining some of the previous examples (of creating addresses and retrieving UTXOs) with some new RPC commands for creating, signing, and sending a transaction — much as you've done previously from the command line.

There are five steps:

1. Create two addresses, one that will act as recipient and the other for change.
    
2. Select a UTXO and set transaction details.
    
3. Create a raw transaction.
    
4. Sign the raw transaction with the private key of the UTXO.
    
5. Broadcast the transaction on the bitcoin testnet.
    

### \1. Select UTXO & Set Transaction Details

In the following code snippet you first select the UTXO which we want to spend. Then you get its address, transaction id, and the vector index of the output.

utxos = rpc_client.listunspent()  
selected_utxo = utxos[0] # again, selecting the first utxo here  
utxo_address = selected_utxo['address']  
utxo_txid = selected_utxo['txid']  
utxo_vout = selected_utxo['vout']  
utxo_amt = float(selected_utxo['amount'])

Next, you also retrieve the recipient address to which you want to send the bitcoins, calculate the amount of bitcoins you want to send, and calculate the miner fee and the change amount. Here, the amount is arbitrarily split in two and a miner fee is arbitrarily set.

recipient_address = new_address  
recipient_amt = utxo_amt / 2 # sending half coins to recipient  
miner_fee = 0.00000300 # choose appropriate fee based on your tx size  
change_address = new_change_address  
change_amt = float('%.8f'%((utxo_amt - recipient_amt) - miner_fee))

> :warning: **WARNING:** Obviously a real program would make more sophisticated choices about what UTXO to use, what to do with the funds, and what miner's fee to pay.

### \2. Create Raw Transaction

Now you have all the information to send a transaction, but before you can send one, you have to create a transaction.

txids_vouts = [{"txid": utxo_txid, "vout": utxo_vout}]  
addresses_amts = {f"{recipient_address}": recipient_amt, f"{change_address}": change_amt}  
unsigned_tx_hex = rpc_client.createrawtransaction(txids_vouts, addresses_amts)

Remember that the format of the createrawtransaction command is:

$ bitcoin-cli createrawtransaction '[{"txid": <utxo_txid>, "vout": <vector_id>}]' '{"": }'

The txids_vouts is thus a list and the addresses_amts is a python dictionary, to match with the format of createrawtransaction.

If you want to see more about the details of the transaction that you've created, you can use decoderawtransaction, either in Python 3 or with bitcoin-cli.

### \3. Sign Raw Transaction

Signing a transaction is often the trickiest part of sending a transaction programmatically. Here you retrieve a private key from an address with dumpprivkey and place it in an array:

address_priv_key = [] # list of priv keys of each utxo  
address_priv_key.append(rpc_client.dumpprivkey(utxo_address))

You can then use that array (which should contain the private keys of every UTXO that is being spent) to sign your unsigned_tx_hex:

signed_tx = rpc_client.signrawtransactionwithkey(unsigned_tx_hex, address_priv_key)

This returns a JSON object with the signed transaction's hex, and whether it was signed completely or not:

### \4. Broadcast Transaction

Finally, you are ready to broadcast the signed transaction on the bitcoin network:

send_tx = rpc_client.sendrawtransaction(signed_tx['hex'])

### Run Your Code

The [sample code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_4_sendtx.py) is full of print statements to demonstrate all of the data available at every point:

## $ python3 sendtx.py  
Creating a Transaction

## Transaction Details:

## UTXO Address.......: mv9cjEnS2o1EygBMdrz99LzhM8KeEMoXDg  
UTXO Txid..........: 84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e  
Vector ID of Output: 0  
UTXO Amount........: 1e-05  
Tx Amount..........: 5e-06  
Recipient Address..: tb1qca0elxxqzw5xc0s3yq5qhapzzj90ka0zartu6y  
Change Address.....: tb1qrveukqrvqm9h6fua99xvcxgnvdx507dg8e8hrt  
Miner Fee..........: 3e-06  
Change Amount......: 2e-06

---

## Unsigned Transaction Hex: 02000000015e53fb6f63b7defa28e61c28cfc3033361138a0d33dd1fad29ae58c6fe7f20840000000000ffffffff02f401000000000000160014c75f9f98c013a86c3e1120280bf422148afb75e2c8000000000000001600141b33cb006c06cb7d279d294ccc1913634d47f9a800000000

---

## Signed Transaction:

## {'complete': True,  
'hex': '02000000015e53fb6f63b7defa28e61c28cfc3033361138a0d33dd1fad29ae58c6fe7f2084000000006a47304402205da9b2234ea057c9ef3b7794958db6c650c72dedff1a90d2915147a5f6413f2802203756552aba0dd8ebd71b0f28341becc01b28d8b28af063d7c8ce89f9c69167f8012102d0541b9211aecd25913f7fdecfc1b469215fa326d52067b1b3f7efbd12316472ffffffff02f401000000000000160014c75f9f98c013a86c3e1120280bf422148afb75e2c8000000000000001600141b33cb006c06cb7d279d294ccc1913634d47f9a800000000'}

---

TXID of sent transaction: 187f8baa222f9f37841d966b6bad59b8131cfacca861cbe9bfc8656bd16a44cc

## Summary: Accessing Bitcoind with Python

Accessing Bitcoind with Python is very easy while using the python-bitcoinrpc library. The first thing to always do is to establish a connection with your bitcoind instance, then you can call all of the bitcoin API calls as described in the bitcoin-core documentation. This makes it easy to create small or large programs to manage your own node, check balances, or create cool applications on top, as you access the full power of bitcoin-cli.

## What's Next?

Learn more about "Talking to Bitcoin in Other Languages" in [18.5: Accessing Bitcoin with Rust](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_5_Accessing_Bitcoind_with_Rust.md).

## Variant: Build Python from Source

If you need to install Python 3 from source, follow these instructions, then continue with ["Create a BitcoinRPC Project"](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_4_Accessing_Bitcoind_with_Python.md#create-a-bitcoinrpc-project).

### \1. Install Dependencies

$ sudo apt-get install build-essential checkinstall  
$ sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev

### \2. Download & Extract Python

$ wget [https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz](https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz)  
$ tar -xzf Python-3.8.3.tgz

### \3. Compile Python Source & Check Installation:

$ cd Python-3.8.3  
$ sudo ./configure --enable-optimizations  
$ sudo make -j 8 # enter the number of cores of your system you want to use to speed up the build process.  
$ sudo make altinstall  
$ python3.8 --version

After you get the version output, remove the source file:

$ rm Python-3.8.3.tgz

# 18.5: Accessing Bitcoind with Rust

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the Rust programming language and the [bitcoincore-rpc](https://github.com/rust-bitcoin/rust-bitcoincore-rpc) [crate](https://github.com/rust-bitcoin/rust-bitcoincore-rpc).

## Set Up Rust

You need to install both Rust and Cargo.

They can be installed via curl. Just use the "default" installation:

$ curl [https://sh.rustup.rs](https://sh.rustup.rs/) -sSf | sh

If everything goes well, you should see:

Rust is installed now. Great!

You'll then need to either logout and back in, or else add Cargo's binary directory to your path by hand:

$ source $HOME/.cargo/env

### Set Up bitcoincore-rpc

For most programming languages, you need to install a Bitcoin RPC library before you create your first project, but here you'll do it as part of your project creation.

### Create a bitcoincore-rpc Project

You can create a new project using cargo new btc_test:

$ cargo new btc_test  
Created binary (application) btc_test package

This will create a btc_test directory that contains a "hello world" source-code example in src/main.rs and a Cargo.toml file.

You'll compile and run your code with cargo run:

$ cd btc_test  
$ cargo run  
Compiling btc_test v0.1.0 (/home/standup/btc_test)  
Finished dev [unoptimized + debuginfo] target(s) in 0.14s  
Running target/debug/btc_test  
Hello, world!

> :information_source: **NOTE:** if you run into error linker ‘cc’ not found, you'll have to install a C compiler. If on Linux, go ahead and install the [development tools](https://www.ostechnix.com/install-development-tools-linux/).

In order to access the bitcoincore-rpc crate (library), you must add it to your Cargo.toml file under the section dependencies:

[dependencies]  
bitcoincore-rpc = "0.11.0"

When you cargo run again, it will install the crate and its (numerous) dependencies.

$ cargo run  
Updating crates.io index  
...  
Compiling bitcoin v0.23.0  
Compiling bitcoincore-rpc-json v0.11.0  
Compiling bitcoincore-rpc v0.11.0  
Compiling btc_test v0.1.0 (/home/standup/btc_test)  
Finished dev [unoptimized + debuginfo] target(s) in 23.56s  
Running target/debug/btc_test  
Hello, world!

When you are using bitcoin-rpc, you will typically need to include the following:

use bitcoincore_rpc::{Auth, Client, RpcApi};

## Build Your Connection

To create a Bitcoin RPC client, modify the src/main.rs:

use bitcoincore_rpc::{Auth, Client, RpcApi};

fn main() {  
let rpc = Client::new(  
"http://localhost:18332".to_string(),  
Auth::UserPass("StandUp".to_string(), "password".to_string()),  
)  
.unwrap();  
}

As usual, make sure to insert your proper user name and password from ~/.bitcoin/bitcoin.conf. Here, they're used as the arguments for Auth::UserPass.

> :link: **TESTNET vs MAINNET:** And, as usual, use port 8332 for mainnet.

When you're done, you should also close your connection:

let _ = rpc.stop().unwrap();

cargo run should successfully compile and run the example with one warning warning: unused variable: rpc

### Make an RPC Call

RPC calls are made using the rpc Client that you created:

let mining_info = rpc.get_mining_info().unwrap();  
println!("{:#?}", mining_info);

Generally, the words in the RPC call are separated by _s. A complete list is available at the [crate docs](https://crates.io/crates/bitcoincore-rpc).

### Make an RPC Call with Arguments

Sending an RPC call with arguments using Rust just requires knowing how the function is laid out. For example, the get_block function is defined as follows in the [docs](https://docs.rs/bitcoincore-rpc/0.11.0/bitcoincore_rpc/trait.RpcApi.html#method.get_block):

fn get_block(&self, hash: &BlockHash) -> Result

You just need to allow it to borrow a blockhash, which can be retrieved (for example) by get_best_block_hash.

Here's the complete code to retrieve a block hash, turn that into a block, and print it.

let hash = rpc.get_best_block_hash().unwrap();    
let block = rpc.get_block(&hash).unwrap();    
    
println!("{:?}", block);

> **NOTE:** Another possible call that we considered for this section was get_address_info, but unfortunately as of this writing, the bitcoincore-rpc function doesn't work with recent versions of Bitcoin Core due to the crate not addressing the latest API changes in Bitcoin Core. We expect this will be solved in the next crate's release, but in the meantime, _caveat programmer_.

### Run Your Code

You can access the [src code](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_5_main-getinfo.rs) and run it. Unfortunately, the "Block" info will come out a bit ugly because this example doesn't include a library to prettify it.

$ cargo run  
Compiling btc_test v0.1.0 (/home/standup/btc_test)  
Finished dev [unoptimized + debuginfo] target(s) in 1.61s  
Running target/debug/btc_test  
GetMiningInfoResult {  
blocks: 1832335,  
current_block_weight: None,  
current_block_tx: None,  
difficulty: 4194304.0,  
network_hash_ps: 77436285865245.1,  
pooled_tx: 4,  
chain: "test",  
warnings: "Warning: unknown new rules activated (versionbit 28)",  
}  
Block { header: BlockHeader { version: 541065216, prev_blockhash: 000000000000027715981d5a3047daf6819ea3b8390b73832587594a2074cbf5, merkle_root: 4b2e2c2754b6ed9cf5c857a66ed4c8642b6f6b33b42a4859423e4c3dca462d0c, time: 1599602277, bits: 436469756, nonce: 218614401 }, txdata: [Transaction { version: 1, lock_time: 0, input: [TxIn { previous_output: OutPoint { txid: 0000000000000000000000000000000000000000000000000000000000000000, vout: 4294967295 }, script_sig: Script(OP_PUSHBYTES_3 8ff51b OP_PUSHBYTES_22 315448617368263538434f494e1d00010320a48db852 OP_PUSHBYTES_32 ), sequence: 4294967295, witness: [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0](https://en.wikipedia.org/wiki/0,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200,%200) }], output: [TxOut { value: 19721777, script_pubkey: Script(OP_HASH160 OP_PUSHBYTES_20 011beb6fb8499e075a57027fb0a58384f2d3f784 OP_EQUAL) }, TxOut { value: 0, script_pubkey: Script(OP_RETURN OP_PUSHBYTES_36 aa21a9ed63363f3620ab5e38b8860a50c84050e5ec31af3636bbd73f01ba9f14103100ee) }] }, Transaction { version: 2, lock_time: 1832282, input: [TxIn { previous_output: OutPoint { txid: cbf880f73d421baf0aa4f0d28e63ba00e5bc6bd934b91eb0641354ce5ca42f7e, vout: 0 }, script_sig: Script(OP_PUSHBYTES_22 00146b8dbd32e5deb90d22934e1513bae6e70156cd50), sequence: 4294967294, witness: [[48, 68, 2, 32, 13, 89, 205, 30, 67, 24, 196, 83, 65, 224, 44, 138, 98, 58, 81, 135, 132, 209, 23, 166, 23, 44, 3, 228, 95, 102, 166, 214, 62, 38, 155, 147, 2, 32, 119, 2, 34, 246, 148, 255, 166, 10, 90, 52, 242, 32, 74, 241, 123, 148, 89, 199, 197, 3, 152, 134, 242, 215, 109, 61, 241, 241, 13, 70, 86, 207, 1], [2, 192, 145, 170, 206, 55, 4, 36, 138, 145, 217, 50, 19, 73, 130, 136, 245, 131, 184, 142, 239, 75, 13, 67, 17, 177, 57, 86, 151, 139, 89, 35, 109]] }], output: [TxOut { value: 1667908, script_pubkey: Script(OP_HASH160 OP_PUSHBYTES_20 908ca2b8b49ccf53efa2226afa85f6cc58dfd7e7 OP_EQUAL) }, TxOut { value: 9093, script_pubkey: Script(OP_DUP OP_HASH160 OP_PUSHBYTES_20 42ee67664ce16edefc68ad0e4c5b7ce2fc2ccc18 OP_EQUALVERIFY OP_CHECKSIG) }] }, ...] }

## Look Up Funds

You can look up funds without optional arguments using the get_balance function:

let balance = rpc.get_balance(None, None).unwrap();  
println!("Balance: {:?} BTC", balance.as_btc());

As shown, the as_btc() function helps to output the balance in a readable form:

Balance: 3433.71692741 BTC

## Create an Address

Creating an address demonstrates how to make an RPC call with multiple optional arguments specified (e.g., a label and an address type).

// Generate a new address  
let myaddress = rpc  
.get_new_address(Option::Some("BlockchainCommons"), Option::Some(json::AddressType::Bech32))  
.unwrap();  
println!("address: {:?}", myaddress);

This will also require you to bring the json definition into scope:

use bitcoincore_rpc::{json, Auth, Client, RpcApi};

## Send a Transaction

You now have everything you need to create a transaction, which will be done in five parts:

1. List UTXOs
    
2. Populate Variables
    
3. Create Raw Transaction
    
4. Sign Transaction
    
5. Send Transaction
    

### \1. List UTXOs

To start the creation of a transaction, you first find a UTXO to use. The following takes the first UTXO with at least 0.01 BTC

let unspent = rpc  
.list_unspent(  
None,  
None,  
None,  
None,  
Option::Some(json::ListUnspentQueryOptions {  
minimum_amount: Option::Some(Amount::from_btc(0.01).unwrap()),  
maximum_amount: None,  
maximum_count: None,  
minimum_sum_amount: None,  
}),  
)  
.unwrap();

let selected_tx = &unspent[0];

println!("selected unspent transaction: {:#?}", selected_tx);

This will require bringing more structures into scope:

use bitcoincore_rpc::bitcoin::{Address, Amount};

Note that you're passing list_unspent five variables. The first four (minconf, maxconf, addresses, and include_unsafe) aren't used here. The fifth is query_options, which we haven't used before, but has some powerful filtering options, including the ability to only look at UTXOs with a certain minimum (or maximum) value.

### \2. Populate Variables

To begin populating the variables that you'll need to create a new transaction, you create the input from the txid and the vout of the UTXO that you selected:

let selected_utxos = json::CreateRawTransactionInput {  
txid: selected_tx.txid,  
vout: selected_tx.vout,  
sequence: None,  
};

Next, you can calculate the amount you're going to spend by subtracting a mining fee from the funds in the UTXO:

// send all bitcoin in the UTXO except a minor value which will be paid to miners  
let unspent_amount = selected_tx.amount;  
let amount = unspent_amount - Amount::from_btc(0.00001).unwrap();

Finally, you can create a hash map of the address and the amount to form the output:

let mut output = HashMap::new();  
output.insert(  
myaddress.to_string(),  
amount,  
);

Another trait is necessary for the output variable: HashMap. It allows you to store values by key, which you need to represent {address : amount} information.

use std::collections::HashMap;

### \3. Create Raw Transaction

You are ready to create a raw transaction:

let unsigned_tx = rpc  
.create_raw_transaction(&[selected_utxos], &output, None, None)  
.unwrap();

### \4. Sign Transaction

Signing your transaction can be done with a simple use of sign_raw_transaction_with_wallet:

let signed_tx = rpc  
.sign_raw_transaction_with_wallet(&unsigned_tx, None, None)  
.unwrap();

println!("signed tx {:?}", signed_tx.transaction().unwrap());

### \5. Send Transaction

Finally, you can broadcast the transaction:

let txid_sent = rpc  
.send_raw_transaction(&signed_tx.transaction().unwrap())  
.unwrap();

println!("{:?}", txid_sent);

### Run Your Code

You can now run the complete code from the [src](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_5_main-sendtx.rs).

$ cargo run  
Compiling btc_test v0.1.0 (/home/standup/btc_test)  
warning: unused variable: unspent_amount  
--> src/main.rs:86:9  
|  
86 | let unspent_amount = selected_tx.amount;  
| ^^^^^^^^^^^^^^ help: if this is intentional, prefix it with an underscore: _unspent_amount  
|  
= note: #[warn(unused_variables)] on by default

warning: 1 warning emitted

Finished dev [unoptimized + debuginfo] target(s) in 2.11s    
 Running `target/debug/btc_test`  

Balance: 0.01031434 BTC  
address: tb1qx5jz36xgt9q2rkh4daee8ewfj0g5z05v8qsua2  
selected unspent transaction: ListUnspentResultEntry {  
txid: 84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e,  
vout: 1,  
address: Some(  
tb1qrcf8c29966tvqxhwrtd2se3rj6jeqtll3r46a4,  
),  
label: None,  
redeem_script: None,  
witness_script: None,  
script_pub_key: Script(OP_0 OP_PUSHBYTES_20 1e127c28a5d696c01aee1adaa8662396a5902fff),  
amount: Amount(1029734 satoshi),  
confirmations: 1246,  
spendable: true,  
solvable: true,  
descriptor: Some(  
"wpkh([ce0c7e14/0'/1'/26']02c581259ba7e6aef6d7ea23adb08f7c7f10c4c678f2e097a4074639e7685d4805)#j3pctfhf",  
),  
safe: true,  
}  
unsigned tx Transaction {  
version: 2,  
lock_time: 0,  
input: [  
TxIn {  
previous_output: OutPoint {  
txid: 84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e,  
vout: 1,  
},  
script_sig: Script(),  
sequence: 4294967295,  
witness: [],  
},  
],  
output: [  
TxOut {  
value: 1028734,  
script_pubkey: Script(OP_0 OP_PUSHBYTES_20 352428e8c85940a1daf56f7393e5c993d1413e8c),  
},  
],  
}  
signed tx Transaction { version: 2, lock_time: 0, input: [TxIn { previous_output: OutPoint { txid: 84207ffec658ae29ad1fdd330d8a13613303c3cf281ce628fadeb7636ffb535e, vout: 1 }, script_sig: Script(), sequence: 4294967295, witness: [[48, 68, 2, 32, 98, 230, 199, 113, 156, 242, 158, 42, 148, 229, 239, 44, 9, 226, 127, 219, 72, 51, 26, 135, 44, 212, 179, 200, 213, 63, 56, 167, 0, 55, 236, 235, 2, 32, 41, 43, 30, 109, 60, 162, 124, 67, 20, 126, 4, 107, 124, 95, 9, 200, 132, 246, 147, 235, 176, 55, 59, 45, 190, 18, 211, 201, 143, 62, 163, 36, 1], [2, 197, 129, 37, 155, 167, 230, 174, 246, 215, 234, 35, 173, 176, 143, 124, 127, 16, 196, 198, 120, 242, 224, 151, 164, 7, 70, 57, 231, 104, 93, 72, 5]] }], output: [TxOut { value: 1028734, script_pubkey: Script(OP_0 OP_PUSHBYTES_20 352428e8c85940a1daf56f7393e5c993d1413e8c) }] }  
b0eda3517e6fac69e58ae315d7fe7a1981e3a858996cc1e3135618cac9b79d1a

## Summary: Accessing Bitcoind with Rust

bitcoincore-rpc is a simple and robust crate that will allow you to interact with Bitcoin RPC using Rust. However, as of this writing it has fallen behind Bitcoin Core, which might cause some issues with usage.

## What's Next?

Learn more about "Talking to Bitcoin in Other Languages" in [18.6: Accessing Bitcoin with Swift](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_6_Accessing_Bitcoind_with_Swift.md).

# 18.6: Accessing Bitcoind with Swift

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section explains how to interact with bitcoind using the Swift programming language and your own RPC client.

## Set Up Swift on Your Mac

To date, you've built all of your alternative-programming-language development environments on your Debian virtual node. However, that's not the best platform for Swift. Though there is a version of Swift available for Ubuntu platforms, it's not fully featured, and it works somewhat differently from the Mac-native Swift. A "variant" at the bottom of this section explains how to set it up, but be warned that you'll be in uncharted territory.

Instead, we suggest creating an optimal Swift environment on a Mac. There are four major steps in doing so.

### \1. Install Xcode

You're going to need Xcode, the integrated development enviroment for Swift and Objective-C. That can be easily installed by going to the Mac App Store and Getting Xcode.

#### Alternative: Install by Hand

Some people advise against an App Store install because it's somewhat all-or-nothing; it also won't work if you're still using Mojave because you want to avoid Catalina's incompatibilities. In that case you can download directly from the [Developer Area](https://developer.apple.com/download/more/) at Apple.

If you're using Mojave, you'll need the xip file for Xcode 10.3.1. Otherwise, get the newest one.

Once it's downloaded, you can click on the xip to extract it, then move the Xcode app to your Applications folder.

(Either way, you should have Xcode installed in your Applications folder at the end of this step.)

### \2. Install the Gordian Server

You're also going to need a Bitcoin node on your Mac, so that you can communicate with it. Technically, you could use a remote node and access it with the RPC login and password over the net. However, we suggest you instead install a full node directly on your Mac, because that's the safest and cleanest setup, ensuring that none of your communications leave your machine.

To easily install a full node on your Mac, use Blockchain Commons' [GordianServer for MacOS](https://github.com/BlockchainCommons/GordianServer-macOS). See the [installation instructions](https://github.com/BlockchainCommons/GordianServer-macOS#installation-instructions) in the README, but generally all you have to do is download the current dmg file, open it, and install that app in your Applications directory too.

Afterward, run the GordianServer App, and tell it to Start Testnet.

> :link: **TESTNET vs. MAINNET:** Or Start Mainnet.

#### \3. Make Your Gordian bitcoin-cli Accessible

When you want to access the bitcoin-cli created by GordianServer on your local Mac, you can find it at ~/.standup/BitcoinCore/bitcoin-VERSION/bin/bitcoin-cli, for example ~/.standup/BitcoinCore/bitcoin-0.20.1/bin/bitcoin-cli.

You may wish to create an alias for that:

alias bitcoin-cli="~/.standup/BitcoinCore/bitcoin-0.20.1/bin/bitcoin-cli -testnet"

> :link: **TESTNET vs. MAINNET:** Obviously, the -testnet parameter is only required if you're running on testnet.

### \4. Find Your GordianServer Info

Finally, you'll need your rpcuser and rpcpassword information. That's in ~/Library/Application Support/Bitcoin/bitcoin.conf by default under Gordian.

$ grep rpc ~/Library/Application\ Support/Bitcoin/bitcoin.conf  
rpcuser=oIjA53JC2u  
rpcpassword=ebVCeSyyM0LurvgQyi0exWTqm4oU0rZU  
...

## Build Your Connection by Hand

At the time of this writing, there isn't an up-to-date, simple-to-use Bitcoin RPC Library that's specific for Swift, something that you can drop in and immediately start using. Thus, you're going to do something you're never done before: build an RPC connection by hand.

### Write the RPC Transmitter

This just requires writing a function that passes RPC commands on to bitcoind in the correct format:

func makeCommand(method: String, param: Any, completionHandler: @escaping (Any?) -> Void) -> Void {

RPC connections to bitcoind use the HTML protocol, which means that you need to do three things: create a URL; make a URLRequest; and initiate a URLSession.

#### \1. Create a URL

Within the function, you need to create a URL from your IP, port, rpcuser, rpcpassword, and wallet:

let testnetRpcPort = "18332"    
let nodeIp = "127.0.0.1:\(testnetRpcPort)"    
let rpcusername = "oIjA53JC2u"    
let rpcpassword = "ebVCeSyyM0LurvgQyi0exWTqm4oU0rZU"    
let walletName = ""

The actual RPC connection to Bitcoin Core is built using a URL of the format "http://rpcusername:rpcpassword@nodeIp/walletName":

let walletUrl = "http://\(rpcusername):\(rpcpassword)@\(nodeIp)/\(walletName)"    
  
let url = URL(string: walletUrl)

This means that your sample variables result in the following URL:

http://oIjA53JC2u:ebVCeSyyM0LurvgQyi0exWTqm4oU0rZU@127.0.0.1:18332/

Which should look a lot like the URL used in some of the previous sections for RPC connections.

#### \2. Create a URLRequest

With that URL in you hand, you can now create a URLRequest, with the POST method and the text/plain content type. The HTTP body is then the familiar JSON object that you've been sending whenever you connect directly to Bitcoin Core's RPC ports, as first demonstrated when using Curl in [§4.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/04_4__Interlude_Using_Curl.md).

var request = URLRequest(url: url!)    
request.httpMethod = "POST"    
request.setValue("text/plain", forHTTPHeaderField: "Content-Type")    
request.httpBody = "{\"jsonrpc\":\"1.0\",\"id\":\"curltest\",\"method\":\"\(method)\",\"params\":[\(param)]}".data(using: .utf8)

#### \3. Create a URLSession

Finally, you're ready to build a URLSession around your URLRequest.

let session = URLSession(configuration: .default)    
let task = session.dataTask(with: request as URLRequest) { data, response, error in

The completion handler for dataTask needs to check for errors:

    do {    
  
        if error != nil {    
  
                //Handle the error    
                    
        } else {

And then parse the data that you're receiving. Here, you're pulling the JSON results into an NSDictionary:

            if let urlContent = data {    
                        
                do {    
                            
                    let json = try JSONSerialization.jsonObject(with: urlContent, options: JSONSerialization.ReadingOptions.mutableLeaves) as! NSDictionary

After that, there's more error handling and more error handling and then you can eventually return the dictionary result using the completionHandler that you defined for the new makeCommand function:

                    if let errorCheck = json["error"] as? NSDictionary {    
                                                                
                        if let errorMessage = errorCheck["message"] as? String {    
  
                            print("FAILED")    
                            print(errorMessage)    
  
                        }    
                                
                    } else {    
                                
                        let result = json["result"]    
                        completionHandler(result)    
                            
                    }    
                            
                } catch {    
                            
                        //Handle error here    
                            
                }

Of course you eventually have to tell the task to start:

task.resume()

And that's "all" there is to doing that RPC interaction by hand using a programming language such as Swift.

> :pray: **THANKS:** Thanks to @Fonta1n3 who provided the [main code](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line/issues/137) for our RPC Transmitter.

### Make An RPC Call

Having written the makeCommand RPC function, you can send an RPC call by running it. Here's getblockchaininfo:

let method = "getblockchaininfo"  
let param = ""

makeCommand(method: method,param: param) { result in

print(result!)  

}

### Make an RPC Call with Arguments

You could similarly grab the current block count from that info and use that to (reduntantly) get the hash of the current block, by using the param parameter:

let method = "getblockchaininfo"  
let param = ""

makeCommand(method: method,param: param) { result in

let blockinfo = result as! NSDictionary    
let block = blockinfo["blocks"] as! NSNumber    
    
let method = "getblockhash"    
makeCommand(method: method,param: block) { result in    
    print("Blockhash for \(block) is \(result!)")    
}  

}

### Run Your Code

The complete code is available in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_6_getinfo.playground). Load it into your Xcode playground and then "Editor -> Run Playground" and you should get results like:

{  
bestblockhash = 00000000000000069725608ebc5b59e520572a8088cbc57ffa5ba87b7f300ac7;  
blocks = 1836745;  
chain = test;  
chainwork = 0000000000000000000000000000000000000000000001cc3e9f8e0bc6b71196;  
difficulty = "16508683.81195478";  
headers = 1836745;  
initialblockdownload = 0;  
mediantime = 1601416765;  
pruned = 0;  
"size_on_disk" = 28205538354;  
softforks = {  
bip34 = {  
active = 1;  
height = 21111;  
type = buried;  
};  
bip65 = {  
active = 1;  
height = 581885;  
type = buried;  
};  
bip66 = {  
active = 1;  
height = 330776;  
type = buried;  
};  
csv = {  
active = 1;  
height = 770112;  
type = buried;  
};  
segwit = {  
active = 1;  
height = 834624;  
type = buried;  
};  
};  
verificationprogress = "0.999999907191804";  
warnings = "Warning: unknown new rules activated (versionbit 28)";  
}  
Blockhash for 1836745 is 00000000000000069725608ebc5b59e520572a8088cbc57ffa5ba87b7f300ac7

## Look Up Funds

With your new makeCommand for RPC functions, you can similarly run a command like getwalletinfo or getbalance:

var method = "getwalletinfo"  
var param = ""

makeCommand(method: method,param: param) { result in

print(result!)  

}

method = "getbalance"  
makeCommand(method: method,param: param) { result in

let balance = result as! NSNumber    
print("Balance is \(balance)")  

}

Which returns:

Balance is 0.01  
{  
"avoid_reuse" = 0;  
balance = "0.01";  
hdseedid = bf493318f548df8e25c390d6a7f70758fd6b3668;  
"immature_balance" = 0;  
keypoololdest = 1599723938;  
keypoolsize = 999;  
"keypoolsize_hd_internal" = 1000;  
paytxfee = 0;  
"private_keys_enabled" = 1;  
scanning = 0;  
txcount = 1;  
"unconfirmed_balance" = 0;  
walletname = "";  
walletversion = 169900;  
}

## Create an Address

Creating an address is simple enough, but what about creating a legacy address with a specific label? That requires two parameters in your RPC call.

Since the simplistic makeCommand function in this section just passes on its params as the guts of a JSON Object, all you have to do is correctly format those guts. Here's one way to do so:

method = "getnewaddress"  
param = ""learning-bitcoin", "legacy""

makeCommand(method: method,param: param) { result in

let address = result as! NSString    
print(address)  

}

Running this in the Xcode playground produces a result:

mt3ZRsmXHVMMqYQPJ8M74QjF78bmqrdHZF

That result is obviously a Legacy address; its label can then be checked from the command line:

$ bitcoin-cli getaddressesbylabel "learning-bitcoin"  
{  
"mt3ZRsmXHVMMqYQPJ8M74QjF78bmqrdHZF": {  
"purpose": "receive"  
}  
}

Success!

> :information_source: **NOTE:** As we often say in these coding examples, a real-world program would be much more sophisticated. In particular, you'd want to be able to send an actual JSON Object as a parameter, and then have your makeCommand program parse it and input it to the URLSession appropriately. What we have here maximizes readability and simplicity without focusing on ease of use.

## Send a Transaction

As usual, sending a transaction (the hard way) is a multi-step process:

1. Generate or receive a receiving address
    
2. Find an unspent UTXO
    
3. Create a raw transaction
    
4. Sign the raw transaction
    
5. Send the raw transaction
    

You'll use the address that you generated in the previous step as your recipient.

### \1. Find an Unspent UTXO

The listunspent RPC lets you find your UTXO:

method = "listunspent"    
param = ""    
    
makeCommand(method: method,param: param) { result in    
  
    let unspent = result as! NSArray    
    let utxo = unspent[0] as! NSDictionary    
        
    let txid = utxo["txid"] as! NSString    
    let vout = utxo["vout"] as! NSInteger    
    let amount = utxo["amount"] as! NSNumber    
    let new_amount = amount.floatValue - 0.0001

As in other examples, you're going to arbitrarily grab the 0th UTXO, and pull the txid, vout, and amount from it.

> :information_source **NOTE:** Once again, a real-life program would be much more sophisticated.

### \2. Create a Raw Transaction

Creating a raw transaction is the trickiest thing because you need to get all of your JSON objects, arrays, and quotes right. Here's how to do so in Swift, using the transmitter's very basic param formatting:

    method = "createrawtransaction"    
    param="[ { \"txid\": \"\(txid)\", \"vout\": \(vout) } ], { \"\(address)\": \(new_amount)}"    
    makeCommand(method: method,param: param) { result in    
  
        let hex = result as! NSString

### \3. Sign the Raw Transaction

Signing your transaction just requires you to run the signrawtransactionwithwallet RPC, using your new hex:

        method = "signrawtransactionwithwallet"    
        param = "\"\(hex)\""    
            
        makeCommand(method: method,param: param) { result in    
  
            let signedhexinfo = result as! NSDictionary    
            let signedhex = signedhexinfo["hex"] as! NSString

### \4. Send the Raw Transaction

Sending your transaction is equally simple:

            method = "sendrawtransaction"    
            param = "\"\(signedhex)\""    
  
            makeCommand(method: method,param: param) { result in    
  
                let new_txid = result as! NSString    
                print("TXID: \(new_txid)")    
                    
            }    
        }             
    }    
}  

}

The code for this transaction sender can be found in the [src directory](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/src/18_6_sendtx.playground).

## Use Swift in Other Ways

That covers our usual discussions of programming Bitcoin RPC in a language, but Swift is a particularly important language since it can be deployed on mobile devices, one of the prime venues for wallets. As such, you may wish to consider a few other libraries:

- The Blockchain Commons [ios-Bitcoin framework](https://github.com/BlockchainCommons/iOS-Bitcoin) converts the Libbitcoin library from C++ to Swift
    
- [Libwally Swift](https://github.com/blockchain/libwally-swift) is a Swift wrapper for Libwally
    

## Summary: Accessing Bitcoind with Swift

Swift is a robust modern programming language that unfortunately doesn't yet have any easy-to-use RPC libraries ... which just gave us the opportunity to write an RPC-access function of our own. With that in hand, you can interact with bitcoind on a Mac or build companion applications over on an iPhone, which is a perfect combination for airgapped Bitcoin work.

## What's Next?

Learn about Lightning in [Chapter 19: Understanding Your Lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md).

## Variant: Deploy Swift on Ubuntu

If you prefer to deploy Swift on Ubuntu, you can do so, though the functionality isn't the same. Some of the code in this chapter will likely generate errors that you'll need to resolve, and you'll also need to do more work to link in C libraries.

To get started, install some required Debian libraries:

$ sudo apt-get install clang  
$ sudo apt-get install libcurl4 libpython2.7 libpython2.7-dev

If you're using Debian 10 or higher (and you really should be), you'll also need to backdate a few libraries to get older versions:

$ sudo apt-get install libtinfo5 libncurses5

Afteward you can download and install Swift:

$ wget [https://swift.org/builds/swift-5.1.3-release/ubuntu1804/swift-5.1.3-RELEASE/swift-5.1.3-RELEASE-ubuntu18.04.tar.gz](https://swift.org/builds/swift-5.1.3-release/ubuntu1804/swift-5.1.3-RELEASE/swift-5.1.3-RELEASE-ubuntu18.04.tar.gz)  
$ tar xzfv swift-5.1.3-RELEASE-ubuntu18.04.tar.gz  
$ sudo mv swift-5.1.3-RELEASE-ubuntu18.04 /usr/share/swift

To be able to use your new Swift setup, you need to update your PATH in your .bashrc:

$ echo "export PATH=/usr/share/swift/usr/bin:$PATH" >> ~/.bashrc  
$ source ~/.bashrc

You can now test Swift out with the --version argument:

$ swift --version  
Swift version 5.1.3 (swift-5.1.3-RELEASE)  
Target: x86_64-unknown-linux-gnu

### Create a Project

Once you've installed Swift on your Ubuntu machine, you can create projects with the package init command:

$ mkdir swift-project  
$ cd swift-project/  
/swift-project$ swift package init --type executable  
Creating executable package: swift-project  
Creating Package.swift  
Creating README.md  
Creating .gitignore  
Creating Sources/  
Creating Sources/swift-project/main.swift  
Creating Tests/  
Creating Tests/LinuxMain.swift  
Creating Tests/swift-projectTests/  
Creating Tests/swift-projectTests/swift_projectTests.swift  
Creating Tests/swift-projectTests/XCTestManifests.swift

You'll then edit Sources/.../main.swift and when you're ready to compile, you can use the build command:

$ swift build  
[4/4] Linking swift-project

Finally, you'll be able to run the program from the .build/debug directory:

$ .build/debug/swift-project  
Hello, world!

Good luck!

# Chapter 19: Understanding Your Lighting Setup

> :information_source: **NOTE:** This is a draft in progress, so that I can get some feedback from early reviewers. It is not yet ready for learning.

The previous chapter concluded our work with Bitcoin proper, through CLI, scripting, and programming languages. However, there are many other utilities within the Bitcoin ecosystem: this chapter and the next cover what may be the biggest and most important: the Lightning Network. Here you'll begin work with the lightning-cli command-line interface, understanding a core lightning setup and its features, including some examples and basic configuration.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Assess that a core lightning Node is Installed and Up-to-date
    
- Perform Basic Lightning Wallet Commands
    
- Create a LIghtning Channel
    

Supporting objectives include the ability to:

- Understand the Basic Lightning Configuration
    
- Understand the Interaction of Lightning Peers
    
- Understand How to Lightning
    

## Table of Contents

- [Section One: Verifying Your core lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_1_Verifying_Your_Lightning_Setup.md)
    
- [Section Two: Knowing Your core lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2_Knowing_Your_lightning_Setup.md)
    
    - [Interlude: Accessing a Second Lightning Node](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2__Interlude_Accessing_a_Second_Lightning_Node.md)
        
- [Section Three: Creating a Lightning Channel](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_3_Setting_Up_a_Channel.md)
    

# 19.1: Creating a core lightning Setup

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

In this section, you'll install and verify core lightning, your utility for accessing the Lightning Network.

> :book: _**What is the Lightning Network?**_ The Lightning Network is a decentralized network that uses the smart contract functionality of the Bitcoin blockchain to enable instant payments across a network of participants. Lightning is built as a layer-2 protocol that interacts with Bitcoin to allow users to exchange their bitcoins "off-chain". :book: _**What is a layer-2 protocol?**_ Layer 2 refers to a secondary protocol built on top of the Bitcoin blockchain system. The main goal of these protocols is to solve the transaction speed and scaling difficulties that are present in Bitcoin: Bitcoin is not able to process thousands of transactions per second (TPS), so layer-2 protocols have been created to solve the blockchain scalability problem. These solutions are also known as "off-chain" scaling solutions.

## Install core Lightning

If you used the [Bitcoin Standup Scripts](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts), you may have already installed Lightning at the beginning of this course. You can test this by seeing if lightningd is running:

$ ps auxww | grep -i lightning  
standup 31213 0.0 0.2 24144 10424 pts/0 S 15:38 0:00 lightningd --testnet  
standup 31214 0.0 0.1 22716 7444 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/autoclean  
standup 31215 0.0 0.2 22992 8248 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/bcli  
standup 31216 0.0 0.1 22756 7604 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/keysend  
standup 31217 0.0 0.1 22776 7648 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/pay  
standup 31218 0.0 0.1 22720 7652 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/txprepare  
standup 31219 0.0 0.1 22744 7716 pts/0 S 15:38 0:00 /usr/local/bin/../libexec/c-lightning/plugins/spenderp  
standup 31227 0.0 0.1 22748 7384 pts/0 SL 15:38 0:00 /usr/local/libexec/c-lightning/lightning_hsmd  
standup 31228 0.0 0.2 23044 8192 pts/0 S 15:38 0:00 /usr/local/libexec/c-lightning/lightning_connectd  
standup 31229 0.0 0.1 22860 7556 pts/0 S 15:38 0:00 /usr/local/libexec/c-lightning/lightning_gossipd  
standup 32072 0.0 0.0 6208 888 pts/0 S+ 15:50 0:00 grep -i lightning

If not, you'll need to install it now. Unfortunately, if you're using Debian you'll need to install it by hand, by compiling the source code — but it should still be pretty simple if you follow these instructions. If you happen to be on a standard Ubuntu system, instead try [Installing from Ubuntu ppa](#variant-install-from-ubuntu-ppa), and you can always attempt [Installing Pre-compiled Binaries](#variant-install-pre-compiled-binaries).

> :book: _**What is core lightning?**_ There are three different implementations of Lightning at present: core lightning, LND, and Eclair. They should all be functionally compatible, based on the same [BOLT RFCs](https://github.com/lightningnetwork/lightning-rfc/blob/master/00-introduction.md), but their implementation details may be different. We've chosen core lightning as the basis of our course because it's also part of the same [Elements Project](https://github.com/ElementsProject) that also contains Libwally.

### Compile the core lightning Source Code

Installing Lightning from source code should actually be pretty simple if you follow these instructions.

You _probably_ want to do this on an unpruned node, as working with pruned nodes on Lightning may cause issues with installation and usage. If you set up your node way back at the start of this course to be pruned, you may wish to replace it with an unpruned node now. (If you're using testnet, you should be able to use the same type of machine as you did for your pruned node.)

> :warning: **WARNING:** You actually can run core lightning on a pruned node. However, as the [Lightning repo](https://github.com/ElementsProject/lightning#pruning) notes, there may be issues. To make it work you have to ensure that your Lightning node is only ever trying to update info on blocks that your Bitcoin node has not pruned. To do so you must make sure (1) that your Bitcoin node is fully up to date before you start your Lightning node for the first time; and (2) that your Lightning node never falls too far behind your Bitcoin node (for a standard 550-block pruning, it can never be turned off for 4 or more days). So, you can do it, but it does introduce some danger, which isn't a good idea if you're running a production service.

With that, you're ready to install Lightning:

First, install dependencies, including development requirements.

$ sudo apt-get install -y \  
autoconf automake build-essential git libtool libgmp-dev \  
libsqlite3-dev python3 python3-mako net-tools zlib1g-dev libsodium-dev \  
gettext  
$ sudo apt-get install -y valgrind python3-pip libpq-dev

These can take a while, because there are a number of them, and some are large.

Second, clone the Lightning repo:

$ cd ~  
$ git clone [https://github.com/ElementsProject/lightning.git](https://github.com/ElementsProject/lightning.git)  
$ cd lightning

You can now use the pip3 you installed to install additional requirements for the compilation, and configure it all:

$ pip3 install -r requirements.txt  
$ ./configure

Now, compile. This may also take some time depending your machine.

$ make

Afterward, all you need to do is install:

$ sudo make install

## Check Your installation

You can confirm you have installed lightningd correctly using the help parameter:

$ lightningd --help  
lightningd: WARNING: default network changing in 2020: please set network=testnet in config!  
Usage: lightningd  
A bitcoin lightning daemon (default values shown for network: testnet).  
--conf= Specify configuration file  
--lightning-dir= Set base directory: network-specific  
subdirectory is under here  
(default: "/home/javier/.lightning")  
--network Select the network parameters (bitcoin,  
testnet, regtest, litecoin or  
litecoin-testnet) (default: testnet)  
--testnet Alias for --network=testnet  
--signet Alias for --network=signet  
--mainnet Alias for --network=bitcoin

## Run lightningd

You'll begin your exploration of the Lightning network with the lightning-cli command. However,lightningd _must_ be running to use lightning-cli, as lightning-cli sends JSON-RPC commands to the lightningd (all just as with bitcoin-cli and bitcoind).

If you installed core lightning by hand, you'll now need to start it:

$ nohup lightningd --testnet &

### Run lightningd as a service

If you prefer, you can install lightningd as a service that will run every time you restart your machine. The following will do so, and start it running immediately:

$ cat > ~/lightningd.service << EOF

# It is not recommended to modify this file in-place, because it will

# be overwritten during package upgrades. If you want to add further

# options or overwrite existing ones then use

# $ systemctl edit bitcoind.service

# See "man systemd.service" for details.

# Note that almost all daemon options could be specified in

# /etc/lightning/config, except for those explicitly specified as arguments

# in ExecStart=

[Unit]  
Description=c-lightning daemon  
[Service]  
ExecStart=/usr/local/bin/lightningd --testnet

# Process management

####################  
Type=simple  
PIDFile=/run/lightning/lightningd.pid  
Restart=on-failure

# Directory creation and permissions

####################################

# Run as standup

User=standup

# /run/lightningd

RuntimeDirectory=lightningd  
RuntimeDirectoryMode=0710

# Hardening measures

####################

# Provide a private /tmp and /var/tmp.

PrivateTmp=true

# Mount /usr, /boot/ and /etc read-only for the process.

ProtectSystem=full

# Disallow the process and all of its children to gain

# new privileges through execve().

NoNewPrivileges=true

# Use a new /dev namespace only populated with API pseudo devices

# such as /dev/null, /dev/zero and /dev/random.

PrivateDevices=true

# Deny the creation of writable and executable memory mappings.

MemoryDenyWriteExecute=true  
[Install]  
WantedBy=multi-user.target  
EOF  
$ sudo cp ~/lightningd.service /etc/systemd/system  
$ sudo systemctl enable lightningd.service  
$ sudo systemctl start lightningd.service

### Enable Remote Connections

If you have some sort of firewall, you'll need to open up port 9735, to allow other Lightning nodes to talk to you.

If you use ufw from Bitcoin Standup, this is done as follows:

$ sudo ufw allow 9735

## Verify your Node

You can check if your Lightning node is ready to go by comparing the output of bitcoin-cli getblockcount with the blockheight result from lightning-cli getinfo.

$ bitcoin-cli -testnet getblockcount  
1838587  
$ lightning-cli --testnet getinfo  
{  
"id": "03d4592f1244cd6b5a8bb7fba6a55f8a91591d79d3ea29bf8e3c3a405d15db7bf9",  
"alias": "HOPPINGNET",  
"color": "03d459",  
"num_peers": 0,  
"num_pending_channels": 0,  
"num_active_channels": 0,  
"num_inactive_channels": 0,  
"address": [  
{  
"type": "ipv4",  
"address": "74.207.240.32",  
"port": 9735  
},  
{  
"type": "ipv6",  
"address": "2600:3c01::f03c:92ff:fe48:9ddd",  
"port": 9735  
}  
],  
"binding": [  
{  
"type": "ipv6",  
"address": "::",  
"port": 9735  
},  
{  
"type": "ipv4",  
"address": "0.0.0.0",  
"port": 9735  
}  
],  
"version": "v0.9.1-96-g6f870df",  
"blockheight": 1838587,  
"network": "testnet",  
"msatoshi_fees_collected": 0,  
"fees_collected_msat": "0msat",  
"lightning-dir": "/home/standup/.lightning/testnet"  
}

In this case, the blockheight is shown as 1838587 by both commends.

You may instead get an error, depending on the precise situation.

If the Bitcoin node is still sycing with bitcoin network you should see a message like this:

"warning_bitcoind_sync": "Bitcoind is not up-to-date with network."

If your lightning daemon is not up-to-date, you'll get a message like this:

"warning_lightningd_sync": "Still loading latest blocks from bitcoind."

If you tried to run on a pruned blockchain where the Bitcoin node wasn't up to date when you started the Lightning node, you'll get error messages in your log like this:

bitcoin-cli -testnet getblock 0000000000000559febee77ab6e0be1b8d0bef0f971c7a4bee9785393ecef451 0 exited with status 1

## Create Aliases

We suggest creating some aliases to make it easier to use core lightning.

You can do so by putting them in your .bash_profile.

cat >> ~/.bash_profile <<EOF  
alias lndir="cd ~/.lightning/" #linux default core lightning path  
alias lnc="lightning-cli"  
alias lnd="lightningd"  
alias lninfo='lightning-cli getinfo'  
EOF

After you enter these aliases you can either source ~/.bash_profile to input them or just log out and back in.

Note that these aliases include shortcuts for running lightning-cli, for running lightningd, and for going to the core lightning directory. These aliases are mainly meant to make your life easier. We suggest you create other aliases to ease your use of frequent commands (and arguments) and to minimize errors. Aliases of this sort can be even more useful if you have a complex setup where you regularly run commands associated with Mainnet, with Testnet, _and_ with Regtest, as explained further below.

With that said, use of these aliases in _this_ document might accidentally obscure the core lessons being taught about core lightning, so we'll continue to show the full commands; adjust for your own use as appropriate.

## Optional: Modify Your Server Types

> :link: **TESTNET vs MAINNET:** When you set up your node, you choose to create it as either a Mainnet, Testnet, or Regtest node. Though this document presumes a testnet setup, it's worth understanding how you might access and use the other setup types — even all on the same machine! But, if you're a first-time user, skip on past this, as it's not necessary for a basic setup.

When lightningd starts up, it usually reads a configuration file whose location is dependent on the network you are using (default: ~/.lightning/testnet/config). This can be changed with the –conf and –lightning-dir flags.

~/.lightning/testnet$ ls -la config  
-rw-rw-r-- 1 user user 267 jul 12 17:08 config

There is also a general configuration file (default: ~/.lightning/config). If you want to run several different sorts of nodes simultaneously, you must leave the testnet (or regtest) flag out of this configuration file. You should then choose whether you're using the mainnet, the testnet, or your regtest every time you run lightningd or lightning-cli.

Your setup may not actually have any config files: core lightning will run with a good default setup without them.

## Summary: Verifying your Lightning setup

Before you start playing with lightning, you should make sure that your aliases are set up, your lightningd is running, and your node is synced. You may also want to set up some access to alternative lightning setups, on other networks.

## What's Next?

Continue "Understanding Your Lightning Setup" with [§19.2: Knowing Your Lightning Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2_Knowing_Your_lightning_Setup.md).

## Variant: Install from Ubuntu ppa

If you are using a Ubuntu version other than Debian, you can install core lightning using [Ubuntu ppa](https://launchpad.net/~lightningnetwork/+archive/ubuntu/ppa):

$ sudo apt-get install -y software-properties-common  
$ sudo add-apt-repository -u ppa:lightningnetwork/ppa  
$ sudo apt-get install lightningd

## Variant: Install Pre-compiled Binaries

Another method for installing Lightning is to use the precompiled binaries on the [Github repo](https://github.com/ElementsProject/lightning/releases). Choose the newest tarball, such as clightning-v0.9.1-Ubuntu-20.04.tar.xz.

After downloading it, you need to move to root directory and unpackage it:

$ cd /  
$ sudo tar xf ~/clightning-v0.9.1-Ubuntu-20.04.tar.xz

Warning: this will require you to have the precise same libraries as were used to create the binary. It's often easier to just recompile.

# Interlude: Accessing a Second Lightning Node

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

When you played with Bitcoin you were accessing an existing network, and that made it relatively easy to work with: you just turned on bitcoind and you were immediately interacting with the network. That's now how Lightning works: it's fundamentally a peer-to-peer network, built up from the connections between any two individual nodes. In other words, to interact with the Lightning Network, you'll need to first find a node to connect to.

There are four ways to do so (the first three of which are possible for your first connection):

## Ask for Information on a Node

If someone else already has a Lightning node on the network of your choice, just ask them for their ID.

If they are are running core lightning, they just need to use the getinfo command:

$ lightning-cli getinfo  
lightning-cli: WARNING: default network changing in 2020: please set network=testnet in config!  
"id": "03240a4878a9a64aea6c3921a434e573845267b86e89ab19003b0c910a86d17687",  
"alias": "VIOLETGLEE",  
"color": "03240a",  
"num_peers": 0,  
"num_pending_channels": 0,  
"num_active_channels": 0,  
"num_inactive_channels": 0,  
"address": [  
{  
"type": "ipv4",  
"address": "74.207.240.32",  
"port": 9735  
}  
],  
"binding": [  
{  
"type": "ipv6",  
"address": "::",  
"port": 9735  
},  
{  
"type": "ipv4",  
"address": "0.0.0.0",  
"port": 9735  
}  
],  
"version": "v0.9.1-96-g6f870df",  
"blockheight": 1862854,  
"network": "testnet",  
"msatoshi_fees_collected": 0,  
"fees_collected_msat": "0msat",  
"lightning-dir": "/home/standup/.lightning/testnet"  
}

They can then tell you their id (03240a4878a9a64aea6c3921a434e573845267b86e89ab19003b0c910a86d17687). They will also need to tell you their IP address (74.207.240.32) and port (9735).

## Create a New core lightning Node

However, for testing purposes, you probably want to have a second node under you own control. The easiest way to do so is to create a second core lightning node on a new machine, using either Bitcoin Standup, per [§2.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md) or compiling it by hand, per [§19.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_1_Verifying_Your_Lightning_Setup.md).

Once you have your node running, you can run getinfo to retrieve your information, as shown above.

## Create a New LND Node

However, for our examples in the next chapter, we're instead going to create an LND node. This will allow us to demonstrate a bit of the depth of the Lightning ecosystem by showing how similar commands work on the two different platforms.

One way to create an LND node is to run the Bitcoin Standup Scripts again on a new machine, but this time to choose LND, per [§2.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/2_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md).

Another is to compile LND from source code on a machine where you'rea already running a Bitcoin node, as follows.

### Compile the LND Source Code

First, you need to download and install Go:

$ wget --progress=bar:force https://dl.google.com/go/"go1.14.4"."linux"-"amd64".tar.gz -O ~standup/"go1.14.4"."linux"-"amd64".tar.gz  
$ /bin/tar xzf ~standup/"go1.14.4"."linux"-"amd64".tar.gz -C ~standup  
$ sudo mv ~standup/go /usr/local

Be sure that the Go version is the most up to date (it's go1.14.4 at the current time), and the platform and architecture are right for your machine. (The above will work for Debian.)

Update your path:

$ export GOPATH=~standup/gocode  
$ export PATH="$PATH":/usr/local/go/bin:"$GOPATH"/bin

Then be sure that go works:

$ go version  
go version go1.14.4 linux/amd64

You'll also need git and make:

$ sudo apt-get install git  
$ sudo apt-get install build-essential

You're now ready to retrieve LND. Be sure to get the current verison (currently v0.11.0-beta.rc4).

$ go get -d github.com/lightningnetwork/lnd

And now you can compile:

$ cd "$GOPATH"/src/github.com/lightningnetwork/lnd  
$ git checkout v0.11.0-beta.rc4  
$ make  
$ make install

This will install to ~/gocode/bin, which is $GOPATH/bin.

You should move it to global directories:

$ sudo cp $GOPATH/bin/lnd $GOPATH/bin/lncli /usr/bin

### Create an LND Config File

Unlike with core lightning, you will need to create a default config file for LND.

However first, you need to enable ZMQ on your Bitcoind, if you didn't already in [§16.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/16_3_Receiving_Bitcoind_Notifications_with_C.md).

This requires adding the following to your ~/.bitcoin/bitcoin.conf file if it's not already there:

zmqpubrawblock=tcp://127.0.0.1:28332  
zmqpubrawtx=tcp://127.0.0.1:28333

If you're using a Bitcoin config file from Standup or some other specialized conf, be sure you're putting your new commands in the correct section. Ideally, they should go near the top of the file, otherwise in the [test] section (assuming, as usual, that you're testing on testnet).

You must then restart bitcoin (or just reboot your machine). You can test that it's working as follows:

$ bitcoin-cli getzmqnotifications  
[  
{  
"type": "pubrawblock",  
"address": "tcp://127.0.0.1:28332",  
"hwm": 1000  
},  
{  
"type": "pubrawtx",  
"address": "tcp://127.0.0.1:28333",  
"hwm": 1000  
}  
]

Now you're ready to create a config file.

First, you need to retrieve your rpcuser and rpcpassword. Here's an automated way to do so:

$ BITCOINRPC_USER=$(cat ~standup/.bitcoin/bitcoin.conf | grep rpcuser | awk -F = '{print $2}')  
$ BITCOINRPC_PASS=$(cat ~standup/.bitcoin/bitcoin.conf | grep rpcpassword | awk -F = '{print $2}')

> :warning: **WARNING:** Obviously, never store your RPC password in a shell variable in a production environment.

Then, you can write the file:

$ mkdir ~/.lnd  
$ cat > ~/.lnd/lnd.conf << EOF  
[Application Options]  
maxlogfiles=3  
maxlogfilesize=10  
#externalip=1.1.1.1 # change to your public IP address if required.  
alias=StandUp  
listen=0.0.0.0:9735  
debuglevel=debug  
[Bitcoin]  
bitcoin.active=1  
bitcoin.node=bitcoind  
bitcoin.testnet=true  
[Bitcoind]  
bitcoind.rpchost=localhost  
bitcoind.rpcuser=$BITCOINRPC_USER  
bitcoind.rpcpass=$BITCOINRPC_PASS  
bitcoind.zmqpubrawblock=tcp://127.0.0.1:28332  
bitcoind.zmqpubrawtx=tcp://127.0.0.1:28333  
EOF

### Create an LND Service

Finally, you can create an LND service to automatically run lnd:

$ cat > ~/lnd.service << EOF

# It is not recommended to modify this file in-place, because it will

# be overwritten during package upgrades. If you want to add further

# options or overwrite existing ones then use

# $ systemctl edit lnd.service

# See "man systemd.service" for details.

# Note that almost all daemon options could be specified in

# /etc/lnd/lnd.conf, except for those explicitly specified as arguments

# in ExecStart=

[Unit]  
Description=LND Lightning Network Daemon  
Requires=bitcoind.service  
After=bitcoind.service  
[Service]  
ExecStart=/usr/bin/lnd  
ExecStop=/usr/bin/lncli --lnddir /var/lib/lnd stop  
PIDFile=/run/lnd/lnd.pid  
User=standup  
Type=simple  
KillMode=process  
TimeoutStartSec=60  
TimeoutStopSec=60  
Restart=always  
RestartSec=60  
[Install]  
WantedBy=multi-user.target  
EOF

You'll then need to install that and start things up:

$ sudo cp ~/lnd.service /etc/systemd/system  
$ sudo systemctl enable lnd  
$ sudo systemctl start lnd

(Expect this to take a minute the first time.)

### Enable Remote Connections

Just as with core lightning, you're going to need to make LND accessible to other nodes. Here's how to do so if you use ufw, as per the Bitcoin Standup setups:

$ sudo ufw allow 9735

### Create a Wallet

The first time you run LND, you must create a wallet:

$ lncli --network=testnet create

LND will ask you for a password and then ask if you want to enter an existing mnemonic (just hit n for the latter one).

You should now have a functioning lnd, which you can verify with getinfo:

$ lncli --network=testnet getinfo  
{  
"version": "0.11.0-beta.rc4 commit=v0.11.0-beta.rc4",  
"commit_hash": "fc12656a1a62e5d69430bba6e4feb8cfbaf21542",  
"identity_pubkey": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"alias": "StandUp",  
"color": "#3399ff",  
"num_pending_channels": 0,  
"num_active_channels": 0,  
"num_inactive_channels": 0,  
"num_peers": 2,  
"block_height": 1862848,  
"block_hash": "000000000000000ecb6fd95e1f486283d48683aa3111b6c23144a2056f5a1532",  
"best_header_timestamp": "1602632294",  
"synced_to_chain": true,  
"synced_to_graph": false,  
"testnet": true,  
"chains": [  
{  
"chain": "bitcoin",  
"network": "testnet"  
}  
],  
"uris": [  
],  
"features": {  
"0": {  
"name": "data-loss-protect",  
"is_required": true,  
"is_known": true  
},  
"5": {  
"name": "upfront-shutdown-script",  
"is_required": false,  
"is_known": true  
},  
"7": {  
"name": "gossip-queries",  
"is_required": false,  
"is_known": true  
},  
"9": {  
"name": "tlv-onion",  
"is_required": false,  
"is_known": true  
},  
"13": {  
"name": "static-remote-key",  
"is_required": false,  
"is_known": true  
},  
"15": {  
"name": "payment-addr",  
"is_required": false,  
"is_known": true  
},  
"17": {  
"name": "multi-path-payments",  
"is_required": false,  
"is_known": true  
}  
}  
}

This node's ID is 032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543. Although this command doesn't show you the IP address and port, they should be the IP address for your machine and port 9735.

## Listen to Gossip

If you were already connected to the Lightning Network, and were "gossipping" with peers, you might also be able to find information on peers automatically, through the listpeers command:

c$ lightning-cli --network=testnet listpeers  
{  
"peers": [  
{  
"id": "0302d48972ba7eef8b40696102ad114090fd4c146e381f18c7932a2a1d73566f84",  
"connected": true,  
"netaddr": [  
"127.0.0.1:9736"  
],  
"features": "02a2a1",  
"channels": []  
}  
]  
}

However, that definitely won't be the case for your first interaction with the Lightning Network.

## Summary: Accessing a Second Lightning Node

You always need two Lightning nodes to form a channel. If you don't have someone else who is testing things out with you, you're going to need to create a second one, either using core lightning or (as we will in our examples) LND.

## What's Next?

Though you've possibly created an LND, core lightning will remain the heart of our examples until we need to start using both of them, in [Chapter 19](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_0_Understanding_Your_Lightning_Setup.md).

Continue "Understanding Your Lightning Setup" with [§19.3: Setting Up_a_Channel](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_3_Setting_Up_a_Channel.md).

# 19.2: Knowing Your core lightning Setup

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

Before you begin accessing the Lightning Network, you should come to a better understanding of your setup.

## Know Your core lightning Directory

When using core lightning, everything is kept in the ~/.lightning directory.

The main directory just contains directories for whichever networks are configured, in this case testnet:

$ ls ~/.lightning  
testnet

The ~/.lightning/testnet directory will then contains the guts of your setup:

$ ls ~/.lightning/testnet3  
config gossip_store hsm_secret lightningd.sqlite3 lightningd.sqlite3-journal lightning-rpc

> :link: **TESTNET vs MAINNET:** If you're using mainnet, then _everything_ will instead be placed in the main ~/.lightning/bitcoin directory. These various setups _do_ elegantly stack, so if you are using mainnet, testnet, and regtest, you'll find that ~/.lightning/bitcoin contains your config file and your mainnet data, the ~/.lightning/testnet directory contains your testnet data, and the ~/.lightning/regtest directory contains your regtest data.

## Know Your lightning-cli Commands

Most of your early work will be done with the lightning-cli command, which offers an easy interface to lightningd, just like bitcoin-cli does.

You've already seen that the help command will gives you a list of other commands:

$ lightning-cli help  
lightning-cli: WARNING: default network changing in 2020: please set network=testnet in config!  
=== bitcoin ===

feerates style  
Return feerate estimates, either satoshi-per-kw ({style} perkw) or satoshi-per-kb ({style} perkb).

newaddr [addresstype]  
Get a new {bech32, p2sh-segwit} (or all) address to fund a channel (default is bech32)

reserveinputs outputs [feerate] [minconf] [utxos]  
Reserve inputs and pass back the resulting psbt

sendpsbt psbt  
Finalize, extract and send a PSBT.

signpsbt psbt  
Sign this wallet's inputs on a provided PSBT.

txdiscard txid  
Abandon a transaction created by txprepare

txprepare outputs [feerate] [minconf] [utxos]  
Create a transaction, with option to spend in future (either txsend and txdiscard)

txsend txid  
Sign and broadcast a transaction created by txprepare

unreserveinputs psbt  
Unreserve inputs, freeing them up to be reused

withdraw destination satoshi [feerate] [minconf] [utxos]  
Send to {destination} address {satoshi} (or 'all') amount via Bitcoin transaction, at optional {feerate}

=== channels ===

close id [unilateraltimeout] [destination] [fee_negotiation_step]  
Close the channel with {id} (either peer ID, channel ID, or short channel ID). Force a unilateral close after {unilateraltimeout} seconds (default 48h). If {destination} address is provided, will be used as output address.

fundchannel_cancel id  
Cancel inflight channel establishment with peer {id}.

fundchannel_complete id txid txout  
Complete channel establishment with peer {id} for funding transactionwith {txid}. Returns true on success, false otherwise.

fundchannel_start id amount [feerate] [announce] [close_to] [push_msat]  
Start fund channel with {id} using {amount} satoshis. Returns a bech32 address to use as an output for a funding transaction.

getroute id msatoshi riskfactor [cltv] [fromid] [fuzzpercent] [exclude] [maxhops]  
Show route to {id} for {msatoshi}, using {riskfactor} and optional {cltv} (default 9). If specified search from {fromid} otherwise use this node as source. Randomize the route with up to {fuzzpercent} (default 5.0). {exclude} an array of short-channel-id/direction (e.g. [ '564334x877x1/0', '564195x1292x0/1' ]) or node-id from consideration. Set the {maxhops} the route can take (default 20).

listchannels [short_channel_id] [source]  
Show channel {short_channel_id} or {source} (or all known channels, if not specified)

listforwards  
List all forwarded payments and their information

setchannelfee id [base] [ppm]  
Sets specific routing fees for channel with {id} (either peer ID, channel ID, short channel ID or 'all'). Routing fees are defined by a fixed {base} (msat) and a {ppm} (proportional per millionth) value. If values for {base} or {ppm} are left out, defaults will be used. {base} can also be defined in other units, for example '1sat'. If {id} is 'all', the fees will be applied for all channels.

=== network ===

connect id [host] [port]  
Connect to {id} at {host} (which can end in ':port' if not default). {id} can also be of the form id@host

disconnect id [force]  
Disconnect from {id} that has previously been connected to using connect; with {force} set, even if it has a current channel

listnodes [id]  
Show node {id} (or all, if no {id}), in our local network view

listpeers [id] [level]  
Show current peers, if {level} is set, include logs for {id}

ping id [len] [pongbytes]  
Send peer {id} a ping of length {len} (default 128) asking for {pongbytes} (default 128)

=== payment ===

createonion hops assocdata [session_key]  
Create an onion going through the provided nodes, each with its own payload

decodepay bolt11 [description]  
Decode {bolt11}, using {description} if necessary

delexpiredinvoice [maxexpirytime]  
Delete all expired invoices that expired as of given {maxexpirytime} (a UNIX epoch time), or all expired invoices if not specified

delinvoice label status  
Delete unpaid invoice {label} with {status}

invoice msatoshi label description [expiry] [fallbacks] [preimage] [exposeprivatechannels]  
Create an invoice for {msatoshi} with {label} and {description} with optional {expiry} seconds (default 1 week), optional {fallbacks} address list(default empty list) and optional {preimage} (default autogenerated)

listinvoices [label]  
Show invoice {label} (or all, if no {label})

listsendpays [bolt11] [payment_hash]  
Show sendpay, old and current, optionally limiting to {bolt11} or {payment_hash}.

listtransactions  
List transactions that we stored in the wallet

sendonion onion first_hop payment_hash [label] [shared_secrets] [partid]  
Send a payment with a pre-computed onion.

sendpay route payment_hash [label] [msatoshi] [bolt11] [payment_secret] [partid]  
Send along {route} in return for preimage of {payment_hash}

waitanyinvoice [lastpay_index] [timeout]  
Wait for the next invoice to be paid, after {lastpay_index} (if supplied). If {timeout} seconds is reached while waiting, fail with an error.

waitinvoice label  
Wait for an incoming payment matching the invoice with {label}, or if the invoice expires

waitsendpay payment_hash [timeout] [partid]  
Wait for payment attempt on {payment_hash} to succeed or fail, but only up to {timeout} seconds.

=== plugin ===

autocleaninvoice [cycle_seconds] [expired_by]  
Set up autoclean of expired invoices.

estimatefees  
Get the urgent, normal and slow Bitcoin feerates as sat/kVB.

fundchannel id amount [feerate] [announce] [minconf] [utxos] [push_msat]  
Fund channel with {id} using {amount} (or 'all'), at optional {feerate}. Only use outputs that have {minconf} confirmations.

getchaininfo  
Get the chain id, the header count, the block count, and whether this is IBD.

getrawblockbyheight height  
Get the bitcoin block at a given height

getutxout txid vout  
Get informations about an output, identified by a {txid} an a {vout}

listpays [bolt11]  
List result of payment {bolt11}, or all

pay bolt11 [msatoshi] [label] [riskfactor] [maxfeepercent] [retry_for] [maxdelay] [exemptfee]  
Send payment specified by {bolt11} with {amount}

paystatus [bolt11]  
Detail status of attempts to pay {bolt11}, or all

plugin subcommand=start|stop|startdir|rescan|list  
Control plugins (start, stop, startdir, rescan, list)

sendrawtransaction tx  
Send a raw transaction to the Bitcoin network.

=== utility ===

check command_to_check  
Don't run {command_to_check}, just verify parameters.

checkmessage message zbase [pubkey]  
Verify a digital signature {zbase} of {message} signed with {pubkey}

getinfo  
Show information about this node

getlog [level]  
Show logs, with optional log {level} (info|unusual|debug|io)

getsharedsecret point  
Compute the hash of the Elliptic Curve Diffie Hellman shared secret point from this node private key and an input {point}.

help [command]  
List available commands, or give verbose help on one {command}.

listconfigs [config]  
List all configuration options, or with [config], just that one.

listfunds  
Show available funds from the internal wallet

signmessage message  
Create a digital signature of {message}

stop  
Shut down the lightningd process

waitblockheight blockheight [timeout]  
Wait for the blockchain to reach {blockheight}, up to {timeout} seconds.

=== developer ===

dev-listaddrs [bip32_max_index]  
Show addresses list up to derivation {index} (default is the last bip32 index)

dev-rescan-outputs  
Synchronize the state of our funds with bitcoind

---

run lightning-cli help <command> for more information on a specific command

## Know your Lightning Info

A variety of lightning-cli commands can give you additional information on your lightning node. The most general ones are:

$ lightning-cli --testnet listconfigs  
$ lightning-cli --testnet listfunds  
$ lightning-cli --testnet listtransactions  
$ lightning-cli --testnet listinvoices  
$ lightning-cli --testnet listnodes

- listconfigs: The listconfigs RPC command lists all configuration options.
    
- listfunds: The listfunds RPC command displays all funds available, either in unspent outputs (UTXOs) in the internal wallet or funds locked in currently open channels.
    
- listtransactions: The listtransactions RPC command returns transactions tracked in the wallet. This includes deposits, withdrawals, and transactions related to channels.
    
- listinvoices: The listinvoices RPC command retrieves the status of a specific invoice, if it exists, or the status of all invoices if given no argument.
    
- listnodes: The listnodes RPC command returns nodes that your server has learned about via gossip messages, or a single one if the node id was specified.
    

For example lightning-cli listconfigs gives you a variety of information on your setup:

c$ lightning-cli --testnet listconfigs  
{  
"# version": "v0.8.2-398-g869fa08",  
"lightning-dir": "/home/standup/.lightning",  
"network": "testnet",  
"allow-deprecated-apis": true,  
"rpc-file": "lightning-rpc",  
"plugin": "/usr/local/bin/../libexec/c-lightning/plugins/fundchannel",  
"plugin": "/usr/local/bin/../libexec/c-lightning/plugins/autoclean",  
"plugin": "/usr/local/bin/../libexec/c-lightning/plugins/bcli",  
"plugin": "/usr/local/bin/../libexec/c-lightning/plugins/pay",  
"plugin": "/usr/local/bin/../libexec/c-lightning/plugins/keysend",  
"plugins": [  
{  
"path": "/usr/local/bin/../libexec/c-lightning/plugins/fundchannel",  
"name": "fundchannel"  
},  
{  
"path": "/usr/local/bin/../libexec/c-lightning/plugins/autoclean",  
"name": "autoclean",  
"options": {  
"autocleaninvoice-cycle": null,  
"autocleaninvoice-expired-by": null  
}  
},  
{  
"path": "/usr/local/bin/../libexec/c-lightning/plugins/bcli",  
"name": "bcli",  
"options": {  
"bitcoin-datadir": null,  
"bitcoin-cli": null,  
"bitcoin-rpcuser": null,  
"bitcoin-rpcpassword": null,  
"bitcoin-rpcconnect": null,  
"bitcoin-rpcport": null,  
"bitcoin-retry-timeout": null,  
"commit-fee": "500"  
}  
},  
{  
"path": "/usr/local/bin/../libexec/c-lightning/plugins/pay",  
"name": "pay"  
},  
{  
"path": "/usr/local/bin/../libexec/c-lightning/plugins/keysend",  
"name": "keysend"  
}  
],  
"disable-plugin": [],  
"always-use-proxy": false,  
"daemon": "false",  
"wallet": "sqlite3:///home/user/.lightning/testnet/lightningd.sqlite3",  
"wumbo": false,  
"wumbo": false,  
"rgb": "03fce2",  
"alias": "learningBitcoin",  
"pid-file": "/home/user/.lightning/lightningd-testnet.pid",  
"ignore-fee-limits": false,  
"watchtime-blocks": 144,  
"max-locktime-blocks": 720,  
"funding-confirms": 3,  
"commit-fee-min": 200,  
"commit-fee-max": 2000,  
"cltv-delta": 6,  
"cltv-final": 10,  
"commit-time": 10,  
"fee-base": 1,  
"rescan": 15,  
"fee-per-satoshi": 10,  
"max-concurrent-htlcs": 483,  
"min-capacity-sat": 10000,  
"offline": "false",  
"autolisten": true,  
"disable-dns": "false",  
"enable-autotor-v2-mode": "false",  
"encrypted-hsm": false,  
"rpc-file-mode": "0600",  
"log-level": "DEBUG",  
"log-prefix": "lightningd"  
}

## Summary: Knowing Your lightning Setup

The ~/.lightning directory contains all of your files, while lightning-cli help and a variety of info commands can be used to get more information on how your setup and Lightning Network work.

## What's Next?

You're going to need to have a second Linode node to test out the actual payment of invoices. If you need support in setting one up, read [Interlude: Accessing a Second Lightning Node](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2__Interlude_Accessing_a_Second_Lightning_Node.md).

Otherwise, continue "Understanding Your Lightning Setup" with [§19.3: Setting Up_a_Channel](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_3_Setting_Up_a_Channel.md).

# 19.3: Creating a Lightning Channel

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

You now understand the basics of your Lightning setup, and hopefully have either created or been given info on a second Lightning node. You're ready to create your first Lightning Network channel. Of course, you'll need to understand what is, and how it's created using core lightning.

> :book: _**What is a Lighting Channel?**_ Simply, a lightning channel is a money tube that allows fast, cheap and private transfers of money without sending transactions to the blockchain. More technically a channel is a 2-of-2 multisignature on-chain Bitcoin transaction that establishes a trustless financial relationship between two people or two agents. A certain amount of money is deposited into the channel, when then mantains a local database with bitcoin balance for both parties, keeping track of how much money they each have from the initial amount. The two users can then exchange bitcoins through their Lightning channel without ever writing to the Bitcoin blockchain. Only when they want to close out their channel do they settle their bitcoins to the blockchain, based on the final division of coins. :book: _**How do Lightning Channels Create a Lightning Network?**_ Although a Lightning channel only allows payment between two users, channels can be connected together to form a network that allows payments between members that doesn't have a direct channel between them. This creates a network among multiple people built from pairwise connections.

In this section, we will continue using our core lightning setup as our primary node.

## Create a Channel

Creating a Lightning channel requires the following steps:

- Fund your core lightning wallet with some satoshis.
    
- Connect to a remote node as a peer.
    
- Open a channel.
    

### Fund Your core lightning Wallet

In order to move funds to a Lightning channel first requires funding your core lightning wallet.

> :book: _**What is a core lightning wallet?**_ core lightning's standard implementation comes with a integrated Bitcoin wallet that allows you send and receive on-chain bitcoin transactions. This wallet will be used to create new channels.

The first thing you need to do is send some satoshis to your core lightning wallet. You can create a new address using lightning-cli newaddr command. This generates a new address that can subsequently be used to fund channels managed by the core lightning node. You can specify the type of address wanted; if not specified, the address generated will be a bech32.

$ lightning-cli --testnet newaddr  
{  
"address": "tb1qefule33u7ukfuzkmxpz02kwejl8j8dt5jpgtu6",  
"bech32": "tb1qefule33u7ukfuzkmxpz02kwejl8j8dt5jpgtu6"  
}

You can then send funds to this address using bitcoin-cli sendtoaddress (or any other methodlogy you prefer). For this example, we have done so in the transaction [11094bb9ac29ce5af9f1e5a0e4aac2066ae132f25b72bff90fcddf64bf2feb02](https://blockstream.info/testnet/tx/11094bb9ac29ce5af9f1e5a0e4aac2066ae132f25b72bff90fcddf64bf2feb02).

This transaction is called the [funding transaction](https://github.com/lightningnetwork/lightning-rfc/blob/master/03-transactions.md#funding-transaction-output), and it needs to be confirmed before funds can be used.

> :book: _**What is a Funding Transaction?**_ A funding transaction is a Bitcoin transaction that places money into a Lightning channel. It may be single-funded (by one participant) or dual-funded (by both). From there on, Lightning transactions are all about reallocating the ownership of the funding transaction, but they only settle to the blockchain when the channel is closed.

To check you local balance you should use lightning-cli listfunds command:

c$ lightning-cli --testnet listfunds  
{  
"outputs": [],  
"channels": []  
}

Since the funds do not yet have six confirmations, there is no balance available. After six confirmations you should see a balance:

c$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "11094bb9ac29ce5af9f1e5a0e4aac2066ae132f25b72bff90fcddf64bf2feb02",  
"output": 0,  
"value": 300000,  
"amount_msat": "300000000msat",  
"scriptpubkey": "0014ca79fcc63cf72c9e0adb3044f559d997cf23b574",  
"address": "tb1qefule33u7ukfuzkmxpz02kwejl8j8dt5jpgtu6",  
"status": "confirmed",  
"blockheight": 1780680,  
"reserved": false  
}  
],  
"channels": []  
}

Note that the value is listed in satoshis or microsatoshis, not Bitcoin!

> :book: _**What are satoshis and msat?**_ You already met satoshis way back in [§3.4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_4_Receiving_a_Transaction.md). One satoshi is one hundred millionth of a bitcoin, so 300,000 satoshi = 0.003 BTC. A satoshi is the smallest unit of currency on the Bitcoin network. But, the Lightning network can go smaller, so 1,000 msat, or millisatoshis, equal one satoshi. That means that 1 msat is one hundred billionth of a bitcoin, and 300,000,000 msat = 0.003 BTC.

Now that you have funded your core lightning wallet you will need information about a remote node to start creating channel process.

### Connect to a Remote Node

The next thing you need to do is connect your node to a peer. This is done with the lightning-cli connect command. Remember that if you want more information on this command, you should type lightning-cli help connect.

To connect your node to a remote peer you need its id, which represents the target node’s public key. As a convenience, id may be of the form id@host or id@host:port. You may have retrieved this with lightning-cli getinfo (on core lightning) or lncli --network=testnet getinfo (on LND) as discussed in the [previous interlude](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2__Interlude_Accessing_a_Second_Lightning_Node.md).

We've selected the LND node, 032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543, which is located at IP address 45.33.35.151, which we're going to connect to from our core lightning node:

$ lightning-cli --network=testnet connect [032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543@45.33.35.151](mailto:032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543@45.33.35.151)  
{  
"id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"features": "02a2a1"  
}

### Open a Channel

The fundchannel RPC command opens a payment channel with a peer by committing a funding transaction to the blockchain. You should use lightning-cli fundchannel command to do so, with the following parameters:

- **id** is the peer id return from connect.
    
- **amount** is the amount in satoshis taken from the internal wallet to fund the channel. The value cannot be less than the dust limit, currently set to 546, nor more than 16.777.215 satoshi (unless large channels were negotiated with the peer).
    
- **feerate** is an optional feerate used for the opening transaction and as initial feerate for commitment and HTLC transactions.
    
- **announce** is an optional flag that triggers whether to announce this channel or not. It defaults to true. If you want to create an unannounced private channel set it to false.
    
- **minconf** specifies the minimum number of confirmations that used outputs on the channel opening processe should have. Default is 1.
    
- **utxos** specifies the utxos to be used to fund the channel, as an array of “txid:vout”.
    

Now you can open the channel like this:

$ lightning-cli --testnet fundchannel 032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543 100000 urgent true 1  
{  
"tx": "0200000000010193dc3337837f091718f47b71f2eae8b745ec307231471f6a6aab953c3ea0e3b50100000000fdffffff02a0860100000000002200202e30365fe321a435e5f66962492163302f118c13e215ea8928de88cc46666c1d07860100000000001600142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c024730440220668a7c253c9fd83fc1b45e4a52823fb6bc5fad30da36240d4604f0d6981a6f4502202aeb1da5fbbc8790791ef72b3378005fe98d485d22ffeb35e54a6fbc73178fb2012103b3efe051712e9fa6d90008186e96320491cfe1ef1922d74af5bc6d3307843327c76c1c00",  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"channel_id": "1d3cf2126ae36e12be3aee893b385ed6a2e19b1da7f4e579e3ef15ca234d6966",  
"outnum": 0  
}

To confirm channel status use lightning-cli listfunds command:

c$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "unconfirmed",  
"reserved": false  
},  
{  
"txid": "b5e3a03e3c95ab6a6a1f47317230ec45b7e8eaf2717bf41817097f833733dc93",  
"output": 1,  
"value": 200000,  
"amount_msat": "200000000msat",  
"scriptpubkey": "0014ed54b65eae3da99b23a48bf8827c9acd78079469",  
"address": "tb1qa42tvh4w8k5ekgay30ugyly6e4uq09rfpqf9md",  
"status": "confirmed",  
"blockheight": 1862831,  
"reserved": true  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": true,  
"state": "CHANNELD_AWAITING_LOCKIN",  
"channel_sat": 100000,  
"our_amount_msat": "100000000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

While this new channel with 100,000 satoshis is unconfirmed, its state will be CHANNELD_AWAITING_LOCKIN. Note that unconfirmed change of 99847 satoshis is also showing as a new transaction in the wallet. After all six confirmations are completed, the channel will change to CHANNELD_NORMAL state, which will be its permanent state. At this time, a short_channel_id will also appear, such as:

     "short_channel_id": "1862856x29x0",

These values denote where the funding transaction can be found on the blockchain. It appears in the form block x txid x vout.

In this case, 1862856x29x0 means:

- Created on the 1862856th block;
    
- with a txid of 29; and
    
- an vout of 0.
    

You may need to use this short_channel_id for certain commands in Lightning.

This funding transaction can also be found onchain at [66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d](https://blockstream.info/testnet/tx/66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d)

> :book: _**What is Channel Capacity?**_ In a Lightning Channel, both sides of the channel own a portion of its capacity. The amount on your side of the channel is called _local balance_ and the amount on your peer’s side is called _remote balance_. Both balances can be updated many times without closing the channel (when the final balance is sent to the blockchain), but the channel capacity cannot change without closing or splicing it. The total capacity of a channel is the sum of the balance held by each participant in the channel.

## Summary: Setting up a channel

You need to create a channel with a remote node to be able to receive and send money over the Lightning Network.

## What's Next?

You're ready to go! Move on to [Chapter 20: Using Lightning](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_0_Using_Lightning.md).

# Chapter 20: Using Lightning

> :information_source: **NOTE:** This is a draft in progress, so that I can get some feedback from early reviewers. It is not yet ready for learning.

In this chapter you'll continue work with the lightning-cli command-line interface. You'll create invoices, perform payments, and close channels — all of the major activities for using Lightning.

## Objectives for This Chapter

After working through this chapter, a developer will be able to:

- Perform payments on the Lightning Network.
    
- Apply closure to a Lightning channel.
    

Supporting objectives include the ability to:

- Understand the format of invoices.
    
- Understand the life cycle of Lightning Network payments.
    
- Know how to expand the Lightning Network.
    

## Table of Contents

- [Section One: Generating a Payment Request](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_1_Generate_a_Payment_Request.md)
    
- [Section Two: Paying an Invoice](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_2_Paying_a_Invoice.md)
    
- [Section Three: Closing a Lightning Channel](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_3_Closing_a_Channel.md)
    
- [Section Four: Expanding the Lightning Network](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_4_Lightning_Network_Review.md)
    

# 20.1: Generating a Payment Request

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

This section describes how payments work on the Lightning Network, how to create a payment request (or _invoice_), and finally how to make sense of it. Issuing invoices depends on your having a second Lightning node, as described in [Accessing a Second Lightning Node](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2__Interlude_Accessing_a_Second_Lightning_Node.md). These examples will use an LND node as their secondary node, to further demonstrate the possibilities of the Lightning Network. To differentiate between the nodes in these examples, the prompts will be shown as c$ for the core lightning node and lnd$ as the LND node. If you want to reproduce this steps, you should [install your own secondary LND node](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_2__Interlude_Accessing_a_Second_Lightning_Node.md#creating-a-new-lnd-node).

> :book: ***What is an Invoice?** Almost all payments made on the Lightning Network require an invoice, which is nothing more than a **request for payment** made by the recipient of the money and sent by variety of means to the paying user. All payment requests are single use. Lightning invoices use bech32 encoding, which is already used by Segregated Witness for Bitcoin.

## Create an Invoice

To create a new invoice on core lightning you would use the lightning-cli --testnet invoice command.

Here's how it would work with core lightning, using arguments of an amount (in millisatoshis), a label, and a description.

c$ lightning-cli --testnet invoice 100000 joe-payment "The money you owe me for dinner"  
{  
"payment_hash": "07a1c4bd7a38b4dea35f301c173cd8f9aac253b66bd8404d7ad829f226342490",  
"expires_at": 1603305795,  
"bolt11": "lntb1u1p0cw3krpp5q7suf0t68z6dag6lxqwpw0xclx4vy5akd0vyqnt6mq5lyf35yjgqdpj235x2grddahx27fq09hh2gr0wajjqmt9ypnx7u3qv35kumn9wgxqyjw5qcqp2sp5r3puay46tffdyzldjv39fw6tzdgu2hnlszamqhnmgjsuxqxavpgs9qy9qsqatawvx44x5qa22m7td84jau5450v7j6sl5224tlv9k5v7wdygq9qr4drz795lfnl52gklvyvnha5e5lx72lzzmgzcfnp942va5thmhsp5sx7c2",  
"warning_capacity": "No channels",  
"warning_mpp_capacity": "The total incoming capacity is still insufficient even if the payer had MPP capability."  
}

However, for this example we're going to instead generate an invoice on an LND node, and then pay it on the core lightning node. This requires LND's slightly different addinvoice command. You can use --amt argument to indicate amount to be paid (in millisatoshis) and add a description using the --memo argument.

lnd$ lncli -n testnet addinvoice --amt 10000 --memo "First LN Payment - Learning Bitcoin and Lightning from the Command line."  
{  
"r_hash": "6cacdedc95b89eec15e5244bd0957b88c0ab58b153eee549735b995344bc16bb",  
"payment_request": "lntb100u1p0cwnqtpp5djkdahy4hz0wc909y39ap9tm3rq2kk9320hw2jtntwv4x39uz6asdr5ge5hyum5ypxyugzsv9uk6etwwssz6gzvv4shymnfdenjqsnfw33k76twypskuepqf35kw6r5de5kueeqveex7mfqw35x2gzrdakk6ctwvssxc6twv5hqcqzpgsp5a9ryqw7t23myn9psd36ra5alzvp6lzhxua58609teslwqmdljpxs9qy9qsq9ee7h500jazef6c306psr0ncru469zgyr2m2h32c6ser28vrvh5j4q23c073xsvmjwgv9wtk2q7j6pj09fn53v2vkrdkgsjv7njh9aqqtjn3vd",  
"add_index": "1"  
}

Note that these invoices don't directly reference the channel you created: that's necessary for payment, but not for requesting payment.

## Understand an Invoice

The bolt11 payment_request that you created is made up of two parts: one is human readable and the other is data.

> :book: **What is a BOLT?** The BOLTs are the individual [specifications for the Lightning Network](https://github.com/lightningnetwork/lightning-rfc).

### Read the Human-Readable Invoice Part

The human readable part of your invoices starts with an ln. It is lnbc for Bitcoin mainnet, lntb for Bitcoin testnet, or lnbcrt for Bitcoin regtest. It then lists the funds requested in the invoice.

For example, look at your invoice from your LND node:

lntb100u1p0cwnqtpp5djkdahy4hz0wc909y39ap9tm3rq2kk9320hw2jtntwv4x39uz6asdr5ge5hyum5ypxyugzsv9uk6etwwssz6gzvv4shymnfdenjqsnfw33k76twypskuepqf35kw6r5de5kueeqveex7mfqw35x2gzrdakk6ctwvssxc6twv5hqcqzpgsp5a9ryqw7t23myn9psd36ra5alzvp6lzhxua58609teslwqmdljpxs9qy9qsq9ee7h500jazef6c306psr0ncru469zgyr2m2h32c6ser28vrvh5j4q23c073xsvmjwgv9wtk2q7j6pj09fn53v2vkrdkgsjv7njh9aqqtjn3vd

The human readable part is ln + tb + 100u.

lntb says that this is a Lightning Network invoice for Testnet bitcoins.

100u says that it is for 100 bitcoins times the microsatoshi multiplier. There are four (optional) funds multipliers:

- m (milli): multiply by 0.001
    
- u (micro): multiply by 0.000001
    
- n (nano): multiply by 0.000000001
    
- p (pico): multiply by 0.000000000001
    

100 BTC * .000001 = .0001 BTC, which is the same as 10,000 satoshis.

### Read the Data Invoice Part

The rest of the invoice (1p0cwnqtpp5djkdahy4hz0wc909y39ap9tm3rq2kk9320hw2jtntwv4x39uz6asdr5ge5hyum5ypxyugzsv9uk6etwwssz6gzvv4shymnfdenjqsnfw33k76twypskuepqf35kw6r5de5kueeqveex7mfqw35x2gzrdakk6ctwvssxc6twv5hqcqzpgsp5a9ryqw7t23myn9psd36ra5alzvp6lzhxua58609teslwqmdljpxs9qy9qsq9ee7h500jazef6c306psr0ncru469zgyr2m2h32c6ser28vrvh5j4q23c073xsvmjwgv9wtk2q7j6pj09fn53v2vkrdkgsjv7njh9aqqtjn3vd) contains a timestamp, specifically tagged data, and a signature. You obviously can't read it yourself, but you can ask core lightning's lightning-cli to do so with the decodepay command:

c$ lightning-cli --testnet decodepay lntb100u1p0cwnqtpp5djkdahy4hz0wc909y39ap9tm3rq2kk9320hw2jtntwv4x39uz6asdr5ge5hyum5ypxyugzsv9uk6etwwssz6gzvv4shymnfdenjqsnfw33k76twypskuepqf35kw6r5de5kueeqveex7mfqw35x2gzrdakk6ctwvssxc6twv5hqcqzpgsp5a9ryqw7t23myn9psd36ra5alzvp6lzhxua58609teslwqmdljpxs9qy9qsq9ee7h500jazef6c306psr0ncru469zgyr2m2h32c6ser28vrvh5j4q23c073xsvmjwgv9wtk2q7j6pj09fn53v2vkrdkgsjv7njh9aqqtjn3vd  
{  
"currency": "tb",  
"created_at": 1602702347,  
"expiry": 3600,  
"payee": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"msatoshi": 10000000,  
"amount_msat": "10000000msat",  
"description": "First LN Payment - Learning Bitcoin and Lightning from the Command line.",  
"min_final_cltv_expiry": 40,  
"payment_secret": "e946403bcb54764994306c743ed3bf1303af8ae6e7687d3cabcc3ee06dbf904d",  
"features": "028200",  
"payment_hash": "6cacdedc95b89eec15e5244bd0957b88c0ab58b153eee549735b995344bc16bb",  
"signature": "304402202e73ebd1ef974594eb117e8301be781f2ba289041ab6abc558d432351d8365e902202a8151c3fd13419b9390c2b976503d2d064f2a6748b14cb0db64424cf4e572f4"  
}

Here's what the most relevent elements mean:

1. currency: The currency being paid.
    
2. created_at: Time when the invoice was created. This is measured in UNIX time, which is seconds since 1970.
    
3. expiry: The time when your node marks the invoice as invalid. Default is 1 hour or 3600 seconds.
    
4. payee: The public key of the person (node) receiving the Lightning Network payment.
    
5. msatoshi and amount_msat: The amount of satoshis to be paid.
    
6. description: The user-input description.
    
7. payment_hash: The hash of the preimage that is used to lock the payment. You can only redeem a locked payment with the corresponding preimage to the payment hash. This enables routing on the Lightning Network without trusting third parties, by creating a **Conditional Payment** to be filled.
    
8. signature: The DER-encoded signature.
    

> :book: *_**What are Conditional Payments?**_ Although Lightning Channels are created between two participants, multiple channels can be connected together, forming a payment network that allows payments between all the network participants, even those without a direct channel between them. This is done using an smart contract called a **Hashed Time Locked Contract**. :book: _**What is a Hashed Time Locked Contract (HTLC)?**_ A Hashed Time Locked Contract is a conditional payment that use hashlocks and timelocks to ensure payment security. The receiver must present a payment preimage or generate a cryptographic proof of payment before a given time, otherwise the payer can cancel the contract by spending it. These contracts are created as outputs from the **Commitment Transaction**. :book: _**What is a Commitment Transaction?**_ A Commitment Transaction is a transaction that spends the original funding transaction. Each peer holds the other peer's signature, meaning that either one can spent his commitment transaction whatever he wants. After each new commitment transaction is created the old one is revoked. The commitment transaction is one way that the funding transaction can be unlocked on the blockchain, as discussed in [§20.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_3_Closing_a_Channel.md).

### Check Your Invoice

There are two crucial elements to check in the invoice. The first, obviously, is the payment amount, which you've already examined in the human-readable part. The second is the payee value, which is the pubkey of the recipient (node):

"payee": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",

You need to check that's the expected recipient.

Looking back at [§20.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_3_Closing_a_Channel.md), you can see that's indeed the peer ID that you used when you created your channel. You could also verify it on the opposite node with the getinfo command.

lnd$ lncli -n testnet getinfo  
{  
"version": "0.11.0-beta.rc4 commit=v0.11.0-beta.rc4",  
"commit_hash": "fc12656a1a62e5d69430bba6e4feb8cfbaf21542",  
"identity_pubkey": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"alias": "StandUp",  
"color": "#3399ff",  
"num_pending_channels": 0,  
"num_active_channels": 1,  
"num_inactive_channels": 0,  
"num_peers": 3,  
"block_height": 1862983,  
"block_hash": "00000000000000c8c2f58f6da2ae2a3884d6e84f55d0e1f585a366f9dfcaa860",  
"best_header_timestamp": "1602702331",  
"synced_to_chain": true,  
"synced_to_graph": true,  
"testnet": true,  
"chains": [  
{  
"chain": "bitcoin",  
"network": "testnet"  
}  
],  
"uris": [  
],  
"features": {  
"0": {  
"name": "data-loss-protect",  
"is_required": true,  
"is_known": true  
},  
"5": {  
"name": "upfront-shutdown-script",  
"is_required": false,  
"is_known": true  
},  
"7": {  
"name": "gossip-queries",  
"is_required": false,  
"is_known": true  
},  
"9": {  
"name": "tlv-onion",  
"is_required": false,  
"is_known": true  
},  
"13": {  
"name": "static-remote-key",  
"is_required": false,  
"is_known": true  
},  
"15": {  
"name": "payment-addr",  
"is_required": false,  
"is_known": true  
},  
"17": {  
"name": "multi-path-payments",  
"is_required": false,  
"is_known": true  
}  
}  
}

However, the payee may also be someone brand new, in which case you'll likely need to check with the web site or person who issued the invoice to ensure that it's correct.

## Summary: Generating a Payment Request

In most cases you need to receive an invoice to use Lightning Network payments. In this example we've created one manually, but if you had a production environment, you'd likely have systems automatically doing this whenever someone purchases products or services. Of course, once you've received an invoice, you need to understand how to read it!

## What's Next?

Continue "Using Lightning" with [§20.2: Paying_a_Invoice](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_2_Paying_a_Invoice.md).

# 20.2: Paying an Invoice

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

In this chapter you will learn how to pay an invoice using lightning-cli pay command. It assumes that you've already looked over the invoice, per [§20.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_1_Generate_a_Payment_Request.md) and determined it was valid.

## Check your Balance

Obviously, the first thing you need to do is make sure that you have enough funds to pay an invoice. In this case, the channel set up previously with 032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543 contains 100,000 satoshis. This will be the channel used to pay the invoice.

c$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "confirmed",  
"blockheight": 1862856,  
"reserved": false  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": true,  
"state": "CHANNELD_NORMAL",  
"short_channel_id": "1862856x29x0",  
"channel_sat": 100000,  
"our_amount_msat": "100000000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

If you didn't have enough funds, you'd need to create a new channel.

## Pay Your Invoice

You use lightning-cli pay command to pay an invoice. It will attempt to find a route to the given destination and send the funds requested. Here that's very simple because there's a direct channel between the payer and the recipient:

c$ lightning-cli --testnet pay lntb100u1p0cwnqtpp5djkdahy4hz0wc909y39ap9tm3rq2kk9320hw2jtntwv4x39uz6asdr5ge5hyum5ypxyugzsv9uk6etwwssz6gzvv4shymnfdenjqsnfw33k76twypskuepqf35kw6r5de5kueeqveex7mfqw35x2gzrdakk6ctwvssxc6twv5hqcqzpgsp5a9ryqw7t23myn9psd36ra5alzvp6lzhxua58609teslwqmdljpxs9qy9qsq9ee7h500jazef6c306psr0ncru469zgyr2m2h32c6ser28vrvh5j4q23c073xsvmjwgv9wtk2q7j6pj09fn53v2vkrdkgsjv7njh9aqqtjn3vd  
{  
"destination": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"payment_hash": "6cacdedc95b89eec15e5244bd0957b88c0ab58b153eee549735b995344bc16bb",  
"created_at": 1602704828.948,  
"parts": 1,  
"msatoshi": 10000000,  
"amount_msat": "10000000msat",  
"msatoshi_sent": 10000000,  
"amount_sent_msat": "10000000msat",  
"payment_preimage": "1af4a9bb830e49b6bc8f0bef980630e189e3794ad1705f06ad1b9c71571dce0c",  
"status": "complete"  
}

Note that here all the amounts are in msats, not sats!

### Pay Your Invoice Across the Network

However, you do _not_ need to have a channel with a node in order to pay them. There just needs to be a reasonable route across the Lightning Network.

Imagine that you received this teeny payment request for 11,111 msat:

c$ lightning-cli --testnet decodepay lntb111110p1p0cw43ppp5u0ngjytlw6ywec3x784jale4xd7h058g9u4mthcaf9rl2f7g8zxsdp2t9hh2gr0wajjqmt9ypnx7u3qv35kumn9wgs8gmm0yyxqyjw5qcqp2sp5kj4xhrthmfgcgyl84zaqpl9vvdjwm5x368kr09fu5nym74setw4s9qy9qsq8hxjr73ee77vat0ay603e4w9aa8ag9sa2n55xznk5lsfrjffxxdj2k0wznvcfa98l4a57s80j7dhg0cc03vwqdwehkujlzxgm0xyynqqslwhvl  
{  
"currency": "tb",  
"created_at": 1602704929,  
"expiry": 604800,  
"payee": "02f3d74746934494fa378235e5bc44cfdbb5b8779d839263fb7f9218be032f6f61",  
"msatoshi": 11111,  
"amount_msat": "11111msat",  
"description": "You owe me for dinner too!",  
"min_final_cltv_expiry": 10,  
"payment_secret": "b4aa6b8d77da518413e7a8ba00fcac6364edd0d1d1ec37953ca4c9bf56195bab",  
"features": "028200",  
"payment_hash": "e3e689117f7688ece226f1eb2eff35337d77d0e82f2bb5df1d4947f527c8388d",  
"signature": "304402203dcd21fa39cfbcceadfd269f1cd5c5ef4fd4161d54e9430a76a7e091c929319b02202559ee14d984f4a7fd7b4f40ef979b743f187c58e035d9bdb92f88c8dbcc424c"  
}

If you tried to pay it, and you didn't have a route to the recipient through the Lightning Network, you could expect an error like this:

c$ lightning-cli --testnet pay lntb111110p1p0cw43ppp5u0ngjytlw6ywec3x784jale4xd7h058g9u4mthcaf9rl2f7g8zxsdp2t9hh2gr0wajjqmt9ypnx7u3qv35kumn9wgs8gmm0yyxqyjw5qcqp2sp5kj4xhrthmfgcgyl84zaqpl9vvdjwm5x368kr09fu5nym74setw4s9qy9qsq8hxjr73ee77vat0ay603e4w9aa8ag9sa2n55xznk5lsfrjffxxdj2k0wznvcfa98l4a57s80j7dhg0cc03vwqdwehkujlzxgm0xyynqqslwhvl  
{  
"code": 210,  
"message": "Ran out of routes to try after 11 attempts: see paystatus",  
"attempts": [  
{  
"status": "failed",  
"failreason": "Error computing a route to 02f3d74746934494fa378235e5bc44cfdbb5b8779d839263fb7f9218be032f6f61: "Could not find a route" (205)",  
"partid": 1,  
"amount": "11111msat"  
},  
...

But what if a host that you had a channel with opened a channel with the intended recipient?

In that case, when you go to pay the invoice, it will _automatically work_!

c$ lightning-cli --testnet pay lntb111110p1p0cw43ppp5u0ngjytlw6ywec3x784jale4xd7h058g9u4mthcaf9rl2f7g8zxsdp2t9hh2gr0wajjqmt9ypnx7u3qv35kumn9wgs8gmm0yyxqyjw5qcqp2sp5kj4xhrthmfgcgyl84zaqpl9vvdjwm5x368kr09fu5nym74setw4s9qy9qsq8hxjr73ee77vat0ay603e4w9aa8ag9sa2n55xznk5lsfrjffxxdj2k0wznvcfa98l4a57s80j7dhg0cc03vwqdwehkujlzxgm0xyynqqslwhvl  
{  
"destination": "02f3d74746934494fa378235e5bc44cfdbb5b8779d839263fb7f9218be032f6f61",  
"payment_hash": "e3e689117f7688ece226f1eb2eff35337d77d0e82f2bb5df1d4947f527c8388d",  
"created_at": 1602709081.324,  
"parts": 1,  
"msatoshi": 11111,  
"amount_msat": "11111msat",  
"msatoshi_sent": 12111,  
"amount_sent_msat": "12111msat",  
"payment_preimage": "ec7d1b28a7b877cd92b83be396899e8bfc3ecb0b4f944f65afb4be7d0ee72617",  
"status": "complete"  
}

That's the true beauty of the Lightning Network there: with no effort from the peer-to-peer participants, their individual channels become a network!

> :book: _**How Do Payments Work Across the Network?**_ Say that node A has a channel open with node B, node B has a channel open with node C, and node A receives an invoice from node C for 11,111 msat. Node A pays node B the 11,111 msat, plus a small fee, and then node B pays the 11,111 msat to node C. Easy enough. Except remember that all channels actually are just records of who owns how much of the Funding Transaction. So what really happens is 11,111 msat of the Funding Transaction on channel A-B shifts from A to B, and then 11,111 msat of the Funding Transaction on channel B-C shifts from B to C. This means that two things are required for this payment to work: first, each channel must have sufficient capacity for the payment; and second, the payer on each channel must own enough of the capacity to make the payment.

Note that in this example, 12,111 msat were sent to pay an invoice of 11,111 msat: the extra being a very small, flat fee (not a percentage) that was paid to the intermediary.

## Check your Balance

Having successfully made a payment, you should see that your funds have changed accordingly.

Here's what funds looked like for the paying node following the initial payment of 10,000 satoshis:

c$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "confirmed",  
"blockheight": 1862856,  
"reserved": false  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": true,  
"state": "CHANNELD_NORMAL",  
"short_channel_id": "1862856x29x0",  
"channel_sat": 90000,  
"our_amount_msat": "90000000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

Note that the channel capacity remains at 100,000 satoshis (it never changes!), but that our_amount is now just 90,000 satoshis (or 90,000,000 msat).

After paying the second invoice, for 11,111 msat, the funds change again accordingly:

$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "confirmed",  
"blockheight": 1862856,  
"reserved": false  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": true,  
"state": "CHANNELD_NORMAL",  
"short_channel_id": "1862856x29x0",  
"channel_sat": 89987,  
"our_amount_msat": "89987000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

our_amount is now just 89,987 satoshis, having paid 11,111 msat plus a 1,000 msat fee.

## Summary: Paying a Invoice

Once you've got an invoice, it's easy enough to pay with a single command in Lightning. Even if you don't have a channel to a recipient, payment is that simple, provided that there's a route between you and the destination node.

## What's Next?

Continue "Using Lighting" with [§20.3: Closing a Channel](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_3_Closing_a_Channel.md).

# 20.3: Closing a Channel

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

In this chapter you'll learn how to close a channel using lightning-cli close command-line interface. Closing a channel means you and your counterparty will send their agreed-upon channel balance to the blockchain, whereby you must pay blockchain transaction fees and wait for the transaction to be mined. A closure can be cooperative or non-cooperative, but it works either way.

In order to close a channel, you first need to know the ID of the remote node; you can retrieve it in one of two ways.

## Find your Channels by Funds

You can use the lightning-cli listfunds command to see your channels. This RPC command displays all funds available, either in unspent outputs (UTXOs) in the internal wallet or locked up in currently open channels.

c$ lightning-cli --testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "confirmed",  
"blockheight": 1862856,  
"reserved": false  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": true,  
"state": "CHANNELD_NORMAL",  
"short_channel_id": "1862856x29x0",  
"channel_sat": 89987,  
"our_amount_msat": "89987000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

"message_flags": 1,  
"channel_flags": 2,  
"active": true,  
"last_update": 1595508075,  
"base_fee_millisatoshi": 1000,  
"fee_per_millionth": 1,  
"delay": 40,  
"htlc_minimum_msat": "1000msat",  
"htlc_maximum_msat": "280000000msat",  
"features": ""  
}

You could retrieve the ID of the 0th channel into a variable like this:

c$ nodeidremote=$(lightning-cli --testnet listfunds | jq '.channels[0] | .peer_id')

## Find your Channels with JQ

The other way to find channels to close is to the use the listchannels command. It returns data on channels that are known to the node. Because channels may be bidirectional, up to two nodes will be returned for each channel (one for each direction).

However, Lightning's gossip network is very effective, and so in a short time you will come to know about thousands of channels. That's great for sending payments across the Lightning Network, but less useful for discovering your own channels. To do so requires a bit of jq work.

First, you need to know your own node ID, which can be retrieved with getinfo:

c$ nodeid=$(lightning-cli --testnet getinfo | jq .id)  
c$ echo $nodeid  
"03240a4878a9a64aea6c3921a434e573845267b86e89ab19003b0c910a86d17687"  
c$

You can then use that to look through listchannels for any channels where your node is either the source or the destination:

c$ lightning-cli --testnet listchannels | jq '.channels[] | select(.source == '$nodeid' or .destination == '$nodeid')'  
{  
"source": "03240a4878a9a64aea6c3921a434e573845267b86e89ab19003b0c910a86d17687",  
"destination": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"short_channel_id": "1862856x29x0",  
"public": true,  
"satoshis": 100000,  
"amount_msat": "100000000msat",  
"message_flags": 1,  
"channel_flags": 0,  
"active": true,  
"last_update": 1602639570,  
"base_fee_millisatoshi": 1,  
"fee_per_millionth": 10,  
"delay": 6,  
"htlc_minimum_msat": "1msat",  
"htlc_maximum_msat": "99000000msat",  
"features": ""  
}

There's our old favorite 032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543 again, as the destination.

Once you know what you've got, you can store it in a variable:

c$ nodeidremote=$(lightning-cli --testnet listchannels | jq '.channels[] | select(.source == '$nodeid' or .destination == '$nodeid') | .destination')

## Close a Channel

Now that you have a remote node ID, you're ready to use the lightning-cli close command to close a channel. By default, it will attempt to close the channel cooperatively with the peer; if you want to close it unilaterally set the unilateraltimeout argument with the number of seconds to wait. (If you set it to 0 and the peer is online, a mutual close is still attempted.) For this example, you will attempt a mutual close.

c$ lightning-cli --testnet close $nodeidremote 0  
{  
"tx": "02000000011d3cf2126ae36e12be3aee893b385ed6a2e19b1da7f4e579e3ef15ca234d69660000000000ffffffff021c27000000000000160014d39feb57a663803da116402d6cb0ac050bf051d9cc5e01000000000016001451c88b44420940c52a384bd8a03888e3676c150900000000",  
"txid": "f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f",  
"type": "mutual"  
}

The closing transaction on-chain is [f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f](https://blockstream.info/testnet/tx/f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f).

It's this closing transaction that actually disburses the funds that were traded back and forth through Lightning transactions. This can be seen by examining the transaction:

$ bitcoin-cli --named getrawtransaction txid=f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f verbose=1  
{  
"txid": "f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f",  
"hash": "3a6b3994932ae781bab80e159314bad06fc55d3d33453a1d663f9f9415c9719c",  
"version": 2,  
"size": 334,  
"vsize": 169,  
"weight": 673,  
"locktime": 0,  
"vin": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"vout": 0,  
"scriptSig": {  
"asm": "",  
"hex": ""  
},  
"txinwitness": [  
"",  
"304402207f8048e29192ec86019bc83be8b4cac5d1fc682374538bed0707f58192d41c390220512ebcde122d53747feedd70c09153a40c56d09a5fec02e47642afdbb20aa2ac01",  
"3045022100d686a16084b60800fa0f6b14c25dca1c13d10a55c5fb7c6a3eb1c5f4a2fb20360220555f5b6e672cf9ef82941f7d46ee03dd52e0e848b9f094a41ff299deb8207cab01",  
"522102f7589fd8366252cdbb37827dff65e3304abd5d17bbab57460eff71a9e32bc00b210343b980dff4f2723e0db99ac72d0841aad934b51cbe556ce3a1b257b34059a17052ae"  
],  
"sequence": 4294967295  
}  
],  
"vout": [  
{  
"value": 0.00010012,  
"n": 0,  
"scriptPubKey": {  
"asm": "0 d39feb57a663803da116402d6cb0ac050bf051d9",  
"hex": "0014d39feb57a663803da116402d6cb0ac050bf051d9",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q6w07k4axvwqrmggkgqkkev9vq59lq5we5fcrzn"  
]  
}  
},  
{  
"value": 0.00089804,  
"n": 1,  
"scriptPubKey": {  
"asm": "0 51c88b44420940c52a384bd8a03888e3676c1509",  
"hex": "001451c88b44420940c52a384bd8a03888e3676c1509",  
"reqSigs": 1,  
"type": "witness_v0_keyhash",  
"addresses": [  
"tb1q28ygk3zzp9qv223cf0v2qwygudnkc9gfp30ud4"  
]  
}  
}  
],  
"hex": "020000000001011d3cf2126ae36e12be3aee893b385ed6a2e19b1da7f4e579e3ef15ca234d69660000000000ffffffff021c27000000000000160014d39feb57a663803da116402d6cb0ac050bf051d9cc5e01000000000016001451c88b44420940c52a384bd8a03888e3676c1509040047304402207f8048e29192ec86019bc83be8b4cac5d1fc682374538bed0707f58192d41c390220512ebcde122d53747feedd70c09153a40c56d09a5fec02e47642afdbb20aa2ac01483045022100d686a16084b60800fa0f6b14c25dca1c13d10a55c5fb7c6a3eb1c5f4a2fb20360220555f5b6e672cf9ef82941f7d46ee03dd52e0e848b9f094a41ff299deb8207cab0147522102f7589fd8366252cdbb37827dff65e3304abd5d17bbab57460eff71a9e32bc00b210343b980dff4f2723e0db99ac72d0841aad934b51cbe556ce3a1b257b34059a17052ae00000000",  
"blockhash": "000000000000002a214b1ffc3a67c64deda838dd24d12154c15d3a6f1137e94d",  
"confirmations": 1,  
"time": 1602713519,  
"blocktime": 1602713519  
}

The input of the transaction is 66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d, which was the funding transaction in [§19.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/19_3_Setting_Up_a_Channel.md). The transaction then has two outputs, one for the remote node and the other for the local core lightning wallet. The output on index 0 corresponds to the remote node with a value of 0.00010012 BTC; and the output on index 1 corresponds to the local node with a value of 0.00089804 BTC.

Lightning will similarly show 89804 satoshis returned as a new UTXO in its wallet:

$ lightning-cli --network=testnet listfunds  
{  
"outputs": [  
{  
"txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"output": 1,  
"value": 99847,  
"amount_msat": "99847000msat",  
"scriptpubkey": "00142fe02e5be9283e8c5bcb93ae61421baf8cb64f9c",  
"address": "tb1q9lszuklf9qlgck7tjwhxzssm47xtvnuu4jslf8",  
"status": "confirmed",  
"blockheight": 1862856,  
"reserved": false  
},  
{  
"txid": "f68de52d80a1076e36c677ef640539c50e3d03f77f9f9db4f13048519489593f",  
"output": 1,  
"value": 89804,  
"amount_msat": "89804000msat",  
"scriptpubkey": "001451c88b44420940c52a384bd8a03888e3676c1509",  
"address": "tb1q28ygk3zzp9qv223cf0v2qwygudnkc9gfp30ud4",  
"status": "confirmed",  
"blockheight": 1863006,  
"reserved": false  
}  
],  
"channels": [  
{  
"peer_id": "032a7572dc013b6382cde391d79f292ced27305aa4162ec3906279fc4334602543",  
"connected": false,  
"state": "ONCHAIN",  
"short_channel_id": "1862856x29x0",  
"channel_sat": 89987,  
"our_amount_msat": "89987000msat",  
"channel_total_sat": 100000,  
"amount_msat": "100000000msat",  
"funding_txid": "66694d23ca15efe379e5f4a71d9be1a2d65e383b89ee3abe126ee36a12f23c1d",  
"funding_output": 0  
}  
]  
}

### Understand the Types of Closing Channels.

The close RPC command attempts to close a channel cooperatively with its peer or unilaterally after the unilateraltimeout argument expires. This bears some additional discussion, as it goes to the heart of Lightning's trustless design:

Each participant of a channel is able to create as many Lightning payments to their counterparty as their funds allow. Most of the time there will be no disagreements between the participants, so there will only be two on-chain transactions, one opening and the other closing the channel. However, there may be scenarios in which one peer is not online or does not agree with the final state of the channel or where someone tries to steal funds from the other party. This is why there are both cooperative and forced closes.

#### Cooperative Close

In the case of a cooperative close, both channel participants agree to close the channel and settle the final state to the blockchain. Both participants must be online; the close is performed by broadcasting an unconditional spend of the funding transaction with an output to each peer.

#### Force Close

In the case of a force close, only one participant is online or the participants disagree on the final state of the channel. In this situation, one peer can perform an unilateral close of the channel without the cooperation of the other node. It's performed by broadcasting a commitment transaction that commits to a previous channel state that both parties have agreed upon. This commitment transaction contains the channel state divided in two parts: the balance for each participant and all the pending payments (HTLCs).

To perform this kind of close, you must specify an unilateraltimeout argument. If this value is not zero, the close command will unilaterally close the channel when that number of seconds is reached:

c$ lightning-cli --network=testnet close $newidremote 60  
{  
"tx": "0200000001a1091f727e6041cc93fead2ea46b8402133f53e6ab89ab106b49638c11f27cba00000000006a40aa8001df85010000000000160014d22818913daf3b4f86e0bcb302a5a812d1ef6b91c6772d20",  
"txid": "02cc4c647eb3e06f37fcbde39871ebae4333b7581954ea86b27b85ced6a5c4f7",  
"type": "unilateral"  
}

## Summary: Closing a Channel

When you close a channel you perform an on-chain transaction ending your financial relationship with the remote node To close a channel, you must take into account its status and the type of closure you want to execute.

## What's Next?

Continue "Using Lightning" with [§20.4: Expanding the Lightning Network](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/20_4_Lightning_Network_Review.md).

# 20.4: Expanding the Lightning Network

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

These two chapters have covered just a few of the most important activities with Lightning. There's lots more that can be done, and lots of variety possible. What follows are some pointers forward.

## Use core lightning Plugins

core lightning is a lightweight, highly customizable, and standard compliant implementation of the Lightning Network protocol. It extends it functionality using Plugins. Mainly, these are subprocesses that are initiated by the lightningd daemon and can interact with lightningd in a variety of ways:

- Command line options allow plugins to register their own command line arguments, which are then exposed through lightningd.
    
- JSON-RPC command passthrough allows plugins to add their own commands to the JSON-RPC interface.
    
- Event stream subscriptions provide plugins with a push-based notification mechanism for lightnind.
    
- Hooks are a primitive option that allows plugins to be notified about events in the lightningd daemon and modify its behavior or pass on custom behaviors.
    

A plugin may be written in any language and can communicate with lightningd through the plugin's stdin and stdout. JSON-RPCv2 is used as protocol on top of the two streams, with the plugin acting as server and lightningd acting as client.

The lightningd GitHub repo maintains a updated list of [plugins](https://github.com/lightningd/plugins) available.

## Use Mobile Wallets

We currently know of two mobile lightning wallets that support the core lightning implementation.

For iOS devices FullyNoded is an open-source iOS Bitcoin wallet that connects via Tor V3 authenticated service to your own full node. FullyNoded functionality is currently under active development and in early beta testing phase.

- [FullyNoded](https://github.com/Fonta1n3/FullyNoded/blob/master/Docs/Lightning.md)
    

SparkWallet is a minimalistic wallet GUI for core lightning, accessible over the web or through mobile and desktop apps for Android.

- [SparkWallet](https://github.com/shesek/spark-wallet)
    

## Use Different Lightning Implementations

core lightning isn't your only option. Today there are three widely used implementations of the Lightning Network. All of them follow the [Basis of Lightning Technology (BOLT) documents](https://github.com/lightningnetwork/lightning-rfc), which describe a layer-2 protocol for off-chain bitcoin transfers. The specifications are currently a work-in-progress that is still being drafted.

    
|Name|Description|BitcoinStandup|Language|Repository|
|---|---|---|---|---|
|C-lighting|Blockstream|X|C|[Download](https://github.com/ElementsProject/lightning)|
|LND|Lightning Labs|X|Go|[Download](https://github.com/lightningnetwork/lnd)|
|Eclair|ACINQ|-|Scala|[Download](https://github.com/ACINQ/eclair)|

  
  

## Maintain Backups

Your Lightning node needs to be online all the time, otherwise your counterparty could send a previous channel status and steal your funds. However, there is another scenario in which funds can be lost, and that is when a hardware failure occurs that prevents the node from establishing a cooperative closure with the counterparty. This will probably mean that if you do not have an exact copy of the state of the channel before the failure, you will have an invalid state that could cause the other node to assume it as an attempted fraud and use the penalty transaction. In this case, all funds will be lost. To avoid this undesirable situation a solution based on the high availability of postgresQL database [exists](https://github.com/gabridome/docs/blob/master/c-lightning_with_postgresql_reliability.md).

We haven't tested this solution.

## Summary: Expanding the Lightning Network

You can use different implementations, plugins, mobile wallets, or backups to expand your Lightning experience.

## What's Next?

You've completed Learning Bitcoin from the Command Line, though if you never visited the [Appendices](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A0_Appendices.md) of alternate setups, you can do so now.

Otherwise, we encourage you to join developer communities, to program, and to put your new knowledge to work.

You can also help us here at Blockchain Commons with Issues or PRs for Learning Bitcoin or for any of our other repos, or you can even become a [Sponsor](https://github.com/sponsors/BlockchainCommons). You can also help out by spreading the word: let people on social media know about the course and what you learned from it!

Now get out there and make the Blockchain community a better place!

# Appendices

The main body of this course suggests a fairly standard setup for Bitcoin testing. What follows in these appendices are a better explanation of that setup and some options for alternatives.

## Objectives for This Section

After working through these appendices, a developer will be able to:

- Decide among Multiple Methods for Creating a Bitcoin Blockchain
    

Supporting objectives include the ability to:

- Understand the Bitcoin Standup Setup
    
- Perform a Compilation of Bitcoin by Hand
    
- Understand the Power of Regtest
    
- Use a Regtest Environment
    

## Table of Contents

- [Appendix One: Understanding Bitcoin Standup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A1_0_Understanding_Bitcoin_Standup.md)
    
- [Appendix Two: Compiling Bitcoin from Source](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A2_0_Compiling_Bitcoin_from_Source.md)
    
- [Appendix Three: Using Bitcoin Regtest](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A3_0_Using_Bitcoin_Regtest.md)
    

# Appendix I: Understanding Bitcoin Standup

[§2.1: Setting Up a Bitcoin Core VPS with StackScript](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md) explains the process of creating a Bitcoin node using [Bitcoin-Standup-Scripts](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts). The following appendix explains what the major sections of the script do. You may wish to follow along in [Linode Standup](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) in another window.

## Step 1: Hostname

Your host's name is stored in /etc/hostname and set with the hostname command. It also appears in /etc/hosts.

## Step 2: Timezone

Your host's timezone is stored in /etc/timezone, then an appropriate file from /usr/share/zoneinfo/ is copied to /etc/localtime

## Step 3: Updating Debian

The apt-get package manager is used to bring your machine up to date and to install gnupg, git, the random-number generators haveged and xxd, and the uncomplicated firewall ufw.

The apt-get commands are run with -y, which should force all questions to be answered "yes", and allow the script to be run without interaction (e.g., as a StackScript). That failed with the Debian 13 update, with some questions going unanswered and locking up the script, so the -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" options were added to say, "We're really serious, no questions!"

Your machine is setup to automatically stay up to date with echo "unattended-upgrades unattended-upgrades/enable_auto_updates boolean true" | debconf-set-selections.

## Step 4: Setting Up a User

A standup user is created, which will be used for your Bitcoin applications. It also has sudo permissions, allowing you to take privileged actions with this account.

If you supplied a Standup SSH key, it will allow you access to this account (otherwise, you must use the password you created in setup).

If you supplied an IP address, ssh access will be limited to that address, per /etc/hosts.allow.

## Step 5: Setting Up Tor

Tor is installed to provide protected (hidden) services to access Bitcoin's RPC commands through your server. See [§14.1: Verifying Your Tor Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_1_Verifying_Your_Tor_Setup.md) for more information on your Tor Setup.

If you supplied an authorized client for the hidden services, access will be limited to that key, per /var/lib/tor/standup/authorized_clients. If you did not, [§14.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/14_2_Changing_Your_Bitcoin_Hidden_Services.md) explains how to do so at a later date.

## Step 6: Installing Bitcoin

Bitcoin is installed in ~standup/.bitcoin. Your configuration is stored in ~standup/.bitcoin/bitcoin.conf.

Be sure that the checksums verified per [§2.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md), otherwise you could be exposed to a supply-chain attack.

## Step 7: Installing QR Encoder

To keep everything compatible with [GordianSystem](https://github.com/BlockchainCommons/GordianSystem) a QR code is created at /qrcode.png. This can be read from a QuickConnect client such as [GordianWallet](https://github.com/BlockchainCommons/GordianWallet-iOS).

## Conclusion — Understanding Bitcoin Standup

Bitcoin Standup uses scripts to try and match much of the functionality of a [GordianNode](https://github.com/BlockchainCommons/GordianNode-macOS). It should provide you with a secure Bitcoin environment built on a foundation of Bitcoin Core and Tor for RPC communications.

## What's Next?

If you were in the process of creating a Bitcoin node for use in this course, you should return to [§2.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md).

If you are reading through the appendices, continue with [Appendix II: Compiling Bitcoin from Source](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A2_0_Compiling_Bitcoin_from_Source.md).

# Appendix II: Compiling Bitcoin from Source

This course presumes that you will use a script to create a Bitcoin environment, either using Bitcoin Standup for Linode per [§2.1](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_1_Setting_Up_a_Bitcoin-Core_VPS_with_StackScript.md), or via some other means per [§2.2](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_2_Setting_Up_Bitcoin_Core_Other.md). However, you may prefer to compile Bitcoin by hand.

This has the following benefits:

1. You will always be up-to-date with the latest release. Caveat: Being always updated is not necessary for Bitcoin Core since the software is always backwards compatible, meaning an old version of Bitcoin Core will still be able to participate in the Bitcoin network, though you may not have the latest features. You should always check the features of a new release before updating.
    
2. You won't need to depend on pre-compiled Bitcoin Core binaries. This requires less trust. Even though the maintainers of Bitcoin Core do a great job of maintaining the integrity of the code, a pre-compiled binary is a few steps removed from source code. When you compile from the source code, the code can be inspected before compilation.
    
3. You can customize the build, doing things such as disabling the wallet or the GUI.
    

## Prepare your Environment

This tutorial uses Debian 10.4.kv0 OS on an amd64 architecture(64-bit computers), but you can use this tutorial on any Debian based system (e.g. Ubuntu, Mint, etc.). For other Linux systems, you can adapt the following steps with the package manager for that system.

You can have basic or no familiarity with the command line as long as you have enthusiasm. The terminal is your most powerful ally, not something to be feared. You can simply copy and paste the following commands to compile bitcoin. (A command with a "$" is a normal user command, and one with a "#" is a super-user/root command.)

If your user is not in the sudoers list then do the following:

$ su root

# apt-get install sudo

# usermod -aG sudo

# reboot

## Install Bitcoin

### Step 1: Update Your System

First, update the system using:

$ sudo apt-get update

### Step 2: Install Git and Dependencies

Install git, which will allow you to download the source code, and build-essential, which compiles the code:

$ sudo apt-get install git build-essential -y

Afterward, install remaining dependencies:

$ sudo apt-get install libtool autotools-dev automake pkg-config bsdmainutils python3 libssl-dev libevent-dev libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libminiupnpc-dev libzmq3-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler ccache -y

### Step 3: Download the Source Code

Once the dependencies are installed, download the repository (repo) containing the Bitcoin source code from github:

$ git clone [https://github.com/bitcoin/bitcoin.git](https://github.com/bitcoin/bitcoin.git)

Check the contents of the repo:

$ ls bitcoin

It should approximately match the following contents:

![](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/public/LBftCLI-compiling_bitcoin-git.png)

### Step 4: Install Berkley DB v4.8

1. Enter contrib directory: $ cd bitcoin/contrib/
    
2. Run the following command: $ ./install_db4.sh pwd
    

Once it's downloaded you should see the following output. Take note of the output, you will use it to configure bitcoin while building:

![](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/public/LBftCLI-compiling_bitcoin-db4.png)

### Step 5: Compile Bitcoin Core

It is recommended that you compile from a tagged branch, which is more stable, unless you want to try the bleeding edge of bitcoin development. Run the following command to get the list of tags, ordered from the most recent:

$ git tag -n | sort -V

Then choose a tag such as v0.20.0:

$ git checkout

Once you've selected a tag branch, execute the following from inside the bitcoin directory. The should be the output of the install_db4.sh script.

$ ./autogen.sh  
$ export BDB_PREFIX='/db4'  
$ ./configure BDB_LIBS="-L${BDB_PREFIX}/lib -ldb_cxx-4.8" BDB_CFLAGS="-I${BDB_PREFIX}/include"  
$ make # build bitcoin core

### Step 6: Test the Build

If you want to check your build (which is a good idea), run the following tests:

1. $ make check will run Unit Tests, which should all return PASS.
    
2. $ test/functional/test_runner.py --extended will run extended functional tests. Omit --extended flag if you want to skip a few tests. This will take a while.
    

### Step 7: Run or Install Bitcoin Core

Now that you have compiled Bitcoin Core from source, you can start using it or install it for global availability.

#### Run Bitcoin Core without Installing

To just run Bitcoin Core:

$ src/qt/bitcoin-qt to launch the GUI. $ src/bitcoind to run bitcoin on the command line.

### Install Bitcoin Core

To install:

$ sudo make install will install bitcoin core globally. Once installed you can then run bitcoin from anywhere in the command line, just as any other software like so: $ bitcoin-qt for the GUI or bitcoind and then bitcoin-cli for command line.

## Finalize Your System

By compiling Bitcoin from source, you've increased the trustlessness of your setup. However, you're far short of all the additional security provided by a Bitcoin Standup setup. To resolve this, you may want to walk through the entire [Linode Stackscript](https://github.com/BlockchainCommons/Bitcoin-Standup-Scripts/blob/master/Scripts/LinodeStandUp.sh) and step-by-step run all the commands. The only place you need to be careful is in Step 6, which installs Bitcoin. Skip just past where you've verified your binaries, and continue from there.

## Summary: Compiling Bitcoin from Source

If you wanted the increased security of installing Bitcoin from source, you should now have that. Hopefully, you've also gone through the Linode Stackscript to set up a more secure server.

## What's Next?

If you were in the process of creating a Bitcoin node for use in this course, you should continue on with [Chapter 3: Understanding Your Bitcoin Setup](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/03_0_Understanding_Your_Bitcoin_Setup.md).

If you are reading through the appendices, continue with [Appendix III: Using Bitcoin Regtest](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A3_0_Using_Bitcoin_Regtest.md).

# Appendix III: Using Bitcoin Regtest

> :information_source: **NOTE:** This section has been recently added to the course and is an early draft that may still be awaiting review. Caveat reader.

The majority of this course presumes that you will either use the Mainnet or Testnet. However, those aren't the only choices. While developing Bitcoin applications, you might want to keep your applications isolated from these public blockchains. To do so, you can create a blockchain from scratch using the Regtest, which has one other major advantage over Testnet: you choose when to create new blocks, so you have complete control over the environment.

## Start Bitcoind on Regtest

After [setting up your Bitcoin-Core VPS](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/02_0_Setting_Up_a_Bitcoin-Core_VPS.md) or [compiling from source](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/A2_0_Compiling_Bitcoin_from_Source.md), you are now able to use regtest. To start your bitcoind on regtest and create a private Blockchain, use the following command:

$ bitcoind -regtest -daemon -fallbackfee=1.0 -maxtxfee=1.1

The arguments -fallbackfee=1.0 -maxtxfee=1.1 will prevent the Fee estimation failed. Fallbackfee is disabled error.

On regtest, usually there are not enough transactions so bitcoind cannot give a reliable estimate and, without it, the wallet will not create transactions unless it is explicitly set the fee.

### Reset the Regtest Blockchain

If you wish, you can later restart your Regtest with a new blockchain.

Regtest wallets and blockchain state (chainstate) are saved in the regtest subdirectory of the Bitcoin configuration directory:

user@mybtc:~/.bitcoin# ls  
bitcoin.conf regtest testnet3

To start a brand new Blockchain using regtest, all you have to do is delete the regtest folder and restart the Bitcoind:

$ rm -rf regtest

## Generate Regtest Wallet

Before generating blocks, it is necessary to load a wallet using loadwallet or create a new one with createwallet. Since version 0.21, Bitcoin Core does not automatically create new wallets on startup.

The argument descriptors=true creates a native descriptor wallet, that stores scriptPubKey information using output descriptors. If it is false, it will create a legacy wallet, where keys are used to implicitly generate scriptPubKeys and addresses.

$ bitcoin-cli -regtest -named createwallet wallet_name="regtest_desc_wallet" descriptors=true

## Generate Blocks

You can generate (mine) new blocks on a regtest chain using the RPC method generate with an argument for how many blocks to generate. It only makes sense to use this method on regtest; due to the high difficulty it's very unlikely that it will yield to new blocks on the mainnet or testnet:

$ bitcoin-cli -regtest -generate 101  
[  
"57f17afccf28b9296048b6370312678b6d8e48dc3a7b4ef7681d18ed3d91c122",  
"631ff7b8135ce633c774828be3b8505726459eb65c339aab981b10363befe5a7",  
...  
"1162dbfe025c7da94ee1128dc26d518a94508f532c19edc0de6bc673a909d02c",  
"20cb2e815c3d42d6a117a204a0b5e726ab641c826e441b5b3417aca33f2aba48"  
]

> :warning: WARNING. Note that you must add the -regtest argument after each bitcoin-cli command to correctly access your Regtest environment. If you prefer, you can include a regtest=1 command in your ~/.bitcoin/bitcoin.conf file.

Because a block must have 100 confirmations before that reward can be spent, you generate 101 blocks, providing access to the coinbase transaction from block #1. Because this is a new blockchain using Bitcoin’s default rules, the first blocks pay a block reward of 50 bitcoins. Unlike mainnet, in regtest mode only the first 150 blocks pay a reward of 50 bitcoins. The reward halves after 150 blocks, so it pays 25, 12.5, and so on...

The output is the block hash of every block generated.

> :book: _**What is a coinbase transaction?**_ A coinbase is the inputless transaction created when a new block is mined and given to the miner. It's how new bitcoins enter the ecosystem. The value of coinbase transactions decay over time. On the mainnet, it halves every 210,000 blocks and ends entirely with the 6,929,999th block, which is currently predicted for the 22nd century. As of May 2020, the coinbase reward is 6.25 BTC.

### Verify Your Balance

After mining blocks and getting the rewards, you can verify the balance on your wallet:

$ bitcoin-cli -regtest getbalance  
50.00000000

## Use the Regtest

Now you should be able to use this balance for any type of interaction on your private Blockchain, such as sending Bitcoin transactions according to [Chapter 4](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/\(04_0_Sending_Bitcoin_Transactions.md\)).

It is important to note that for any transactions to complete, you will have to generate (mine) new blocks, so that the transactions can be included.

For example, to create a transaction and include it in a block, you should first use the sendtoaddress command:

$ bitcoin-cli -regtest sendtoaddress [address] 15.1  
e834a4ac6ef754164c8e3f0be4f34531b74b768199ffb244ab9f6cb1bbc7465a

The output is the transaction hash included in the blockchain. You can verify the details using the gettransaction:

$ bitcoin-cli -regtest gettransaction e834a4ac6ef754164c8e3f0be4f34531b74b768199ffb244ab9f6cb1bbc7465a  
{  
"amount": 0.00000000,  
"fee": -0.00178800,  
"confirmations": 0,  
"trusted": false,  
"txid": "e834a4ac6ef754164c8e3f0be4f34531b74b768199ffb244ab9f6cb1bbc7465a",  
"walletconflicts": [  
],  
"time": 1513204730,  
"timereceived": 1513204730,  
"bip125-replaceable": "unknown",  
"details": [  
{  
"account": "",  
"address": "mjtN3C97kuWMgeBbxdB7hG1bjz24Grx2vA",  
"category": "send",  
"amount": -15.10000000,  
"label": "",  
"vout": 1,  
"fee": -0.00178800,  
"abandoned": false  
},  
{  
"account": "",  
"address": "mjtN3C97kuWMgeBbxdB7hG1bjz24Grx2vA",  
"category": "receive",  
"amount": 15.10000000,  
"label": "",  
"vout": 1  
}  
],  
"hex": "020000000f00fe2c7b70b925d0d40011ce96f8991fee5aba9537bd1b6913b37c37b041a57c00000000494830450221009ad02bfeee2a49196a99811ace20e2e7fefd16d33d525884edbc64bf6e2b1db502200b94f4000556391b0998932edde3033ba2517733c7ddffb87d91f6b756629fe201feffffff06a9301a2b39875b68f8058b8e2ad0b658f505e44a67e1e1d039140ae186ed1f0000000049483045022100c65cd13a85af6fcfba74d2852276a37076c89a7642429aa111b7986eea7fd6c7022012bbcb633d392ed469d5befda8df0a6b96e1acfa342f559877edebc2af7cb93401feffffff434b6f67e5e068401553e89f739a3edc667504597f29feb8edafc2b081cc32d90000000049483045022100b86ecc43e602180c787c36465da7fc8d1e8bfba23d6f49c37190c20889f2dfa0022032c3aec3ceefbb7a33c040ef19090cacbfd6bc9c5cd8e94252eb864891c6f34501feffffff4c65b43f8568ce58fc4c55d24ba0742e9878a031fdfae0fadac7247f42cc1f8e0000000049483045022100d055acfce852259dde051dc61792f94277d094c5da96752f925582b8e739868f02205e69add76e6b001073ad6b7df5f32a681fc8513ee0f6e126ee1c2d45149bd91d01feffffff5a72d60b58300974c5d4731e29b437ea61b87b6733bb3ca6ce5548ef8887d05b0000000049483045022100a7f5b2ee656a5a904fb27f982210de6858dfb165777ec969a77ea1c2c82975a4022001a1a563dbc3714047ec855f7aee901e756b851e255f35435e85c2ba7b0abd8401feffffff60d68e9d5650d55bc9e0b2a65ed27a3b9bceac4955760aa1560408854c3b148d000000004948304502210081a6f0c8232c52f3eaca825965077e88b816e503834989be4afb3f44f87eb98202207ae8becb99efe379fb269f477e7bb70d117dcb83e106c53b7addaa9715029da101feffffff63e2239425aad544f6e1157d5ee245d2500d4e9e9daf8049e0a38add6246da890000000049483045022100e0ab1752e8fbb244b63f7dd5649f2222e0dc42fae293b758e0c28082f77560b60220013f72fbe50acf4af197890b4d18fa89094055ed66f9226a6b461cc4ff560f8e01feffffff6aad4151087f4209ace714193dd64f770305dfb89470b79cca538b88253fbbef0000000049483045022100fee4a5f7ec6e8b55bd6aa0e93b5399af724039171d998b926e8095b70953d5f202203db0d4ef9d1bd57aeff0fe3d47d4358ec0559135dac8107507741eef0638279201feffffff7ddbca5854e25e6a2dfeacfe5828267cd1ef5d86e1da573fe2c2b21b45ecd6ce0000000049483045022100bf45241525592df4625642972dbc940ef74771139dd844bc6a9517197d01488c02203c99ca98892cc2693e8fbb9a600962eec84494fb8596acf0d670822624e497c901feffffff8672949de559e76601684c4ac3731599fd965d0c412e7df9f8ec16038d4420a60000000049483045022100b5a9bd3c6718c6bd2a8300bbd1d9de0ff1c5d02aeb6a659c52bb88958e7e3b0302207f710db1ef975c22edf54e063169aae31bbe470166cc0e5c34fd27b730b8e7d001feffffff8e006b0bb8cef2c5c2a11c8c2aa7d3ba01cb4386c7f780c45bc1014142b425f00000000048473044022046dc9db8daeb09b7c0b9f48013c8af2d0a71f688adaa8d91b40891768c852d4a02204fa15da6d58851191344a56c63bf51a540ec03f73117a3446230bb58a8a4bcce01feffffffbad05b8f86182b9b7c9c5aaa9ce3dc8d08a76848e49a2d9b8dcfb0f764bb26ca000000004847304402200682379dc36cb486309eac4913f41ac19638525677edad45ca8d9a2b0728b12f02203fb44f8a46cbc4c02f5699d7d4d9cd810bdf7e7c981b421218ccbcb7b73845f501feffffffd35228fe9ef0a742eacffc4a13f15ed7ba23854e6cb49d5010810ac11b5bdf690000000048473044022030045b882500808bd707f4654becc63de070818c82716310d39576decdd724e3022034d3b41cb5e939f0011bb5251be7941b6077fde5f4eff59afd8e49a2844288f701fefffffff5ae4cbd4ae8d68b5a34be3231cdc88b660447175f39cf7a86397f37641d4aa70000000049483045022100afe16f0de96a8629d6148f93520d690f30126c37e7f7f05300745a1273d7eb7202200933f6b371c4ea522570f3ec2aee9be2b59730b634e828f543bcdb019cf4749901fefffffff633f61ac61683221cc3d2665cf4bcf193af1c8ffe9d3d756ba83cc5eb7643250000000049483045022100ef0b8853c94d60634eff2fc1d4d75872aacb0a2d3242308b7ee256b24739c614022069fe9be8288bdd635871c263c46be710c001729d43f6fbc1350ed1a693c4646301feffffff0250780000000000001976a91464ed7fb2fe0b06f4cad0d731b122222e3e91088a88ac80c5005a000000001976a9142fed0f02d008f89f6a874168e506e2d4f9bcbfb888acd32b0000"  
}

However, you must now finalize it by creating blocks on the blockchain. Most applications require six block confirmations to consider the transaction as irreversible. If that is your case, you can mine additional six blocks into your regtest chain:

$ bitcoin-cli -regtest -generate 6  
[  
"33549b2aa249f0a814db4a2ba102194881c14a2ac041c23dcc463b9e4e128e9f",  
"2cc5c2012e2cacf118f9db4cdd79582735257f0ec564418867d6821edb55715e",  
"128aaa99e7149a520080d90fa989c62caeda11b7d06ed1965e3fa7c76fa1d407",  
"6037cc562d97eb3984cca50d8c37c7c19bae8d79b8232b92bec6dcc9708104d3",  
"2cb276f5ed251bf629dd52fd108163703473f57c24eac94e169514ce04899581",  
"57193ba8fd2761abf4a5ebcb4ed1a9ec2e873d67485a7cb41e75e13c65928bf3"  
]

## Test with NodeJS

When you are on regtest, you are able to simulate edge cases and attacks that might happen in the real world, such as double spend.

As discussed elsewhere in this course, using software libraries might give you more sophisticated access to some RPC commands. In this case, [bitcointest by dgarage](https://github.com/dgarage/bitcointest) for NodeJS can be used to simulate a transaction from one wallet to another; you can check [their guide](https://www.npmjs.com/package/bitcointest) for more specific attack simulations, such as double spend.

See [§18.3](file:///Users/manuel/Learning-Bitcoin-from-the-Command-Line-master/18_3_Accessing_Bitcoind_with_NodeJS.md) for the most up-to-date info on install NodeJS, then add bitcointest:

$ npm install -g bitcointest

After installing bitcointest, you can create a test.js file with the following content:

file: test.js

const { BitcoinNet, BitcoinGraph } = require('bitcointest');  
const net = new BitcoinNet('/usr/local/bin', '/tmp/bitcointest/', 22001, 22002);  
const graph = new BitcoinGraph(net);

try {

console.log('Launching nodes...');

const nodes = net.launchBatchS(4);  
const [ n1, n2 ] = nodes;  
net.waitForNodesS(nodes, 20000);

console.log('Connected!');  
const blocks = n1.generateBlocksS(110);  
console.info('Generated 110 blocks');

console.log(n2.balance (before) = ${n2.getBalanceS()});

const sometxid = n1.sendToNodeS(n2, 100);  
console.log(Generated transaction = ${sometxid});  
n1.generateBlocksS(110);  
n2.waitForBalanceChangeS(0);

const sometx = n2.getTransactionS(sometxid);  
console.log(n2.balance (after) = ${n2.getBalanceS()});

} catch (e) {  
console.error(e);  
net.shutdownS();  
throw e;  
}

As shown, this will generate blocks and a transaction:

$ node test.js  
Launching nodes...  
Connected!  
Generated 110 blocks  
n2.balance (before) = 0  
Generated transaction = 91e0040c26fc18312efb80bad6ec3b00202a83465872ecf495c392a0b6afce35  
n2.after (before) = 100

## Summary: Using Bitcoin Regtest

A regtest environment for Bitcoin works just like any testnet environment, except for the fact that you have the ability to easily and quickly generate blocks.

> :fire: _**What is the power of regtest?**_ The biggest power of regtest is that you can quickly mine blocks, allowing you to rush the blockchain along, to test transactions, timelocks, and other features that you'd otherwise have to sit around and wait on. However, the other power is that you can run it privately, without connecting to a public blockchain, allowing you to test our proprietary ideas before releasing them into the world.

## What's Next?

If you visited this Appendix while working on some other part of the course, you should get back there.

But otherwise, you've reached the end! Other people who have worked their way through this course have become professional Bitcoin developers and engineers, including some of whom have contributed to [Blockchain Commons](https://www.blockchaincommons.com/). We encourage you to do the same! Just get out there are start working on some of your own Bitcoin code with what you learned.