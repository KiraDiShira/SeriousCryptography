**Encryption** is the principal application of **cryptography**; it makes data incomprehensible in order to ensure its **confidentiality**. Encryption uses an algorithm called a **cipher** and a secret value called the **key**; if you don’t know the secret key, you can’t decrypt, nor can you learn any bit of information on the encrypted message—and neither can any attacker.

In **symmetric encryption**, the key used to decrypt is the same as the key used to encrypt (unlike **asymmetric encryption**, or **public-key encryption**, in which the key used to decrypt is different from the key used to encrypt).

When we’re encrypting a message, **plaintext** refers to the unencrypted message and **ciphertext** to the encrypted message.

<img src="https://github.com/KiraDiShira/SeriousCryptography/blob/master/1ENCRYPTION/Images/Enc_1.PNG" />

For some ciphers, the ciphertext is the same size as the plaintext; for some others, the ciphertext is slightly longer. However, ciphertexts can never be shorter than plaintexts.

## The Vigenère Cipher

letters are shifted by values defined by a key, a collection of letters that represent numbers based on their position in the alphabet. For example, if the key is DUH, letters in the plaintext are shifted using the values 3, 20, 7 because D is three letters after A, U is 20 letters after A, and H is seven letters after A. The 3, 20, 7 pattern repeats until you’ve encrypted the entire plaintext. For example, the word CRYPTO would encrypt to FLFSNV using DUH as the key: C is shifted three positions to F, R is shifted 20 positions to L, and so on.

# How Ciphers Work

We can try to abstract out the workings of a cipher, first by identifying its two main components: a **permutation** and a **mode of operation**. A permutation is a function that transforms an item (in cryptography, a letter or a group of bits) such that each item has a unique inverse (for example, the Caesar cipher’s three-letter shift). A mode of operation is an algorithm that uses a permutation to process messages of arbitrary size.

## The Permutation

Most classical ciphers work by replacing each letter with another letter— in other words, by performing a *substitution*.

A cipher’s substitution can’t be just any substitution. It should be a permutation, which is a rearrangement of the letters A to Z, such that each letter has a unique inverse.

For example, a substitution that transforms the letters A, B, C, and D, respectively to C, A, D, and B is a permutation, because each letter maps onto another single letter. But a substitution that transforms A, B, C, D to D, A, A, C is not a permutation, because both B and C map onto A. With a permutation, each letter has exactly one inverse.

Still, not every permutation is secure. In order to be secure, a cipher’s permutation should satisfy three criteria:

- The permutation should be determined by the key
- Different keys should result in different permutations.
- The permutation should look random: There should be no pattern in the ciphertext after performing a permutation, because patterns make a permutation predictable for an attacker, and therefore less secure. For example, the Vigenère cipher’s substitution is pretty predictable: if you determine that A encrypts to F, you could conclude that the shift value is 5 and you would also know that B encrypts to G, that C encrypts to H, and so on. However, with a randomly chosen permutation, knowing that A encrypts to F would only tell you that B does not encrypt to F.

We’ll call a permutation that satisfies these criteria a **secure permutation**. But as you’ll see next, a secure permutation is necessary but not sufficient on its own for building a secure cipher. A cipher will also need a mode of operation to support messages of any length.

## The Mode of Operation

Say we have a secure permutation that transforms A to X, B to M, and N to L, for example. The word BANANA therefore encrypts to MXLXLX, where each occurrence of A is replaced by an X. Using the same permutation for all the letters in the plaintext thus reveals any duplicate letters in the plaintext. By analyzing these duplicates, you might not learn the entire message, but you’ll learn *something* about the message.

The mode of operation (or just mode) of a cipher mitigates the exposure of duplicate letters in the plaintext by using different permutations for duplicate letters.

To build a secure cipher, you must combine a secure permutation with a secure mode. Ideally, this combination prevents attackers from learning anything about a message other than its length.

## Perfect Encryption: The One-Time Pad

It guarantees perfect secrecy. The one-time pad takes a plaintext, P, and a random key, K, that’s the same length as P and produces a ciphertext C, defined as

```
C = P ⊕ K
```
