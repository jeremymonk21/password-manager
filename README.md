# password-manager



## **Project Overview**

This project involved the development of a secure and user-friendly GUI-based Password Manager using Python and the Tkinter library. The Password Manager allows users to store, retrieve, and manage their passwords securely, employing encryption techniques to protect sensitive information.

## **Features**

### **1. User-friendly Interface:**

- Implemented a clean and intuitive graphical user interface (GUI) using Tkinter.
- Organized input fields for service, username, and password for easy interaction.
-![image](https://github.com/jeremymonk21/password-manager/assets/153461563/a692e7ea-564e-45ae-aa40-b77c7ac23290)


### **2. Encryption for Passwords:**

- Utilized the **`cryptography.fernet`** library to encrypt and decrypt passwords securely.
- Enhanced the security of stored passwords to safeguard sensitive data.

### **3. Data Persistence:**

- Implemented data persistence using a JSON file (**`passwords.json`**) to store encrypted passwords.
- Ensured that passwords remain securely stored across different sessions.

### **4. Password Management Operations:**

- **Save Password:**
    - Captured and encrypted user-provided service, username, and password.
    - Added functionality to save the encrypted password securely.
- **Retrieve Password:**
    - Enabled users to retrieve passwords by entering the service name.
    - Decrypts and displays the retrieved password securely.
- **List Accounts:**
    - Provided an option to list all stored accounts for user convenience.
    - Displayed a message box containing the list of accounts.

### **5. Error Handling and Security Measures:**

- Implemented error handling for scenarios such as file not found and JSON decoding errors.
- Ensured secure handling of encoded passwords with proper padding and decoding.

### **6. Secure Data Transmission:**

- Employed secure data transmission using encryption, protecting sensitive information from unauthorized access.

## **Technologies Used**

- **Python 3:** The primary programming language used for development.
- **Tkinter:** Employed for building the graphical user interface.
- **Cryptography:** Utilized the Fernet symmetric key encryption for secure password handling.
- **JSON:** Used for storing and retrieving encrypted passwords in a structured manner.

## **Usage**

1. **Save a Password:**
    - Enter the service, username, and password.
    - Click the "Save Password" button to securely store the encrypted password.
2. **Retrieve a Password:**
    - Enter the service name.
    - Click the "Get Password" button to retrieve and decrypt the stored password.
3. **List Accounts:**
    - Click the "List Accounts" button to view a list of all stored accounts.

## **Security Measures**

- **Encryption:** Passwords are encrypted using Fernet symmetric key encryption, enhancing data security.
- **Error Handling:** Robust error handling to address file not found and JSON decoding errors.
- **Secure Transmission:** Ensured secure transmission and storage of passwords to prevent unauthorized access.

## **Conclusion**

This Python GUI Password Manager project demonstrates a commitment to enhancing user security and convenience. By incorporating encryption and secure coding practices, the application provides a reliable solution for managing passwords in a secure and user-friendly manner.

# EXPLAINING THE CODE 

### **1. Import Statements:**

```python
pythonCopy code
import tkinter as tk
from tkinter import messagebox
from cryptography.fernet import Fernet
import json
from base64 import b64encode, b64decode
import binascii

```

- **tkinter:** The standard GUI library for Python, used to create the graphical user interface.
- **messagebox:** Part of tkinter, used for displaying informative or warning messages.
- **cryptography.fernet:** A library for symmetric (same key for encryption and decryption) key encryption, used for securing passwords.
- **json:** Used for reading and writing JSON data.
- **base64:** Used for encoding and decoding data in Base64 format.
- **binascii:** Handles errors during Base64 decoding.

### **2. PasswordManagerGUI Class:**

### Constructor (**`__init__`** method):

```python
pythonCopy code
def __init__(self, master):
    # ... (GUI setup code)

    # Generate or load the encryption key
    self.key = Fernet.generate_key()
    self.cipher_suite = Fernet(self.key)

    # Create a PasswordManager instance
    self.password_manager = PasswordManager(self.cipher_suite)

    # Create GUI elements
    # ... (Label, Entry, Button setup)

# Other methods: save_password, get_password, list_accounts

```

- **`__init__` Method:**
    - Initializes the GUI window and sets up various elements like labels, entry fields, and buttons.
    - Generates an encryption key using **`Fernet`** and creates an instance of the **`PasswordManager`** class.

### **3. PasswordManager Class:**

### Constructor (**`__init__`** method):

```python
pythonCopy code
def __init__(self, cipher_suite):
    self.cipher_suite = cipher_suite
    self.file_path = "passwords.json"
    self.passwords = self.load_data()

```

- **`__init__` Method:**
    - Initializes the **`PasswordManager`** instance with a given **`cipher_suite`** (used for encryption/decryption).
    - Sets the file path for storing passwords as "passwords.json".
    - Calls the **`load_data`** method to load existing password data or create an empty dictionary.

### Encryption and Decryption Methods:

```python
pythonCopy code
def encrypt(self, data):
    return self.cipher_suite.encrypt(data.encode())

def decrypt(self, data):
    return self.cipher_suite.decrypt(data).decode()

```

- **`encrypt` Method:**
    - Encrypts the provided data (password) by encoding it and using the **`Fernet`** cipher.
- **`decrypt` Method:**
    - Decrypts the provided data (encrypted password) using the **`Fernet`** cipher and decodes it.

### Password Management Methods:

```python
pythonCopy code
def add_password(self, service, username, password):
    # ... (code for adding a password)

def get_password(self, service):
    # ... (code for retrieving a password)

def get_account_list(self):
    # ... (code for getting a list of accounts)

```

- **`add_password` Method:**
    - Adds a new password for a given service, encrypting it before storage.
- **`get_password` Method:**
    - Retrieves the encrypted password for a given service.
- **`get_account_list` Method:**
    - Returns a list of all stored account names.

### File I/O Methods:

```python
pythonCopy code
def load_data(self):
    # ... (code for loading data from the "passwords.json" file)

def save_data(self):
    # ... (code for saving data to the "passwords.json" file)

```

- **`load_data` Method:**
    - Reads and loads existing password data from the "passwords.json" file.
    - Handles Base64 decoding errors and Unicode decoding errors during the loading process.
- **`save_data` Method:**
    - Writes the current password data to the "passwords.json" file, ensuring proper encoding.

### **4. Tkinter GUI Elements:**

- Labels, Entry widgets, and Button widgets for capturing service, username, and password information.
- Button actions (**`save_password`**, **`get_password`**, **`list_accounts`**) are connected to the corresponding methods in the **`PasswordManagerGUI`** class.

### **5. Application Execution:**

```python
pythonCopy code
# Create the Tkinter window
root = tk.Tk()
app = PasswordManagerGUI(root)

# Run the Tkinter event loop
root.mainloop()

```

- Creates an instance of the **`Tk`** class to represent the main window.
- Instantiates the **`PasswordManagerGUI`** class and starts the Tkinter event loop, allowing the GUI to be interactive.

This code provides a simple yet effective implementation of a GUI Password Manager, utilizing encryption for securing sensitive information and a JSON file for persistent data storage. It demonstrates key principles of GUI development, encryption, and file handling in Python
