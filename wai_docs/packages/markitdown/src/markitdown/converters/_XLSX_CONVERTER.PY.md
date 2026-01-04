# packages/markitdown/src/markitdown/converters/_xlsx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_xlsx_converter.py",
  "file_hash": "e8c3a4beb34b69c86a17c3ee673927421b3d6c514dcb8eb0c55123dc4af04f8c",
  "last_updated": "2026-01-04T17:22:50.631460+00:00",
  "functions": {
    "XlsxConverter": {
      "hash": "ecb8134ee89d75eea30d18bd0f2094a510ee1b3135284d515ba1028d20193ea1",
      "lines": "36-97",
      "last_updated": "2026-01-04T17:22:46.597437+00:00"
    },
    "XlsConverter": {
      "hash": "c8b0d0e3ead14d570d535614262b17d3ec2a2a5a850f14e38e9d3a7e72295014",
      "lines": "98-158",
      "last_updated": "2026-01-04T17:22:50.631401+00:00"
    }
  }
}
```

</details>



The Python file `_xlsx_converter.py` implements two classes, `XlsxConverter` and `XlsConverter`, which are responsible for converting XLSX and XLS files, respectively, into Markdown format. Each class inherits from `DocumentConverter` and provides methods to check if the input file is accepted based on its MIME type or file extension, and to perform the conversion from the spreadsheet format to Markdown. The conversion process involves reading the contents of the spreadsheet, converting each sheet to HTML, and then transforming that HTML into Markdown format.

The `XlsxConverter` class specifically handles files with the `.xlsx` extension and the MIME type prefix `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`. It utilizes the `pandas` library with the `openpyxl` engine to read the spreadsheet data. The `XlsConverter` class manages files with the `.xls` extension and MIME types such as `application/vnd.ms-excel`, using `pandas` with the `xlrd` engine for reading. Both classes raise a `MissingDependencyException` if the required dependencies are not available.

The file imports several modules, including `pandas`, `openpyxl`, and `xlrd`, as well as custom modules such as `HtmlConverter`, `DocumentConverter`, `DocumentConverterResult`, `MissingDependencyException`, and `StreamInfo`. It defines constants for accepted MIME types and file extensions for both XLSX and XLS formats. The methods `accepts` and `convert` are key interfaces that determine whether a file can be processed and execute the conversion, respectively. The data structures manipulated include `BinaryIO` for file streams and `DocumentConverterResult` for returning the Markdown content.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `XlsxConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (17 unique functions)</summary>

- `DocumentConverterResult`
- `HtmlConverter`
- `MissingDependencyException`
- `XlsxConverter`
- `__init__`
- `accepts`
- `convert`
- `convert_string`
- `format`
- `lower`
- `read_excel`
- `startswith`
- `strip`
- `super`
- `to_html`
- `type`
- `with_traceback`

</details>

### `XlsConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (17 unique functions)</summary>

- `DocumentConverterResult`
- `HtmlConverter`
- `MissingDependencyException`
- `XlsConverter`
- `__init__`
- `accepts`
- `convert`
- `convert_string`
- `format`
- `lower`
- `read_excel`
- `startswith`
- `strip`
- `super`
- `to_html`
- `type`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `XlsxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_xlsx_converter.py:36`](/packages/markitdown/src/markitdown/converters/_xlsx_converter.py#L36-L97)

**Nested Functions:** `__init__`, `accepts`, `convert`  
**Dependencies:** `DocumentConverterResult`, `HtmlConverter`, `MissingDependencyException`, `XlsxConverter`, `__init__`, `accepts`, `convert`, `convert_string`, `format`, `lower`, `read_excel`, `startswith`, `strip`, `super`, `to_html` *(+2 more)*  


# XlsxConverter Documentation

## Overview
`XlsxConverter` is a class that extends `DocumentConverter`. It converts XLSX files into Markdown format, where each sheet in the XLSX file is represented as a separate Markdown table.

## Constructor
### `__init__(self)`
Initializes an instance of the `XlsxConverter` class. It calls the constructor of the superclass `DocumentConverter` and initializes an instance of `HtmlConverter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type or file extension.

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the XLSX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `bool`: Returns `True` if the file extension is in `ACCEPTED_XLSX_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_XLSX_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided XLSX file stream into Markdown format.

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the XLSX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `DocumentConverterResult`: An object containing the converted Markdown content. The `markdown` attribute of this object contains the Markdown representation of the XLSX file, with each sheet formatted as a Markdown table.

## Dependencies
- The function uses the `pandas` library to read the XLSX file. It specifically calls `pd.read_excel` with the `openpyxl` engine.
- The function also relies on the `HtmlConverter` class to convert HTML content to Markdown.
- The function checks for the presence of a dependency related to XLSX conversion, raising a `MissingDependencyException` if the dependency is not met.

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

**Nested Functions:** `__init__`, `accepts`, `convert`  
**Dependencies:** `DocumentConverterResult`, `HtmlConverter`, `MissingDependencyException`, `XlsConverter`, `__init__`, `accepts`, `convert`, `convert_string`, `format`, `lower`, `read_excel`, `startswith`, `strip`, `super`, `to_html` *(+2 more)*  


# XlsConverter Documentation

## Overview
`XlsConverter` is a class that extends `DocumentConverter` to convert XLS files into Markdown format. Each sheet in the XLS file is represented as a separate Markdown table.

## Constructor
### `__init__(self)`
Initializes an instance of `XlsConverter`. It calls the constructor of the parent class `DocumentConverter` and initializes an instance of `HtmlConverter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type and file extension.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the file.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns:
- `bool`: Returns `True` if the file extension is in `ACCEPTED_XLS_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_XLS_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided XLS file stream into Markdown format.

#### Parameters:
- `file_stream` (BinaryIO): The input stream of the XLS file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns:
- `DocumentConverterResult`: An object containing the converted Markdown content in the `markdown` attribute.

## Dependencies
- `pandas`: Used to read the XLS file and convert sheets to HTML.
- `HtmlConverter`: An instance variable used to convert HTML content to Markdown.
- `xlrd`: Required for reading XLS files.
- `MissingDependencyException`: Raised if the necessary dependencies are not available.

## Usage Example
```python
converter = XlsConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    markdown_output = result.markdown
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
