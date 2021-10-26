# Simplified AES

### _Implementation using Client-Server Communication_

- Enter two alphabets long secretkey i.e. 16-bits of data.

## Client Server Communication

- ### client.py

  - **modules(built-in)**
    - multiprocessing: _sending and receiving message oriented pickles with ease_
    - pickle: _to send and receive objects_
    - hashlib: _to hash message using different hashing algorithms_
  - **modules(created)**
    - rsa _(rsa.py)_: rsa class for encryption, decryption and compute public and private keys
    - encryption _(encryption.py)_: aes variant encryption and key generation
  - **inputs** :
    - message
    - secret key
    - client key parameters
  - **operations**
    - requests and receives server public key from server _(server.py)_
    - encrypts secret key and sends it to the server
    - encrypts plaintext and sends ciphertext to the server
    - sends client public key to the server
    - computes client signature by hasing message and sends it to the server

- ### server.py
  - **modules(built-in)**
    - multiprocessing: _sending and receiving message oriented pickles with ease_
    - pickle: _to send and receive objects_
    - hashlib: _to hash message using different hashing algorithms_
  - **modules(created)**
    - rsa _(rsa.py)_: _rsa class for encryption, decryption and compute public and private keys_
    - decryption _(decryption.py)_: _aes variant decryption and key generation_
  - **inputs** :
    - server key parameters
  - **operations**
    - sends server public key to client _(client.py)_
    - receives encyrpted secret key from client
    - receives encyrpted plaintext(cipher text) from client
    - decrypts ciphertext using aes variant
    - receives client public key for signature verification
    - computes client signature by hasing message and verifies it with the message digest

---

## Modules

- ### func.py
  - isPrime(): returns True if a number is prime False otherwise
  - gcd(): return the greatest common divisor of an integer
  - is_coprime(): return True if two integers are co-prime i.e. their gcd is 1
  - modInverse(): returns the modular inverse of a mod b
  - ConvertToInt(): converts a string to its integer equivalent using each character's ASCII value
  - ConvertToStr(): takes the integer output of ConvertToInt() as an input to compute the string fed in ConvertToInt()
- ### rsa.py

  _Rsa class for encryption, decryption and key generation_

  - **Module _(created)_**
    - func _(func.py)_
  - **Parameters**: Key Generation Paramters (p,q,r)
  - **Variables**:
    - `p`,`q`,`e` (key generation parameters)
    - `n` _(p\*q)_
    - `phi` _(p-1)(q-1)_
    - `prKey` (private Key)
    - `pubKey` (public key)
    - `plaintext` (message to be encrypted)
    - `ciphertext` (encrypted message)
    - `f` (flag for key parameters validation)
  - **Methods**:
    - Constructor: initialises key parameters, validates them and generates key if key parameters valid
    - genKey(): generates public key and private upon validation else assigns `f = 1`
    - validate(): checks the validity of key generation parameters
    - encrypt(): encrypts the `plaintext` with `prkey` generated using `genKey()`. Also, a duplicate function can be used independently without instantiating the class object.
    - decrypt(): decrypts the `ciphertext` with the `pubKey` generated using `genKey()`. Also, a duplicate function can be used independently without instantiating the class object.

- ### aes.py
  - tobits(): converts string into bit array
  - frombits(): converts the bitarray from `tobits()` back into the original string.
  - formatMsg(): slices the string into list with each element of size 16-bits for encryption/decryption.
  - modInverse(): returns the modular inverse of a mod b
  - formBlocks(): converts string of data into a list with each element representing a block (4-bits)
  - addKey(): complimentary function to perform XOR operationg
  - SubNib(): to perform subsitution operation while encryption and key generation using `encryptBox`
  - dSubNib(): performs inverse substituion during decryption using `decryptBox`
  - RotNib(): performs row shift operation
  - galoisMultiply(): performs mix colum operation
  - keyGeneration(): to generate keys `K0`,`K1`,`K2` and `K3`
  - encryption(): to encrypt message and returns the ciphertext
  - decryption(): to decrypt a ciphertext and returns the original plaintext

---

:cyclone: :cyclone: :cyclone:
