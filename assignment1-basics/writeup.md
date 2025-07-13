# Problem 1: Understanding Unicode
**1.1 What Unicode character does `chr(0)` return?**

```python
>>> chr(0)
'\x00'
```
It means NULL.

**1.2 How does this character’s string representation `(__repr__())` differ from its printed representation?**


```python
>>> "123".__repr__()
"'123'"
>>> print("123")
123
```
`__repr__()` returns official string representation, that is, a string which is defined in method `__repr__()` of this class, while `print()` transforms the object into string and output the string directly. 

**1.3 What happens when this character occurs in text? It may be helpful to play around with the following in your Python interpreter and see if it matches your expectations:**
```python
>>> chr(0)
>>> print(chr(0))
>>> "this is a test" + chr(0) + "string"
>>> print("this is a test" + chr(0) + "string")
```

```python
>>> chr(0)
'\x00'
>>> print(chr(0))

>>> "this is a test" + chr(0) + "string"
'this is a test\x00string'
>>> print("this is a test" + chr(0) + "string")
this is a teststring
```

---

# Problem 2: Unicode Encodings
**2.1 What are some reasons to prefer training our tokenizer on UTF-8 encoded bytes, rather than
UTF-16 or UTF-32? It may be helpful to compare the output of these encodings for various
input strings.**

```python
>>> len(utf8_encoded)
23
>>> len(utf16_encoded)
28
>>> len(utf32_encoded)
56
```
There are three main reasons:
1. utf8 needs least space to encode a string.
2. utf8 code could be processed byte by byte.
3. most of the webpage use utf8.

**2.2 Consider the following (incorrect) function, which is intended to decode a UTF-8 byte string into
a Unicode string. Why is this function incorrect? Provide an example of an input byte string
that yields incorrect results.**
```python
def decode_utf8_bytes_to_str_wrong(bytestring: bytes):
    return "".join([bytes([b]).decode("utf-8") for b in bytestring])

>>> decode_utf8_bytes_to_str_wrong("hello".encode("utf-8"))
'hello'
```
Since the utf8 code could not be decoded byte by byte.

**2.3 Give a two byte sequence that does not decode to any Unicode character(s).**
```python
>>> b'\xe4\xbd'.decode()
Traceback (most recent call last):
  File "<python-input-37>", line 1, in <module>
    b'\xe4\xbd'.decode()
    ~~~~~~~~~~~~~~~~~~^^
UnicodeDecodeError: 'utf-8' codec can't decode bytes in position 0-1: unexpected end of data
```
