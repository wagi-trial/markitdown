# packages/markitdown/src/markitdown/converters/_pdf_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_pdf_converter.py",
  "file_hash": "783d77e34018b07e80a0bb9f90325c9de5251a4caedbd39568c4b0c3eaf2ae8f",
  "last_updated": "2025-12-23T15:51:33.073577+00:00",
  "functions": {
    "PdfConverter": {
      "hash": "7c528d84934d2a0b3b0ca8a62c114a3fe0113a34beeab6714483380075ca6e6f",
      "lines": "31-78",
      "last_updated": "2025-12-23T15:51:33.073486+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_pdf_converter.py` implements a PDF to Markdown conversion functionality through the `PdfConverter` class, which inherits from the `DocumentConverter` base class. This class provides methods to determine if a given file can be accepted for conversion and to perform the actual conversion from PDF format to Markdown text. The conversion process utilizes the `pdfminer` library to extract text from PDF files.

The main class defined in this file is `PdfConverter`, which includes two primary methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream's MIME type or file extension matches accepted formats for PDF files, specifically looking for the MIME types "application/pdf" and "application/x-pdf" and the file extension ".pdf". The `convert` method verifies the availability of the required `pdfminer` dependency and extracts text from the PDF file stream, returning the result as a `DocumentConverterResult` instance containing the extracted Markdown text.

The code explicitly imports the `pdfminer` library and its `high_level` module for text extraction. It also imports several components from the local module, including `DocumentConverter`, `DocumentConverterResult`, `StreamInfo`, and `MissingDependencyException`. The file defines constants for accepted MIME type prefixes and file extensions, and it manipulates types such as `BinaryIO` and `Any` from the `typing` module. The `convert` method raises a `MissingDependencyException` if the `pdfminer` library is not available, ensuring that the required dependency is present before attempting to perform the conversion.

## Functions and Classes

## `PdfConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_pdf_converter.py:31`](/packages/markitdown/src/markitdown/converters/_pdf_converter.py#L31-L78)

# PdfConverter Class Documentation

## Overview
The `PdfConverter` class is a subclass of `DocumentConverter` that is designed to convert PDF files into Markdown format. The conversion process disregards most style information, resulting in output that is primarily plain text.

## Method: accepts

### Description
The `accepts` method determines if the provided file stream and stream information are acceptable for conversion by checking the file extension and MIME type.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the PDF file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including its MIME type and extension.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `bool`: Returns `True` if the file extension or MIME type is acceptable for conversion; otherwise, returns `False`.

### Logic
The method checks if the file extension is in the predefined list of accepted file extensions (`ACCEPTED_FILE_EXTENSIONS`). If not, it checks if the MIME type starts with any of the prefixes defined in `ACCEPTED_MIME_TYPE_PREFIXES`.

## Method: convert

### Description
The `convert` method performs the actual conversion of the PDF file to Markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the PDF file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `DocumentConverterResult`: An object containing the converted Markdown text extracted from the PDF file.

### Logic
1. The method checks for the presence of a dependency required for PDF conversion. If the dependency is missing, it raises a `MissingDependencyException`.
2. It asserts that `file_stream` is an instance of `io.IOBase`.
3. It uses `pdfminer.high_level.extract_text` to extract text from the `file_stream` and returns it encapsulated in a `DocumentConverterResult`.

## Dependencies
- `pdfminer.high_level`: This module is used for extracting text from PDF files.
- `MissingDependencyException`: This exception is raised if the required dependencies for PDF conversion are not met.

## Usage Example
```python
from io import BytesIO

# Assuming `PdfConverter` is properly imported and initialized
converter = PdfConverter()
file_stream = BytesIO(b"%PDF-1.4 ...")  # Example PDF binary content
stream_info = StreamInfo(mimetype="application/pdf", extension=".pdf")

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)  # Output the converted Markdown text
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
