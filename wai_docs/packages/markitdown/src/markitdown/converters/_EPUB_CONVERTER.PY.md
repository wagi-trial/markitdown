# packages/markitdown/src/markitdown/converters/_epub_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_epub_converter.py",
  "file_hash": "c79684e502e1195256a725afe5387f67602202d3e9115aeb1581cda9203b1873",
  "last_updated": "2026-01-04T17:20:11.003211+00:00",
  "functions": {
    "EpubConverter": {
      "hash": "7077160e323ef1cb63e5ecbb15f9c5186de51184e3b0b037829fea1c4e852282",
      "lines": "26-147",
      "last_updated": "2026-01-04T17:20:11.003153+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_epub_converter.py` implements an EPUB to Markdown conversion process through the `EpubConverter` class, which inherits from the `HtmlConverter` class. The primary operations of this file include accepting EPUB file streams based on their MIME type and file extension, extracting metadata and content from EPUB files, and converting that content into Markdown format while preserving certain structural elements like headings and tables.

The `EpubConverter` class contains several methods: 
- `__init__`: Initializes the converter and creates an instance of `HtmlConverter`.
- `accepts`: Determines if the provided file stream is an acceptable EPUB format based on its MIME type or file extension.
- `convert`: Handles the conversion of the EPUB file stream into Markdown, extracting metadata and content from the EPUB structure, and formatting it accordingly.
- `_get_text_from_node`: Extracts a single text value from a specified XML tag.
- `_get_all_texts_from_nodes`: Retrieves all text values from a specified XML tag.

The code explicitly imports modules such as `os`, `zipfile`, and `defusedxml.minidom` for file handling and XML parsing. It also utilizes types from the `typing` module, including `BinaryIO`, `Any`, `Dict`, and `List`. The file defines constants for accepted MIME type prefixes and file extensions, as well as a mapping of file extensions to their corresponding MIME types. The data structures manipulated within the file include dictionaries for storing metadata and manifest items, lists for spine order and converted Markdown content, and instances of `DocumentConverterResult` to encapsulate the final output of the conversion process.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `EpubConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`
- `_get_text_from_node`
- `_get_all_texts_from_nodes`

<details>
<summary><strong>Calls/Dependencies</strong> (35 unique functions)</summary>

- `DocumentConverterResult`
- `EpubConverter`
- `HtmlConverter`
- `StreamInfo`
- `ZipFile`
- `__init__`
- `_get_all_texts_from_nodes`
- `_get_text_from_node`
- `accepts`
- `append`
- `basename`
- `capitalize`
- `convert`
- `get`
- `getAttribute`
- `getElementsByTagName`
- `hasattr`
- `information`
- `insert`
- `isinstance`
- `items`
- `join`
- `len`
- `lower`
- `metadata`
- `namelist`
- `open`
- `order`
- `parse`
- `split`
- `splitext`
- `startswith`
- `strip`
- `super`
- `tag`

</details>

</details>



## Functions and Classes

## `EpubConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_epub_converter.py:26`](/packages/markitdown/src/markitdown/converters/_epub_converter.py#L26-L147)

**Nested Functions:** `__init__`, `accepts`, `convert`, `_get_text_from_node`, `_get_all_texts_from_nodes`  
**Dependencies:** `DocumentConverterResult`, `EpubConverter`, `HtmlConverter`, `StreamInfo`, `ZipFile`, `__init__`, `_get_all_texts_from_nodes`, `_get_text_from_node`, `accepts`, `append`, `basename`, `capitalize`, `convert`, `get`, `getAttribute` *(+20 more)*  


# EpubConverter Documentation

## Overview
`EpubConverter` is a class that extends `HtmlConverter` and is designed to convert EPUB files into Markdown format. The conversion process preserves style information, such as headings and tables, where possible.

## Parameters

### `__init__(self)`
- **Parameters**: None
- **Usage**: Initializes an instance of the `EpubConverter` class and calls the constructor of the parent class `HtmlConverter`. It also initializes a private attribute `_html_converter` which is an instance of `HtmlConverter`.

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the EPUB file to be converted.
  - `stream_info` (StreamInfo): An object that contains metadata about the file, including:
    - `mimetype` (str): The MIME type of the file.
    - `extension` (str): The file extension.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns**: `bool` - Returns `True` if the file is accepted for conversion based on its MIME type or extension; otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the EPUB file to be converted.
  - `stream_info` (StreamInfo): An object that contains metadata about the file, including:
    - `mimetype` (str): The MIME type of the file.
    - `extension` (str): The file extension.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns**: `DocumentConverterResult` - An object containing:
  - `markdown` (str): The converted Markdown content.
  - `title` (str): The title of the EPUB document extracted from its metadata.

## Dependencies
- `zipfile`: Used to read and extract files from the EPUB archive.
- `minidom`: Used to parse XML files, specifically for reading the EPUB metadata.
- `os`: Used to manipulate file paths.
- `Dict`, `List`: Type hints from the `typing` module.
- `HtmlConverter`: The parent class that provides HTML to Markdown conversion functionality.
- `StreamInfo`: A class that encapsulates metadata about the file being processed.
- `DocumentConverterResult`: A class that encapsulates the result of the conversion process.

## Usage Example
```python
from io import BytesIO

# Create an instance of EpubConverter
converter = EpubConverter()

# Example EPUB file stream (as a binary stream)
epub_file_stream = BytesIO(b'...')  # Replace with actual EPUB binary data
stream_info = StreamInfo(mimetype='application/epub+zip', extension='epub')

# Check if the converter accepts the file
if converter.accepts(epub_file_stream, stream_info):
    # Perform the conversion
    result = converter.convert(epub_file_stream, stream_info)
    print(result.markdown)  # Output the converted Markdown content
    print(result.title)     # Output the title of the EPUB document
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
