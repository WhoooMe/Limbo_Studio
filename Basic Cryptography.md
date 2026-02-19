#Intermediate #Basic-Cryptography #RSA #ModInverse #HashAttack #CTF #VS-Code #CLI #WSL

## Goals
By the end of this module, students will:
+ Understand modular inverse and its role in cryptography.
+ Understand how RSA works internally.
+ Implement a small RSA system in Python.
+ Identify and exploit weak RSA configurations.
+ Understand basic hash attacks used in CTF challenges.
+ Distinguish between symmetric and asymmetric cryptography.

## Prerequisites
Participants must have completed:
+ Basic Python Scripting mdodule.
+ Intro to Python for Cryptography (Bytes, XOR, Modular Arithmetic, Caesar) module.
+ Comfortable with `pow(a, b, m)`, `math.gcd()`, Loops and functions, and Basic hashing (MD5/SHA).

## \<Modular Inverse ++\>
In the previous module, we learned about modular arithmetic, GCD, and how numbers work in circular systems. Now we'll discuss number theory. In modular systems, we can't perform division directly. Instead, we use a concept called modular inverse.

This concept is crucial in modern cryptography, particularly RSA, because it's used to generate private keys. In this section, we'll understand what modular inverse is, when it occurs, and why it's crucial in public-key cryptography. Here are some things we'll discuss:

### 1. What is Modular Inverse?
Let's start with the simplest thing. In ordinary mathematics, if we have `3 × 4 = 12`, then 4 can be thought of as a "pair" of 3 to make 12. Now, in the modulo system, we're looking for something different. We want to find a number x such that:
```scss
3 × 'x' ≡ 1 (mod 11)
# This means:
# We want the result of multiplying 3 and x modulo 11 to be 1.
```
So the correct answer is 4 because it can be calculated manually like this:
```matlab
3 × 4 = 12
12 % 11 = 1
# So: The modular inverse of 3 modulo 11 is 4
```
> [!NOTE]
> So it can be said that the Modular Inverse is a number that when multiplied in the modulo system will produce the value 1.

Last but not least, in ordinary mathematics, division is done by performing inverse multiplication. Example `10 ÷ 2` = `10 × 1/2`
But in modular arithmetic, we cannot divide. Instead, we replace division by multiplying by the modular inverse. So, `a / b (mod m)` = `a × b⁻¹ (mod m)`

### 2. Why is it called an "inverse"?
Because it essentially reverses the effect of multiplication, like in the example above, `3 × 4 ≡ 1 (mod 11)`, which means 4 is the number that "reverses" 3 back to 1 in the modulo 11 system. So, it's similar to:
> XOR-ing twice with the same key will return to the original value. Modular inverse reverses the effect of multiplication.

### 3. When Does a Modular Inverse Exist
A modular inverse doesn't always exist and requires that `gcd(a, m) = 1`. This means a and m must be coprime and must have no common factors other than 1. Example:
+ If there is an inverse
```python
import math
math.gcd(3, 11) # 1
# This means there is an inverse.
```
+ If there is no inverse:
```python
import math
math.gcd(6, 12) # 6
# Not coprime, that's mean no modular inverse.
# This happens because if they have the same factors, then it is impossible to produce the number 1 in the modulo system.
```

### 4. How to Calculate in Python
Python itself makes it easy by simply adding the `math` library, like this:
```python
import math
a = 3
m = 11
print(pow(a, -1, m)) # 4
# pow(a, -1, m) means: Find the modular inverse of a with respect to 'm'.
```

## \<Understanding RSA Internals\>
Simply put, RSA is an asymmetric cryptographic algorithm, meaning it uses two different keys:
+ Public key for encryption
+ Private key for decryption

Unlike Caesar or XOR, which use a single key, RSA mathematically separates the encryption and decryption processes.

### 1. How is RSA built?
RSA is built on three main foundations prime numbers, modular arithmetic, and modular inverse. Simply put, RSA uses **two prime numbers** to form a mathematical system that generates **two related keys**.

So, what makes RSA secure is not that its algorithm is hidden. Rather, its workings are publicly known. Its security relies on one crucial principle:
> It is very difficult to factor large numbers that are the product of two prime numbers.

If someone only knows the product (without knowing the **two prime numbers**), finding the prime factors requires enormous computational effort. This is what makes RSA secure even though its algorithm is publicly known.

### 2. How is RSA Made?
Now let's see how the two keys in RSA are formed.

+ The first step is to choose two prime numbers, for example `p = 11` and `q = 13`.
> Prime numbers because they have special mathematical properties that allow the RSA modular system to function correctly and be structured. Furthermore, if the prime numbers are large, their products are very difficult to refactor again.

+ Calculate n
> Then multiply the two prime numbers `n = p * q # 143`. This value of n is called the modulus and will be used in the public and private keys. All encryption and decryption processes will then be carried out modulo 'n'.

+ Calculate φ(n) or phi(n)
> Next, we calculate a value called the Eulerian Contigent Function: `phi = (p - 1) * (q - 1) #120`
>
> This value of φ(n) is important because it defines the **mathematical space** in which RSA operates. Without knowing p and q, this value cannot be easily calculated.

+ Select the Public Exponent (e)
> Next, we can choose a number e with two conditions: `1 < e < φ(n)` and `gcd(e, φ(n)) = 1` (must be coprime). For example:
```python
import math
e = 7
math.gcd(e, phi) # 1
# Since the result is 1, e is valid.
# This value of e is called the public exponent and will be part of the public key.
```

