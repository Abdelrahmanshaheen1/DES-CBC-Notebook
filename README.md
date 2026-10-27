# DES Encryption with CBC Mode — From Scratch

A from-scratch implementation of DES (Data Encryption Standard) and CBC (Cipher Block Chaining) mode in Python, built directly on the bit-level DES specification rather than using a crypto library.

## What's implemented

- **Core DES tables:** Initial Permutation (IP), Final Permutation (FP), Expansion (E), all 8 S-boxes, and the P-box permutation — encoded directly as the standard DES bit-position tables.
- **Feistel structure:** 16 rounds of expansion → XOR with the round key → S-box substitution → P-box permutation → swap, exactly matching DES's design.
- **CBC chaining:** plaintext is split into 64-bit blocks (zero-padded if needed), and each block is XORed with the previous ciphertext block (or the IV, for the first block) before DES encryption — the standard CBC construction that prevents identical plaintext blocks from producing identical ciphertext.

## Known simplification

The round keys used in the 16 Feistel rounds are a **fixed, repeated 48-bit placeholder key** rather than being derived per-round from a master key via DES's real key schedule (PC-1/PC-2 permutations and the per-round left-shift rotations). So the Feistel network, S-box substitution, and CBC chaining are all implemented and verified to run correctly — the per-round key *derivation* step is the one piece simplified out. Worth knowing before treating this as a complete DES implementation.

## Verified

Converted to a script and executed end-to-end: runs without errors, correctly produces 16 rounds of Feistel output for a test block, and successfully CBC-encrypts a multi-block plaintext, printing the intermediate state (post-XOR block, each round's L/R halves) at every step.

## Skills demonstrated

Implementing a real block cipher at the bit level — permutation tables, Feistel rounds, S-box substitution — and a correct understanding of why block cipher modes like CBC exist (chaining dependency between blocks) rather than just calling `encrypt()` from a library.
