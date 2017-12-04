# Decentralized Trusted Content Protocol

## Basic metadata fields

### type

The type of the content, such as image, article, file, media, etc

### language

The main language used in this content. Language name representation follows the definition in [RFC4646](http://www.ietf.org/rfc/rfc4646.txt). For example "zh-CN", "en-US".

### title

The title of the content.

### abstract

The description of the subject of the content.

### category

A comma separated list of words describing the categories.
For example, "news,economy".

This field should be provided by the author when creating the article for accuracy.
However categorization algorithms could be used for assistance
or in the absence of author's decision.

### created

The time when this article is created.

This field is a UNIX timestamp representing time in milliseconds starts from
Jan 1, 1970 in UTC.

This field can be provided as a proof of article creation time,
or [Trusted Timestamp](https://en.wikipedia.org/wiki/Trusted_timestamping),
due to the inalterability provided by Blockchain.

### creator

Author's name.

### creator_id

The author's unique id.

Author's identity is represented by a pair of
[public and private keys](https://en.wikipedia.org/wiki/Public-key_cryptography).
For security reasons only the hash of the public key is published on Blockchain to
verify the author's identity.

The algorithm used to create the key pair is [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
Key length should be longer than 2048 bit.

The creator_id is an [SHA1](https://en.wikipedia.org/wiki/SHA-1) hash of the public key generated.
The hash should be encoded in [Base36](https://en.wikipedia.org/wiki/Base36) format.

### content_hash

Fingerprint represented by the hash of the content.

The content_hash is an [SHA1](https://en.wikipedia.org/wiki/SHA-1) hash of the public key generated.
The hash should be encoded in hex digits.

### signature

Signature is calculated by representing all the DTCP data in a
[JSON](http://www.json.org) string,
except the signature field itself, calculate the [SHA1](https://en.wikipedia.org/wiki/SHA-1)
hash of the JSON string, and then sign the hash with private key.

The fields in the JSON array must be sorted alphabetically before signing. 

Signature algorithm used is [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)).
