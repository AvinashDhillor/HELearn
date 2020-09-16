# Learning about homomorphic encryption

### Step - 1

First we need to understand basic maths behind Homormorphic encryption (Discrete Maths)

Starting with `Ring and fields`
- [Ring](https://www.youtube.com/watch?v=BVf5FFIbaaQ)
- [(Important) Fields](https://www.youtube.com/watch?v=KCSZ4QhOw0I)
- [Polynomial Ring](https://www.youtube.com/watch?v=BR-x96FXS9s)

### Step - 2

Question : How encryption works ?

Answer : Encryption works on the problem that is still unsolvable.
         E.g. RSA-2048 contains 617 decimal number which can not be factorized to 2 prime number till now. It is still unsolved by quantumn computer.
         If we build a quantum computer that can find prime factors then RSA encryption can be cracked.

- [RSA number](https://www.wikiwand.com/en/RSA_numbers)

### Example of RSA working.
- [source](https://www.wikiwand.com/simple/RSA_algorithm) - wikipedia
 
![image](/images/img1.png)

**Similary**, Homomorphic encryption work in the problem of Ring-LWE(similar to LWE) and we can perform computation operation on encrypted data.
- [Main source](https://blog.openmined.org/build-an-homomorphic-encryption-scheme-from-scratch-with-python/)

**Basic concept**
- [Learning with errors](https://www.youtube.com/watch?v=sXvoX9uDr8Q&t=1s&ab_channel=BillBuchananOBE)
- [Ring Learning with errors](https://www.youtube.com/watch?v=hN5TQiz2gWs&t=630s&ab_channel=BillBuchananOBE) - Concept of polynomial is added in LWE (means polynomial with same degree are calculated)
  - [Another video for RLWH for better understanding](https://www.youtube.com/watch?v=QZBkhmqyBTA&ab_channel=BillBuchananOBE)
  - [Articles for above videos](https://medium.com/asecuritysite-when-bob-met-alice/learning-with-errors-and-ring-learning-with-errors-23516a502406)

## Ring-Learning with errors(Problem behind homomorphic encryption)

### How to Generating Public keys and private Keys using Ring-learning with errors.(Coult not find RLWE video source but it is going to follow same approach)

- [Public/Private key generation](https://www.youtube.com/watch?v=MBdKvBA5vrw&t=377s&ab_channel=BillBuchananOBE)

Function to generater polynomial matrix of random number, secret key and errors
```
def gen_binary_poly(size):
    """Generates a polynomial with coeffecients in [0, 1]
    Args:
        size: number of coeffcients, size-1 being the degree of the
            polynomial.
    Returns:
        array of coefficients with the coeff[i] being 
        the coeff of x ^ i.
    """
    return np.random.randint(0, 2, size, dtype=np.int64)


def gen_uniform_poly(size, modulus):
    """Generates a polynomial with coeffecients being integers in Z_modulus
    Args:
        size: number of coeffcients, size-1 being the degree of the
            polynomial.
    Returns:
        array of coefficients with the coeff[i] being 
        the coeff of x ^ i.
    """
    return np.random.randint(0, modulus, size, dtype=np.int64)


def gen_normal_poly(size):
    """Generates a polynomial with coeffecients in a normal distribution
    of mean 0 and a standard deviation of 2, then discretize it.
    Args:
        size: number of coeffcients, size-1 being the degree of the
            polynomial.
    Returns:
        array of coefficients with the coeff[i] being 
        the coeff of x ^ i.
    """
    return np.int64(np.random.normal(0, 2, size=size))

```

Following function is used for key generation

```
def keygen(size, modulus, poly_mod):
    """Generate a public and secret keys
    Args:
        size: size of the polynoms for the public and secret keys.
        modulus: coefficient modulus.
        poly_mod: polynomial modulus.
    Returns:
        Public and secret key.
    """
    sk = gen_binary_poly(size)
    a = gen_uniform_poly(size, modulus)
    e = gen_normal_poly(size)
    b = polyadd(polymul(-a, sk, modulus, poly_mod), -e, modulus, poly_mod)
    return (b, a), sk

```
The public-key (b, a) can then be used for encryption, and the secret-key sk for decryption.


### How to Encrypt the data using public key and RLWE concept 

-[] ()

### 

