# packages/markitdown/src/markitdown/converters/_doc_intel_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_doc_intel_converter.py",
  "file_hash": "d80c5cf9efdf1b1da8f7c8f3482286cdcbfffdb795e6383a6615b93c75755bca",
  "last_updated": "2026-01-04T17:19:48.771242+00:00",
  "functions": {
    "DocumentIntelligenceFileType": {
      "hash": "fc4145aa6fbc65e9a16c231affe24a334fe4fb8aa0562d2c18416f9d47c61276",
      "lines": "55-70",
      "last_updated": "2026-01-04T17:19:34.514103+00:00"
    },
    "_get_mime_type_prefixes": {
      "hash": "e7f387c3b5f3511bb67eb9f24c79bf9e780ac9c799abe51c0754aa9fccc78be7",
      "lines": "71-103",
      "last_updated": "2026-01-04T17:19:38.747260+00:00"
    },
    "_get_file_extensions": {
      "hash": "5b494b2614363580aade9e4500fd93c9a83490a56ac0f0a5db602f7ba5b9ea93",
      "lines": "104-129",
      "last_updated": "2026-01-04T17:19:42.355180+00:00"
    },
    "DocumentIntelligenceConverter": {
      "hash": "514280464e4c62ec58342c7770249363c4cff95be2c6769b31430a6f99bb4893",
      "lines": "130-255",
      "last_updated": "2026-01-04T17:19:48.771170+00:00"
    }
  }
}
```

</details>



The Python file `_doc_intel_converter.py` implements a specialized document converter that utilizes Azure's Document Intelligence service to extract text from various document formats. The primary class defined in this file is `DocumentIntelligenceConverter`, which inherits from `DocumentConverter`. This class is responsible for initializing the converter with an endpoint, API version, and authentication credentials, and it checks for the availability of required dependencies. The converter supports multiple file types, including DOCX, PPTX, XLSX, PDF, JPEG, PNG, BMP, and TIFF.

The file defines an enumeration `DocumentIntelligenceFileType`, which lists the supported file types for the converter. It also includes two utility functions: `_get_mime_type_prefixes`, which returns a list of MIME type prefixes corresponding to the specified file types, and `_get_file_extensions`, which returns the file extensions for those types. These functions facilitate the handling of different document formats by providing necessary metadata for file type identification.

The code explicitly imports several modules from the Azure SDK, including `DocumentIntelligenceClient`, `AnalyzeDocumentRequest`, `AnalyzeResult`, `DocumentAnalysisFeature`, `AzureKeyCredential`, `TokenCredential`, and `DefaultAzureCredential`. These imports are essential for interacting with the Azure Document Intelligence API. The file also defines data structures such as the `DocumentIntelligenceFileType` enum and utilizes type hints for function parameters and return types, enhancing code clarity and type safety. Additionally, the file handles exceptions related to missing dependencies, ensuring that the converter operates correctly only when all required components are available.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `DocumentIntelligenceFileType`

<details>
<summary><strong>Calls/Dependencies</strong> (1 unique function)</summary>

- `DocumentIntelligenceFileType`

</details>

### `_get_mime_type_prefixes`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `_get_mime_type_prefixes`
- `append`

</details>

### `_get_file_extensions`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `_get_file_extensions`
- `append`

</details>

### `DocumentIntelligenceConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `_analysis_features`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (27 unique functions)</summary>

- `AnalyzeDocumentRequest`
- `AzureKeyCredential`
- `DefaultAzureCredential`
- `DocumentConverterResult`
- `DocumentIntelligenceClient`
- `DocumentIntelligenceConverter`
- `MissingDependencyException`
- `__init__`
- `_analysis_features`
- `_get_file_extensions`
- `_get_mime_type_prefixes`
- `accepts`
- `api_version`
- `begin_analyze_document`
- `convert`
- `credential`
- `endpoint`
- `file_types`
- `filetypes`
- `get`
- `lower`
- `read`
- `result`
- `startswith`
- `sub`
- `super`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `DocumentIntelligenceFileType`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:55`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L55-L70)

**Dependencies:** `DocumentIntelligenceFileType`  


# Documentation for DocumentIntelligenceFileType

## Overview
`DocumentIntelligenceFileType` is an enumeration class that defines the various file types supported by the Document Intelligence Converter. The enumeration inherits from `str` and `Enum`, allowing each file type to be treated as a string while providing a set of predefined constants.

## Enum Members
The enumeration includes the following members:

### No OCR
- `DOCX`: Represents the Microsoft Word document file type. Value: `"docx"`
- `PPTX`: Represents the Microsoft PowerPoint presentation file type. Value: `"pptx"`
- `XLSX`: Represents the Microsoft Excel spreadsheet file type. Value: `"xlsx"`
- `HTML`: Represents the HyperText Markup Language file type. Value: `"html"`

### OCR
- `PDF`: Represents the Portable Document Format file type. Value: `"pdf"`
- `JPEG`: Represents the Joint Photographic Experts Group image file type. Value: `"jpeg"`
- `PNG`: Represents the Portable Network Graphics image file type. Value: `"png"`
- `BMP`: Represents the Bitmap image file type. Value: `"bmp"`
- `TIFF`: Represents the Tagged Image File Format file type. Value: `"tiff"`

## Parameters
The `DocumentIntelligenceFileType` class does not accept any parameters during instantiation. It is a predefined enumeration with fixed values.

## Return Value
The members of the `DocumentIntelligenceFileType` enumeration return string values that correspond to the file types defined in the enumeration. Each member can be accessed directly to obtain its string representation.

## Dependencies
The implementation of `DocumentIntelligenceFileType` relies on the following external modules:
- `str`: Built-in Python type for string representation.
- `Enum`: A class from the `enum` module in Python, which provides the base functionality for creating enumerations.

## Usage Example
An example of how to use the `DocumentIntelligenceFileType` enumeration is as follows:

```python
file_type = DocumentIntelligenceFileType.PDF
print(file_type)  # Output: pdf
``` 

This example demonstrates accessing the `PDF` member of the enumeration and printing its string value.

---
## `_get_mime_type_prefixes`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:71`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L71-L103)

