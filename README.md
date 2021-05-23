# Hashcash-Based Key Derivation Function

A simple, key-derivation-function (KDF) with a Hashcash-like algorithm for Proof-of-Work (PoW). The PoW algorithm uses ordered iteration which makes multithreading useless.



### Usage:

```bash
./hbkdf <text to generate key from> <no. of trailing zeroes in hex rep of target hash>
```

Note 1: The larger the second argument is, the more work needs to be done in order to mine the key.

Note 2: Being a KDF, this function is deterministic, viz. same output is generated for the same input.



### Example:

Command:

```bash
time ./hbkdf "password" 5
```

Output:

```bash
Key:  10493
Final SHA512:  8166b9706d8429d1b5896bdd86e297132388932db79eea4a019fb9d65369192726fd7fe36346c4e2004e31ebe33f10e53a60700e2e72103f43b2528b68100000

real    0m1.025s
user    0m1.025s
sys     0m0.000s
```



Command:

```bash
time ./hbkdf "password" 7
```

Output:

```bash
Key:  213C310
Final SHA512:  05a68c6b202d1037666280f8d6833839ad97785abf3e3022399d111104695c5106fe5c202b9a6f89326ede047fd26f37ddc708d8b6316204fc43ddde90000000

real    1m14.669s
user    1m14.621s
sys     0m0.040s
```

