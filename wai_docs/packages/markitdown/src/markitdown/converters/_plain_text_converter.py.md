# packages/markitdown/src/markitdown/converters/_plain_text_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_plain_text_converter.py",
  "file_hash": "591077d5c51905345a3ad7f21a639d37458e9ef16eebb87cc1102f7f92eba59c",
  "last_updated": "2025-12-23T15:51:45.329041+00:00",
  "functions": {
    "PlainTextConverter": {
      "hash": "71f304f6b2b284c2f5ba049c411da46f3c56610d3c727056978930bb9a3d2cbd",
      "lines": "33-72",
      "last_updated": "2025-12-23T15:51:45.328937+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_plain_text_converter.py` implements a `PlainTextConverter` class that extends the `DocumentConverter` class. This converter is designed to handle the conversion of plain text and similar file types into a markdown format. The class includes methods to determine if a given file stream is acceptable for conversion based on its MIME type, file extension, and character set. 

The main functions and their responsibilities in this file include:
- `accepts`: This method checks if the provided file stream and its associated metadata (MIME type and file extension) are acceptable for conversion. It returns `True` if the file has a specified charset or if the MIME type or extension matches predefined accepted values.
- `convert`: This method reads the content from the file stream, decodes it based on the specified charset if available, or uses the `charset_normalizer` library to determine the best encoding. It returns a `DocumentConverterResult` containing the converted markdown text.

The file explicitly imports several modules, including `sys`, `BinaryIO`, `Any` from the `typing` module, and `from_bytes` from the `charset_normalizer` library. It also imports `DocumentConverter` and `DocumentConverterResult` from a parent module, as well as `StreamInfo`. The code manipulates data structures such as `StreamInfo`, which encapsulates metadata about the file stream, and utilizes lists for accepted MIME type prefixes and file extensions to validate input files.

## Functions and Classes

## `PlainTextConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_plain_text_converter.py:33`](/packages/markitdown/src/markitdown/converters/_plain_text_converter.py#L33-L72)

# PlainTextConverter Documentation

## Overview
`PlainTextConverter` is a subclass of `DocumentConverter` designed to handle documents with the content type `text/plain`. It provides methods to determine if a file can be accepted for conversion and to convert the file's content to a markdown format.

## Methods

### accepts

#### Description
The `accepts` method checks if the provided file stream can be accepted for conversion based on its MIME type, file extension, and character set.

#### Parameters
- `file_stream` (BinaryIO): A binary stream of the file content that is to be checked for acceptance.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
  - `charset` (Optional[str]): The character set of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter, not used in the implementation.

#### Returns
- `bool`: Returns `True` if the file can be accepted for conversion, otherwise returns `False`.

#### Logic
1. If `stream_info.charset` is not `None`, the method returns `True`.
2. If the file extension is in `ACCEPTED_FILE_EXTENSIONS`, the method returns `True`.
3. If the MIME type starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`, the method returns `True`.
4. If none of the above conditions are met, the method returns `False`.

### convert

#### Description
The `convert` method reads the content of the provided file stream and converts it into markdown format.

#### Parameters
- `file_stream` (BinaryIO): A binary stream of the file content that is to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `charset` (Optional[str]): The character set of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter, not used in the implementation.

#### Returns
- `DocumentConverterResult`: An object containing the converted markdown text.

#### Logic
1. If `stream_info.charset` is provided, the method reads the file content and decodes it using the specified charset.
2. If `stream_info.charset` is not provided, the method reads the file content and converts it to a string using `from_bytes(file_stream.read()).best()`.
3. The method returns a `DocumentConverterResult` containing the markdown text.

## Dependencies
- `DocumentConverter`: The base class that `PlainTextConverter` extends.
- `StreamInfo`: A class that encapsulates metadata about the file being processed.
- `DocumentConverterResult`: A class used to return the result of the conversion.
- `from_bytes`: A function used to convert byte data to a string format.

## Usage Example
```python
converter = PlainTextConverter()
file_stream = open('example.txt', 'rb')  # Open a binary file stream
stream_info = StreamInfo(mimetype='text/plain', extension='txt', charset='utf-8')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
file_stream.close()
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
