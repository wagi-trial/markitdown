# packages/markitdown/src/markitdown/converters/_pdf_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_pdf_converter.py",
  "file_hash": "783d77e34018b07e80a0bb9f90325c9de5251a4caedbd39568c4b0c3eaf2ae8f",
  "last_updated": "2026-01-04T17:21:40.991440+00:00",
  "functions": {
    "PdfConverter": {
      "hash": "7c528d84934d2a0b3b0ca8a62c114a3fe0113a34beeab6714483380075ca6e6f",
      "lines": "31-78",
      "last_updated": "2026-01-04T17:21:40.991383+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_pdf_converter.py` implements a PDF to Markdown conversion functionality through the `PdfConverter` class, which inherits from the `DocumentConverter` class. This class provides methods to determine if a given file can be accepted for conversion and to perform the conversion itself. The `accepts` method checks if the input file stream's MIME type or file extension matches the accepted criteria for PDF files. The `convert` method processes the PDF file stream using the `pdfminer` library to extract text, returning the result in a `DocumentConverterResult` format.

The primary class defined in this file is `PdfConverter`, which includes two methods: `accepts` and `convert`. The `accepts` method evaluates whether the provided file stream is a valid PDF based on its MIME type and extension. The `convert` method performs the actual conversion from PDF to Markdown, raising a `MissingDependencyException` if the required `pdfminer` library is not available. The code explicitly imports the `pdfminer` library and its `high_level` module for text extraction, as well as several other modules for type hinting and exception handling.

The file defines and manipulates specific data structures and types, including `BinaryIO` for file streams, `Any` for flexible keyword arguments, and `StreamInfo` for metadata about the input stream. The `DocumentConverterResult` type is used to encapsulate the result of the conversion, specifically the extracted Markdown text. The code also handles exceptions related to missing dependencies, ensuring that any issues with importing `pdfminer` are captured and reported appropriately.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `PdfConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (12 unique functions)</summary>

- `DocumentConverterResult`
- `MissingDependencyException`
- `PdfConverter`
- `accepts`
- `convert`
- `extract_text`
- `format`
- `isinstance`
- `lower`
- `startswith`
- `type`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `PdfConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_pdf_converter.py:31`](/packages/markitdown/src/markitdown/converters/_pdf_converter.py#L31-L78)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `DocumentConverterResult`, `MissingDependencyException`, `PdfConverter`, `accepts`, `convert`, `extract_text`, `format`, `isinstance`, `lower`, `startswith`, `type`, `with_traceback`  


# PdfConverter Class Documentation

## Overview
The `PdfConverter` class is a subclass of `DocumentConverter` that provides functionality to convert PDF files into Markdown format. The conversion process disregards most style information, resulting in a plain-text representation of the PDF content.

## Method: accepts

### Description
The `accepts` method determines if the provided file stream and stream information are acceptable for conversion.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the PDF file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the file.
- `**kwargs` (Any): Additional options to pass to the converter (not used in the implementation).

### Returns
- `bool`: Returns `True` if the file extension is in `ACCEPTED_FILE_EXTENSIONS` or if the MIME type starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`. Returns `False` otherwise.

## Method: convert

### Description
The `convert` method performs the actual conversion of the PDF file to Markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the PDF file to be converted. It is asserted to be an instance of `io.IOBase`.
- `stream_info` (StreamInfo): An object containing metadata about the file (not used in the conversion process).
- `**kwargs` (Any): Additional options to pass to the converter (not used in the implementation).

### Returns
- `DocumentConverterResult`: An object containing the result of the conversion, specifically:
  - `markdown` (str): The extracted text from the PDF file, represented in Markdown format.

### Exceptions
- Raises `MissingDependencyException` if there is a missing dependency required for the conversion process. This is checked against the `_dependency_exc_info` variable.

## Dependencies
- The method `convert` relies on the `pdfminer.high_level.extract_text` function to extract text from the PDF file.
- The class references `DocumentConverterResult` to encapsulate the conversion result.
- The class assumes the presence of `ACCEPTED_FILE_EXTENSIONS` and `ACCEPTED_MIME_TYPE_PREFIXES` for validating file types.

## Usage Example
```python
from io import BytesIO

# Create an instance of PdfConverter
converter = PdfConverter()

# Prepare a binary stream for a PDF file
pdf_file_stream = BytesIO(b"%PDF-1.4...")  # Example binary content of a PDF
stream_info = StreamInfo(mimetype="application/pdf", extension="pdf")

# Check if the converter accepts the file
if converter.accepts(pdf_file_stream, stream_info):
    # Perform the conversion
    result = converter.convert(pdf_file_stream, stream_info)
    print(result.markdown)  # Output the converted Markdown text
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