+ Calculate the Private Key (d)
> Now comes the most important part, where we find the number `d`, which is the modular inverse of e with respect to `φ(n)`, where `d = pow(e, -1, phi)`.

This means mathematically `e × d ≡ 1 (mod φ(n)` and this value of `d` is called the **private exponent**. Without the modular inverse, we cannot obtain `d`, and without `d`, RSA cannot decrypt the message.

After all the calculations, you will have:
+ Public key → (e, n)
+ Private key → (d, n)

The public key can be shared with anyone so that others can encrypt messages for us. But, the private key must be kept secret because only with this key can the message be decrypted.

### 3. Encryption and Decryption Process
For example, suppose there is a message in the form of the number `m = 9`. Encryption can be done with:
```ini
c = m^e mod n
c = pow(m, e, n)`.
```
Meanwhile, to restore the message (Decryption), you can do it with:
```ini
m = c^d mod n.
original = pow(c, d, n).
# The message is restored to its original state.
```

## \<Breaking Weak RSA\>
Now the question arises, "Under what conditions can RSA be broken?". Because in the world of CTF and Cybersecurity, systems are rarely perfect. There are usually small weaknesses that can be exploited. Here, we will try to do just that.

### 1. The Value of 'n' is Too Small (Easy to Factor)
The security of RSA depends on the difficulty of factoring `n = p × q` and if `n` is too small, an attacker can easily find the values ​​of `p` and `q`. For example:
```ini
n = 143
# We can quickly find:
# 143 = 11 × 13
```

### 2. Public Exponent Too Small
Typically, in secure RSA implementations, the public exponent value used is 65537. This number was chosen because it is large enough to be secure and yet still efficient. However, if someone uses a value that is too small, such as `e = 3` and RSA is used without padding, a weakness can arise.

Recall the RSA encryption formula:
> c = m^e mod n.

This means raising the plaintext `m `to the power of `e`, then modulating it by `n`. Now, if `e` is very small (for example, 3), then the message value `m` is also small, and the resulting m³ is still smaller than `n`. If m³ < n, then the modulo process does nothing, because the value has not yet exceeded the `n` limit. There is no "wrap around" in a modular system. Here's an example:
```python
m = 5 e = 3
c = 125
# If 125 < n, then: m = cube root of 125 so the result is 5.
# Without private key, factorization, knowing phi(n). This is called a low exponent attack.
```

### 3. Implementation Errors
Sometimes RSA is not weak in theory, but rather due to incorrect implementation, for example:
+ `p` and `q`are too close together.
+ Using the same prime in two different systems.
+ Reusing the modulus.
+ Leaking part of the private key.

In CTFs, weaknesses like these often become entry points for attacks.

## \<Hash Attacks in CTF\>
In simple terms, hash converts input data (text, files, passwords) into a string of unique characters with a fixed length.

### 1. Why Hash is One-Way?
Hashes are designed as one-way functions. This means it's easy to compute a hash from an input, but very difficult (mathematically) to return the hash to the original input. For example:
```python
import hashlib
hashlib.md5("password".encode()).hexdigest()
```
It's easy to convert it. But, if you're only given `5f4dcc3b5aa765d61d8327deb882cf99`. Because, theoretically, there's no mathematical formula to "reverse" the hash to `password`.

### 2. Why MD5 is Broken?
MD5 was once very popular. But it is now considered broken because:
+ Two different inputs can be created with the same hash (collision).
+ It is not secure for modern security systems.
+ It is vulnerable to brute force attacks because it is fast to calculate.

In the real world, MD5 is no longer used for serious security (replaced by SHA-256, SHA-3, etc.). However, in CTFs, MD5 is often used because:
+ It is fast to calculate.
+ It is vulnerable to attack.
+ Suitable for practicing hash cracking concepts.

### 3. Dictionary Attack Concept
Because hashes cannot be mathematically reversed, attackers use a different approach:
> Guess the input, hash it, and then match the result. This is called a dictionary attack.

For example:
```python
import hashlib

target = "5f4dcc3b5aa765d61d8327deb882cf99"

words = ["admin", "password", "123456"]

for word in words:
    if hashlib.md5(word.encode()).hexdigest() == target:
        print("Found:", word)
```
This script works by:
+ Pick a word from the `list.`
+ Hash the word.
+ `Compare` it to the target.
+ If it `matches`, find the plaintext.

So, since we're not "flipping" the hash, we're just guessing until we find a match.

## \<Symmetric vs Asymmetric Cryptography\>
Before closing this module, it is important to understand the differences between the two main types of cryptography: symmetric and asymmetric.

### 1. Symmetric Cryptography
In symmetric cryptography, the key used for encryption and decryption is the same. This means:
+ The sender and recipient must have the same secret key.
+ If the key is leaked, all messages can be read.

Examples of popular symmetric algorithms is AES, DES.

### 2. Asymmetric Cryptography
In asymmetric cryptography, two different but mathematically related keys are used. This means:
+ Public key → for encryption
+ Private key → for decryption

Examples of popular asymmetric algorithms is RSA.

So, it can be said that symmetric and asymmetric Cryptography are distinguished by their key structures, but these differences affect how the security system works. Like:
+ Symmetricuses a single key for both encryption and decryption. Fast and efficient, but there are challenges in securely sharing the key.
+ Asymmetric cryptography uses two different keys (public and private). It's more secure for initial communication, but computationally slower.

## Output
After this module, participants will not only understand cryptography theory, but will also:
+ Be able to read RSA problems in CTFs.
+ Be able to identify configuration weaknesses.
+ Be able to perform basic attacks based on mathematics and logic in CTFs.
+ Understand the relationship between theory and exploitation practice.
