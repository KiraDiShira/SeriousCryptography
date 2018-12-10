**Encryption** is the principal application of **cryptography**; it makes data incomprehensible in order to ensure its **confidentiality**. Encryption uses an algorithm called a **cipher** and a secret value called the **key**; if you don’t know the secret key, you can’t decrypt, nor can you learn any bit of information on the encrypted message—and neither can any attacker.

In **symmetric encryption**, the key used to decrypt is the same as the key used to encrypt (unlike **asymmetric encryption**, or **public-key encryption**, in which the key used to decrypt is different from the key used to encrypt).

When we’re encrypting a message, **plaintext** refers to the unencrypted message and **ciphertext** to the encrypted message.

<img src="https://github.com/KiraDiShira/SeriousCryptography/blob/master/1ENCRYPTION/Images/Enc_1.PNG" />

For some ciphers, the ciphertext is the same size as the plaintext; for some others, the ciphertext is slightly longer. However, ciphertexts can never be shorter than plaintexts.

We can try to abstract out the workings of a cipher, first by identifying its two main components: a **permutation** and a **mode of operation**. A permutation is a function that transforms an item (in cryptography, a letter or a group of bits) such that each item has a unique inverse (for example, the Caesar cipher’s three-letter shift). A mode of operation is an algorithm that uses a permutation to process messages of arbitrary size.

## The Permutation

Most classical ciphers work by replacing each letter with another letter— in other words, by performing a *substitution*.

A cipher’s substitution can’t be just any substitution. It should be a permutation, which is a rearrangement of the letters A to Z, such that each letter has a unique inverse.

For example, a substitution that transforms the letters A, B, C, and D, respectively to C, A, D, and B is a permutation, because each letter maps onto another single letter. But a substitution that transforms A, B, C, D to D, A, A, C is not a permutation, because both B and C map onto A. With a permutation, each letter has exactly one inverse.

Still, not every permutation is secure. In order to be secure, a cipher’s permutation should satisfy three criteria:

- The permutation should be determined by the key
- Different keys should result in different permutations.
- The permutation should look random
