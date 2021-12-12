## RSA
```
Public Key Cryptography** where a public key is used to encrypt data and only a secret, private key can be used to decrypt the data
```

>The **Public Key** is made up of (_n_, _e_)

>The **Private Key** is made up of (_n_, _d_)

>The message is represented as _m_ and is converted into a number

>ciphertext is represented by _c_

>_p_ and _q_ are prime numbers which make up n

>_e_ is public exponent

>_n_ is the modulus and it length in bits is the bit length

> _d_ is the private exponent

>The totient λ(_n_) is used to compute _d_ and is equal to the lcm(_p_-1, _q_-1), another definition for λ(_n_) is that λ(_pq_) = lcm(λ(_p_), λ(_q_))

n e d m c p q