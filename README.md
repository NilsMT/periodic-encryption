# Periodic Encryption

## Summary

This package allows you to encrypt and decrypt messages by the mean of `Vigenère Cipher` and `Periodic Table of Elements`.

## Table of contents

1. [Installation](#installation)
2. [About this package](#about-this-package)
3. [In a nutshell how does it work](#in-a-nutshell-how-does-it-work)
4. [Package Documentation](#package-documentation)
    - [Encryption Category](#encryption-category)
    - [Element Category](#element-category)
    - [Vigenère Cipher Category](#vigenère-cipher-category)

## Installation

Enter the following command :
```sh
pip install periodicencryption
```

## About this package

This package allow you to encrypt and decrypt messages by the mean of `Vigenère Cipher` and `Periodic Table of Elements`.

## In a nutshell how does it work

Strings are made up of characters, those characters have a unique code (generally called ASCII code). As it turns out, elements of the periodic table have number linked to them. So this package basicaly retrieve the chemical elements that share the same numbers as the characters. Then that list of element is encoded using a `Vigenère Cipher`

## Package Documentation

### Encryption Category

#### giveKeysFromList
```py
giveKeysFromList(elementList: list[pt.core.Element]) -> tuple[str, str]
```
Generates the private and public keys, needed for the encryption process, from a list of Chemical Elements.

#### giveKeysFromString
```py
giveKeysFromString(string: str) -> tuple[str, str]
```
Generates the private and public keys, needed for the encryption process, from a string.

#### encrypt
```py
encrypt(row: str, message: str) -> str
```
Encrypts a message using the Vigenère cipher and the periodic table elements.

#### decrypt
```py
decrypt(row: str, publicKey: str, privateKey: str, message: str) -> str
```
Decrypts a message using the Vigenère cipher and the periodic table elements.

### Element Category

#### LoopCounterElement
```py
class LoopCounterElement(pt.core.Element)
```
A custom element class to handle elements with codes out of the periodic table range.

- Stores in the mass: `900 + loop counter` how many times we looped out of range over the periodic table to finally fit the ASCII code in the table.
- The name stores the element that we are finally able to fit into as the last part of this element name.

#### getElementByNumber
```py
getElementByNumber(number: int) -> pt.core.Element
```
Returns the element by its number.

#### getElementByName
```py
getElementByName(name: str) -> pt.core.Element
```
Returns the element by its name.

#### getLastElement
```py
getLastElement() -> pt.core.Element
```
Returns the last element of the periodic table.

#### getElementBySymbol
```py
getElementBySymbol(symbol: str) -> pt.core.Element
```
Returns the element by its symbol.

#### turnCharacterIntoElement
```py
turnCharacterIntoElement(character: chr) -> pt.core.Element
```
Converts a character into an element.

#### turnStringIntoElements
```py
turnStringIntoElements(string: str) -> list[pt.core.Element]
```
Converts a string into a list of elements.

#### turnElementIntoCharacter
```py
turnElementIntoCharacter(element: pt.core.Element) -> chr
```
Converts an element into a character.

#### turnElementsIntoString
```py
turnElementsIntoString(elementList: list[pt.core.Element]) -> str
```
Converts a list of elements into a string.

### Vigenère Cipher Category

#### generateRow
```py
generateRow() -> str
```
Generates a row of characters that can be used for Vigenère cipher.
- Includes ASCII letters, digits, special characters, whitespace, and some accented letters.

#### generateTable
```py
generateTable(row: str, publicKey: str) -> pd.DataFrame
```
Generates the Vigenère table by shifting the row based on the `publicKey`.
- The `publicKey` determines the shifting for each row.

#### encode
```py
encode(row: str, publicKey: str, privateKey: str, message: str) -> str
```
Encodes a message using the Vigenère cipher.

#### decode
```py
decode(row: str, publicKey: str, privateKey: str, encoded_message: str) -> str
```
Decodes a message using the Vigenère cipher.