# Hashcash-Based Key Derivation Function

A simple, key-derivation-function (KDF) with a deterministic Hashcash-like algorithm for Proof-of-Work (PoW). The PoW algorithm uses ordered iteration which makes multithreading useless. Also, the demand for memory increases as the algorithm proceeds. 

*Memory-hard*: Each newly computed SHA512 is appended to a list in-memory which gets randomly sampled every iteration. By the time the key is found for a 4X5=20 bit partial hash collision for example, the list size might be ~ (2^20)x64 byte ~ 64 MB. For 4X4 bit collision, the size would be ~ 4 MB.



### Usage:

```bash
./hbkdf <text to generate key from> <no. of trailing zeroes in hex rep of target hash>
```

Note 1: The larger the second parameter is, the more work needs to be done in order to mine the key.

**Warning: Using any integer >=6 as the second parameter might hang your system**. Well, it did mine!

Note 2: Being a KDF, this function is deterministic, viz. same output is generated for the same input.

Tip: If a strong key is required within a given time, use the `timeout` command. If a key is found by the stipulated time limit, great. Otherwise, try with a new text as the first parameter to `hbkdf`.



### Example:

Note the variation in time required for different parameters.



Command:

```bash
time ./hbkdf "password" 5
```

Output:

```bash
Hex-Key: 3100
Final SHA512: 595968a12466631c4b445e9ee33febae1200d1b2fae1eac45e902c1d192e754392e58f6848813c45abfe51d96644ed38246cb7446e6a554349437bc25f200000

real    0m0.139s
user    0m0.129s
sys     0m0.010s
```



Command:

```bash
time ./hbkdf "weak password" 5
```

Output:

```bash
Hex-Key: b88250
Final SHA512: bc4b1ab9e49703445ce9c68e12d8a10d8dbc18b55b5bdf8d57d0690f521dc9ae5a52216911c2b585f7cc02d56a32fec913c842d58c9ff15f39d14d2b7c100000

real    0m17.826s
user    0m17.675s
sys     0m0.141s
```



Command: 

```bash
time ./hbkdf "password" 4
```

Output:

```bash
Hex-Key: 3100
Final SHA512: 595968a12466631c4b445e9ee33febae1200d1b2fae1eac45e902c1d192e754392e58f6848813c45abfe51d96644ed38246cb7446e6a554349437bc25f200000

real    0m0.104s
user    0m0.104s
sys     0m0.001s
```



Command: 

```bash
time ./hbkdf "weak password" 4
```

Output:

```bash
Hex-Key: 758b0
Final SHA512: 126c881ccdfc67e74f669cabd8402dbac8f15e109503806374f623c2f2411b7422d1243bdc9743b59f8f0dea612e8a2792b8d1bb0afeb99017e08542473d0000

real    0m1.436s
user    0m1.403s
sys     0m0.033s
```

