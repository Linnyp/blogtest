---
title: "What Are Bitcoin Ordinals & How We Go Here? A Beginner's Guide"
description: "Learn the what when and why about Bitcoin Ordinals as we take you on a trip down crypto ar memory lane..."
author: "Linax"
date: "2025-08-04"
readTime: "5 min read"
category: "Guides"
tags: ["Bitcoin", "Ordinals", "Ethereum", "NFT"]
heroImage: "https://raw.githubusercontent.com/Linnyp/blogtest/main/images/heroes/bitcoincabinet.jpg"
featured: false
difficulty: "Beginner"
seoKeywords:
  [
    "evm payments",
    "mint bitcoin ordinals",
    "ethereum payments",
    "usdc usdt",
    "cross-chain minting",
  ]
lastUpdated: "2025-08-04"
tableOfContents: true
newsletter: true
comments: true
socialSharing: true
---

## Introduction

If you've landed here on this article, you're probably already familiar with NFTs, but for those who've not yet had the pleasure of colliding with this new world, let's set the stage. NFT stands for "Non-Fungible Token" — essentially a digital certificate of ownership that says "I own this specific digital item." Like a deed to a house, but for digital art, music, or collectibles. The "non-fungible" part just means each digital certificate is unique and can't be replaced with something else of equal value.

The year was 2021, NFTs exploded into the mainstream, promising to solve a fundamental problem: how do you prove ownership of something digital? After all, digital files can be copied infinitely. NFTs offered a solution by creating a permanent record on the blockchain that says "Person X owns digital item Y."

Anyone online during this time invariably saw NFTs being talked about. Headlining articles from major news outlets, social feeds full of colorful cartoon monkey profile pictures (PFPs), and hordes of prominent figures ranging from celebrities to corporate brands like Nike all rushing to take part.

Sunshine and rainbows, except for one fundamental flaw.

You may be saying, "Okay, so I have a certificate that says I own this cool little art image and some directions to where the image is actually located, but where IS it actually being stored?"

Most NFTs — especially those on Ethereum and other similar smart contract networks — don't actually store the digital content on the blockchain itself. Instead, they store a link that points to where the content is hosted, usually on centralized servers or distributed systems like IPFS. Your expensive NFT? It's essentially a very expensive bookmark.

Here's the problem: imagine you buy an expensive NFT today. Six months later, you go to show it off, but instead of your digital art, you see an error message that says "image not found." What happened? The website hosting your image went offline. Maybe the company behind the project shut down, or they stopped paying their web hosting fees. The NFT that pointed to your digital collectable now points to digital nothing.

In comes ol' faithful, Bitcoin. What if there was a way to store digital content directly on the blockchain itself without relying on centralized third parties? What if your digital art didn't just have a certificate of ownership, but actually lived permanently on the most secure network ever created?

Welcome to the world of Bitcoin Ordinals — where your digital art isn't just linked to the blockchain, it literally lives there forever. This isn't just an incremental improvement; it's a fundamental reimagining of what digital ownership can be. Let's explore the most significant development in digital ownership since the invention of the blockchain itself.

## The Story of Digital Ownership (Or: How We Got Here)

