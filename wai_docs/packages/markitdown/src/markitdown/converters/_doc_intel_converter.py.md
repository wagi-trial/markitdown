# packages/markitdown/src/markitdown/converters/_doc_intel_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_doc_intel_converter.py",
  "file_hash": "d80c5cf9efdf1b1da8f7c8f3482286cdcbfffdb795e6383a6615b93c75755bca",
  "last_updated": "2025-12-23T15:49:29.864216+00:00",
  "functions": {
    "DocumentIntelligenceFileType": {
      "hash": "fc4145aa6fbc65e9a16c231affe24a334fe4fb8aa0562d2c18416f9d47c61276",
      "lines": "55-70",
      "last_updated": "2025-12-23T15:49:12.256819+00:00"
    },
    "_get_mime_type_prefixes": {
      "hash": "e7f387c3b5f3511bb67eb9f24c79bf9e780ac9c799abe51c0754aa9fccc78be7",
      "lines": "71-103",
      "last_updated": "2025-12-23T15:49:17.473067+00:00"
    },
    "_get_file_extensions": {
      "hash": "5b494b2614363580aade9e4500fd93c9a83490a56ac0f0a5db602f7ba5b9ea93",
      "lines": "104-129",
      "last_updated": "2025-12-23T15:49:21.417784+00:00"
    },
    "DocumentIntelligenceConverter": {
      "hash": "514280464e4c62ec58342c7770249363c4cff95be2c6769b31430a6f99bb4893",
      "lines": "130-255",
      "last_updated": "2025-12-23T15:49:29.864130+00:00"
    }
  }
}
```

</details>



The Python file `_doc_intel_converter.py` implements functionality for converting various document types using Azure's Document Intelligence service. It defines a specialized converter, `DocumentIntelligenceConverter`, which extends the `DocumentConverter` class to extract text from documents of specified file types. The file supports operations for determining accepted MIME types and file extensions for a range of document formats, including DOCX, PPTX, XLSX, PDF, JPEG, PNG, BMP, and TIFF.

The main classes and functions in this file include:
- `DocumentIntelligenceFileType`: An enumeration that lists the file types supported by the Document Intelligence Converter.
- `_get_mime_type_prefixes`: A function that returns a list of MIME type prefixes corresponding to the specified document types.
- `_get_file_extensions`: A function that returns a list of file extensions associated with the specified document types.
- `DocumentIntelligenceConverter`: The primary class responsible for initializing the Document Intelligence client and managing the conversion process. It requires an endpoint and supports authentication via AzureKeyCredential or TokenCredential.

The code explicitly imports modules from the Azure SDK, including `DocumentIntelligenceClient`, `AnalyzeDocumentRequest`, `AnalyzeResult`, `DocumentAnalysisFeature`, `AzureKeyCredential`, `TokenCredential`, and `DefaultAzureCredential`. It also handles the potential absence of these dependencies by defining placeholder classes in case of import errors. The file manipulates data structures such as lists and enumerations to manage file types and their corresponding properties effectively.

## Functions and Classes

## `DocumentIntelligenceFileType`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:55`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L55-L70)

# DocumentIntelligenceFileType

## Overview
`DocumentIntelligenceFileType` is an enumeration class that defines a set of file types supported by the Document Intelligence Converter. The enumeration is derived from the `str` class and the `Enum` class, allowing for string representation of the file types.

## Enum Members
The enumeration includes the following members:

### No OCR
- `DOCX`: Represents the file type for Microsoft Word documents. Value: `"docx"`
- `PPTX`: Represents the file type for Microsoft PowerPoint presentations. Value: `"pptx"`
- `XLSX`: Represents the file type for Microsoft Excel spreadsheets. Value: `"xlsx"`
- `HTML`: Represents the file type for HTML documents. Value: `"html"`

### OCR
- `PDF`: Represents the file type for Portable Document Format files. Value: `"pdf"`
- `JPEG`: Represents the file type for JPEG image files. Value: `"jpeg"`
- `PNG`: Represents the file type for Portable Network Graphics image files. Value: `"png"`
- `BMP`: Represents the file type for Bitmap image files. Value: `"bmp"`
- `TIFF`: Represents the file type for Tagged Image File Format files. Value: `"tiff"`

## Parameters
The `DocumentIntelligenceFileType` class does not accept any parameters during instantiation. It is an enumeration and its members can be accessed directly.

