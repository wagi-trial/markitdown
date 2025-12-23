# packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py",
  "file_hash": "9443fd8b0135ddfabbf8b3ba2c0433d27f6a2db6e5e28f0091854bdb234ff1d4",
  "last_updated": "2025-12-23T15:51:21.667785+00:00",
  "functions": {
    "OutlookMsgConverter": {
      "hash": "19c9d890bd5df5e1f54aef0e6c785a55b9e7859e75f5df8b7eb68cb917da813a",
      "lines": "24-150",
      "last_updated": "2025-12-23T15:51:21.667678+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py` implements the `OutlookMsgConverter` class, which is responsible for converting Outlook `.msg` files into Markdown format. The conversion process involves extracting email metadata, such as headers (From, To, Subject) and the email body content, using the `olefile` package to parse the structure of the `.msg` file.

The main class defined in this file is `OutlookMsgConverter`, which inherits from `DocumentConverter`. It includes two primary methods: `accepts` and `convert`. The `accepts` method determines whether a given file stream is compatible with the converter by checking the file extension and MIME type, as well as verifying if the file is an OLE file. The `convert` method performs the actual conversion, raising a `MissingDependencyException` if the required `olefile` dependency is not available. It constructs a Markdown string containing the extracted email headers and body content, which is returned as a `DocumentConverterResult`.

The code explicitly imports the `olefile` module, which is used to handle the parsing of `.msg` files. Other imported modules include `sys`, `Any`, `Union`, and `BinaryIO` from the `typing` module, as well as `StreamInfo`, `DocumentConverter`, `DocumentConverterResult`, and `MissingDependencyException` from relative imports. The file defines constants for accepted MIME type prefixes and file extensions, and it manipulates data structures such as dictionaries for headers and strings for Markdown content. The `_get_stream_data` helper method is also defined to safely extract and decode stream data from the `.msg` file.

## Functions and Classes

## `OutlookMsgConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py:24`](/packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py#L24-L150)

# OutlookMsgConverter Documentation

## Overview
The `OutlookMsgConverter` class is a subclass of `DocumentConverter` that converts Outlook `.msg` files into Markdown format. It extracts email metadata such as headers (From, To, Subject) and the body content using the `olefile` package to parse the structure of the `.msg` file.

## Parameters

### `accepts`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the file to be checked. This stream is used to determine if the file is an acceptable format for conversion.
  - `stream_info` (StreamInfo): An object containing metadata about the file, including its MIME type and extension.
  - `**kwargs` (Any): Additional options that may be passed to the converter, though these are not explicitly used in the implementation.
- **Returns**: `bool`
  - Returns `True` if the file is an accepted format for conversion based on its extension or MIME type, or if it is identified as an OLE file that contains specific properties indicating it is an Outlook file. Returns `False` otherwise.

### `convert`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the `.msg` file to be converted.
  - `stream_info` (StreamInfo): An object containing metadata about the file.
  - `**kwargs` (Any): Additional options that may be passed to the converter, though these are not explicitly used in the implementation.
- **Returns**: `DocumentConverterResult`
  - Contains:
    - `markdown` (str): A string representing the converted Markdown content, including email headers and body.
    - `title` (str or None): The subject of the email, extracted from the headers.

### `_get_stream_data`
- **Parameters**:
  - `msg` (Any): An instance of `olefile.OleFileIO` representing the opened `.msg` file.
  - `stream_path` (str): The path to the specific stream within the `.msg` file from which data is to be extracted.
- **Returns**: `Union[str, None]`
  - Returns the decoded string data from the specified stream path, or `None` if the data cannot be extracted.

## Dependencies
- The class relies on the `olefile` package to handle the parsing of `.msg` files. The code checks for the presence of `olefile` and raises a `MissingDependencyException` if it is not available.
- The code also uses `DocumentConverterResult`, which is presumably defined elsewhere in the codebase.

## Usage Example
```python
from io import BytesIO

# Assuming `stream_info` is an instance of StreamInfo with appropriate attributes
file_stream = BytesIO(b'...')  # Replace with actual binary content of a .msg file
converter = OutlookMsgConverter()

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
    print(result.title)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
