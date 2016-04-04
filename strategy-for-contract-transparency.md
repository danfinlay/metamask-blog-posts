Best read by people who are familiar with [Ethereum](https://www.ethereum.org/).

In this article I’ll be discussing the issue of increasing the legibility of public contracts.  I suggest an approach to improve contract legibility, and ultimately leave a few open issues for discussion and exploration related to establishing trust in an untrusted network.

Ethereum is a powerful virtual machine run in a decentralized fashion via the blockchain. This provides the opportunity for public applications to be run in an unprecedentedly transparent fashion, with their pure machine instructions available for anyone to read. This has important implications for any program that needs to be trusted by the public, like a vote counting system.

However, there’s currently a pretty poorly-defined space in terms of how to present a contract to a normal user in a way that they can fully understand the contract they are interacting with!

Currently a user will know the information they submit to the contract and how much currency they are submitting to it, but as far as knowing what the contract is doing, they are limited to viewing the compiled contract source, which is only in byte code.

While this byte code can be analyzed to derive the exact function of the contract, a casual user is entirely unlikely to conduct this analysis, and even the average Ethereum developer is unlikely to undergo this process, as byte code is much more obscure than the higher-level language that most programs are written in.

This leaves the average user with a huge leap of faith when interacting with blockchain applications. While the byte code may be public, it is so obscure that it is virtually useless to the average person, and only by assuming good intentions can any user currently interact with a blockchain application.

One obvious way to make contract code more legible is to present the original source code, potentially annotated with comments. It is not unreasonable to publish the source code for a contract on the blockchain, along with the compiler version used to derive the exact byte code, much like a name registry maps a name to a contract address. I might call this a **source code registry**.

Once this information is public, it would be sensible for people to publish whether they had been able to successfully compile the referenced contract code with the provided source code. I might call this a **compilation testimony**, which might live on a **compilation testimony registry**.

Once those testimonies have been published, we are re-confronted with the problem of trust on an untrusted network.  This is everyone’s favorite problem to solve, writing new review systems. How can a new user, approaching this ecosystem, know that a given source code, with a number of people testifying for its accuracy, accurately compiles to the target contract’s code?

This happens to be a popular problem to solve, and rather than present a “correct” solution, I’ll suggest that an ideal situation would cultivate an ecosystem of ways to trust, ranging from initial authorities to web of trust.  Once these previous two contracts are available, the exact method of trust can be left to interface and experience designers.

Additionally, the compilation and testimony process could easily be automated, and run by multiple parties, creating a pool of well-established automated compilation testifying services, which could eventually become easy to trust by default for a known Ethereum ecosystem developer (like [Metamask](https://metamask.io)), allowing for a transaction verification UI that gives the user as much easy-to-digest information as possible before consenting to a transaction.

Source code may still not be the most human readable format, but with good comments, it can be lightyears ahead of the current situation. There are ideas floating around making contracts more human-readable, like [NatSpec](https://github.com/ethereum/wiki/wiki/Ethereum-Natural-Specification-Format), which requires the contract author to follow a specific format for legibility, and others should also be seriously explored and pursued, because Ethereum’s trustworthiness is fundamentally limited by the casual legibility of its public contracts.