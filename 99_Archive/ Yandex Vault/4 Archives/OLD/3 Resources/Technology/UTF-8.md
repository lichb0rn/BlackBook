---
uuid: 20221126061229
created: 2022-11-26T06:12:29
alias: utf-8
---

# [[UTF-8]]

## Binary representation
Each character in **UTF-8 varies in size from 1 byte to 4 bytes**. The encoding has some bits reserved to determine how many bytes this character uses from the first byte:
- A byte with its **most significant bit having 0** value is, on its own, a character. The character is **1 byte**.
- A byte with its **three most significant bits having 110 value**, along with the following byte, represent a character. The **character is 2 bytes.**
- A byte with its four **most significant bits having 1110 value**, along with the two following bytes, represent a character. The **character is 3 bytes.**
- A byte with its **five most significant bits having 11110 value**, along with the three following bytes, represent a character. The **character is 4 bytes**.

Any byte with its two most significant bits having 10 value is a byte that is part of a character (following byte). It doesn’t provide enough information on its own without the leading byte.

The number of bits available to store the value for UTF-8 is calculated as follows:
- 1 byte: 8 bits - 1 reserved = 7 available bits
- 2 bytes: 16 bits - 5 reserved = 11 available bits
- 3 bytes: 24 bits - 8 reserved = 16 available bits
- 4 bytes: 32 bits - 11 reserved = 21 available bits”

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- ℹ️ Source:: [[Expert Swift]]
- 🏷️ Tags:: [[Encoding]], [[Swift Strings]]