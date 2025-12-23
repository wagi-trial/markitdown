# packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py",
  "file_hash": "79c4da06af57c75e05e33b4cf9f23761f7c5e41337ef1568afea3203492e7360",
  "last_updated": "2025-12-23T15:44:55.089417+00:00",
  "functions": {
    "register_converters": {
      "hash": "d1151c41ec4ee9534e7bb2921a3c3bd3ddf1b9aa7454bd9153585f54d0f89d10",
      "lines": "25-33",
      "last_updated": "2025-12-23T15:44:49.297944+00:00"
    },
    "RtfConverter": {
      "hash": "cea9f57d91a21172a298075eccbd5bd1cb867aedeba608ce8c6587e4c33bc7ec",
      "lines": "34-72",
      "last_updated": "2025-12-23T15:44:55.089315+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py` implements a plugin for the MarkItDown framework that facilitates the conversion of RTF (Rich Text Format) files into Markdown format. The file defines a function `register_converters`, which is called during the initialization of MarkItDown instances to register the `RtfConverter` class as a document converter. The `RtfConverter` class is responsible for determining whether a given file stream is acceptable for conversion based on its MIME type or file extension, and for performing the actual conversion from RTF to Markdown.

The main components of the file include the `register_converters` function and the `RtfConverter` class. The `register_converters` function takes an instance of `MarkItDown` and registers an instance of `RtfConverter`. The `RtfConverter` class extends the `DocumentConverter` class and implements two methods: `accepts`, which checks if the provided file stream is of an acceptable type based on predefined MIME type prefixes and file extensions, and `convert`, which reads the file stream, decodes it using the specified or default character encoding, and converts the RTF content to Markdown using the `rtf_to_text` function from the `striprtf` module.

The file explicitly imports several modules, including `locale`, `BinaryIO` and `Any` from the `typing` module, and the `rtf_to_text` function from the `striprtf.striprtf` module. It also imports classes from the `markitdown` module, specifically `MarkItDown`, `DocumentConverter`, `DocumentConverterResult`, and `StreamInfo`. The code defines constants for accepted MIME type prefixes and file extensions, which are used in the `accepts` method to validate input streams. The `RtfConverter` class manipulates data structures such as `StreamInfo` and `DocumentConverterResult`, which are integral to the conversion process.

## Functions and Classes

## `register_converters`

**Location:** [`packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py:25`](/packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py#L25-L33)

# Function Documentation: register_converters

## Description
The `register_converters` function is invoked during the construction of `MarkItDown` instances to register converters that are provided by plugins. The function specifically creates an instance of `RtfConverter` and registers it with the provided `markitdown` instance.

## Parameters

- `markitdown` (MarkItDown): 
  - Type: `MarkItDown`
  - Constraints: Must be an instance of the `MarkItDown` class.
  - Usage: This parameter is used to call the `register_converter` method to attach the `RtfConverter` instance.

- `**kwargs`: 
  - Type: `dict`
  - Constraints: Accepts any number of keyword arguments.
  - Usage: This parameter is not utilized within the function implementation.

## Return Value
The function does not return any value (return type is `None`). Its purpose is to perform a side effect of registering a converter with the `markitdown` instance.

## Dependencies
- The function relies on the `MarkItDown` class, which must have a method named `register_converter`.
- The function also requires the `RtfConverter` class to be defined and accessible within the scope of the function.

## Usage Example
```python
markitdown_instance = MarkItDown()
register_converters(markitdown_instance)
```

---
## `RtfConverter`

**Location:** [`packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py:34`](/packages/markitdown-sample-plugin/src/markitdown_sample_plugin/_plugin.py#L34-L72)

# RtfConverter Documentation

## Overview
The `RtfConverter` class is a subclass of `DocumentConverter` that provides functionality to convert RTF (Rich Text Format) files into a simpler text format. The conversion process involves reading the input file stream, decoding it using a specified character set, and transforming the RTF content into plain text.

## Method: accepts

### Description
The `accepts` method determines whether the provided file stream and its associated metadata are acceptable for conversion based on file extension and MIME type.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the input file. This parameter is used to read the file's content.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file, which is checked against accepted prefixes.
  - `extension` (str): The file extension, which is checked against accepted file extensions.
- `**kwargs` (Any): Additional keyword arguments that are not utilized in the method.

### Returns
- `bool`: Returns `True` if the file's extension is in the list of accepted file extensions or if the MIME type starts with any of the accepted MIME type prefixes. Returns `False` otherwise.

## Method: convert

### Description
The `convert` method performs the actual conversion of the RTF file to plain text. It reads the content of the file stream, decodes it using the specified character set, and converts the RTF content to text.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the input RTF file. This parameter is used to read the file's content.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `charset` (str): The character set encoding to use for decoding the file stream. If not provided, the system's default encoding is used.
- `**kwargs` (Any): Additional keyword arguments that are not utilized in the method.

### Returns
- `DocumentConverterResult`: An object containing the result of the conversion, which includes:
  - `title` (None): The title is set to `None`.
  - `markdown` (str): The converted plain text derived from the RTF content.

## Dependencies
- `locale`: The `locale` module is used to obtain the system's preferred character encoding if no charset is provided.
- `rtf_to_text`: A function that converts RTF formatted strings to plain text. This function is called within the `convert` method.

## Usage Example
```python
# Example usage of RtfConverter
converter = RtfConverter()
file_stream = open('example.rtf', 'rb')  # Open an RTF file in binary mode
stream_info = StreamInfo(mimetype='application/rtf', extension='rtf', charset='utf-8')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)  # Output the converted plain text
file_stream.close()
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
