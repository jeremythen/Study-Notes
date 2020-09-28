# Blockchain

## Cryptography

Secret writing. A way to encrypt a message to send it and then decrypt it.

## Public and Private keys

The public key is used to share it, so they can send you an encrypted message with the public key, and then, you use the private key to decrypt it.
The public key is created from the private key. With the private key you can know the public key, but with the public key you cannot know the private key. Hence, it's security feature.

## Digital Signature

Uses public/private key pairs to function.
When the message is sent it is signed with the private key. When it is receive it verifies that it was created by the private key.
This way they really know who you are, that you are who you say you are.

With the Public/Private Key Pair infrastructure is how the Blockchain does the transactions.

## Nonce

A number that is used only once. Used in digital transmissions to reduce duplicate transactions.

## Hash Functions

Take data of any length and converts it to a fixed length representation, shorter or longer than the original.
It goes one way.
Good to encrypt.
Creates an almost unique identifier.

Blockchain uses SHA-256 algorithm.

## Notes

The Blockchain is said to be Peer to peer.
Blockchain database is decentralized.

DLT Distributed Ledger Technology

For a transaction to be processed and inserted into the blockchain, consensus must be reached by all participating devices.
Miners create the necessary hash signatures that allows new blocks to be appended to the chain.
Miners find the nonce by creating the winning hash, called proof of work, provides integrity. Because we don't want to be too easy to add blocks, because that would be a security issue.

Once a transaction takes place, there is no way back. Transactions cannot be reversed.

## Bitcoins

If a person loses their private key, they lose the bitcoins associated with them. This is the crypto in cryptocurrencies.

For a transaction to be processed, it must meet 2 conditions:

1. There must be a consensus over all the distributed databases that a transaction is legit (the source has that amount of bitcoins, the destination can receive it)
2. A miner in the network succeeds in resolving specific hash output based on specific input. This is the Proof of work.

Each new block address is a hash of the previous one. If someone tries to change a previous block, then the hash will change, the next block will complain and it will not be permitted.

### Miner

They provide proof of work by completing a math problem and thus give permission for a new block to be inserted.
The can earn money, generated from the transaction fee.
One transaction at a time.

## Terms

- Smart Contracts (software code that runs on top of a blockchain)
- Hyperledger
- Altcoins, Altchains, ICOs
- Identity management and blockchain
- Distributed ledger

## Links

- civic.com
- blockauth.org
- bitnation.co
- identifi.github.io
- blockchainhub.net
- governmentblockchain.org
-
