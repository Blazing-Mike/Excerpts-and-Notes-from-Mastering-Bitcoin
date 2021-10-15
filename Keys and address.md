## Chapter 4 : Key and addresses
private key is simply a number, picked at random. Ownership and control over the private key is the root of user control over all funds associated with the corresponding
bitcoin address. The private key is used to create signatures that are required to spend bitcoin by proving ownership of funds used in a transaction. 

Generating a private key from a random number

The first and most important step in generating keys is to find a secure source of entropy, or randomness. Creating a bitcoin key is essentially the same as “Pick a number between 1 and 2^256.” 

Public Keys : The public key is calculated from the private key using elliptic curve multiplication,
which is irreversible: 

``` K = k * G, ```

 where k is the private key, G is a constant point called the generator point, and K is the resulting public key. 

## Elliptic Curve Cryptography Explained

Elliptic curve cryptography is a type of asymmetric or public key cryptography based on the discrete logarithm problem as expressed by addition and multiplication on the
points of an elliptic curve

### Generating a Public Key

where k is the private key, G is the generator point, and K is the resulting public key, a point on the curve. Because the generator point is always the same for all bitcoin users, a private key k multiplied with G will always result in the same public key K. The relationship between k and K is fixed, but can only be calculated in one direction, from k to K. That’s why a bitcoin address (derived from K) can be shared with anyone and does not reveal the user’s private key (k).
K = (x,y), a public key is a point (x,y) on an elliptic curve. Because the curve expresses a mathematical function, a point on the curve represents a solution to the equation and, therefore, if we know the x coordinate we can calculate the y coordinate by solving the equation y2 mod p = (x3 + 7) mod p. 

### Bitcoin Addresses

Bitcoin address is a string of digits and characters that can be shared with anyone who wants to send you money. Addresses produced from public keys consist of a string of numbers and letters, beginning with the digit “1.”
The bitcoin address is derived from the public key through the use of one-way cryptographic hashing. A “hashing algorithm” or simply “hash algorithm” is a one-way function that produces a fingerprint or “hash” of an arbitrary-sized input. Crypto‐
graphic hash functions are used extensively in bitcoin: in bitcoin addresses, in script addresses, and in the mining Proof-of-Work algorithm. The algorithms used to make a bitcoin address from a public key are the Secure Hash Algorithm (SHA) and the RACE Integrity Primitives Evaluation Message Digest (RIPEMD), specifically SHA256 and RIPEMD160. Starting with the public key K, we compute the SHA256 hash and then compute theRIPEMD160 hash of the result, producing a 160-bit (20-byte) number:

``` = RIPEMD160(SHA256 (K) ```
where K is the public key and A is the resulting bitcoin address.
### Base58 and Base58Check Encoding

Base58 is a text-based binary-encoding format developed for use in bitcoin and used in many other cryptocurrencies. It offers a balance between compact representation, readability, and error detection and prevention.
To add extra security against typos or transcription errors, Base58Check is a Base58 encoding format, frequently used in bitcoin, which has a built-in error-checking code. 
The checksum is an additional four bytes added to the end of the data that is being encoded. The checksum is derived from the hash of the encoded data and can therefore be used to detect and prevent transcription and typing errors. This prevents a mistyped bitcoin address from being accepted by the wallet software as a valid destination, an error that would otherwise result in loss of funds.

In bitcoin, most of the data presented to the user is Base58Check-encoded to make it
compact, easy to read, and easy to detect errors. The version prefix in Base58Check encoding is used to create easily distinguishable formats, which when encoded in Base58 contain specific characters at the beginning of the Base58Check-encoded payload.

### Key Formats
Both private and public keys can be represented in a number of different formats. These representations all encode the same number, even though they look different. These formats are primarily used to make it easy for people to read and transcribe keys without introducing errors.

## Advanced Keys and Addresses

### Encrypted Private Keys (BIP-38)

BIP-38 proposes a common standard for encrypting private keys with a passphrase and encoding them with Base58Check so that they can be stored securely on backup media, transported securely between wallets, or kept in any other conditions where the key might be exposed. The standard for encryption uses the Advanced Encryption Standard (AES), a standard established by the NIST and used broadly in data encryption implementations for commercial and military applications.

A BIP-38 encryption scheme takes as input a bitcoin private key, usually encoded in the WIF, as a Base58Check string with the prefix of “5.” Additionally, the BIP-38 encryption scheme takes a passphrase—a long password—usually composed of several words or a complex string of alphanumeric characters. The result of the BIP-38 encryption scheme is a Base58Check-encoded encrypted private key that begins with the prefix 6P.

## Pay-to-Script Hash (P2SH) and Multisig Addresses
Bitcoin addresses that begin with the number “3” are pay-to-script hash (P2SH)addresses, sometimes erroneously called multisignature or multisig addresses. They designate the beneficiary of a bitcoin transaction as the hash of a script, instead of the owner of a public key.
A P2SH address is created from a transaction script, which defines who can spend a transaction output. Encoding a P2SH address involves using the same double-hash function as used during creation of a bitcoin address, only applied on the script instead of the public key

 script hash = RIPEMD160(SHA256(script))

P2SH is not necessarily the same as a multisignature standard transaction. A P2SH address most oten represents a multisignature script, but it might also represent a script encoding other types of transactions.

### Multisignature addresses and P2SH
Currently, the most common implementation of the P2SH function is the multisignature address script. As the name implies, the underlying script requires more than one signature to prove ownership and therefore spend funds. The bitcoin multisignature feature is designed to require M signatures (also known as the “threshold”) from a total of N keys, known as an M-of-N multisig, where M is equal to or less than N. 

### Vanity Addresses
Vanity addresses are valid bitcoin addresses that contain human-readable messages.Vanity addresses are no less or more secure than any other address. They depend on the same Elliptic Curve Cryptography (ECC) and SHA as any other address. You can no more easily find the private key of an address starting with a vanity pattern than you can any other address

### Paper wallet
Paper wallets are bitcoin private keys printed on paper. Often the paper wallet also includes the corresponding bitcoin address for convenience, but this is not necessary because it can be derived from the private key. Paper wallets are a very effective way to create backups or offline bitcoin storage, also known as “cold storage.




