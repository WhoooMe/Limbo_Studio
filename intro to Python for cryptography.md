#Beginner #Cryptography #BytesAndEncoding #XOROperations #ModularMath #Hashing #VSCode #CryptoMath #venv

## Goals
By the end of this module, students will understand how Python represents and manipulates bytes, strings, and encoding formats commonly used in cryptography. They will be able to identify various data representations such as hex and base64, perform essential operations like hashing, XOR computation, and modular arithmetic, and analyze simple encoded or encrypted data.

## Prerequisites
Participants should have basic knowledge of Python and the command line to ensure smooth implementation of this module.
which you may also need:
+ Basic Python scripting (variables, data types, loops, functions)
+ Familiarity with Linux command-line operations
+ Understanding of virtual environments (venv)
+ Basic knowledge of encoding and hashing
+ Completion of the previous module: [Basic-Python-Scripting.md]

## Core Materials

## <Characters & Bytes as Numbers Fundamentals>
In this section, students will understand that computers don't read letters, but rather numbers. All the text we see is actually a numerical representation processed in bytes.

### 1. Why Don't Computers Read Letters?
Why does a computer read the word `HELLO` as `72 69 76 76 79`?

Because, at the most basic level, computers can only understand binary numbers (0 and 1). Meanwhile, letters are simply visual representations of numbers that have been agreed upon through certain encoding standards. Here's a simple example in Python:
```python
print(ord("A"))
# Output: 65
# This means that the letter "A" is actually the number 65.
```

### 2. ASCII Table
Simply put, ASCII or (American Standard Code for Information Interchange) is a standard that maps characters to numbers. Here's a simple example.
```python
Character A:	65
Character B:	66
Character a:	97
Character 0:	48
Character space:	32
```
Note the important pattern in the example above, where the uppercase letters A–Z have ASCII codes 65–90, while the lowercase letters a–z have ASCII codes 97–122, this will be useful later when studying cryptography techniques such as Caesar Cipher.

### 3. ord() dan chr()
Python itself provides two important functions for performing conversions, such as:
+ `ord()` which will change characters to numbers. Example:
```python
print(ord("C"))
# Output: 67
```
+ `chr()` which will convert numbers to characters. Example:
```python
print(chr(67))
# Output: 'C'
```

### 4. String to List of Numbers
In Python itself, we can convert an entire string into a list of numbers using the previous function. Here's an example in Python:
```python
text = "HELLO" # Plain text that you want to change
numbers = [ord(c) for c in text] # Convert each character to its ASCII value
print(numbers)
# Output: [72, 69, 76, 76, 79]
```

### 5. Bytes Object
Basically, bytes are the raw binary data used by Cryptographic algorithms. While humans read plain text, computers process bytes (numbers from 0–255). Here's an example in Python:
+ A string `"Hello"` is human-readable text. Meanwhile;
+ Bytes `b"Hello"` are the encoded binary representation.
The code implementation in Python itself can be created using the string `.encode()` method, which will convert a plain text string into a series of bytes. Here's an example:
```python
text = "hello"
byte_data = text.encode()
print(byte_data)
# Output: b'hello'
# If you want the result to be a series of numbers, we can write the list command in print like this.
print(list(byte_data)) # Output: [104, 101, 108, 108, 111]
```

### 6. Encode & Decode (UTF-8)
Computers store and process text in the form of bytes, not simple strings. For text to be processed by cryptographic algorithms, we must convert it into bytes using a specific encoding system. One of the most common encodings is UTF-8.

+ Encode
Simply put, UTF-8 is an encoding standard that converts characters into byte representations. Because most ASCII characters have the same byte value in UTF-8, that means "A" = 65, etc., here's an example of using UTF-8 encoding in Python.
```python
text = "Cyber"
byte_data = text.encode("utf-8")
print(byte_data)
print(list(byte_data))
# Output:
# b'Cyber'
# [67, 121, 98, 101, 114]
```
+ Decode
Meanwhile, UTF-8 decoding itself is the process of converting bytes back into human-readable text. We can do this using the `.decode()` method. Here's an example.
```python
b = [67, 121, 98, 101, 114]  # List of ASCII values
byte_data = bytes(b)         # Convert list to bytes
decoded_text = byte_data.decode("utf-8") # Decode bytes to string
print(decoded_text)
# Output: "Cyber"
```

## \<Modular Arithmetic\>
Modular arithmetic is a system of calculations that operates within certain limits and is cyclical. If the result of a calculation exceeds these limits, the value will return to the beginning. A simple example can be seen in a clock, as it only has 12 digits and after 12 digits, it returns to 0. With modular arithmetic, we can understand how messages can "cycle" within a system, resulting in encryption and decryption processes.

