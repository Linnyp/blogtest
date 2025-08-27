---
title: "What Are Runes: runestones, etching, and minting"
description: "Quick step-by-step guide on setting up an Ordinals compatible wallet."
author: "Linax"
authorAvatar: "https://raw.githubusercontent.com/Linnyp/blogtest/main/images/avatars/linax.png"
date: "2025-08-25"
category: "Guides"
heroImage: "https://raw.githubusercontent.com/Linnyp/blogtest/main/images/heroes/bitcoinrunesFontBlk.png"
featured: false
seoKeywords:
  [
    "bitcoin ordinals wallet",
    "ordinals wallet setup",
    "xverse wallet",
    "unisat wallet",
    "bitcoin wallet guide",
  ]
lastUpdated: "2025-08-25"
---

## Introduction

In the world of Bitcoin, innovation doesn’t stop at simple payments. Over the past few years, projects like **Ordinals** have shown us that Bitcoin can host digital collectibles similar to NFTs on Ethereum. But as the ecosystem grows, new systems are emerging to give users even more tools to create and trade digital assets. One of the most promising of these systems is called **Runes**.

Runes make it possible to create **fungible tokens** — interchangeable units like meme coins or community tokens — directly on Bitcoin. This expands Bitcoin’s role beyond Ordinals (which are non-fungible and unique) and brings it into the same conversation as platforms like Ethereum, Solana, and others where fungible tokens have fueled massive ecosystems.

If you’ve ever wondered how meme coins or community tokens might work on Bitcoin, or what makes Runes different from Ordinals, this guide breaks it down in simple terms.

## What Exactly Are Runes?

At a high level, **Runes are Bitcoin-native digital tokens**. Unlike Ordinals inscriptions, which are unique and one-of-a-kind like NFTs, runes are interchangeable and identical. This makes them useful for things like meme coins, loyalty points, in-game currencies, or even experimental decentralized finance on Bitcoin.

Every rune is managed through something called a **Runestone**, which is just the protocol message stored inside a Bitcoin transaction. These runestones record instructions like creating a new rune, minting more of an existing one, or transferring runes between people.

Think of runestones as the “spellbooks” that tell the Bitcoin blockchain how runes should exist and move around.

## How Runes Are Created: Etching

Runes don’t just appear out of nowhere — they have to be **etched** into existence. Etching is like creating the blueprint for a new token. When someone etches a rune, they decide its permanent properties, such as:

- **Name** – The rune’s name, made up of letters A–Z, up to 26 characters. Example: “UNCOMMONGOODS.” Names can also include small spacers (like •) for readability.
- **Divisibility** – How small the rune can be divided, like decimal places for money. A divisibility of 0 means no splitting, while a divisibility of 2 means you can split it into hundredths.
- **Symbol** – An optional icon or character that represents the rune, like $, 🧿, or any Unicode symbol. If none is chosen, a default “¤” scarab is used.
- **Premine** – Whether the creator allocates some of the rune to themselves at the beginning.
- **Terms** – Rules that control whether new units of the rune can be created, such as block height limits, caps, or open minting windows.

Once a rune is etched, these properties are **set in stone** — they can never be changed, even by the original creator.

## Minting Runes

After a rune has been etched, new units can be created through a process called **minting**. Minting is like pressing new coins in a factory.

If the rune has **open minting terms**, anyone can mint new units by making the right kind of transaction, as long as the conditions (like block height, cap, or fixed amount per mint) are still valid.

For example:

- A rune might allow minting only between block 800,000 and 810,000.
- Each mint might create 100 new units.
- Once a cap of 1,000,000 units is reached, minting stops forever.

This system ensures that runes can have scarcity and predictable supply — important features for both collectibles and fungible tokens.

## Transferring and Using Runes

Once runes exist, they can be transferred between users, just like Bitcoin. Every transaction involving runes uses a runestone to define how those tokens move from the inputs to the outputs.

Special instructions called **edicts** can tell the blockchain exactly how to allocate runes across different outputs. And if no specific instructions are given, the runes default to going to the first usable output in the transaction.

Runes can even be **burned** — permanently destroyed — by sending them to an unspendable address (an OP_RETURN). Burning can be used as a supply control tool or for symbolic community gestures.

## Risks and Edge Cases: Cenotaphs

Not every runestone works perfectly. Sometimes they can be malformed, due to errors or intentional upgrades to the protocol. These broken runestones are called **cenotaphs**.

When a cenotaph occurs:

- Runes going into that transaction may be burned.
- Runes etched during it may become unmintable.
- Mint attempts may count toward a cap but produce no usable runes.

In practice, cenotaphs act as a kind of **upgrade mechanism**, letting the system evolve without tricking old versions of the software into misinterpreting data.

## Why Runes Matter

So why are Runes important in the broader Bitcoin ecosystem?

- **Expanding Bitcoin’s Utility** – They allow fungible tokens, similar to ERC-20 tokens on Ethereum, but on the Bitcoin blockchain.
- **Fuel for Meme Coins** – Just as Dogecoin or Pepe coins found communities, Bitcoin-native meme coins could explode through Runes.
- **Community & Gaming Tokens** – Runes could power community economies, loyalty systems, or in-game assets.
- **DeFi Potential** – While still experimental, Runes could open the door to decentralized finance applications on Bitcoin.

In short, Runes are about **broadening what Bitcoin can do**, beyond store-of-value and NFTs, into a full-fledged digital asset ecosystem.

## Conclusion

Runes bring fungible tokens to Bitcoin in a way that complements the rise of Ordinals. While Ordinals focus on **unique digital artifacts**, Runes make it possible to create and trade **interchangeable tokens** — perfect for meme coins, gaming, and new kinds of community-driven experiments.

Through **runestones**, Bitcoin transactions can etch new runes, mint supply under set rules, and transfer them across the network. And while technical details like edicts, pointers, and cenotaphs keep things precise, the big picture is simple: Runes are Bitcoin’s answer to the question, _“What about tokens?”_

As the ecosystem develops, Runes may play a key role in expanding Bitcoin from the world’s most secure blockchain into the foundation of an even richer digital economy.
