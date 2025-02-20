# Periodic Encryption

Classical cryptography, enhanced by chemistry !

## Summary

This package allows you to encrypt and decrypt messages by the mean of `Vigenere Cipher` and `Periodic Table of Elements`.

Here is a quick example :
```py
from periodicencryption import vc, en # importing the vigenerecipher and encryption modules

message = "Hello, World!"

row = vc.generate_row() #table row (i.e. which characters are allowed to be encrypted)

encrypted, puk, prk = en.encrypt_keys_auto(row, message)

print(encrypted)
print(f"public key : {puk}")
print(f"private key : {prk}")

decrypted = en.decrypt(row, encrypted, puk, prk)

print(decrypted)
```
```
AeVvco6q&q0kWwXj!FNyskRjlq
public key : 74.921595HafniumArsenic178.486
private key : HafniumAsHfArsenic
Hello, World!
```

## Table of contents

1. [Installation](#installation)
2. [In a nutshell how does it work](#in-a-nutshell-how-does-it-work)
3. [Package Documentation](#package-documentation)
   - [Encryption sub-package](#encryption-sub-package)
     - [generate_keys](#generate_keys)
     - [encrypt_keys_manual](#encrypt_keys_manual)
     - [encrypt_keys_auto](#encrypt_keys_auto)
     - [decrypt](#decrypt)
   - [Element sub-package](#element-sub-package)
     - [CounterElement](#counterelement)
     - [get_el_by_number](#get_el_by_number)
     - [get_el_by_name](#get_el_by_name)
     - [get_el_by_symbol](#get_el_by_symbol)
     - [get_last_el](#get_last_el)
     - [turn_chr_into_el](#turn_chr_into_el)
     - [turn_str_into_el](#turn_str_into_el)
     - [turn_el_into_chr](#turn_el_into_chr)
     - [turn_el_into_str](#turn_el_into_str)
   - [Vigenerecipher sub-package](#vigenerecipher-sub-package)
     - [generate_row](#generate_row)
     - [generate_table](#generate_table)
     - [vigenere_encode](#vigenere_encode)
     - [vigenere_decode](#vigenere_decode)

## Installation

Enter the following command :
```sh
pip install periodicencryption
```
Then import the package :
```py
import periodicencryption
```

## In a nutshell how does it work

Strings are made up of characters, those characters have a unique code (generally called ASCII code). As it turns out, elements of the periodic table have number linked to them. So this package basicaly retrieve the chemical elements that share the same numbers as the characters. Then that list of element is encoded using a `Vigenere Cipher`

Also don't worry, characters code that exceed 118 (the highest number amongst the periodic table) are handled using a custom element

## Package Documentation

### Package Structure

The main package is structured like that :
```
periodicencryption
    - encryption
    - element
    - vigenerecipher
```

And there are aliases :

| Sub-package | Alias |
|:---|:---|
| encryption | en |
| element | el |
| vigenerecipher | vc |

Which mean you could either use `from periodicencryption import element` or `from periodicencryption import el`

## Encryption sub-package

This sub-package contain everything related to the Vigenere cipher.<br>
It can be accessed via those two methods :
```py
from periodicencryption import en
from periodicencryption import encryption
```

### generate_keys
```py
generate_keys(string: str) -> tuple[str, str]
```
Generates public and private keys from a string.

#### Args:
- `string` (str): The string to generate the keys from.

#### Raises:
- `ValueError`: If the element list is empty.

#### Returns:
- `tuple[str, str]`: The public and private keys.

---

### encrypt_keys_manual
```py
encrypt_keys_manual(row: str, message: str, public_key: str, private_key: str) -> str
```
Encrypts a message using the Vigenère cipher and the periodic table elements, with the specified keys.

#### Args:
- `row` (str): The row of characters to use (i.e. which characters are allowed to be encrypted).
- `message` (str): The message to encrypt.
- `public_key` (str): The public key.
- `private_key` (str): The private key.

#### Raises:
- `ValueError`: If the message is empty.

#### Returns:
- `str`: The encrypted message.

---

### encrypt_keys_auto
```py
encrypt_keys_auto(row: str, message: str) -> tuple[str, str, str]
```
Encrypts a message using the Vigenère cipher and the periodic table elements, with automatically generated keys.

#### Args:
- `row` (str): The row of characters to use (i.e. which characters are allowed to be encrypted).
- `message` (str): The message to encrypt.

#### Raises:
- `ValueError`: If the message is empty.

#### Returns:
- `tuple[str, str, str]`: The encrypted message, the public key, and the private key.

---

### decrypt
```py
decrypt(row: str, encoded: str, public_key: str, private_key: str) -> str
```
Decrypts a message using the Vigenère cipher and the periodic table elements.

#### Args:
- `row` (str): The row of characters to use (i.e. which characters are allowed to be encrypted).
- `encoded` (str): The encoded message.
- `public_key` (str): The public key.
- `private_key` (str): The private key.

#### Raises:
- `ValueError`: If the message is empty.

#### Returns:
- `str`: The decrypted message.

---

## Element sub-package

This sub-package contain everything related to chemical elements.<br>
It can be accessed via those two methods :
```py
from periodicencryption import el
from periodicencryption import element
```

### CounterElement
```py
class CounterElement(pt.core.Element)
```
A custom element class to handle elements with codes out of the periodic table range.<br>
It stores the mass (`900 + <loop counter>`) to track how many times the code looped out of the periodic table, and stores the final element used to fit the ASCII code in the table.

#### Args:
- `cnt` (int): The loop counter (i.e., how many times we looped out of range over the periodic table).
- `el` (pt.core.Element): The element that we are able to fit into after looping.

#### Class Methods:
- `split_symbol(symbol: str) -> tuple[str, int]`: Splits a symbol into the element symbol and the counter.

---

### get_el_by_number
```py
get_el_by_number(number: int) -> pt.core.Element
```
Returns the element by its number.

#### Args:
- `number` (int): The number of the element.

#### Returns:
- `pt.core.Element`: The element.

---

### get_el_by_name
```py
get_el_by_name(name: str) -> pt.core.Element
```
Returns the element by its name.

#### Args:
- `name` (str): The name of the element.

#### Returns:
- `pt.core.Element`: The element.

---

### get_el_by_symbol
```py
get_el_by_symbol(symbol: str) -> pt.core.Element
```
Returns the element by its symbol.

#### Args:
- `symbol` (str): The symbol of the element.

#### Returns:
- `pt.core.Element`: The element.

---

### get_last_el
```py
get_last_el() -> pt.core.Element
```
Returns the last element of the periodic table.

#### Returns:
- `pt.core.Element`: The last element.

---

### turn_chr_into_el
```py
turn_chr_into_el(character: chr) -> pt.core.Element
```
Converts a character into an element.

#### Args:
- `character` (chr): The character to convert.

#### Returns:
- `pt.core.Element`: The resulting element.

---

### turn_str_into_el
```py
turn_str_into_el(string: str) -> list[pt.core.Element]
```
Converts a string into a list of elements.

#### Args:
- `string` (str): The string to convert.

#### Returns:
- `list[pt.core.Element]`: The resulting list of elements.

---

### turn_el_into_chr
```py
turn_el_into_chr(element: pt.core.Element) -> chr
```
Converts an element into a character.

#### Args:
- `element` (pt.core.Element): The element to convert.

#### Returns:
- `chr`: The resulting character.

---

### turn_el_into_str
```py
turn_el_into_str(element_list: list[pt.core.Element]) -> str
```
Converts a list of elements into a string.

#### Args:
- `element_list` (list[pt.core.Element]): The list of elements to convert.

#### Returns:
- `str`: The resulting string.

---

## Vigenerecipher sub-package

This sub-package contain everything related to the Vigenere cipher.<br>
It can be accessed via those two methods :
```py
from periodicencryption import vc
from periodicencryption import vigenerecipher
```

### generate_row
```py
generate_row() -> str
```
Generates a row for the Vigenère table.

#### Returns:
- `str`: A string containing letters, digits, special characters, whitespace, and letters with diacritics.

---

### generate_table
```py
generate_table(row: str, public_key: str) -> pd.DataFrame
```
Generates a Vigenère table.

#### Args:
- `row` (str): The row to be used in the table.
- `public_key` (str): The public key to be used in the table.

#### Raises:
- `ValueError`: If every character of the public key is not in the row.

#### Returns:
- `pd.DataFrame`: The Vigenère table.

---

### vigenere_encode
```py
vigenere_encode(row: str, message: str, public_key: str, private_key: str) -> str
```
Encodes a message using the Vigenère cipher.

#### Args:
- `row` (str): The row to be used in the table.
- `message` (str): The message to be encoded.
- `public_key` (str): The public key to be used in the table.
- `private_key` (str): The private key to be used in the table.

#### Returns:
- `str`: The encoded message.

---

### vigenere_decode
```py
vigenere_decode(row: str, encoded_message: str, public_key: str, private_key: str) -> str
```
Decodes a message using the Vigenère cipher.

#### Args:
- `row` (str): The row to be used in the table.
- `encoded_message` (str): The message to be decoded.
- `public_key` (str): The public key to be used in the table.
- `private_key` (str): The private key to be used in the table.

#### Returns:
- `str`: The decoded message.

---
