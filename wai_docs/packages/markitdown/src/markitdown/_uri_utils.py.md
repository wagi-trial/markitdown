# packages/markitdown/src/markitdown/_uri_utils.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_uri_utils.py",
  "file_hash": "9ef5e35d6bd2dad17e11893b717c410b2ee2df04c60997b555ecfff12535cce7",
  "last_updated": "2025-12-23T15:47:05.879218+00:00",
  "functions": {
    "file_uri_to_path": {
      "hash": "156aa082eb4435c443d8bdd79e0d7f73acb1f0b8320a3ef2e548923dd86709b2",
      "lines": "8-18",
      "last_updated": "2025-12-23T15:47:02.497808+00:00"
    },
    "parse_data_uri": {
      "hash": "3ebebf4d6b8918f035c7d7b38e3a7d64f9eaf94b4f2323c66049da9bd337f1a3",
      "lines": "19-53",
      "last_updated": "2025-12-23T15:47:05.879129+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_uri_utils.py` implements two primary functions: `file_uri_to_path` and `parse_data_uri`. The `file_uri_to_path` function converts a file URI into a local file path. It checks that the URI scheme is "file" and raises a `ValueError` if it is not. The function extracts the network location and converts the path component into an absolute path using `url2pathname`, returning both the network location and the absolute path as a tuple.

The `parse_data_uri` function processes a data URI, validating that it starts with "data:". It splits the URI into its header and data components, raising a `ValueError` for malformed URIs. The function identifies whether the data is base64 encoded and extracts the MIME type and any additional attributes from the header. It decodes the data accordingly, returning the MIME type, a dictionary of attributes, and the content as bytes.

The code imports several modules: `base64`, `os`, `Tuple`, `Dict` from `typing`, and functions from `urllib.request` and `urllib.parse`. It manipulates data structures such as tuples and dictionaries, specifically returning a tuple containing a string or `None`, a dictionary of string key-value pairs, and a bytes object. The code does not define any classes but focuses on the functional operations related to URI handling.

## Functions and Classes

## `file_uri_to_path`

**Location:** [`packages/markitdown/src/markitdown/_uri_utils.py:8`](/packages/markitdown/src/markitdown/_uri_utils.py#L8-L18)

# Documentation for `file_uri_to_path`

## Function Overview
The `file_uri_to_path` function converts a file URI into a local file path. It parses the URI and checks if it uses the "file" scheme. If the scheme is valid, it retrieves the network location and the absolute path of the file.

## Parameters
- `file_uri` (str): A string representing the file URI to be converted. This parameter must be a valid file URI. If the URI does not use the "file" scheme, a `ValueError` is raised.

## Return Value
The function returns a tuple containing:
- `netloc` (str | None): The network location of the file URI. If the network location is not present, it returns `None`.
- `path` (str): The absolute file path corresponding to the file URI.

## Dependencies
The function explicitly depends on the following external modules:
- `urlparse` from the `urllib.parse` module: Used to parse the file URI.
- `url2pathname` from the `urllib.request` module: Converts the URL path to a local file system path.
- `os` module: Used to obtain the absolute path of the file.

## Usage Example
```python
from typing import Tuple
from urllib.parse import urlparse, url2pathname
import os

# Example invocation
file_uri = "file:///home/user/document.txt"
netloc, path = file_uri_to_path(file_uri)
print(netloc)  # Output: None
print(path)    # Output: /home/user/document.txt (absolute path)
```

---
## `parse_data_uri`

**Location:** [`packages/markitdown/src/markitdown/_uri_utils.py:19`](/packages/markitdown/src/markitdown/_uri_utils.py#L19-L53)

# Function Documentation: `parse_data_uri`

## Description
The `parse_data_uri` function processes a data URI string, extracting the MIME type, attributes, and the content. It validates the input to ensure it conforms to the data URI format and decodes the content based on whether it is base64 encoded or URL encoded.

## Parameters
- `uri` (str): A string representing the data URI to be parsed. 
  - Constraints: The string must start with "data:". If it does not, a `ValueError` is raised. The string must contain a comma (`,`) separating the header from the data. If the comma is missing, a `ValueError` is raised.

## Returns
- Tuple[str | None, Dict[str, str], bytes]: 
  - The first element is the MIME type as a string or `None` if not specified.
  - The second element is a dictionary containing key-value pairs of attributes extracted from the URI.
  - The third element is the content as bytes, decoded from the data portion of the URI. The content is decoded using base64 if the URI specifies "base64"; otherwise, it is URL decoded.

## Dependencies
- The function uses the following external modules:
  - `base64`: For decoding base64 encoded data.
  - `unquote_to_bytes`: Presumably from the `urllib.parse` module, for URL decoding the data.

## Usage Example
```python
uri = "data:text/plain;charset=utf-8,Hello%20World"
mime_type, attributes, content = parse_data_uri(uri)
# mime_type will be 'text/plain'
# attributes will be {'charset': 'utf-8'}
# content will be b'Hello World'
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
