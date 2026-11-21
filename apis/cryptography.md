# Cryptography API

Source: `_G.crypto`

## Summary

The cryptography module applies an encryption algorithm to the provided data, and return the encrypted version as a Base64 string.

This page assumes that the user already has basic understanding of the algorithms implemented.

The module itself contains sub-modules, each for an algorithm or utilities. These are:
- `.AES`
- `.RSA`
- `.Hash`
- `.SecureRNG`
- and `.Base64`

This documentation page will be divided into a reference for each module.

*Please note*
Methods that return binary data return it as base64, there is no need to re-encode it. Decoding is possible, but is not very useful in cases of storage and transimission, which is the primary use case of this module.

## AES

### GenerateKey()
Generates a random secret key.

`returns String`

### GenerateIv()
Generates 12 bytes of random data to be used as the Initialisation Vector (IV).

`returns String`

### GenerateSalt()
Generates 32 bytes of random data to be used as the salt (see `GenerateKeyFromPassword`).

`returns String`

### GenerateKeyFromPassword(string password, string salt)
Generates a key from a provided password, salted with the salt parameter.

`returns String`

### Encrypt(string SecretKey, string IV, string data)
Encrypt the provided data with the key and IV.

`returns String`

### Decrypt(string SecretKey, string IV, string data)
Undoes the encryption on the given data with the key and IV.

`returns String`

## RSA

### GenerateKeyPair()
Generates a random key pair. The public key is first, followed by the private key.

`returns String, String`

### Encrypt(string PublicKey, string data)
Encrypts the data with the given public key.

`returns String`

### Decrypt(string PrivateKey, string data)
Decrypts the data with the given private key.

`returns String`

### Sign(string PrivateKey, string data)
Returns the RSA signature of the data

`returns String`

### Verify(string PublicKey, string data, string signature)
Verifies a signature is valid and from the same key pair as the public key.

`returns Boolean`

## Hash

### SHA256(string data)
returns the SHA-256 hash of the data.

`returns String`

### MD5(string data)
returns the MD5 hash of the data. Not recommended for actual cryptography.

`returns String`

## SecureRNG

### GetRandom()
Returns a random number.

`returns Decimal`

### GetRandomFromMin(number min)
Returns a random number from min.

`returns Decimal`

### GetRandomUpTo(number max)
Returns a random number up to max.

`returns Decimal`

### GetRandomBetween(number min, number max)
Returns a random number between min and max.

`returns Decimal`

## Base64

### Encode(string data)
Returns the data encoded as Base64.

`returns String`

### Decode(string data)
Returns the data originally encoded in Base64.

`returns String`