### 1. Modulo & Negative Modulo
+ Modulo (%),
As we know, modulo is a mathematical operation that finds the remainder of a division. For example:
```python
print(10 % 3)
print(15 % 12)
# Output: 1
# Output: 3
# Because, 10 ÷ 3 = 3 remainder  1 and 15 ÷ 12 = 1 remainder 3 (Easy).
```
In Cryptography, instead of simply thinking of modulo as the “remainder” of a division, it is better to think of modulo as:
> A system that keeps numbers within a limited range by wrapping around when the limit is exceeded.

For example, if we're working modulo 12 (like a clock), then the valid numbers are 0-11. If we go beyond that range, we "Wrap Around". Another example, if it is 10 o’clock and we move forward 5 hours, we do not get 15 o’clock. Instead, the clock wraps around. So the result is 3 o’clock.

This wrapping behavior is called a "Cyclic System", and it is fundamental in Cryptography. Many encryption systems operate within a fixed numeric range, just like a clock.

+ Negative Modulo,
It's not much different from modulo, except that it ensures that each result is positive. For example, in Python:
```python
print(-3 % 17)
print(-3 % 26)
# Output: 14
# Output: 23
```
Remember the previous explanation, just imagine the numbers arranged in a circle from 0 to 16. If you start from 0 and move back 3 steps, then you land in the 14th position. So `-3 mod 17 = 14`. Then what if the number is more negative like `-20 % 17`. All we need to do is add -20 to 17 until the result is positive and you will get the result.

So it can be said that this negative modulo is important for solving several problems related to decryption in cryptography such as Caesar cipher (mod 26), and others.

### 4. Power(a, b, m)
We all know what exponentiation is, and the way to do it in Python is by writing pow(a, b, m). This means `a` raised to the power of `b` modulo `m`, for example.
```python
print(pow(7, 4, 13))
# Process: 7^4 = 2401 and 2401 % 13 = 9
# Output: 9
```
In cryptography, we have to think that we are working in a circular system (mod m), so every time a number increases, we immediately return it to the circle. For example, we multiply in stages and modulate each step immediately.
```matlab
7 mod 13 = 7
7² = 49 → 49 % 13 = 10
7³ = 10 × 7 = 70 → 70 % 13 = 5
7⁴ = 5 × 7 = 35 → 35 % 13 = 9
# The result remains 9.
```
So In modular arithmetic, we work within a finite system and keep the numbers within that system at every step. This is important because in the RSA algorithm in Cryptography, if we do `pow(m, 65537, n)` or calculate the exponent first, then the mod. The computer may run out of memory.

### 5. GCD (Greatest Common Divisor)
GCD is the largest number that can divide two numbers without a remainder. In Python, we can compute it using `math.gcd()`.
```python
import math

print(math.gcd(21, 14))
# Output: 7
```
In GCD, if the result of is 1, the two numbers are called coprime. That means they share no common factors except 1. Example:
```python
import math

print(math.gcd(5, 9))
# Output: 1
```
In Cryptography Instead of thinking of GCD as just “common factors,” think of it like this:
> GCD checks whether two numbers are compatible inside a modular system.

If two numbers share factors, they are not independent in modular arithmetic. If they are coprime (GCD = 1), they can work properly in modular systems.

This is important in Cryptography because if two numbers are relatively prime, then a modular inverse can exist and be part of the RSA private key. A modular inverse of a modulo m exists **if and only if** gcd(a, m) = 1.

## \<Caesar Cipher Proper\>
Simply put, the Caesar Cipher is one of the simplest encryption techniques. Each letter is shifted k positions in the alphabet. For example, with key = 3:
```mathematica
A → D
B → E
C → F
```
After understanding the basic concept of how Caesar Cipher shifts letters, the next step is to implement it properly in code.
Instead of writing a quick script that only works for simple cases, we will build a clean and structured implementation that:
+ Handles uppercase and lowercase correctly.
+ Preserves non-alphabet characters.
+ Uses modular arithmetic properly.
+ Can be reused for both encryption and decryption. Here's the code:

```python
def caesar_encrypt(text, shift): # Encrypts the input text using the Caesar cipher with the specified shift.
    result = "" # Initialize an empty string to store the encrypted result.

    for char in text:
        if char.isalpha(): # Check if the character is an alphabet letter (either uppercase or lowercase).
            base = ord('A') if char.isupper() else ord('a') # Determine the base ASCII value based on whether the character is uppercase or lowercase.
            new_char = chr((ord(char) - base + shift) % 26 + base) # Calculate the new character by shifting the original character's ASCII value.
            result += new_char # Append the new character to the result string.
        else:
            result += char # If the character is not an alphabet letter, append it unchanged to the result string.

    return result # Return the final encrypted string after processing all characters.

print(caesar_encrypt("Hello, World!", 3)) # Print the encrypted result to the console.
# Output: Khoor Zruog!
```
After understanding the code above, there are several things we can find out, such as