![Bored Ape compared to painting |style:full-width|caption:Found in top right corner of your browser](https://raw.githubusercontent.com/Linnyp/blogtest/main/images/article/storyofownership.png)

### The Early Days: Colored Coins and Counterparty

Let's rewind to 2012. Bitcoin was still this quirky internet money, with a wildly fragmented user base consisting of cypherpunks, pizza enthusiasts, and Silk Road entrepreneurs. The term NFT was not a thing yet but some curious minds were already pondering: "What if we could represent OTHER things on the blockchain, not just money?"

Enter colored coins — the original attempt at creating non-fungible (unique) digital assets using Bitcoin. These were regular bitcoins that were "colored" with special meaning, representing everything from company shares to baseball cards.

Shortly after, in 2014 came Counterparty, building on top of ideas laid down by colored coins. Counterparty brought a slightly more structured project that added additional features.

Brick by brick we were getting closer to something special right on Bitcoin, but there was one big problem: these emerging new technologies were by no means user-friendly. The idea was solid, but the execution and timing just made it out of reach for most outside of niche developers and tech wizards, eventually sending the entire concept of digital artifacts back into obscurity.

### The NFT Explosion: Boom & Doom

Fast forward a bit to 2017-18, the crypto landscape is rapidly changing. Ethereum had entered the ring as something fundamentally different from Bitcoin. While Bitcoin was designed to be "digital gold" — a store of value and payment system — Ethereum introduced programmable money through smart contracts. Think of smart contracts as tiny computer programs that automatically execute agreements when certain conditions are met, without needing a middleman.

This was revolutionary because it meant you could build applications on top of the blockchain, not just send money. Suddenly, developers could create digital tokens that represented anything: company shares (ico), voting rights (dao), or even unique digital collectibles (nft). Ethereum became like a global computer that anyone could use to build decentralized applications.

The foundation for modern digital collectibles was silently expanding with legendary projects such as Cryptopunks and Cryptokitties launching on Ethereum, first formalizing the term "NFT" and sending small ripples through the crypto ecosystem. Upcoming key players like OpenSea, a soon-to-be leading NFT exchange platform, were positioning themselves and beginning to paint a vague landscape of digital collectibles on Ethereum.

A few years of relative silence, broken by the loud smack of DeFi summer 2020.

Helping fuel the mania we were seeing in the markets, DeFi provided one of the greatest real world use cases to Ethereum and decentralized permissionless networks to date. Using the new capabilities Ethereum brought to the table allowed ways for people to buy, sell, and exchange their cryptocurrencies in a more direct and decentralized manner, shaking up the traditional central exchange model that currently existed. With this came mass attention to Ethereum.

During this time, notable NFT collections like Bored Ape Yacht Club were being created, but the real turning point came when artist Beeple sold his digital artwork "Everydays: The First 5000 Days" at Christie's Auction House for a staggering $69 million. This single sale launched NFTs into mainstream consciousness and marked the beginning of the global NFT craze.

Here's where things get dicey...

While countless collections of NFTs swept the scene, there was an elephant in the room not many were addressing. Most NFTs aren't actually stored on the Ethereum blockchain.

Mind-blowing, right? That 5-figure Bored Ape? The actual image is probably sitting on some server, and your NFT is basically a fancy receipt that says "I own the thing over there" _points vaguely in the direction of the internet_.

This created some... shall we say, interesting situations:

**The Vanishing Act**: Images disappearing when servers go down

**The Rug Pull**: Creators pulling content offline (intentionally or not)

**The Centralization Trap**: Your "decentralized" asset depending on centralized servers

It's like buying a car but only getting a piece of paper with a picture that says "car" while the actual car stays in someone else's garage. Sure, you "own" it, but do you really?

Into the picture steps Casey Rodarmor with a solution to stir up the pot.

## What Are Bitcoin Ordinals?

Unlike traditional NFTs which are like getting a certificate that says "You own this artwork" — but the actual image is stored on someone else's computer server, Bitcoin Ordinals are like having the artwork permanently etched into an indestructible vault that can never be lost, stolen, or destroyed.

Here's the simple definition: Bitcoin Ordinals are digital artifacts that are permanently inscribed directly onto the Bitcoin blockchain. Not linked to it, not referenced by it, but carved into it.

Think of it this way:
• **Traditional NFTs**: "I own the receipt for that digital art over there"
• **Bitcoin Ordinals**: "The digital art IS permanently part of my Bitcoin"

### The Magic Behind the Madness

Here's where it gets beautifully nerdy. Every single Bitcoin is divisible by tiny units called satoshis (named after Bitcoin's mysterious creator, Satoshi Nakamoto). 1 Bitcoin equals 100 million satoshis. Much like how 1 dollar equals 100 pennies.

