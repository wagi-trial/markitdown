# packages/markitdown/src/markitdown/converters/_zip_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_zip_converter.py",
  "file_hash": "63486d6505ad24addef3dd5ab280e52e6b8b1825a498961478c31c4f318bdef0",
  "last_updated": "2026-01-04T17:23:12.122891+00:00",
  "functions": {
    "ZipConverter": {
      "hash": "90c4dc81930cf51d01054a2fe94d74c96565e70d4b2443069f5932297cb7cebf",
      "lines": "22-117",
      "last_updated": "2026-01-04T17:23:12.122829+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_zip_converter.py` implements a `ZipConverter` class that is responsible for converting ZIP files into markdown format. The conversion process involves extracting the contents of the ZIP file, processing each contained file with appropriate converters based on their file extensions, and compiling the results into a single markdown document. The class also ensures that a temporary directory used for extraction is cleaned up after processing.

The `ZipConverter` class includes two primary methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream is in an accepted format by verifying the MIME type and file extension against predefined lists. The `convert` method performs the actual conversion by reading the ZIP file, iterating through its contents, and converting each file stream into markdown format using the `_markitdown` instance's `convert_stream` method. It handles exceptions related to unsupported formats and file conversion errors without interrupting the overall process.

The file imports several modules, including `zipfile`, `io`, and `os`, as well as types from the `typing` module for type hinting. It also imports specific classes and exceptions from other parts of the `markitdown` package, such as `DocumentConverter`, `DocumentConverterResult`, `StreamInfo`, `UnsupportedFormatException`, and `FileConversionException`. The `ZipConverter` class manipulates instances of `StreamInfo` to manage file metadata, such as file extensions and names, during the conversion process. The output of the conversion is structured as a markdown string, which includes headings for each file extracted from the ZIP archive.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `ZipConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (17 unique functions)</summary>

- `BytesIO`
- `DocumentConverterResult`
- `StreamInfo`
- `ZipConverter`
- `ZipFile`
- `__init__`
- `accepts`
- `basename`
- `convert`
- `convert_stream`
- `lower`
- `namelist`
- `read`
- `splitext`
- `startswith`
- `strip`
- `super`

</details>

</details>



## Functions and Classes

## `ZipConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_zip_converter.py:22`](/packages/markitdown/src/markitdown/converters/_zip_converter.py#L22-L117)

**Nested Functions:** `__init__`, `accepts`, `convert`  
**Dependencies:** `BytesIO`, `DocumentConverterResult`, `StreamInfo`, `ZipConverter`, `ZipFile`, `__init__`, `accepts`, `basename`, `convert`, `convert_stream`, `lower`, `namelist`, `read`, `splitext`, `startswith` *(+2 more)*  


# ZipConverter Documentation

## Overview
`ZipConverter` is a subclass of `DocumentConverter` that converts ZIP files into markdown format. It extracts files contained within the ZIP archive, processes each file using appropriate converters based on their extensions, and combines the results into a single markdown document. After processing, it cleans up any temporary files created during the conversion.

## Parameters

### `__init__`
- **markitdown**: `MarkItDown`
  - This parameter is a required keyword-only argument that represents an instance of the `MarkItDown` class. It is used to convert individual files within the ZIP archive to markdown format.

### `accepts`
- **file_stream**: `BinaryIO`
  - This parameter represents the input stream of the ZIP file.
  
- **stream_info**: `StreamInfo`
  - This parameter contains metadata about the file being processed, including:
    - `mimetype`: The MIME type of the file (optional).
    - `extension`: The file extension (optional).
  
- **kwargs**: `Any`
  - Additional options that can be passed to the converter (not explicitly used in the implementation).

### `convert`
- **file_stream**: `BinaryIO`
  - This parameter represents the input stream of the ZIP file.
  
- **stream_info**: `StreamInfo`
  - This parameter contains metadata about the file being processed, including:
    - `url`: The URL of the file (optional).
    - `local_path`: The local path of the file (optional).
    - `filename`: The name of the file (optional).
  
- **kwargs**: `Any`
  - Additional options that can be passed to the converter (not explicitly used in the implementation).

## Return Value
- Returns an instance of `DocumentConverterResult`.
  - The `markdown` attribute of this instance contains a string representing the combined markdown content generated from the files extracted from the ZIP archive.

## Dependencies
- The implementation explicitly uses the following external modules:
  - `zipfile`: For reading ZIP files.
  - `io`: For handling byte streams.
  - `os`: For file path manipulations.
  - `StreamInfo`: A class that holds metadata about the file.
  - `DocumentConverterResult`: A class that encapsulates the result of the conversion.
  - `UnsupportedFormatException`: An exception raised for unsupported file formats.
  - `FileConversionException`: An exception raised for errors during file conversion.

## Usage Example
```python
from some_module import MarkItDown, ZipConverter, StreamInfo

markitdown_instance = MarkItDown()
zip_converter = ZipConverter(markitdown=markitdown_instance)

with open('example.zip', 'rb') as zip_file:
    stream_info = StreamInfo(
        mimetype='application/zip',
        extension='zip',
        url='example.zip',
        filename='example.zip'
    )
    result = zip_converter.convert(zip_file, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
