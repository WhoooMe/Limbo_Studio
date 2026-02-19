 #Beginner #Basic-Python #Scripting #WSL #VS Code

## Goals
Students will be able to understand core Python concepts, identify basic syntax, and analyze the behavior of simple programs. They can run scripts in various environments, debug basic errors, and build small programs using conditions, loops, and functions. Students will also be able to apply these skills to automate simple tasks and prepare for more advanced cybersecurity scripting.

## Prerequisites
Participants should have the following knowledge or preparation before taking this module:
+ Basic computer literacy and familiarity with navigating files and folders.
+ Ability to use a terminal or command-line interface (e.g., cd, ls, mkdir).
+ A working installation of Python and Visual Studio Code.
+ Basic understanding of how to run commands on Windows, macOS, or Linux.
+ Completion of the environment setup module [Python-Setup.md]

## \<Introduction to Python\>

Python is one of the world's most popular programming languages, used for everything from simple application development to large-scale systems like machine learning, automation, cybersecurity, and data analytics. Its strength lies in its clean, readable syntax, allowing beginners to learn it without being overwhelmed by complex writing rules. Through this workshop, participants will learn the core foundations of Python, which form the basis for building scripts, automating, and preparing them for exploration into more advanced areas such as cybersecurity or ethical hacking.
‎ 
## \<Syntax in Python\>
Python is known for its clean and easy-to-understand syntax, making it perfect for both beginners and professional applications such as automation and cybersecurity. Here are some basic syntaxes in the Python programming language:
‎ 
### 1. Statements & Expressions
In Python, all programs are built from two main components: statements and expressions. While they may seem similar, they serve different functions. Here's how to distinguish them. An expression is a piece of code that produces a value. Every expression always has a result, no matter how small. Here is a simple example `5 + 3` which will produce the value eight.

Another example of an expression:
```python
"Hello" + "World"
10 * 20
x > 5
```
So it can be said that an expression in Python can be:
+ Mathematical operation.
+ Logical operation.
+ Function call.
+ Literal (such as a number or string).
+ Combination of the above.

Meanwhile, a statement is a complete instruction that Python executes. A statement can contain an expression, but it doesn't have to produce a value. For example `print("Hello")`. Here's another example of a statement:
```python
x = 10
if x > 5:
print("Bigger")
```
So it can be said that statements provide instructions, not values. Python itself recognizes many types of statements, such as:
+ Assignment like `x = 5`.
+ Control flow like `if, else, for, while`.
+ Import like `import math`.
+ Function definition like `def myfunc():`.
+ Return like `return x`.
‎ 
### 2. Indentation
Unlike many other languages ​​that use `{}` to mark blocks of code, Python uses indentation. Here's a simple example:
```python
x = 10

if x > 5:
  print("x is greater than 5") # Here is the indentation for the if true condition
else:
  print("x is not greater than 5") # Here is the indentation for the if false condition
```
So, simply put, indentation in Python is used to mark a block of code, whether it's a statement like if, else, elif, for, while, class, etc. Indentation also has a standard rule of 4 spaces, which indicates the level of the code block being executed. Here's a simple example:
```python
if True:
    print("Hello") # Indentation 4 space
    if True:
        print("Wolrd") # Indentation 8 space
```
> [!NOTE]
> These indentation rules are not bound by the number of spaces, but remember to maintain consistency in each block of code created to avoid SyntaxErrors.

### 3. Variables
Variables in Python don't require explicit data type declaration, as the Python programming language automatically recognizes user-defined data types. Therefore, we only need to specify the variable name and its value. Here are some examples:
```python
name = "Jordan" # String type
age = 21 # Integer type
height = 170.5 # Float type
is_member = True # Boolean type
```
Like other programming languages, Python itself consists of several rules for writing variables to prevent errors such as:
+ Must start with a letter or underscore `_`.
+ Can only contain letters, numbers, and `_`
+ Case-sensitive (`Age` and `age` are considered different)
+ Spaces are not allowed
+ Python keywords (e.g., `if`, `while`, `import`, `class`, `return`, `try`, `except`, `def`, `class`, etc.) are not allowed.

