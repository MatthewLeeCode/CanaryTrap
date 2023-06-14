# CanaryTrap

CanaryTrap is a Python package that uses the concept of a "canary trap" to watermark text using unicode spaces. By converting regular spaces to unicode spaces according to a binary pattern, you can add a hidden signature to your text.

## Installation

You can install CanaryTrap using pip:
```
pip install canarytrap
```

## How to use

First, import the package:

```python
import canarytrap as canary
```

To watermark your text, use the `unicode_space_encode` function. You can either provide a binary string or let the function generate a random one:

```python
text = "Hello world this is a test"
watermarked_text, binary_str = canary.unicode_space_encode(text)
print(watermarked_text)  # Watermarked text
print(binary_str)  # Binary string used for watermarking
```

You can convert the watermarked text back to binary using the `unicode_space_to_binary_str` function:

```python
binary_str_back = canary.unicode_space_to_binary_str(watermarked_text)
print(binary_str_back)  # Should be the same as binary_str
```

To check if a text matches a given binary string, use the `unicode_space_match` function:

```python
match = canary.unicode_space_match(watermarked_text, binary_str)
print(match)  # Should be 1.0 if text is not modified
```

This package is very useful for checking the integrity of text, finding leaks, or tracing the origin of text documents.

## Note

The watermark is invisible but can be removed or altered if the text is converted to plain text or the spaces are normalized. Use this package with awareness of its limitations.

Also, if the watermarked text is edited (spaces are added, removed, or replaced), the match percentage returned by the `unicode_space_match` function may be less than 1.0. If you get a match percentage of less than 1.0, it means that the text was likely edited after being watermarked. The match percentage gives an estimate of how much of the original watermark remains in the text.
