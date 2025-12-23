# packages/markitdown/src/markitdown/converters/_xlsx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_xlsx_converter.py",
  "file_hash": "e8c3a4beb34b69c86a17c3ee673927421b3d6c514dcb8eb0c55123dc4af04f8c",
  "last_updated": "2025-12-23T15:52:50.965916+00:00",
  "functions": {
    "XlsxConverter": {
      "hash": "ecb8134ee89d75eea30d18bd0f2094a510ee1b3135284d515ba1028d20193ea1",
      "lines": "36-97",
      "last_updated": "2025-12-23T15:52:45.669996+00:00"
    },
    "XlsConverter": {
      "hash": "c8b0d0e3ead14d570d535614262b17d3ec2a2a5a850f14e38e9d3a7e72295014",
      "lines": "98-158",
      "last_updated": "2025-12-23T15:52:50.965842+00:00"
    }
  }
}
```

</details>



The Python file `_xlsx_converter.py` implements two classes, `XlsxConverter` and `XlsConverter`, which are responsible for converting XLSX and XLS files, respectively, into Markdown format. Each class extends the `DocumentConverter` base class and provides methods to check if the input file is acceptable based on its MIME type and file extension, as well as a method to perform the conversion. The conversion process involves reading the spreadsheet data using the `pandas` library, converting each sheet into an HTML table, and then transforming that HTML into Markdown format using an instance of `HtmlConverter`.

The `XlsxConverter` class specifically handles files with the `.xlsx` extension and the corresponding MIME types, while the `XlsConverter` class manages `.xls` files. Both classes include an `accepts` method to verify if the provided file stream and stream information match the accepted formats. The `convert` method in each class reads the file stream, processes the sheets, and constructs the Markdown output. If the required dependencies (`pandas`, `openpyxl`, and `xlrd`) are not available, a `MissingDependencyException` is raised.

The code explicitly imports the `pandas` library for data manipulation and `openpyxl` and `xlrd` for reading Excel files. It defines constants for accepted MIME types and file extensions for both XLSX and XLS formats. The file also utilizes the `BinaryIO` type for file streams and the `Any` type for additional options in method parameters. The `DocumentConverterResult` class is used to encapsulate the resulting Markdown output from the conversion process.

## Functions and Classes

## `XlsxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_xlsx_converter.py:36`](/packages/markitdown/src/markitdown/converters/_xlsx_converter.py#L36-L97)

# XlsxConverter Documentation

## Class Overview
`XlsxConverter` is a subclass of `DocumentConverter` that converts XLSX files into Markdown format. Each sheet in the XLSX file is represented as a separate Markdown table.

## Constructor
### `__init__(self)`
Initializes an instance of `XlsxConverter`. It calls the parent class constructor and initializes an instance of `HtmlConverter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file based on its MIME type and file extension.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns:
- `bool`: Returns `True` if the file extension is in `ACCEPTED_XLSX_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_XLSX_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided XLSX file into Markdown format.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the XLSX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns:
- `DocumentConverterResult`: An object containing the converted Markdown content. The `markdown` attribute of this object contains the Markdown representation of the XLSX file.

#### Exceptions:
- Raises `MissingDependencyException` if the required dependencies for processing XLSX files are not available.

## Dependencies
- The method `pd.read_excel` from the `pandas` library is used to read the XLSX file.
- The `HtmlConverter` class is instantiated to convert HTML tables to Markdown.
- The `openpyxl` engine is specified for reading XLSX files.

## Usage Example
```python
converter = XlsxConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    markdown_content = result.markdown
```

---
## `XlsConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_xlsx_converter.py:98`](/packages/markitdown/src/markitdown/converters/_xlsx_converter.py#L98-L158)

# XlsConverter Documentation

## Overview
`XlsConverter` is a class that extends `DocumentConverter`. It is designed to convert XLS files into Markdown format, with each sheet in the XLS file represented as a separate Markdown table.

## Constructor
### `__init__(self)`
- Initializes an instance of `XlsConverter`.
- Calls the constructor of the parent class `DocumentConverter`.
- Initializes an instance of `HtmlConverter` and assigns it to the attribute `_html_converter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **Parameters:**
  - `file_stream`: `BinaryIO`
    - A binary stream representing the XLS file to be converted.
  - `stream_info`: `StreamInfo`
    - An object containing metadata about the stream, including:
      - `mimetype`: A string representing the MIME type of the file.
      - `extension`: A string representing the file extension.
  - `**kwargs`: `Any`
    - Additional options to pass to the converter (not used in this method).
- **Returns:** `bool`
  - Returns `True` if the file extension is in `ACCEPTED_XLS_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_XLS_MIME_TYPE_PREFIXES`. Otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **Parameters:**
  - `file_stream`: `BinaryIO`
    - A binary stream representing the XLS file to be converted.
  - `stream_info`: `StreamInfo`
    - An object containing metadata about the stream.
  - `**kwargs`: `Any`
    - Additional options to pass to the converter (used in the HTML conversion).
- **Returns:** `DocumentConverterResult`
  - Returns an instance of `DocumentConverterResult` containing:
    - `markdown`: A string that represents the Markdown content generated from the XLS file, with each sheet formatted as a Markdown table.

## Dependencies
- The method `convert` uses the following external modules:
  - `pandas` (specifically `pd.read_excel`) to read the XLS file.
  - `HtmlConverter` to convert HTML content to Markdown.
- The code checks for a dependency on the `_xls_dependency_exc_info` variable, which indicates whether the required dependencies for handling XLS files are available.

## Usage Example
```python
converter = XlsConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
