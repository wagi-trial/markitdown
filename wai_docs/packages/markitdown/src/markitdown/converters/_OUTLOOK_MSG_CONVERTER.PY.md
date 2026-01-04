# packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py",
  "file_hash": "9443fd8b0135ddfabbf8b3ba2c0433d27f6a2db6e5e28f0091854bdb234ff1d4",
  "last_updated": "2026-01-04T17:21:29.820241+00:00",
  "functions": {
    "OutlookMsgConverter": {
      "hash": "19c9d890bd5df5e1f54aef0e6c785a55b9e7859e75f5df8b7eb68cb917da813a",
      "lines": "24-150",
      "last_updated": "2026-01-04T17:21:29.820163+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py` implements the `OutlookMsgConverter` class, which is responsible for converting Outlook `.msg` files into Markdown format. The converter extracts email metadata, including headers (From, To, Subject) and body content, using the `olefile` package to parse the structure of the `.msg` file. The class provides methods to determine if a given file stream is an acceptable `.msg` file and to perform the conversion to Markdown.

The `OutlookMsgConverter` class contains the following methods:
- `accepts`: This method checks if the provided file stream and its associated metadata (MIME type and file extension) are compatible with the converter. It verifies the file extension and MIME type against predefined accepted values and checks if the file stream is an OLE file.
- `convert`: This method performs the conversion of the `.msg` file to Markdown format. It raises a `MissingDependencyException` if the required `olefile` package is not available. It extracts email headers and body content, formats them into Markdown, and returns a `DocumentConverterResult` containing the Markdown content and the email subject as the title.
- `_get_stream_data`: This helper method retrieves and decodes data from specific streams within the `.msg` file. It attempts to decode the data as UTF-16 first, falling back to UTF-8 if necessary.

The file explicitly imports the `olefile` module, which is used to interact with OLE files, and it relies on several other modules from the same package, including `StreamInfo`, `DocumentConverter`, `DocumentConverterResult`, and `MissingDependencyException`. The code defines and manipulates data structures such as `DocumentConverterResult`, which encapsulates the result of the conversion process, and it uses types like `BinaryIO` and `Any` from the `typing` module to specify method parameters. The constants `ACCEPTED_MIME_TYPE_PREFIXES` and `ACCEPTED_FILE_EXTENSIONS` define the criteria for acceptable file types.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `OutlookMsgConverter`

**Nested Functions:**
- `accepts`
- `convert`
- `_get_stream_data`

<details>
<summary><strong>Calls/Dependencies</strong> (29 unique functions)</summary>

- `DocumentConverterResult`
- `MissingDependencyException`
- `OleFileIO`
- `OutlookMsgConverter`
- `_get_stream_data`
- `accepts`
- `close`
- `convert`
- `decode`
- `exists`
- `first`
- `format`
- `get`
- `headers`
- `isOleFile`
- `isinstance`
- `items`
- `join`
- `listdir`
- `lower`
- `openstream`
- `read`
- `seek`
- `startswith`
- `str`
- `strip`
- `tell`
- `type`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `OutlookMsgConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py:24`](/packages/markitdown/src/markitdown/converters/_outlook_msg_converter.py#L24-L150)

**Nested Functions:** `accepts`, `convert`, `_get_stream_data`  
**Dependencies:** `DocumentConverterResult`, `MissingDependencyException`, `OleFileIO`, `OutlookMsgConverter`, `_get_stream_data`, `accepts`, `close`, `convert`, `decode`, `exists`, `first`, `format`, `get`, `headers`, `isOleFile` *(+14 more)*  


# OutlookMsgConverter Documentation

## Overview
The `OutlookMsgConverter` class is a subclass of `DocumentConverter` that converts Outlook `.msg` files into markdown format. It extracts email metadata such as headers (From, To, Subject) and the email body content using the `olefile` package to parse the structure of the `.msg` file.

## Parameters

### accepts
```python
def accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool
```
- **file_stream**: `BinaryIO`
  - A binary stream representing the `.msg` file to be checked for acceptance.
  
- **stream_info**: `StreamInfo`
  - An object containing metadata about the file, including:
    - `mimetype`: `str` or `None`
      - The MIME type of the file.
    - `extension`: `str` or `None`
      - The file extension of the file.

- **kwargs**: `Any`
  - Additional options to pass to the converter (not used in the implementation).

**Usage**: This method checks if the provided file stream is an accepted `.msg` file based on its extension, MIME type, and OLE file structure.

### convert
```python
def convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult
```
- **file_stream**: `BinaryIO`
  - A binary stream representing the `.msg` file to be converted.

- **stream_info**: `StreamInfo`
  - An object containing metadata about the file (not directly used in the conversion logic).

- **kwargs**: `Any`
  - Additional options to pass to the converter (not used in the implementation).

**Usage**: This method converts the provided `.msg` file into markdown format, extracting email metadata and body content.

## Return Value

### convert
- **Return Type**: `DocumentConverterResult`
- **Contents**:
  - `markdown`: `str`
    - A string containing the markdown representation of the email, including headers and body content.
  - `title`: `str` or `None`
    - The subject of the email, used as the title in the markdown output.

## Dependencies
- **olefile**: The code uses the `olefile` package to handle OLE file structures and extract data from `.msg` files. The presence of this package is asserted before usage.
- **DocumentConverter**: The class inherits from `DocumentConverter`, which is not defined in the provided code but is assumed to be part of the larger codebase.

## Usage Example
```python
from io import BytesIO

# Example binary stream of a .msg file
file_stream = BytesIO(b'...')  # Replace with actual binary content of a .msg file
stream_info = StreamInfo(mimetype='application/vnd.ms-outlook', extension='.msg')

converter = OutlookMsgConverter()

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
    print(result.title)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
