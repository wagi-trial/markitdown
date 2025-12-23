# packages/markitdown/src/markitdown/converters/_zip_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_zip_converter.py",
  "file_hash": "63486d6505ad24addef3dd5ab280e52e6b8b1825a498961478c31c4f318bdef0",
  "last_updated": "2025-12-23T15:53:17.747363+00:00",
  "functions": {
    "ZipConverter": {
      "hash": "90c4dc81930cf51d01054a2fe94d74c96565e70d4b2443069f5932297cb7cebf",
      "lines": "22-117",
      "last_updated": "2025-12-23T15:53:17.747282+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_zip_converter.py` implements the `ZipConverter` class, which is responsible for converting ZIP files into markdown format. The conversion process involves extracting the contents of the ZIP file, processing each contained file using appropriate converters based on their file extensions, and compiling the results into a single markdown document. The class also ensures that temporary files created during the conversion are cleaned up after processing.

The main class defined in this file is `ZipConverter`, which inherits from `DocumentConverter`. The `ZipConverter` class includes two primary methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream and stream information correspond to accepted MIME types or file extensions, specifically looking for ZIP files. The `convert` method handles the extraction of the ZIP file, iterates through its contents, and utilizes the `_markitdown` instance to convert each file stream into markdown format, appending the results to a cumulative markdown string.

The file explicitly imports several modules, including `zipfile`, `io`, and `os`, as well as type hinting utilities from `typing`. It also imports several components from the parent module, such as `DocumentConverter`, `DocumentConverterResult`, `StreamInfo`, `UnsupportedFormatException`, and `FileConversionException`. The `StreamInfo` class is used to encapsulate information about the file streams being processed, including their extensions and filenames. The code defines constants for accepted MIME type prefixes and file extensions, specifically for ZIP files, ensuring that the converter only processes compatible formats.

## Functions and Classes

## `ZipConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_zip_converter.py:22`](/packages/markitdown/src/markitdown/converters/_zip_converter.py#L22-L117)

# ZipConverter Documentation

## Overview
The `ZipConverter` class is a subclass of `DocumentConverter` that converts ZIP files into markdown format by extracting and processing all contained files. It utilizes appropriate converters based on the file extensions of the extracted files and combines the results into a single markdown document. Temporary files created during processing are cleaned up after the conversion is complete.

## Parameters

### `__init__(self, *, markitdown: "MarkItDown")`
- **markitdown**: `MarkItDown`
  - This parameter is an instance of the `MarkItDown` class, which is used to convert individual file streams to markdown format. It is required for the initialization of the `ZipConverter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **file_stream**: `BinaryIO`
  - A binary input stream representing the ZIP file to be converted.
  
- **stream_info**: `StreamInfo`
  - An object containing metadata about the file stream, including:
    - `mimetype`: A string representing the MIME type of the file.
    - `extension`: A string representing the file extension.
  
- **kwargs**: `Any`
  - Additional options that can be passed to the converter (not utilized in the implementation).

- **Returns**: `bool`
  - Returns `True` if the file is accepted for conversion based on its MIME type or file extension, otherwise returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **file_stream**: `BinaryIO`
  - A binary input stream representing the ZIP file to be converted.

- **stream_info**: `StreamInfo`
  - An object containing metadata about the file stream, including:
    - `url`: A string representing the URL of the file.
    - `local_path`: A string representing the local path of the file.
    - `filename`: A string representing the name of the file.

- **kwargs**: `Any`
  - Additional options that can be passed to the converter (not utilized in the implementation).

- **Returns**: `DocumentConverterResult`
  - An object containing the markdown representation of the converted ZIP file. The markdown includes headings for each file extracted from the ZIP, followed by the content converted to markdown format.

## Dependencies
The `ZipConverter` class explicitly depends on the following external modules:
- `zipfile`: Used to handle ZIP file operations.
- `io`: Used for creating in-memory byte streams.
- `os`: Used for file path operations.
- `StreamInfo`: A class that encapsulates metadata about the file stream.
- `DocumentConverterResult`: A class that represents the result of the document conversion process.
- `UnsupportedFormatException`: An exception raised when a file format is not supported.
- `FileConversionException`: An exception raised when a file conversion fails.

## Usage Example
```python
from some_module import MarkItDown, ZipConverter, StreamInfo

# Create an instance of MarkItDown
markitdown_instance = MarkItDown()

# Create an instance of ZipConverter
zip_converter = ZipConverter(markitdown=markitdown_instance)

# Open a ZIP file as a binary stream
with open('example.zip', 'rb') as zip_file:
    stream_info = StreamInfo(
        mimetype='application/zip',
        extension='zip',
        url='example.zip',
        local_path='path/to/example.zip',
        filename='example.zip'
    )
    
    # Check if the converter accepts the file
    if zip_converter.accepts(zip_file, stream_info):
        # Convert the ZIP file to markdown
        result = zip_converter.convert(zip_file, stream_info)
        print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
