# Decentralized Trusted Content Protocol

## Article metadata fields

### similarity_score

Similarity score is a [locality sensitive hash](https://en.wikipedia.org/wiki/Locality-sensitive_hashing)
calculated using [MinHash](https://en.wikipedia.org/wiki/MinHash) algorithm.
It is used to get the estimated similarity between two articles quickly.
With the similarity index built from scores of a large set of articles,
we can identify similar articles in the set to a given article in a very short time.

MinHash algorithm utilizes an array of hash functions (or permutation functions).
In DTCP we choose 126 hash functions, and hashing them into 9 components,
which makes our similarity score a 9 dimensional vector.

The selection of permutation functions are not fixed, however,
for best performance it is better selected according to some rules like [Universal Hashing](http://en.wikipedia.org/wiki/Universal_hashing).

There's another fixed hash function to produce the hash component.
The packing algorithm, together with the parameters used, are given in the following python codes:

```python

    # digests are 126 numbers from the MinHash algorithm
    
    b = 9
    r = 14

    hashes = []

    large_prime = int(18446744073709551557)

    for i in range(0, b):

        hs = int(0)

        for j in range(0, r):
            current = int(digests[i * r + j])
            hs += current * int(7 ** j)
            hs %= large_prime

        hashes.append(hs)

    return hashes
    
    # we got 9 hash components here in the hashes list

```

