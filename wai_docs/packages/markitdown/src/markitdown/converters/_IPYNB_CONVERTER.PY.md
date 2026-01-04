# packages/markitdown/src/markitdown/converters/_ipynb_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_ipynb_converter.py",
  "file_hash": "32ae36fe7f395dbc5c0a3fd3f09b62f2e7c96dba77362530c4f325a7f19ab70e",
  "last_updated": "2026-01-04T17:20:57.853345+00:00",
  "functions": {
    "IpynbConverter": {
      "hash": "d6135afb5c2e77fa50e432305a1c4f41d906121bffaad99a204ccc64c07927c6",
      "lines": "15-97",
      "last_updated": "2026-01-04T17:20:57.853268+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_ipynb_converter.py` implements functionality for converting Jupyter Notebook files (.ipynb) into Markdown format. It defines the `IpynbConverter` class, which extends the `DocumentConverter` base class. This class includes methods for accepting Jupyter Notebook files based on their MIME type and file extension, as well as converting the notebook content into Markdown.

The `IpynbConverter` class contains two primary methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream is a valid Jupyter Notebook by examining its MIME type and file extension, and by reading the content to verify the presence of specific keys in the JSON structure. The `convert` method reads the notebook content, decodes it, and passes it to a helper method `_convert`, which processes the JSON structure of the notebook and constructs the corresponding Markdown output. The `_convert` method handles different cell types (markdown, code, and raw) and formats them appropriately in the Markdown output, while also extracting a title from the notebook metadata or the content itself.

The code imports several modules, including `BinaryIO` and `Any` from the `typing` module, `json` for JSON parsing, and several components from the parent package, such as `DocumentConverter`, `DocumentConverterResult`, `FileConversionException`, and `StreamInfo`. The file manipulates data structures such as dictionaries (for notebook content) and lists (for Markdown output), and it defines interfaces for file streams and conversion results through the `DocumentConverter` class and its associated result type.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `IpynbConverter`

**Nested Functions:**
- `accepts`
- `convert`
- `_convert`

<details>
<summary><strong>Calls/Dependencies</strong> (20 unique functions)</summary>

- `DocumentConverterResult`
- `FileConversionException`
- `IpynbConverter`
- `Notebook`
- `_convert`
- `accepts`
- `append`
- `convert`
- `decode`
- `get`
- `join`
- `loads`
- `lower`
- `lstrip`
- `read`
- `seek`
- `startswith`
- `str`
- `strip`
- `tell`

</details>

</details>



## Functions and Classes

## `IpynbConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_ipynb_converter.py:15`](/packages/markitdown/src/markitdown/converters/_ipynb_converter.py#L15-L97)

**Nested Functions:** `accepts`, `convert`, `_convert`  
**Dependencies:** `DocumentConverterResult`, `FileConversionException`, `IpynbConverter`, `Notebook`, `_convert`, `accepts`, `append`, `convert`, `decode`, `get`, `join`, `loads`, `lower`, `lstrip`, `read` *(+5 more)*  


# IpynbConverter Documentation

## Overview
`IpynbConverter` is a class that extends `DocumentConverter`. It is designed to convert Jupyter Notebook files with the `.ipynb` extension into Markdown format.

## Method: accepts

### Description
The `accepts` method determines if the provided file stream can be processed by the converter based on its MIME type and file extension.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the content of the file to be checked.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
  - `charset` (str, optional): The character encoding of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `bool`: Returns `True` if the file can be accepted for conversion, `False` otherwise.

## Method: convert

### Description
The `convert` method reads the content of a Jupyter Notebook file and converts it into Markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the content of the Jupyter Notebook file.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `charset` (str, optional): The character encoding of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted Markdown content.
  - `title` (str, optional): The title extracted from the notebook metadata or the first heading found in the Markdown cells.

## Method: _convert

### Description
The `_convert` method is a helper function that processes the JSON content of a Jupyter Notebook and generates Markdown output.

### Parameters
- `notebook_content` (dict): A dictionary representation of the Jupyter Notebook content, parsed from JSON.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The generated Markdown content.
  - `title` (str, optional): The title extracted from the notebook metadata or the first heading found in the Markdown cells.

## Exceptions
- `FileConversionException`: Raised if an error occurs during the conversion process.

## Dependencies
- `json`: Used to parse the JSON content of the Jupyter Notebook.
- `DocumentConverter`: The base class that `IpynbConverter` extends.
- `DocumentConverterResult`: The return type for the conversion result.
- `StreamInfo`: A data structure that holds information about the file stream.

## Usage Example
```python
from io import BytesIO

# Create an instance of the converter
converter = IpynbConverter()

# Prepare a mock Jupyter Notebook file stream
notebook_stream = BytesIO(b'{"cells": [{"cell_type": "markdown", "source": ["# Title"]}]}')
stream_info = StreamInfo(mimetype="application/x-ipynb+json", extension=".ipynb", charset="utf-8")

# Check if the converter accepts the file
if converter.accepts(notebook_stream, stream_info):
    # Convert the notebook to Markdown
    result = converter.convert(notebook_stream, stream_info)
    print(result.markdown)  # Outputs the converted Markdown content
    print(result.title)     # Outputs the title extracted from the notebook
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
