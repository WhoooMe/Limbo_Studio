## Unlocking Systems with Python
This material was prepared by the Cyber Security Division for the ### workshop. It serves as a starting point for anyone beginning their journey with Python. The content introduces the required setup and the core concepts that will become the foundation for further programming.

## What is Python?
Python is a high-level and open-source programming language created by Guido van Rossum in 1991. It's provides a clear, readable structure that helps users focus on solving problems instead of dealing with complex syntax.

## Why Python?
 + Beginner Friendly: Python has a simple syntax similar to the English language.
 + Cyber Security: More flexible in scripting making it ideal for automated analysis and understanding system behavior.
 + Powerful Ecosystem: Supported by thousands of libraries that enable rapid development for both beginners and professionals.

---

## Installing Python

### 1. Windows
Suitable for: Users who want a simple installation process and direct integration with Windows tools.

Minimum Requirements:
+ Windows 10 / 11 (64-bit).
+ At least 4 GB RAM.
+ 500 MB free disk space.
+ Internet connection (for installer download).

Steps:
- Download Python from [Python for Windows.](https://www.python.org/downloads/).
- Run the installer, then check “Add Python to PATH” before selecting Install Now.
- Wait until the installation is complete, then click Close.
- Verify the installation by opening PowerShell and running command ``` python --version ```

### 2. macOS
Suitable for: Users who prefer a clean development setup using macOS’s Unix-based environment.

Minimum Requirements:
+ macOS Monterey or later.
+ At least 4 GB of RAM or more.
+ 500 MB of free disk space.
+ Internet connection for download.

Steps:
- Download the installer for macOS at [Python macOS.](https://www.python.org/downloads/macos/)
- Open the ```.pkg``` file and follow the installation instructions until complete.
- Open Terminal and verify the Python version with command ``` python3 --version ```.

---

## Python Environment Setup in VS Code

After installing Python and VS Code, you can start writing your first Python program. VS Code will detect your Python installation automatically, but you’ll need to select the interpreter before running your script. Follow the steps below to get started:

### 1. Create a New Python File
+ Open VS Code.
+ Click `File` > `New File`.
+ Type a simple line of code like ```print("Hello World!")```.
+ Save the file using `Ctrl + S` (or `Cmd + S` on macOS).
+ Choose a folder, then name the file with the extension ```.py```. Here is for the example: ``` hello.py.```

### 2. Select the Python Interpreter
+ Open the Command Palette using `Ctrl + Shift + P` (Windows/Linux) and `Cmd + Shift + P` (macOS)
+ Type “Python: Select Interpreter”.
+ Choose the interpreter that matches your installed Python version\
  (for example: Python 3.x.x -- from python.org).

### 3. Run the Python File
Once the interpreter is selected, you will see a Run button ▷ at the top right of the editor, click on it to run the script or you can also use the terminal and type `python [Python filename].py`

---