**Dependencies:** `_get_mime_type_prefixes`, `append`  


# Documentation for `_get_mime_type_prefixes`

## Function Overview
The `_get_mime_type_prefixes` function retrieves the MIME type prefixes corresponding to a list of specified document file types. It constructs a list of MIME type strings based on the provided file types.

## Parameters
- `types` (List[DocumentIntelligenceFileType]): A list of file types from the `DocumentIntelligenceFileType` enumeration. Each file type is checked against predefined cases to determine its corresponding MIME type prefixes.

## Return Value
- Returns a `List[str]`: A list of strings representing the MIME type prefixes associated with the input file types. The list may contain multiple entries for certain file types.

## MIME Type Mapping
The function maps the following file types to their respective MIME type prefixes:
- `DocumentIntelligenceFileType.DOCX`: 
  - `application/vnd.openxmlformats-officedocument.wordprocessingml.document`
- `DocumentIntelligenceFileType.PPTX`: 
  - `application/vnd.openxmlformats-officedocument.presentationml`
- `DocumentIntelligenceFileType.XLSX`: 
  - `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet`
- `DocumentIntelligenceFileType.HTML`: 
  - `text/html`
  - `application/xhtml+xml`
- `DocumentIntelligenceFileType.PDF`: 
  - `application/pdf`
  - `application/x-pdf`
- `DocumentIntelligenceFileType.JPEG`: 
  - `image/jpeg`
- `DocumentIntelligenceFileType.PNG`: 
  - `image/png`
- `DocumentIntelligenceFileType.BMP`: 
  - `image/bmp`
- `DocumentIntelligenceFileType.TIFF`: 
  - `image/tiff`

## Dependencies
The function relies on the `DocumentIntelligenceFileType` enumeration, which must be defined elsewhere in the codebase. No external modules, APIs, or services are explicitly called within this function.

## Usage Example
```python
file_types = [DocumentIntelligenceFileType.DOCX, DocumentIntelligenceFileType.PDF]
mime_type_prefixes = _get_mime_type_prefixes(file_types)
# mime_type_prefixes will be:
# [
#     "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
#     "application/pdf",
#     "application/x-pdf"
# ]
```

---
## `_get_file_extensions`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:104`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L104-L129)

**Dependencies:** `_get_file_extensions`, `append`  


# Documentation for `_get_file_extensions`

## Function Overview
The `_get_file_extensions` function retrieves the file extensions corresponding to a list of specified document types defined by the `DocumentIntelligenceFileType` enumeration. The function iterates over each document type and appends the appropriate file extension to a list, which is then returned.

## Parameters
- `types` (List[DocumentIntelligenceFileType]): 
  - A list of document types from the `DocumentIntelligenceFileType` enumeration.
  - Each element in the list is checked against predefined document types to determine the corresponding file extensions.

## Return Value
- Returns a List[str]:
  - A list of strings representing the file extensions associated with the provided document types.
  - The possible extensions included in the returned list are:
    - ".docx" for `DocumentIntelligenceFileType.DOCX`
    - ".pptx" for `DocumentIntelligenceFileType.PPTX`
    - ".xlsx" for `DocumentIntelligenceFileType.XLSX`
    - ".pdf" for `DocumentIntelligenceFileType.PDF`
    - ".jpg" and ".jpeg" for `DocumentIntelligenceFileType.JPEG`
    - ".png" for `DocumentIntelligenceFileType.PNG`
    - ".bmp" for `DocumentIntelligenceFileType.BMP`
    - ".tiff" for `DocumentIntelligenceFileType.TIFF`
    - ".html" for `DocumentIntelligenceFileType.HTML`