### 4. Print & String Basics
Print is essentially used to display text, numbers, or calculation results on the user's screen. Here are some examples of print commands in Python:
+ Basic example `print("Hello World")`
+ Print with multiple values ​​where Python automatically puts spaces between arguments `print("My age is", 20)`
+ Print operation results `print("Result =", 5 + 3)`
+ Print without newlines
```python
print("Hello", end=" ")
print("World")
```
+ Print with escape characters
```python
print("Line1\nLine2")
# \n for new line
# \t for tab
# \" for quotation marks
```
+ F-string to insert a variables, for examples:
```python
name = "Alex"
print(f"Hello, {name}")
print(f"5 + 5 = {5 + 5}")
```

### 5. Basic Input
Basically, input itself allows users to provide input to a program so that it can produce a value or action, according to how the program works, for example:
```python
username = input("Enter your name: ")
print("Hello,", username)

age = input("Your age: ")
print(type(age))
```
‎ 
## \<Control Flow\>
Control flow is how Python determines what to execute next based on certain conditions. Without it, a program would simply run in a straight line without any clear direction or purpose. Control flow allows us to make decisions, limit execution, and build more complex logic. Here's an example of control flow:

### 1. If Statement
Used to run code only if a condition evaluates to `true`. Example:
```python
age = 18

if age >= 18:
    print("You are allowed.")
```

### 2. If–Else
`else` here is used to run an alternative block if the condition is not met. Example:
```python
score = 70

if score >= 75:
    print("Pass")
else:
    print("Fail")
```

### 3. If–Elif–Else
`elif` itself is used when there are several different conditions that need to be checked sequentially, it could be said that this is similar to else if in C/C++ language. Example:
```python
value = 0

if value > 0:
    print("Positive")
elif value < 0:
    print("Negative")
else:
    print("Zero")
```

### 4. Nested Conditions
Essentially, nested conditions occur when a program requires complex, multi-level decision-making to achieve a desired goal. This can be accomplished by adding an if or elif statement within an else statement. Example:
```python
age = 20
member = True

if age >= 18:
    if member:
        print("Access granted")
    else:
        print("Membership required")
```

Last but not least, here are some operators that can be used in Control Flow:
+ `==`: Equals.
+ `!=`: Not equal.
+ `>`: Greater.
+ `<`: Less.
+ `>=`: Greater than or equal to.
+ `<=`: Less than or equal to.
+ `and`: Both conditions must be true.
+ `or`: One of the conditions must be true.
+ `not`: Invert True/False values.
‎ 
## \<Loops\>
Loops in Python essentially allow a program to execute blocks of code repeatedly without having to write them manually. Python has two main types of loops: `for loops` and `while loops`, which have different functions. Here's an explanation.

### 1. For loops
Used to repeat something that has a clearly defined number, such as a list, string, or range of numbers. Example:
```pyhton
for i in range(5):
    print(i)
```
Here's the results:
```pyhton
0
1
2
3
4
```
### 2. While loops
Used when we want to repeat until a certain condition is met.
Suitable for: user input, program menus, infinite loops that stop when a certain condition is met, etc. Here's an example:
```python
count = 0

while count < 5:
    print(count)
    count += 1
```
### 3. Break and Continue
Last but not least, there are break and continue statements. Here's an simple explanation.
+ Break is used to stop a loop completely. Here's an example:
```python
for i in range(10):
    if i == 5:
        break
    print(i)
```
+ Continue is used to jump to the next iteration. Here's an example:
```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

## \<Functions\>
Functions in Python are essentially blocks of code that can be called back. So, we only need to write one block of code in a program to be able to use it multiple times without having to rewrite the logic. Functions in Python can be written using the following structure.
```python
def nama_fungsi():
    # isi fungsi
    print("Halo dari fungsi!")
```
To make a function work, we can call it with the code `function_name()` according to the function created. Functions also have parameters. In short, parameters are "slots" where we pass data so the function can work (Local Variables). Here's an example.
```python
def sapa(nama):
    print(f"Halo {nama}!")

sapa("Dewi")
sapa("Raka")
```
There is something no less important to discuss regarding this function, here are some things that this function can do.

### 1. Default Parameter
In a function you can provide parameters that have default values, so that when the function is called it will produce those default values. Example:
```python
def halo(nama="User"):
    print(f"Halo {nama}!")

