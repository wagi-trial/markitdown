# packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py",
  "file_hash": "79c4da06af57c75e05e33b4cf9f23761f7c5e41337ef1568afea3203492e7360",
  "last_updated": "2026-01-04T17:15:36.456524+00:00",
  "functions": {
    "register_converters": {
      "hash": "d1151c41ec4ee9534e7bb2921a3c3bd3ddf1b9aa7454bd9153585f54d0f89d10",
      "lines": "25-33",
      "last_updated": "2026-01-04T17:15:30.439511+00:00"
    },
    "RtfConverter": {
      "hash": "cea9f57d91a21172a298075eccbd5bd1cb867aedeba608ce8c6587e4c33bc7ec",
      "lines": "34-72",
      "last_updated": "2026-01-04T17:15:36.456459+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py` implements a plugin for the MarkItDown framework that provides functionality to convert RTF (Rich Text Format) files into Markdown format. The file defines a function `register_converters` and a class `RtfConverter`, which are responsible for integrating the RTF conversion capability into the MarkItDown system.

The `register_converters` function is called during the initialization of MarkItDown instances. Its responsibility is to register an instance of the `RtfConverter` class with the MarkItDown instance. The `RtfConverter` class extends the `DocumentConverter` class and implements two methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream's MIME type or file extension matches the accepted formats for RTF files. The `convert` method reads the RTF file stream, decodes it using the specified or default character encoding, and converts the RTF content to Markdown using the `rtf_to_text` function from the `striprtf` library. It returns a `DocumentConverterResult` containing the converted Markdown content.

The file explicitly imports several modules and classes, including `locale`, `BinaryIO`, `Any`, and `rtf_to_text` from the `striprtf` library, as well as components from the `markitdown` package such as `MarkItDown`, `DocumentConverter`, `DocumentConverterResult`, and `StreamInfo`. The code defines constants for accepted MIME type prefixes and file extensions, specifically for RTF files. The data structures manipulated include `BinaryIO` for file streams, `StreamInfo` for metadata about the file, and `DocumentConverterResult` for the output of the conversion process.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `register_converters`

<details>
<summary><strong>Calls/Dependencies</strong> (3 unique functions)</summary>

- `RtfConverter`
- `register_converter`
- `register_converters`

</details>

### `RtfConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (10 unique functions)</summary>

- `DocumentConverterResult`
- `RtfConverter`
- `accepts`
- `convert`
- `decode`
- `getpreferredencoding`
- `lower`
- `read`
- `rtf_to_text`
- `startswith`

</details>

</details>



## Functions and Classes

## `register_converters`

**Location:** [`packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py:25`](/packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py#L25-L33)

**Dependencies:** `RtfConverter`, `register_converter`, `register_converters`  


# Function Documentation: register_converters

## Description
The `register_converters` function is called during the construction of `MarkItDown` instances. It registers converters provided by plugins by creating and attaching an instance of `RtfConverter` to the `MarkItDown` instance.

## Parameters

- `markitdown` (MarkItDown): 
  - Type: `MarkItDown`
  - Constraints: Must be an instance of the `MarkItDown` class.
  - Usage: This parameter is used to register the `RtfConverter` instance with the `MarkItDown` instance.

- `**kwargs`:
  - Type: Keyword arguments (dictionary).
  - Constraints: No specific constraints are enforced on the keyword arguments.
  - Usage: This parameter allows for additional keyword arguments to be passed but is not used within the function implementation.

## Return Value
The function does not return a value. It performs an action by registering a converter with the `MarkItDown` instance.

## Dependencies
- The function relies on the `MarkItDown` class and the `RtfConverter` class. Both must be defined and accessible within the scope where this function is called.

## Usage Example
```python
markitdown_instance = MarkItDown()
register_converters(markitdown_instance)
```

---
## `RtfConverter`

**Location:** [`packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py:34`](/packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py#L34-L72)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `DocumentConverterResult`, `RtfConverter`, `accepts`, `convert`, `decode`, `getpreferredencoding`, `lower`, `read`, `rtf_to_text`, `startswith`  


# RtfConverter Documentation

## Overview
`RtfConverter` is a class that extends `DocumentConverter`. It is designed to convert RTF (Rich Text Format) files into a simpler text format. The conversion process involves reading the file stream, decoding it using a specified character set, and then transforming the RTF content into plain text.

## Method: accepts

### Description
The `accepts` method determines whether the provided file stream and stream information are acceptable for conversion based on file extension and MIME type.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional keyword arguments that may be passed but are not used in the implementation.

### Returns
- `bool`: Returns `True` if the file extension is in `ACCEPTED_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

## Method: convert

### Description
The `convert` method reads the provided file stream, decodes it using the specified character set, and converts the RTF content into plain text.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the RTF file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `charset` (str): The character set encoding to use for decoding the file stream.
- `**kwargs` (Any): Additional keyword arguments that may be passed but are not used in the implementation.

### Returns
- `DocumentConverterResult`: An object containing the result of the conversion, which includes:
  - `title` (None): The title of the document, which is set to `None`.
  - `markdown` (str): The plain text representation of the RTF content, generated by the `rtf_to_text` function.

## Dependencies
- `locale`: Used to get the system's preferred character encoding.
- `rtf_to_text`: A function that converts RTF formatted strings to plain text.
- `DocumentConverter`: The base class that `RtfConverter` extends.
- `DocumentConverterResult`: The class used to encapsulate the result of the conversion.

## Usage Example
```python
from io import BytesIO

# Create an instance of RtfConverter
converter = RtfConverter()

# Prepare a mock file stream and stream info
file_stream = BytesIO(b"{\\rtf1\\ansi\\ansicpg1252\\deff0\\nouicompat\\deflang1033{\\fonttbl{\\f0\\fnil\\fcharset0 Calibri;}}")
stream_info = StreamInfo(mimetype="application/rtf", extension=".rtf", charset="utf-8")

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    # Perform the conversion
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