## Return Value
The return value of accessing a member of `DocumentIntelligenceFileType` is of type `str`. Each member returns its associated string value, which represents the file type.

## Dependencies
The implementation of `DocumentIntelligenceFileType` relies on the following external modules:
- `Enum`: This is part of the Python standard library and is used to create enumerations.

## Usage Example
To use the `DocumentIntelligenceFileType` enumeration, you can access its members as follows:

```python
file_type = DocumentIntelligenceFileType.PDF
print(file_type)  # Output: pdf
```

This example demonstrates how to access the `PDF` member of the `DocumentIntelligenceFileType` enumeration and print its string value.

---
## `_get_mime_type_prefixes`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:71`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L71-L103)

# Documentation for `_get_mime_type_prefixes`

## Function Overview
The `_get_mime_type_prefixes` function retrieves the MIME type prefixes corresponding to a list of specified file types defined by the `DocumentIntelligenceFileType` enumeration. It constructs a list of MIME type strings based on the provided file types.

## Parameters
- `types` (List[DocumentIntelligenceFileType]): A list of file types for which MIME type prefixes are to be retrieved. Each item in the list must be an instance of `DocumentIntelligenceFileType`. The function iterates over this list to determine the appropriate MIME type prefixes.

## Return Value
- Returns a List[str]: The function returns a list of strings, each representing a MIME type prefix associated with the input file types. The list may contain multiple entries for certain file types (e.g., HTML and PDF).

## MIME Type Mappings
The function maps the following file types to their respective MIME type prefixes:
- `DocumentIntelligenceFileType.DOCX`: 
  - "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
- `DocumentIntelligenceFileType.PPTX`: 
  - "application/vnd.openxmlformats-officedocument.presentationml"
- `DocumentIntelligenceFileType.XLSX`: 
  - "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
- `DocumentIntelligenceFileType.HTML`: 
  - "text/html"
  - "application/xhtml+xml"
- `DocumentIntelligenceFileType.PDF`: 
  - "application/pdf"
  - "application/x-pdf"
- `DocumentIntelligenceFileType.JPEG`: 
  - "image/jpeg"
- `DocumentIntelligenceFileType.PNG`: 
  - "image/png"
- `DocumentIntelligenceFileType.BMP`: 
  - "image/bmp"
- `DocumentIntelligenceFileType.TIFF`: 
  - "image/tiff"

## Dependencies
The function relies on the `List` type from the `typing` module and the `DocumentIntelligenceFileType` enumeration, which must be defined elsewhere in the codebase.

## Usage Example
```python
from typing import List

# Assuming DocumentIntelligenceFileType is defined and imported
file_types = [DocumentIntelligenceFileType.DOCX, DocumentIntelligenceFileType.PDF]
mime_type_prefixes = _get_mime_type_prefixes(file_types)
# mime_type_prefixes will contain:
# [
#     "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
#     "application/pdf",
#     "application/x-pdf"
# ]
```

---
## `_get_file_extensions`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:104`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L104-L129)

# Documentation for `_get_file_extensions` Function

## Description
The `_get_file_extensions` function retrieves the file extensions corresponding to a list of specified file types defined by the `DocumentIntelligenceFileType` enumeration. The function iterates through the provided file types and appends the appropriate file extensions to a list, which is then returned.

## Parameters
- `types` (List[DocumentIntelligenceFileType]): A list of file types for which the function will return the corresponding file extensions. The function expects this list to contain elements of the `DocumentIntelligenceFileType` enumeration.

## Return Value
- Returns a `List[str]`: A list of strings representing the file extensions associated with the provided file types. The possible extensions include:
  - `.docx` for `DocumentIntelligenceFileType.DOCX`
  - `.pptx` for `DocumentIntelligenceFileType.PPTX`
  - `.xlsx` for `DocumentIntelligenceFileType.XLSX`
  - `.pdf` for `DocumentIntelligenceFileType.PDF`
  - `.jpg` and `.jpeg` for `DocumentIntelligenceFileType.JPEG`
  - `.png` for `DocumentIntelligenceFileType.PNG`
  - `.bmp` for `DocumentIntelligenceFileType.BMP`
  - `.tiff` for `DocumentIntelligenceFileType.TIFF`
  - `.html` for `DocumentIntelligenceFileType.HTML`

## Dependencies
The function relies on the `DocumentIntelligenceFileType` enumeration, which must be defined elsewhere in the codebase. There are no external modules, APIs, or services explicitly called within this function.