### 1. Why do we need case handling? (Uppercase & Lowercase)
Because uppercase and lowercase letters in ASCII code have different ranges, we don't want the results to be corrupted. That's why we use:
```python
base = ord('A') if char.isupper() else ord('a')
# To determine the base ASCII value based on whether the character is uppercase or lowercase.
```
So that uppercase remains uppercase and lowercase remains lowercase.

### 2. Why Use Modulo 26?
The simplest is because there are 26 letters in the alphabet which are marked with the code `(ord(char) - base + shift) % 26`. So this ensures that if you pass Z, you will return to A, this is what makes the system "Circular".

### 3. Why is it made in function form?
Simply put, we want it to be **reusable**, **decryptable**, and **brute-forceable**. To decrypt, simply use a negative shift:
```python
def caesar_decrypt(text, shift):
    return caesar_encrypt(text, -shift)
```

## \<XOR Cipher\>
So, XOR is a binary logic operation that uses the symbol `^` in Python. The most important property of XOR is that if the same key is XORed twice, it will revert to its original value. This is what makes XOR suitable for encryption and decryption, with the same function.

### 1. What is XOR?
Basically, XOR is a logical function and binary operator that produces a value of TRUE if the inputs are **different**, and FALSE if the inputs are the **same**. The following is the basic table:
```
0 ^ 0 = 0
0 ^ 1 = 1
1 ^ 0 = 1
1 ^ 1 = 0
```

### 2. Simple Example
Now let's try the simplest example: writing the command 5^3 in the Code Editor, which will produce the value 6. Why 6?
Because in binary:
```markdown
5 = 101
3 = 011
---------
    110 = 6
```

### 3. XOR for Text Encryption
Since computers work with bytes, we need to XOR each byte with a key. A simple implementation example:
```python
def xor_cipher(text, key):
    result = ""
    for char in text:
        result += chr(ord(char) ^ key)
    return result
encrypted = xor_cipher("HELLO", 42)
print(encrypted)
# ASCII: [72 69 76 76 79] di XOR 42
# Output: boffe
```

### 4. How to Think in Cryptography?
Unlike Caesar, which uses modulo 26 (letters only), XOR operates at the byte level (0–255). This means:
+ Unlimited alphabets.
+ Can encrypt files.
+ Can encrypt binary data. Remember this:
```ini
cipher = plaintext ^ key
plaintext = cipher ^ key
```

## \<Brute Force & Key Space\>
Now that we've learned how to encrypt, let's learn how to attack it. In cryptography, if something can be encrypted, it can theoretically be attacked. This principle is similar to that used in CTF problems or in Cybersecurity, with the only difference being how difficult it is.
### 1. What is Key Space?
Key space is the number of possible keys that can be used. For example, the Caesar Cipher has a shift range of only 0–25. This means its key space has 26 possibilities.

This means an attacker can try all the possible keys in a matter of seconds.

### 2. What is Brute Force?
Brute force is an attack method that tries all possible keys one by one. For example, the Caesar brute force method:
```python
def brute_force_caesar(ciphertext):
    for key in range(26):
        decrypted = caesar_encrypt(ciphertext, -key)
        print(f"Key {key}: {decrypted}")
```
The attacker simply sees which result makes sense and doesn't need to know the key. This is different from XOR, which uses bytes as the key. Therefore, brute force is impossible because it has `2^128 possibilities`.

## Challenges — Easy
**Title: Alphabet Shift Recovery**\
**Task Description: You are given the following ciphertext `fbehuFWI_Iodj`**\
**Your task is to:**
+ Identify the type of cipher used.
+ Recover the original plaintext.
+ Determine the key (shift value).
> [!TIP]
> Hint: Khoor = Hello

**You are allowed to:**
+ Write your own Caesar decrypt function.
+ Use brute force if necessary.


## Challenge 2 — Medium
**Title: XOR Byte Investigation**\
**Task Description: You are given a ciphertext generated using a single-byte XOR key.**

**Ciphertext (in decimal byte values): [79, 70, 69, 69, 66]**\
**The encryption method used: cipher_byte = plaintext_byte ^ key**\
**Your task:**
+ Determine the key.
+ Recover the plaintext.
> [!TIP]
> Hint: Plaintext consists only of uppercase letters.

**What Must to Identify:**
+ Convert numbers to characters.
+ Try possible XOR keys (0–255).
+ Detect meaningful plaintext.
+ Understand small key space weakness.

## Output
Participants must demonstrate understanding of:
+ Characters & bytes representation.
+ Modular arithmetic.
+ GCD & coprime.
+ Caesar & XOR cipher.
+ Brute force attack concept.
