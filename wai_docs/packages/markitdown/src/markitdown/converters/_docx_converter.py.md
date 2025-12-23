# packages/markitdown/src/markitdown/converters/_docx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_docx_converter.py",
  "file_hash": "a6d7a3c55046aa92147aa2afe14c428287e85e3aa3bafe79397de97f0667dd49",
  "last_updated": "2025-12-23T15:49:42.899373+00:00",
  "functions": {
    "DocxConverter": {
      "hash": "88c5c6074ddac1673dfa09b66e5c97dc5e32ac3aeb0a88c2526b0c73d610cb86",
      "lines": "31-84",
      "last_updated": "2025-12-23T15:49:42.899283+00:00"
    }
  }
}
```

</details>



The Python file `_docx_converter.py` implements a `DocxConverter` class that is responsible for converting DOCX files into Markdown format. The conversion process preserves style information, such as headings and tables, to the extent possible. The class inherits from `HtmlConverter` and utilizes the `mammoth` library to facilitate the conversion from DOCX to HTML, which is then transformed into Markdown.

The main class defined in this file is `DocxConverter`. Its constructor initializes an instance of `HtmlConverter`. The class includes two primary methods: `accepts` and `convert`. The `accepts` method determines if the provided file stream is compatible with the converter by checking its MIME type and file extension against predefined accepted values. The `convert` method processes the DOCX file stream by first checking for the presence of required dependencies, then pre-processing the stream, and finally converting the content to HTML using `mammoth`, which is subsequently converted to Markdown.

The file explicitly imports several modules, including `sys`, `io`, and `warnings`, as well as specific components from other modules within the package, such as `HtmlConverter`, `pre_process_docx`, `DocumentConverterResult`, `StreamInfo`, and `MissingDependencyException`. The code defines constants for accepted MIME type prefixes and file extensions, and it manipulates data types such as `BinaryIO` and `Any` for function parameters. The `convert` method also utilizes a `style_map` option for customizing the conversion process.

## Functions and Classes

## `DocxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_docx_converter.py:31`](/packages/markitdown/src/markitdown/converters/_docx_converter.py#L31-L84)

# DocxConverter Class Documentation

## Overview
The `DocxConverter` class is a subclass of `HtmlConverter` that is designed to convert DOCX files into Markdown format. It preserves style information, such as headings, and tables where possible.

## Constructor
### `__init__(self)`
Initializes a new instance of the `DocxConverter` class. It calls the constructor of the parent class `HtmlConverter` and initializes an instance of `HtmlConverter` as `_html_converter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type or file extension.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the file to be converted. This parameter is not directly used in the acceptance logic.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file, which is checked against accepted prefixes.
  - `extension` (str): The file extension, which is checked against accepted extensions.
- `**kwargs` (Any): Additional options that can be passed to the converter. This parameter is not used in the acceptance logic.

#### Returns:
- `bool`: Returns `True` if the file extension is in `ACCEPTED_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided DOCX file stream into Markdown format.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the DOCX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options that can be passed to the converter, including:
  - `style_map` (Optional): A mapping of styles to be applied during the conversion.

#### Returns:
- `DocumentConverterResult`: The result of the conversion, which contains the converted Markdown content.

#### Exceptions:
- Raises `MissingDependencyException` if there is a missing dependency required for the conversion process.

## Dependencies
- The class uses the following external modules:
  - `HtmlConverter`: The parent class from which `DocxConverter` inherits.
  - `mammoth`: A library used to convert DOCX files to HTML.
  - `pre_process_docx`: A function that processes the DOCX file stream before conversion.
  - `MissingDependencyException`: An exception raised when a required dependency is not met.

## Usage Example
```python
from io import BytesIO

# Create an instance of DocxConverter
converter = DocxConverter()

# Example file stream and stream info
file_stream = BytesIO(b'...')  # Replace with actual DOCX file bytes
stream_info = StreamInfo(mimetype='application/vnd.openxmlformats-officedocument.wordprocessingml.document', extension='docx')

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info, style_map=None)
    # Process the result as needed
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