halo()
halo("Mira")
```

### 2. Keyword Arguments
 Keyword arguments are useful when calling functions that have many parameters or default values. Since positional arguments depend on order, passing them incorrectly will assign values to the wrong parameters. The following is an example of using keyword arguments:
```python
def biodata(nama, umur):
    print(f"{nama} berusia {umur} tahun.")

biodata(umur=20, nama="Andi")
```
and this one doesn't use a keyword arguments
```python
def biodata(nama, umur, kota):
    print(nama, umur, kota)

biodata("Dewi", 19, "Denpasar")
```

### 3. Return Value
As the name suggests, the `return` function in a function is used to send the result of that function outside the function itself. Therefore, functions that use `return` can not only do something, but also produce something. Here's an example:
```python
def tambah(a, b):
    return a + b

hasil = tambah(3, 5)
print(hasil)
```

### 4. Return Multiple Values
Python itself also allows users to return multiple values ​​at once from a single function. Here's an example:
```python
def hitung(a, b):
    tambah = a + b
    kurang = a - b
    return tambah, kurang

x, y = hitung(10, 4)
print(x, y)
```

## \<Core Libraries in Cryptography\>
In our future material, we will use several libraries or built-in modules in Python, therefore, here are some libraries commonly used in solving CTF problems.

### 1. hashlib
This module is used to create a hash of data using algorithms such as MD5, SHA-1, SHA-256 or SHA-512. Example:
```python
import hashlib

text = "hello"
hash_object = hashlib.sha256(text.encode())
print(hash_object.hexdigest())
```

### 2. base64
Used to encode bytes into ASCII text. Base64 is not encryption, just encoding so that binary data can be transmitted as text. It is used for data transfer via HTTP, tokens, and many CTF challenges.

### 3. binascii
The binascii library is used to convert binary data (bytes) to hexadecimal or hexadecimal to bytes. In Cryptography, data is often displayed in hex format because it is easier for humans to read than raw bytes.

### 4. math
In the context of cryptography, the math library is often used for basic mathematical functions, particularly `gcd()` (Greatest Common Divisor). This function is crucial in algorithms like RSA, as it is used to check whether two numbers are relatively prime.

### 5. os.urandom
With this library, we can generate random bytes from the operating system. This is typically used for key generation, cryptographic randomness, etc. It usually serves as a source of entropy (the degree of randomness) in cryptographic systems. Example:
```
Low Entropy (Dangerous): Password: 123456 or password
High Entropy (Safe): Result of os.urandom(16): b'\xd1\x8f\x02\x4c...'.
```

### 6. secrets
The secrets library is specifically designed to generate cryptographically secure random numbers. Unlike the random module, which is suitable for simulations or games, secrets uses the operating system's entropy source to ensure its results are unpredictable. Example:
```
import secrets

# Membuat token rahasia untuk link reset password
token = secrets.token_urlsafe(16) 
print(token) # Hasilnya bersih: '_qW2-pL9rGz...'
```

### 7. hmac
The hmac library is used to create a Hash-based Message Authentication Code (HMAC), a mechanism that combines hashing with a secret key. Unlike regular hashing, which only produces a fingerprint of the data, HMAC ensures that the message was actually created by the party possessing the secret key. This is often used in API authentication and data integrity verification.

## Challenges 1 - Simple Login & Menu System
**Objective: Create a simple program that uses input, if-elif-else, loops, dan functions.**\
**Create a program with the following conditions:**\
+ The program prompts the user to enter `Username` and `Password`.
+ If the username is "admin" and the password is "python123", display `Login successful!` and if incorrect, display `Login failed!`.
+ If login is successful, display the following menu:
```markdown
Login successful!
1. Show Greeting
2. Exit
```
> [!TIP]
> Use a while loop so that the menu continues to appear until the user selects Exit.
> 
> Create a separate function for the Greeting menu and use the username as a parameter.

## Output
After completing this module, participants must produce the following:
+ A Python script demonstrating the use of variables, conditionals, loops, and functions.
+ A write-up explaining how the script works, including logic flow and key components.
