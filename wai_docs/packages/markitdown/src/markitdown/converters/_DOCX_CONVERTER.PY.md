# packages/markitdown/src/markitdown/converters/_docx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_docx_converter.py",
  "file_hash": "a6d7a3c55046aa92147aa2afe14c428287e85e3aa3bafe79397de97f0667dd49",
  "last_updated": "2026-01-04T17:20:00.178114+00:00",
  "functions": {
    "DocxConverter": {
      "hash": "88c5c6074ddac1673dfa09b66e5c97dc5e32ac3aeb0a88c2526b0c73d610cb86",
      "lines": "31-84",
      "last_updated": "2026-01-04T17:20:00.178034+00:00"
    }
  }
}
```

</details>



The Python file `_docx_converter.py` implements a `DocxConverter` class that is responsible for converting DOCX files into Markdown format. This class inherits from `HtmlConverter` and utilizes the `mammoth` library to handle the conversion process. The `DocxConverter` class includes methods to check if a given file stream is acceptable for conversion based on its MIME type and file extension, as well as a method to perform the actual conversion of the DOCX file into Markdown.

The `DocxConverter` class contains the following methods:
- `__init__`: Initializes the `DocxConverter` instance and creates an instance of `HtmlConverter`.
- `accepts`: Determines if the provided file stream and its associated `StreamInfo` indicate that the file is a DOCX file based on its MIME type and file extension.
- `convert`: Performs the conversion of the DOCX file to Markdown. It first checks for the presence of the required `mammoth` dependency and raises a `MissingDependencyException` if it is not available. It preprocesses the DOCX file stream, converts it to HTML using `mammoth`, and then converts the resulting HTML to Markdown using the `HtmlConverter`.

The code explicitly imports several modules, including `sys`, `io`, and `warnings`, as well as specific components from the package's structure, such as `HtmlConverter`, `pre_process_docx`, `DocumentConverterResult`, `StreamInfo`, and `MissingDependencyException`. The `DocxConverter` class manipulates binary input streams (`BinaryIO`) and utilizes the `StreamInfo` data structure to access metadata about the file being processed. The file also defines constants for accepted MIME type prefixes and file extensions that are relevant for the conversion process.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `DocxConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (17 unique functions)</summary>

- `DocxConverter`
- `HtmlConverter`
- `MissingDependencyException`
- `__init__`
- `accepts`
- `convert`
- `convert_string`
- `convert_to_html`
- `format`
- `get`
- `information`
- `lower`
- `pre_process_docx`
- `startswith`
- `super`
- `type`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `DocxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_docx_converter.py:31`](/packages/markitdown/src/markitdown/converters/_docx_converter.py#L31-L84)

**Nested Functions:** `__init__`, `accepts`, `convert`  
**Dependencies:** `DocxConverter`, `HtmlConverter`, `MissingDependencyException`, `__init__`, `accepts`, `convert`, `convert_string`, `convert_to_html`, `format`, `get`, `information`, `lower`, `pre_process_docx`, `startswith`, `super` *(+2 more)*  


# DocxConverter Class Documentation

## Overview
The `DocxConverter` class is designed to convert DOCX files into Markdown format. It extends the `HtmlConverter` class and aims to preserve style information, such as headings and tables, during the conversion process.

## Constructor
### `__init__(self)`
- Initializes a new instance of the `DocxConverter` class.
- Calls the constructor of the superclass `HtmlConverter`.
- Creates an instance of `HtmlConverter` and assigns it to the `_html_converter` attribute.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines whether the converter can accept the provided file stream based on its MIME type or file extension.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional options to pass to the converter (not utilized in this method).

#### Returns
- `bool`: Returns `True` if the file extension or MIME type is accepted; otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided DOCX file stream into Markdown format.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the DOCX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options to pass to the converter, including:
  - `style_map` (Optional): A mapping of styles to be applied during the conversion.

#### Returns
- `DocumentConverterResult`: The result of the conversion, which contains the Markdown representation of the DOCX file.

#### Exceptions
- Raises `MissingDependencyException` if there are missing dependencies required for conversion.

## Dependencies
- The class relies on the following external modules:
  - `mammoth`: Used for converting DOCX to HTML.
  - `HtmlConverter`: The superclass from which `DocxConverter` inherits.
  - `pre_process_docx`: A function that processes the DOCX file stream before conversion.
  - `MissingDependencyException`: An exception raised when required dependencies are not met.

## Usage Example
```python
from io import BytesIO

# Create an instance of DocxConverter
converter = DocxConverter()

# Prepare a file stream and stream info
file_stream = BytesIO()  # Replace with actual DOCX file stream
stream_info = StreamInfo(mimetype='application/vnd.openxmlformats-officedocument.wordprocessingml.document', extension='docx')

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    # result now contains the Markdown representation of the DOCX file
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