## Usage Example
```python
from typing import List

# Assuming DocumentIntelligenceFileType is defined and includes the necessary types
file_types = [DocumentIntelligenceFileType.DOCX, DocumentIntelligenceFileType.PDF]
extensions = _get_file_extensions(file_types)
# extensions will be ['.docx', '.pdf']
```

---
## `DocumentIntelligenceConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_doc_intel_converter.py:130`](/packages/markitdown/src/markitdown/converters/_doc_intel_converter.py#L130-L255)

# DocumentIntelligenceConverter Documentation

## Overview
`DocumentIntelligenceConverter` is a subclass of `DocumentConverter` that utilizes Azure's Document Intelligence service to extract text from various document formats. It is designed to handle specific file types and requires appropriate credentials for authentication.

## Constructor

### `__init__`
```python
def __init__(
    self,
    *,
    endpoint: str,
    api_version: str = "2024-07-31-preview",
    credential: AzureKeyCredential | TokenCredential | None = None,
    file_types: List[DocumentIntelligenceFileType] = [
        DocumentIntelligenceFileType.DOCX,
        DocumentIntelligenceFileType.PPTX,
        DocumentIntelligenceFileType.XLSX,
        DocumentIntelligenceFileType.PDF,
        DocumentIntelligenceFileType.JPEG,
        DocumentIntelligenceFileType.PNG,
        DocumentIntelligenceFileType.BMP,
        DocumentIntelligenceFileType.TIFF,
    ],
)
```

### Parameters
- **`endpoint` (str)**: The endpoint URL for the Document Intelligence service. This parameter is required for initializing the service client.
  
- **`api_version` (str, optional)**: The API version to use. Defaults to `"2024-07-31-preview"`. This parameter specifies which version of the API to interact with.

- **`credential` (AzureKeyCredential | TokenCredential | None, optional)**: The credential used for authentication. If not provided, the constructor checks for the `AZURE_API_KEY` environment variable. If the variable is not set, it defaults to `DefaultAzureCredential`.

- **`file_types` (List[DocumentIntelligenceFileType], optional)**: A list of accepted file types for conversion. Defaults to a predefined list of supported file types including DOCX, PPTX, XLSX, PDF, JPEG, PNG, BMP, and TIFF.

### Exceptions
- Raises `MissingDependencyException` if the required dependency `[az-doc-intel]` is not installed.

## Methods

### `accepts`
```python
def accepts(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> bool
```
#### Parameters
- **`file_stream` (BinaryIO)**: A binary stream representing the file to be checked.
  
- **`stream_info` (StreamInfo)**: An object containing metadata about the file, including its MIME type and extension.

- **`**kwargs` (Any)**: Additional options to pass to the converter (not utilized in the implementation).

#### Returns
- **bool**: Returns `True` if the file type is accepted based on its extension or MIME type; otherwise, returns `False`.

### `_analysis_features`
```python
def _analysis_features(self, stream_info: StreamInfo) -> List[str]
```
#### Parameters
- **`stream_info` (StreamInfo)**: An object containing metadata about the file, including its MIME type and extension.

#### Returns
- **List[str]**: A list of analysis features to be used for document analysis. Returns an empty list for certain file types that do not support OCR.

### `convert`
```python
def convert(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```
#### Parameters
- **`file_stream` (BinaryIO)**: A binary stream representing the document to be converted.

- **`stream_info` (StreamInfo)**: An object containing metadata about the file, including its MIME type and extension.

- **`**kwargs` (Any)**: Additional options to pass to the converter (not utilized in the implementation).

#### Returns
- **DocumentConverterResult**: An object containing the converted document text in Markdown format, with comments removed from the content.

## Dependencies
- Requires the `az-doc-intel` package for Document Intelligence functionality.
- Utilizes `AzureKeyCredential` and `TokenCredential` for authentication.
- Requires `DocumentIntelligenceClient` for interacting with the Azure Document Intelligence service.

## Usage Example
```python
converter = DocumentIntelligenceConverter(
    endpoint="https://your-endpoint.azure.com",
    credential=AzureKeyCredential("your-api-key")
)

with open("document.pdf", "rb") as file_stream:
    stream_info = StreamInfo(mimetype="application/pdf", extension=".pdf")
    result = converter.convert(file_stream, stream_info)

print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