## Dependencies
- The function relies on the `DocumentIntelligenceFileType` enumeration, which must be defined elsewhere in the codebase. There are no external modules, APIs, or services explicitly called in this function.

## Usage Example
```python
from typing import List

# Assuming DocumentIntelligenceFileType is defined and imported
file_types = [DocumentIntelligenceFileType.DOCX, DocumentIntelligenceFileType.PDF, DocumentIntelligenceFileType.JPEG]
extensions = _get_file_extensions(file_types)
# extensions will be [".docx", ".pdf", ".jpg", ".jpeg"]
```

---
## `DocumentIntelligenceConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:130`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L130-L255)

**Nested Functions:** `__init__`, `accepts`, `_analysis_features`, `convert`  
**Dependencies:** `AnalyzeDocumentRequest`, `AzureKeyCredential`, `DefaultAzureCredential`, `DocumentConverterResult`, `DocumentIntelligenceClient`, `DocumentIntelligenceConverter`, `MissingDependencyException`, `__init__`, `_analysis_features`, `_get_file_extensions`, `_get_mime_type_prefixes`, `accepts`, `api_version`, `begin_analyze_document`, `convert` *(+12 more)*  


# DocumentIntelligenceConverter Documentation

## Overview
`DocumentIntelligenceConverter` is a subclass of `DocumentConverter` that utilizes Azure's Document Intelligence service to extract text from various document formats. It supports multiple file types and provides functionality to determine if a file can be processed based on its type and MIME type.

## Constructor
### `__init__`
Initializes a new instance of `DocumentIntelligenceConverter`.

#### Parameters
- `endpoint` (str): 
  - The endpoint URL for the Document Intelligence service.
  
- `api_version` (str, optional): 
  - The API version to use. Defaults to `"2024-07-31-preview"`.

- `credential` (AzureKeyCredential | TokenCredential | None, optional): 
  - The credential used for authentication. If not provided, the function checks for the `AZURE_API_KEY` environment variable. If the variable is not set, it uses `DefaultAzureCredential`.

- `file_types` (List[DocumentIntelligenceFileType], optional): 
  - A list of accepted file types for conversion. Defaults to:
    - `DocumentIntelligenceFileType.DOCX`
    - `DocumentIntelligenceFileType.PPTX`
    - `DocumentIntelligenceFileType.XLSX`
    - `DocumentIntelligenceFileType.PDF`
    - `DocumentIntelligenceFileType.JPEG`
    - `DocumentIntelligenceFileType.PNG`
    - `DocumentIntelligenceFileType.BMP`
    - `DocumentIntelligenceFileType.TIFF`

#### Exceptions
- Raises `MissingDependencyException` if the required dependency `[az-doc-intel]` is not installed.

## Methods
### `accepts`
Determines if the converter can process a given file based on its stream information.

#### Parameters
- `file_stream` (BinaryIO): 
  - The binary stream of the file to check.
  
- `stream_info` (StreamInfo): 
  - An object containing metadata about the file, including its MIME type and extension.

- `**kwargs` (Any): 
  - Additional options to pass to the converter.

#### Returns
- (bool): 
  - Returns `True` if the file type or MIME type is acceptable; otherwise, returns `False`.

### `_analysis_features`
Determines which analysis features to use based on the file type.

#### Parameters
- `stream_info` (StreamInfo): 
  - An object containing metadata about the file.

#### Returns
- (List[str]): 
  - A list of analysis features to enable. Returns an empty list if the file type does not support OCR.

### `convert`
Extracts text from the provided file stream using Azure Document Intelligence.

#### Parameters
- `file_stream` (BinaryIO): 
  - The binary stream of the document to convert.
  
- `stream_info` (StreamInfo): 
  - An object containing metadata about the file.

- `**kwargs` (Any): 
  - Additional options to pass to the converter.

#### Returns
- (DocumentConverterResult): 
  - Returns a `DocumentConverterResult` object containing the extracted text in Markdown format.

## Dependencies
- Requires the Azure Document Intelligence client library.
- Requires the optional dependency `[az-doc-intel]` to be installed for functionality.

## Usage Example
```python
converter = DocumentIntelligenceConverter(
    endpoint="https://your-endpoint.com",
    credential=AzureKeyCredential("your-api-key")
)

with open("document.pdf", "rb") as file_stream:
    stream_info = StreamInfo(mimetype="application/pdf", extension=".pdf")
    if converter.accepts(file_stream, stream_info):
        result = converter.convert(file_stream, stream_info)
        print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
