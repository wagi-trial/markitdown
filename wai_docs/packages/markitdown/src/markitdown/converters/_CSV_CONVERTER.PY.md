# packages/markitdown/src/markitdown/converters/_csv_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_csv_converter.py",
  "file_hash": "b796945fb1a449d8199d46b84627cac951f43e40472ba09df8384a6269e111df",
  "last_updated": "2026-01-04T17:19:25.743166+00:00",
  "functions": {
    "CsvConverter": {
      "hash": "eaf6f9f2b517237b8bab5698310eaeb623eacfe515a51dcb652208f3f05157ac",
      "lines": "15-78",
      "last_updated": "2026-01-04T17:19:25.743105+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_csv_converter.py` implements a class named `CsvConverter`, which is responsible for converting CSV files into Markdown tables. The class extends `DocumentConverter`, indicating that it is part of a larger framework for document conversion. The `CsvConverter` class includes methods to check if a given file stream is acceptable for conversion and to perform the actual conversion from CSV format to Markdown format.

The `CsvConverter` class contains two primary methods: `accepts` and `convert`. The `accepts` method determines if the provided file stream and associated stream information (including MIME type and file extension) are suitable for CSV conversion based on predefined accepted MIME types and file extensions. The `convert` method reads the content of the CSV file, parses it using the `csv` module, and constructs a Markdown table from the parsed data. It handles character encoding by checking the charset in the stream info or using the `charset_normalizer` library to determine the best encoding. The resulting Markdown table is returned encapsulated in a `DocumentConverterResult` object.

The file imports several modules, including `csv`, `io`, and `charset_normalizer`, as well as types from the `typing` module. It also imports `DocumentConverter` and `DocumentConverterResult` from a relative path, indicating dependencies on these classes for its functionality. The data structures manipulated in this file include lists for storing CSV rows and the final Markdown table, as well as the `StreamInfo` class, which is used to encapsulate metadata about the file being processed.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `CsvConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (19 unique functions)</summary>

- `CsvConverter`
- `DocumentConverterResult`
- `StringIO`
- `__init__`
- `accepts`
- `append`
- `best`
- `convert`
- `decode`
- `from_bytes`
- `join`
- `len`
- `list`
- `lower`
- `read`
- `reader`
- `startswith`
- `str`
- `super`

</details>

</details>



## Functions and Classes

## `CsvConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_csv_converter.py:15`](/packages/markitdown/src/markitdown/converters/_csv_converter.py#L15-L78)

**Nested Functions:** `__init__`, `accepts`, `convert`  
**Dependencies:** `CsvConverter`, `DocumentConverterResult`, `StringIO`, `__init__`, `accepts`, `append`, `best`, `convert`, `decode`, `from_bytes`, `join`, `len`, `list`, `lower`, `read` *(+4 more)*  


# CsvConverter Documentation

## Overview
`CsvConverter` is a class that extends `DocumentConverter`. It is designed to convert CSV files into Markdown tables.

## Methods

### `__init__(self)`
Initializes a new instance of the `CsvConverter` class. It calls the constructor of the parent class `DocumentConverter`.

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type and file extension.

#### Parameters
- `file_stream` (BinaryIO): The input stream containing the file data.
- `stream_info` (StreamInfo): An object containing metadata about the stream, specifically:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional options to pass to the converter (not used in the implementation).

#### Returns
- `bool`: Returns `True` if the file extension or MIME type is accepted, otherwise returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided CSV file stream into a Markdown table format.

#### Parameters
- `file_stream` (BinaryIO): The input stream containing the CSV file data.
- `stream_info` (StreamInfo): An object containing metadata about the stream, specifically:
  - `charset` (str): The character set used to decode the file content.
- `**kwargs` (Any): Additional options to pass to the converter (not used in the implementation).

#### Returns
- `DocumentConverterResult`: An object containing the converted Markdown table as a string in the `markdown` attribute. If the CSV file is empty, the `markdown` attribute will be an empty string.

## Dependencies
- `csv`: The standard library module used for reading CSV data.
- `io`: The standard library module used for handling streams.
- `from_bytes`: A function that is called to convert bytes to a string (the implementation of this function is not provided in the code).
- `DocumentConverterResult`: A class that encapsulates the result of the conversion (the implementation of this class is not provided in the code).
- `StreamInfo`: A class that holds metadata about the stream (the implementation of this class is not provided in the code).
- `ACCEPTED_FILE_EXTENSIONS`: A collection of accepted file extensions (the implementation of this variable is not provided in the code).
- `ACCEPTED_MIME_TYPE_PREFIXES`: A collection of accepted MIME type prefixes (the implementation of this variable is not provided in the code).

## Usage Example
```python
converter = CsvConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
