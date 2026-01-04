# packages/markitdown/src/markitdown/converters/_plain_text_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_plain_text_converter.py",
  "file_hash": "591077d5c51905345a3ad7f21a639d37458e9ef16eebb87cc1102f7f92eba59c",
  "last_updated": "2026-01-04T17:21:51.931606+00:00",
  "functions": {
    "PlainTextConverter": {
      "hash": "71f304f6b2b284c2f5ba049c411da46f3c56610d3c727056978930bb9a3d2cbd",
      "lines": "33-72",
      "last_updated": "2026-01-04T17:21:51.931549+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_plain_text_converter.py` implements a `PlainTextConverter` class, which is a subclass of `DocumentConverter`. This class is responsible for determining whether a given file stream can be accepted for conversion based on its MIME type, file extension, and character set. It also provides a method to convert the file stream into a Markdown format.

The `PlainTextConverter` class contains two primary methods: `accepts` and `convert`. The `accepts` method evaluates whether the provided `file_stream` can be processed by checking the MIME type, file extension, and character set. It returns a boolean value indicating acceptance. The `convert` method reads the content from the `file_stream`, decodes it based on the specified character set or uses the `charset_normalizer` library to determine the best encoding, and then returns a `DocumentConverterResult` containing the converted Markdown text.

The file imports several modules, including `sys`, `BinaryIO`, and `Any` from the `typing` module, as well as `from_bytes` from the `charset_normalizer` library. It also imports `DocumentConverter` and `DocumentConverterResult` from a relative module `_base_converter`, and `StreamInfo` from another relative module `_stream_info`. The code defines constants for accepted MIME type prefixes and file extensions, which are used in the acceptance criteria for file streams. The `PlainTextConverter` class manipulates the `StreamInfo` data structure to access metadata about the file being processed.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `PlainTextConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (11 unique functions)</summary>

- `DocumentConverterResult`
- `PlainTextConverter`
- `accepts`
- `best`
- `convert`
- `decode`
- `from_bytes`
- `lower`
- `read`
- `startswith`
- `str`

</details>

</details>



## Functions and Classes

## `PlainTextConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_plain_text_converter.py:33`](/packages/markitdown/src/markitdown/converters/_plain_text_converter.py#L33-L72)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `DocumentConverterResult`, `PlainTextConverter`, `accepts`, `best`, `convert`, `decode`, `from_bytes`, `lower`, `read`, `startswith`, `str`  


# PlainTextConverter Documentation

## Overview
`PlainTextConverter` is a subclass of `DocumentConverter` designed to handle documents with the content type `text/plain`. It provides methods to determine if a file can be accepted for conversion and to convert the file's content into a markdown format.

## Methods

### accepts

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the file to be checked for acceptance.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
  - `charset` (Optional[str]): The character set of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `bool`: Returns `True` if the file is accepted for conversion based on the following criteria:
  - If `stream_info.charset` is not `None`.
  - If `stream_info.extension` is in `ACCEPTED_FILE_EXTENSIONS`.
  - If `stream_info.mimetype` starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`.
  
#### Logic
The method first checks if a charset is provided. If so, it accepts the file. If not, it checks the file extension against a predefined list and then checks the MIME type against a list of accepted prefixes.

### convert

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `charset` (Optional[str]): The character set of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `DocumentConverterResult`: An object containing the converted content in markdown format. The `markdown` attribute of this object contains the text content derived from the input file.

#### Logic
If `stream_info.charset` is provided, the method reads the content from `file_stream` and decodes it using the specified charset. If no charset is provided, it uses the `from_bytes` function to convert the binary data to a string. The resulting text is then encapsulated in a `DocumentConverterResult` object.

## Dependencies
- `DocumentConverter`: The base class from which `PlainTextConverter` inherits.
- `StreamInfo`: A class that provides metadata about the file being processed.
- `DocumentConverterResult`: A class used to return the result of the conversion.
- `from_bytes`: A function used to convert binary data to a string.
- `ACCEPTED_FILE_EXTENSIONS`: A predefined list of accepted file extensions.
- `ACCEPTED_MIME_TYPE_PREFIXES`: A predefined list of accepted MIME type prefixes.

## Usage Example
```python
converter = PlainTextConverter()
file_stream = open('example.txt', 'rb')
stream_info = StreamInfo(mimetype='text/plain', extension='txt', charset='utf-8')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
file_stream.close()
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
