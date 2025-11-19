# 🔐 Vigenère Cipher – Python Encryption & Decryption

This project is an implementation of the **Vigenère Cipher**, a classic polyalphabetic substitution technique used for secure message encryption.  
The program can **encrypt and decrypt text** based on a keyword, making it a great introduction to cryptography and algorithmic thinking.

---

## 🚀 Features

### 🔸 Encryption & Decryption
- Uses the Vigenère cipher algorithm  
- Supports both encoding and decoding  
- Shifts characters based on a repeated keyword

### 🔸 Preserves Non-Alphabet Characters
- Spaces and punctuation remain unchanged  
- Only alphabetical characters are encrypted

### 🔸 Case Handling
- Works with uppercase & lowercase  
- Output is produced in lowercase for consistency

### 🔸 Reusable Helper Functions
- `vigenere()` → core cipher logic  
- `encrypt()`  → message encryption  
- `decrypt()`  → message decryption  

---

## 🧠 How the Algorithm Works

The Vigenère cipher uses:
- A **message**
- A **keyword**
- An alphabet-based shift for each character

For each letter:
1. Take the next letter from the keyword  
2. Convert it to an index shift  
3. Apply the shift (+ for encryption, − for decryption)  
4. Wrap around using modulo arithmetic  

This produces a more secure cipher compared to single-shift ciphers like Caesar.

---

## 📌 Code Implementation

```python
text = 'mrttaqrhknsw ih puggrur'
custom_key = 'python'

def vigenere(message, key, direction=1):
    key_index = 0
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    final_message = ''

    for char in message.lower():

        # Append any non-letter character to the message
        if not char.isalpha():
            final_message += char
        else:        
            # Find the right key character to encode/decode
            key_char = key[key_index % len(key)]
            key_index += 1

            # Define the offset and the encrypted/decrypted letter
            offset = alphabet.index(key_char)
            index = alphabet.find(char)
            new_index = (index + offset*direction) % len(alphabet)
            final_message += alphabet[new_index]
    
    return final_message

def encrypt(message, key):
    return vigenere(message, key)
    
def decrypt(message, key):
    return vigenere(message, key, -1)

print(f'\nEncrypted text: {text}')
print(f'Key: {custom_key}')
decryption = decrypt(text, custom_key)
print(f'\nDecrypted text: {decryption}\n')
