![Banner](banner.png)

## **Technical Documentation for Security Analysis Tool**

### **1. Tool Overview**

**Tool Name:** `crypto-password-generator`

**Category:** Cryptography

**Overview:**

`crypto-password-generator` is a command-line tool that generates random, secure passwords. It utilizes core cryptographic operations for password generation.

### **2. Analysis Purposes**

The tool is designed to assist in the creation of strong and secure passwords, mitigating the risk of password compromise. It does not focus on comprehensive security analysis but rather provides a specific utility for password generation in a secure manner.

### **3. Installation Steps**

There is no pip package for this tool. Clone the repository and install the one dependency:

```
git clone https://github.com/ShadowGuard-AI/crypto-password-generator.git
cd crypto-password-generator
pip install -r requirements.txt
```

### **4. Usage Examples**

```
# Basic usage: Generate a 16-character password
python3 main.py

# Specify password length
python3 main.py --length 24
```

**Safeguards:**

- Passwords are generated using a cryptographically secure pseudo-random number generator (CSPRNG) to ensure randomness and unpredictability.
- Users can specify the desired password length to meet specific security requirements.
- The tool does not store or share the generated password, minimizing the risk of compromise.

### **5. Implementation Details**

**Core Functions:**

- `setup_argparse()`: Sets up command-line argument parsing for specifying password length (`-l` / `--length`), a custom salt (`-s` / `--salt`), and the PBKDF2 iteration count (`-i` / `--iterations`), plus `-v` / `--version`. There is no saving option: the generated password is printed to the console and is not written to a file.
- `main()`: Implements the core functionality of password generation.

**Security Features:**

- **CSPRNG:** The random material comes from the Python standard library `secrets` module (`secrets.token_bytes`, at main.py lines 63 and 78), not from the `cryptography` package. The `cryptography` package provides the PBKDF2-HMAC-SHA256 key derivation that stretches that random material.
- **Password Complexity:** The password is the derived key encoded as URL-safe base64 and cut to the requested length, so its characters are letters, digits, `-` and `_`. It does not add symbol classes beyond that alphabet. The exit code is 1 when generation fails (for example a length or iteration count below 1).
- **No Storage or Sharing:** The generated password is not stored or shared anywhere, eliminating the risk of accidental disclosure or compromise.

### **6. License and Compliance Information**

**License:** GNU General Public License v3.0 (GPL-3.0). See the LICENSE file in this repository.

**Compliance:**

- Complies with best practices for password security and randomness.
- Meets industry standards for generating secure passwords.