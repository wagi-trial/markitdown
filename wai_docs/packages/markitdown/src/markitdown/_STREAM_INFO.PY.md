# packages/markitdown/src/markitdown/_stream_info.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_stream_info.py",
  "file_hash": "039bce7e9d0c5e62a6ed55ac6133e7fa530d7025a2ed8372e35538b072f6dbdf",
  "last_updated": "2026-01-04T17:17:26.884408+00:00",
  "functions": {
    "StreamInfo": {
      "hash": "da71b147298d2a65cda88b272af2b7ba885f0aca58cba6a581a4004bee12c172",
      "lines": "6-33",
      "last_updated": "2026-01-04T17:17:26.884348+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/_stream_info.py` implements the `StreamInfo` class, which is designed to encapsulate information related to a file stream. This class includes several optional fields that can be set to `None`, depending on the context in which the stream is opened. The fields defined in the `StreamInfo` class are `mimetype`, `extension`, `charset`, `filename`, `local_path`, and `url`, each of which is of type `Optional[str]`, allowing for the possibility of no value being assigned.

The `StreamInfo` class includes a method called `copy_and_update`, which facilitates the creation of a new `StreamInfo` instance that is a copy of the current instance but with updated values. This method accepts a variable number of `StreamInfo` instances and keyword arguments, updating the new instance's fields with non-`None` values from the provided instances and arguments. The method uses the `asdict` function from the `dataclasses` module to convert the current instance into a dictionary for easy manipulation.

The code explicitly imports the `dataclass` and `asdict` functions from the `dataclasses` module, as well as the `Optional` type from the `typing` module. The `StreamInfo` class is a data structure that organizes the attributes related to a file stream, leveraging Python's type hinting to indicate that certain fields may not always hold a value.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `StreamInfo`

**Nested Functions:**
- `copy_and_update`

<details>
<summary><strong>Calls/Dependencies</strong> (7 unique functions)</summary>

- `StreamInfo`
- `asdict`
- `copy_and_update`
- `isinstance`
- `items`
- `len`
- `update`

</details>

</details>



## Functions and Classes

## `StreamInfo`

**Location:** [`packages/markitdown/src/markitdown/_stream_info.py:6`](/packages/markitdown/src/markitdown/_stream_info.py#L6-L33)

**Nested Functions:** `copy_and_update`  
**Dependencies:** `StreamInfo`, `asdict`, `copy_and_update`, `isinstance`, `items`, `len`, `update`  


# StreamInfo Class Documentation

## Overview
The `StreamInfo` class is designed to store information about a file stream. It contains several optional fields that can be set to `None`, depending on how the stream was opened.

## Attributes
- `mimetype: Optional[str]`
  - Represents the MIME type of the stream.
  - Default value is `None`.

- `extension: Optional[str]`
  - Represents the file extension of the stream.
  - Default value is `None`.

- `charset: Optional[str]`
  - Represents the character set of the stream.
  - Default value is `None`.

- `filename: Optional[str]`
  - Represents the filename derived from the local path, URL, or Content-Disposition header.
  - Default value is `None`.

- `local_path: Optional[str]`
  - Represents the local path if the stream is read from disk.
  - Default value is `None`.

- `url: Optional[str]`
  - Represents the URL if the stream is read from a URL.
  - Default value is `None`.

## Method: copy_and_update
### Description
The `copy_and_update` method creates a copy of the current `StreamInfo` object and updates it with the attributes from the provided `StreamInfo` instances and/or additional keyword arguments.

### Parameters
- `*args`
  - Variable length argument list that accepts one or more `StreamInfo` instances.
  - Each instance must be of type `StreamInfo`.

- `**kwargs`
  - Variable length keyword arguments that represent additional attributes to update in the new `StreamInfo` object.
  - Each key must correspond to an attribute of the `StreamInfo` class.

### Return Value
- Returns a new instance of `StreamInfo` containing:
  - A combination of the attributes from the current instance and any provided `StreamInfo` instances in `args`.
  - Any additional attributes provided through `kwargs`, overriding existing attributes if they are not `None`.

### Dependencies
- The method uses the `asdict` function, which is assumed to be imported from the `dataclasses` module. This function converts the `StreamInfo` instance into a dictionary.

## Usage Example
```python
# Create an instance of StreamInfo
stream_info = StreamInfo(mimetype='text/plain', filename='example.txt')

# Create another instance of StreamInfo
additional_info = StreamInfo(extension='.txt', charset='utf-8')

# Copy and update the original instance with the additional instance and new attributes
updated_stream_info = stream_info.copy_and_update(additional_info, local_path='/path/to/example.txt')

# The updated_stream_info will now contain:
# - mimetype: 'text/plain'
# - extension: '.txt'
# - charset: 'utf-8'
# - filename: 'example.txt'
# - local_path: '/path/to/example.txt'
# - url: None
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
