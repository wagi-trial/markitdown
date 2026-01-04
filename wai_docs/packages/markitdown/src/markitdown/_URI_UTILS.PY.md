# packages/markitdown/src/markitdown/_uri_utils.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_uri_utils.py",
  "file_hash": "9ef5e35d6bd2dad17e11893b717c410b2ee2df04c60997b555ecfff12535cce7",
  "last_updated": "2026-01-04T17:17:38.445042+00:00",
  "functions": {
    "file_uri_to_path": {
      "hash": "156aa082eb4435c443d8bdd79e0d7f73acb1f0b8320a3ef2e548923dd86709b2",
      "lines": "8-18",
      "last_updated": "2026-01-04T17:17:34.958827+00:00"
    },
    "parse_data_uri": {
      "hash": "3ebebf4d6b8918f035c7d7b38e3a7d64f9eaf94b4f2323c66049da9bd337f1a3",
      "lines": "19-53",
      "last_updated": "2026-01-04T17:17:38.444989+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_uri_utils.py` implements two primary functions: `file_uri_to_path` and `parse_data_uri`. The `file_uri_to_path` function converts a file URI into a local file path, ensuring that the URI scheme is "file". It returns a tuple containing the network location (if present) and the absolute path of the file. The `parse_data_uri` function processes a data URI, extracting the MIME type, attributes, and content. It verifies the URI format, decodes the content if it is base64 encoded, and returns a tuple containing the MIME type, a dictionary of attributes, and the decoded content.

The file imports several modules: `base64` for decoding base64 content, `os` for handling file paths, `url2pathname` from `urllib.request` for converting a URL path to a local file path, and `urlparse` and `unquote_to_bytes` from `urllib.parse` for parsing and decoding URIs. These dependencies facilitate the operations of converting and parsing URIs.

The data structures manipulated in this file include tuples and dictionaries. The `file_uri_to_path` function returns a tuple of type `Tuple[str | None, str]`, where the first element can be a string or `None`, and the second element is a string representing the file path. The `parse_data_uri` function returns a tuple of type `Tuple[str | None, Dict[str, str], bytes]`, where the first element is the MIME type (or `None`), the second element is a dictionary of attributes, and the third element is a byte sequence representing the content.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `file_uri_to_path`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `ValueError`
- `abspath`
- `file_uri_to_path`
- `url2pathname`
- `urlparse`

</details>

### `parse_data_uri`

<details>
<summary><strong>Calls/Dependencies</strong> (9 unique functions)</summary>

- `ValueError`
- `b64decode`
- `len`
- `parse_data_uri`
- `partition`
- `pop`
- `split`
- `startswith`
- `unquote_to_bytes`

</details>

</details>



## Functions and Classes

## `file_uri_to_path`

**Location:** [`packages/markitdown/src/markitdown/_uri_utils.py:8`](/packages/markitdown/src/markitdown/_uri_utils.py#L8-L18)

**Dependencies:** `ValueError`, `abspath`, `file_uri_to_path`, `url2pathname`, `urlparse`  


# Documentation for `file_uri_to_path`

## Function Overview
The `file_uri_to_path` function converts a file URI into a local file path. It validates that the provided URI uses the "file" scheme and returns the network location and the absolute path of the file.

## Parameters
- `file_uri` (str): A string representing the file URI to be converted. This parameter must conform to the URI format and specifically use the "file" scheme. If the scheme is not "file", a `ValueError` is raised.

## Return Value
- Returns a tuple of two elements:
  - `netloc` (str | None): The network location part of the URI. If the URI does not contain a network location, this value will be `None`.
  - `path` (str): The absolute path of the file derived from the URI.

## Dependencies
The function relies on the following external modules:
- `urlparse` from the `urllib.parse` module: Used to parse the provided file URI.
- `url2pathname` from the `urllib.request` module: Converts the path component of the URI to a local file system path.
- `os` module: Used to obtain the absolute path of the file.

## Usage Example
```python
from typing import Tuple
from urllib.parse import urlparse, url2pathname
import os

# Example invocation
file_uri = "file:///home/user/document.txt"
netloc, path = file_uri_to_path(file_uri)

print(netloc)  # Output: None (for local files)
print(path)    # Output: /home/user/document.txt (absolute path)
```

---
## `parse_data_uri`

**Location:** [`packages/markitdown/src/markitdown/_uri_utils.py:19`](/packages/markitdown/src/markitdown/_uri_utils.py#L19-L53)

**Dependencies:** `ValueError`, `b64decode`, `len`, `parse_data_uri`, `partition`, `pop`, `split`, `startswith`, `unquote_to_bytes`  


# Function Documentation: `parse_data_uri`

## Description
The `parse_data_uri` function processes a data URI, extracting its MIME type, attributes, and content. It validates the URI format, decodes the data if necessary, and returns structured information.

## Parameters
- `uri` (str): A string representing the data URI to be parsed. 
  - **Constraints**: The string must start with "data:". If it does not, a `ValueError` is raised. The URI must contain a comma (`,`) separating the header from the data. If the comma is missing, a `ValueError` is raised.

## Return Value
The function returns a tuple containing:
- `mime_type` (str | None): The MIME type extracted from the URI. If no MIME type is specified, it defaults to `None`.
- `attributes` (Dict[str, str]): A dictionary containing key-value pairs of attributes parsed from the URI. Keys are attribute names, and values are their corresponding values. If an attribute has no value, it is stored with an empty string.
- `content` (bytes): The decoded content from the data portion of the URI. If the data is base64 encoded, it is decoded using `base64.b64decode`. If not, it is decoded using `unquote_to_bytes`.

## Dependencies
The function explicitly calls the following external modules:
- `base64`: Used for decoding base64 encoded data.
- `unquote_to_bytes`: Presumably from `urllib.parse`, used for decoding percent-encoded data.

## Usage Example
```python
from typing import Tuple, Dict
from urllib.parse import unquote_to_bytes
import base64

# Example data URI
data_uri = "data:text/plain;charset=utf-8;base64,SGVsbG8sIFdvcmxkIQ=="

# Invoking the function
mime_type, attributes, content = parse_data_uri(data_uri)

# Output
print(mime_type)  # Output: text/plain
print(attributes)  # Output: {'charset': 'utf-8'}
print(content)     # Output: b'Hello, World!'
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