Casey Rodarmor had this idea: "What if we number every single satoshi in order of when it was mined, and then attach data to specific satoshis?"

It's like giving every grain of sand on a beach a unique ID number based on the order the grain of sand entered the beach, then writing a tiny story on each grain. Except these grains are digital, the beach is the Bitcoin blockchain, and the stories are permanent.

### Meet Casey Rodarmor: A Dude, An Idea

Initially setting out to release his art in the form of Ethereum NFTs, Bitcoining artist and developer Casey Rodarmor was confronted with the fundamental centralization issues NFTs on Ethereum faced.

With this moral dilemma of hosting his art on a platform where collectors did not own the actual art, he looked back to Bitcoin for a solution, and so Bitcoin Ordinals Protocol was born.

A system designed to number each satoshi (grain of sand). This new simple system alongside some more modern-day upgrades to Bitcoin enabled for the first time a truly viable solution for digital artifacts on Bitcoin.

## The Technology Behind Ordinals (Basically)

![flow chart of Ordinal creation process|style:full-width|caption:Flowchart of Bitcoin Ordinal creation](https://raw.githubusercontent.com/Linnyp/blogtest/main/images/screenshots/connect-wallet-button.png)

### Understanding Satoshis: Bitcoin's Tiny Building Blocks

Remember how we mentioned that every Bitcoin is made up of 100 million satoshis? Here's a slightly deeper look into how:

The Bitcoin Ordinals Protocol takes every single satoshi that has ever been created and assigns it a unique identification number based on the exact order it was created. Think of it like giving every satoshi its own serial number - the first satoshi ever created gets number 1, the second gets number 2, and so on. Before this protocol, all satoshis were treated as identical and interchangeable. Now, each one has its own identity that can be tracked and distinguished from all the others.

The Bitcoin Ordinals Protocol works by:

1. **Numbering**: Every satoshi gets a unique number based on the order it was created
2. **Tracking**: Following these numbered satoshis as they move through the network
3. **Inscribing**: Attaching data to specific satoshis

### What Are Inscriptions?

An inscription is data that gets permanently etched onto a satoshi. Think of it as uploading your digital data (art, music, literature) onto the Bitcoin blockchain by attaching it to a satoshi.

To understand this on a more deeper level takes some technical knowledge of Bitcoins UTXO transaction model.

Here's some of the more technical breakdown:

• **Witness Data**: Bitcoin transactions have a special section called "witness data" (thanks to the SegWit upgrade)
• **Data Storage**: Your image, text, or even HTML code gets stuffed into this witness data
• **Permanent Record**: Once confirmed, this data becomes part of Bitcoin's permanent history

### File Types Supported:

• Images (JPEG, PNG, GIF, SVG)
• Text documents
• Audio files
• HTML/CSS/JavaScript (yes, you can literally run websites on Bitcoin!)
• Pretty much any digital file under 4MB

### Why All This Matters?

This isn't just a cool technical trick — it's a fundamental shift in how digital ownership works:

**Immutability**: Your ordinal can't be changed, deleted, or "rugged" by anyone

**Decentralization**: No single server, company, or entity controls your asset **Permanence**: As long as Bitcoin exists (which, let's be honest, is probably forever), your ordinal exists

It's like the difference between:

Renting an apartment (traditional NFTs)

or

Owning a piece of land with mineral rights (Bitcoin Ordinals)

## Types of Bitcoin Ordinals (The Family Tree)

![twitter user interface with Bitcoin puppet profile picture|style:full-width|caption:Ordinals as PFPs](https://raw.githubusercontent.com/Linnyp/blogtest/main/images/article/twitterpup.png)

### Simple Inscriptions: The Classic Choice

Think of simple inscriptions as the "vanilla ice cream" of ordinals — classic, reliable, and perfect for beginners. These are single-file inscriptions: one image, one audio file, one document.

Perfect for:
• Profile pictures and avatars
• Digital art pieces
• Important documents you want preserved forever

Examples:
• A beautiful digital painting inscribed as inscription #1000
• A historic tweet saved for posterity

### Recursive Inscriptions: The Strong Stuff

Now we're getting into the heavy artillery. Recursive inscriptions are inscriptions that can reference and interact with OTHER inscriptions.

Simple Explanation: Let's say you inscribe a photo as inscription #500. Later, you inscribe some code as inscription #1000 that says "take that photo from #500 and add a border to it." The code inscription is "recursive" because it references and uses the earlier inscription.

Think of it like this:
• A simple inscription is like a single LEGO brick
• A recursive inscription is like instructions that say "take brick #500 and brick #200 and build them into a castle"

What makes them powerful:
• **Building blocks**: New inscriptions can reuse existing ones instead of starting from scratch
• **Interactive content**: You can create games, apps, or art that responds and changes
• **Efficiency**: Instead of inscribing the same image 100 times, you inscribe it once and reference it 100 times

Advanced Use Cases:
• **Interactive Games**: Fully playable games living on Bitcoin
• **Dynamic Art**: Artworks that change based on other inscriptions
• **Complex Applications**: Entire web applications running on Bitcoin

Why They Matter: They transform Bitcoin from a static storage medium into a dynamic computing platform. It's like discovering your storage unit isn't just for keeping stuff — it's actually a fully functional workshop.

### Collection-Based Ordinals: The Community Experience

Collections are where the social aspect of ordinals currently really shines. Think of them as digital trading card sets, but instead of being printed by a company, they're permanently etched into the most secure network in human history.

What Makes Collections Special:
• **Provenance**: Clear history of every piece
• **Rarity**: Transparent scarcity (no hidden minting)
• **Community**: Shared ownership of cultural moments

## Real-World Examples & Use Cases

### Digital Art: More Than Just Pretty Pictures

The art world has embraced ordinals like a long-lost friend. But we're not just talking about profile pictures here — we're talking about legitimate digital art that will outlast most physical galleries.

**Profile Pictures & Avatars**: Your digital identity, permanently stored on the most secure network ever created. No more worrying about your avatar disappearing when some startup runs out of funding.

**Generative Art Projects**: Artists are creating algorithmic masterpieces that generate unique pieces for each inscription.

**Digital Paintings & Photography**: Professional artists are discovering that Bitcoin provides the ultimate provenance and permanence for their digital works.

### Utility Applications: Beyond Art

This is where things get really interesting. Bitcoin isn't just becoming a gallery — it's becoming a Swiss Army knife of digital applications.

**Gaming Assets**: Imagine owning a rare sword in a game, and that sword is permanently yours on Bitcoin. The game company can't delete it, nerf it, or take it away. True digital ownership in gaming is finally here.

**Music Albums**: Musicians are releasing entire albums as ordinals. Your favorite band's new album? It's not just streamed from Spotify — it's permanently part of Bitcoin's history.

**Digital Documents**: Birth certificates, diplomas, contracts — important documents that you want to exist forever, regardless of what happens to governments or institutions.

**Interactive Applications**: People are building entire web applications that run on Bitcoin. Games, calculators, even primitive social networks — all living permanently on the blockchain.

### Cultural Significance: Digital Archaeology

Bitcoin Ordinals are becoming a time capsule of internet culture. Future digital archaeologists will study ordinals to understand what mattered to people in the 2020s.

**Historical Moments**: Major events, memes, and cultural phenomena are being preserved forever. The first ordinal inscription? It's basically the digital equivalent of cave paintings.

**Internet Culture**: Memes, viral videos, and digital art movements are being permanently archived. It's like the Library of Alexandria, but for internet culture, and it can never burn down.

**Community Projects**: Groups are coming together to create shared cultural artifacts. It's beautiful to see communities self-organizing around permanent digital culture.

## How to Get Started with Bitcoin Ordinals (Your Journey Begins)

### What You Need (The Starter Pack)

Getting into ordinals isn't rocket science, but it does require a few specific tools:

**Bitcoin Wallet That Supports Ordinals**: This is crucial. Regular Bitcoin wallets treat all satoshis the same, but ordinal wallets understand which satoshis have special inscriptions. Using a regular wallet is like trying to appreciate a painting while wearing a blindfold.

**Understanding of Bitcoin Fees**: Bitcoin transactions cost money (called fees), and the amount varies based on network congestion. Think of it like Uber surge pricing, but for blockchain transactions.

**Basic Knowledge of Bitcoin Transactions**: You don't need to be a developer, but understanding concepts like UTXOs (Unspent Transaction Outputs) will help you avoid expensive mistakes.

### Your First Steps (The Learning Path)

**Phase 1: Learning (You Are Here!)**
• Understanding what ordinals are ✓
• Learning the basic concepts ✓
• Getting excited about the possibilities ✓

**Phase 2: Setup**
• Choose an ordinal-compatible wallet
• Set up your wallet properly
• Practice with small amounts

**Phase 3: Exploration**
• Browse existing ordinals marketplaces
• See what's out there
• Get inspired by what others have created

**Phase 4: Action**
• Buy your first ordinal, or
• Create (mint) your first inscription
• Join the community

## Conclusion: Your Digital Ownership Journey Starts Now

### Key Takeaways (TL;DR)

• **Bitcoin Ordinals = True Digital Ownership**: Your digital assets are permanently stored on Bitcoin, not just referenced by it
• **Stored Directly on Bitcoin Blockchain**: No external servers, no broken links, no rugpulls
• **Different from Traditional NFTs**: The data IS the asset, not just a pointer to the asset
• **Growing Ecosystem**: Real utility beyond just collectibles, with gaming, music, documents, and interactive apps

[Start your ordinals journey with Ord-x today and start earning points →] < INSERT CTA PROMPTING CONNECTING WALLET

**OR**

Stay in the Loop

Don't miss out on the latest developments in the ordinals space:

• **Weekly Ordinals Insights**: Curated news and analysis
• **Platform Updates**: New features and improvements
• **Community Highlights**: Showcasing amazing community creations

[Join Our Educational Newsletter →] INSERT LEAD MAGNET OFFERING FREE NEWSLETTER

## Additional Resources

### Essential Terms Glossary

**Bitcoin**: The first and most secure cryptocurrency and blockchain network

**Satoshi**: The smallest unit of Bitcoin (1 Bitcoin = 100,000,000 satoshis)

**Ordinals Protocol**: The system for tracking and inscribing individual satoshis

**Inscription**: Data permanently attached to a specific satoshi

**Recursive Inscription**: An inscription that references other inscriptions

**UTXO**: Unspent Transaction Output (how Bitcoin tracks ownership)

**Witness Data**: Part of Bitcoin transactions where inscription data is stored

**Rare Sats**: Satoshis with special properties or inscriptions

### Recommended Wallets

**Xverse**: Mobile-friendly with ordinals support

**Unisat**: Web-based ordinals wallet

**Sparrow Wallet**: Advanced desktop wallet with ordinals features

### Community Hubs

**Ordinals Discord**: Active community discussions

**Bitcoin Twitter**: Follow #Ordinals hashtag

**Ordinals Reddit**: Questions and discussions

**Ord.io**: Ordinals explorer and marketplace

Remember: The ordinals ecosystem is still young and evolving rapidly. Stay curious, start small, and enjoy the journey into the future of digital ownership!

---

This guide was written with love for the Bitcoin and digital art communities. The future of digital ownership is being written on Bitcoin, one satoshi at a time. Welcome to the revolution! 🧡
