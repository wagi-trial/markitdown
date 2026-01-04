# packages/markitdown/src/markitdown/_base_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_base_converter.py",
  "file_hash": "22e88190ef1cdc1a8af6f03aff9cc06a7015d342b4a6f0dd3b91d4a9536567e7",
  "last_updated": "2026-01-04T17:16:34.629863+00:00",
  "functions": {
    "DocumentConverterResult": {
      "hash": "05cf8805cba6d30c91267191ade807a23dd23982aea3f9bee17b896c1791f3a9",
      "lines": "5-41",
      "last_updated": "2026-01-04T17:16:28.633319+00:00"
    },
    "DocumentConverter": {
      "hash": "8a735c8657e5b5186b9c8ee302f5f5582c83fef26cf84995bcf3621b1a3d0a03",
      "lines": "42-106",
      "last_updated": "2026-01-04T17:16:34.629799+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_base_converter.py` implements functionality for converting documents to Markdown format. It defines two primary classes: `DocumentConverterResult` and `DocumentConverter`. The `DocumentConverterResult` class encapsulates the result of a conversion, storing the converted Markdown text and an optional title. It provides a string representation method that returns the Markdown text and includes a soft-deprecated property for accessing the Markdown content via `text_content`.

The `DocumentConverter` class serves as an abstract superclass for all document converters. It defines two methods: `accepts` and `convert`. The `accepts` method is intended to determine if a specific converter can handle a given document based on its `file_stream` and `stream_info`. This method requires subclasses to implement their own logic for acceptance criteria. The `convert` method is designed to perform the actual conversion of the document to Markdown, returning an instance of `DocumentConverterResult`. Both methods require the `file_stream` to be a file-like object that supports `seek()`, `tell()`, and `read()` methods, and they utilize a `StreamInfo` object to access metadata about the file.

The file imports the `Any`, `BinaryIO`, and `Optional` types from the `typing` module, indicating the use of type hints for better code clarity. It also imports the `StreamInfo` class from the `_stream_info` module, which is utilized in the `accepts` and `convert` methods to handle file metadata. The code defines the `DocumentConverterResult` class with attributes for `markdown` and `title`, and the `DocumentConverter` class with abstract methods that must be implemented by subclasses.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `DocumentConverterResult`

**Nested Functions:**
- `__init__`
- `text_content`
- `__str__`

<details>
<summary><strong>Calls/Dependencies</strong> (3 unique functions)</summary>

- `__init__`
- `__str__`
- `text_content`

</details>

### `DocumentConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (10 unique functions)</summary>

- `NotImplementedError`
- `accepts`
- `convert`
- `determination`
- `file`
- `known`
- `read`
- `seek`
- `tell`
- `type`

</details>

</details>



## Functions and Classes

## `DocumentConverterResult`

**Location:** [`packages/markitdown/src/markitdown/_base_converter.py:5`](/packages/markitdown/src/markitdown/_base_converter.py#L5-L41)

**Nested Functions:** `__init__`, `text_content`, `__str__`  
**Dependencies:** `__init__`, `__str__`, `text_content`  


# DocumentConverterResult Class Documentation

## Overview
The `DocumentConverterResult` class encapsulates the result of converting a document to Markdown format. It stores the converted Markdown text and an optional title for the document.

## Parameters
The `__init__` method of the `DocumentConverterResult` class accepts the following parameters:

- `markdown` (str): 
  - Required parameter.
  - Contains the converted Markdown text.
  
- `title` (Optional[str]): 
  - Optional parameter.
  - Represents the title of the document. Defaults to `None`.

## Properties
- `text_content` (str):
  - A soft-deprecated alias for the `markdown` property.
  - Returns the value of `markdown`.
  - Can be set to a new string value, which updates the `markdown` property.

## Methods
- `__str__() -> str`:
  - Returns the converted Markdown text stored in the `markdown` property.

## Return Value
The `__str__` method returns a string that contains the converted Markdown text.

## Dependencies
The `DocumentConverterResult` class does not have any dependencies on external modules, APIs, or services.

## Usage Example
```python
result = DocumentConverterResult(markdown="# Sample Document", title="My Document")
print(result)  # Output: # Sample Document
print(result.text_content)  # Output: # Sample Document
result.text_content = "## Updated Document"
print(result.markdown)  # Output: ## Updated Document
```

---
## `DocumentConverter`

**Location:** [`packages/markitdown/src/markitdown/_base_converter.py:42`](/packages/markitdown/src/markitdown/_base_converter.py#L42-L106)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `NotImplementedError`, `accepts`, `convert`, `determination`, `file`, `known`, `read`, `seek`, `tell`, `type`  


# DocumentConverter Class Documentation

## Overview
The `DocumentConverter` class serves as an abstract superclass for all document converters. It defines the interface for converting documents to Markdown text and provides methods for determining if a specific converter can handle a given document.

## Methods

### accepts

```python
def accepts(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> bool
```

#### Description
The `accepts` method determines if the converter can handle a specific document based on the provided `stream_info`. It primarily evaluates the document's mimetype and extension, and may also consider the URL and filename in certain cases. 

#### Parameters
- `file_stream` (BinaryIO): A file-like object that supports `seek()`, `tell()`, and `read()` methods. This parameter represents the document to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including attributes such as `mimetype`, `extension`, and potentially `url` and `filename`.
- `kwargs` (Any): Additional keyword arguments that can be passed to the converter.

#### Returns
- `bool`: Returns `True` if the converter can handle the document, otherwise returns `False`.

#### Notes
- The method signature is designed to match that of the `convert()` method, ensuring that if `accepts()` returns `True`, the `convert()` method can also process the document.
- In some cases, additional data may need to be read from `file_stream` to make a determination. If this occurs, the file position must be reset before returning.

### convert

```python
def convert(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```

#### Description
The `convert` method is responsible for converting a document into Markdown text.

#### Parameters
- `file_stream` (BinaryIO): A file-like object that supports `seek()`, `tell()`, and `read()` methods. This parameter represents the document to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including attributes such as `mimetype`, `extension`, and potentially `charset`.
- `kwargs` (Any): Additional keyword arguments that can be passed to the converter.

#### Returns
- `DocumentConverterResult`: An object containing the result of the conversion, which includes the title and the Markdown content.

#### Raises
- `FileConversionException`: Raised if the mimetype is recognized but the conversion fails for another reason.
- `MissingDependencyException`: Raised if the converter requires a dependency that is not installed.

## Dependencies
The class references the following types:
- `BinaryIO`: This type is expected to be imported from the `typing` module.
- `StreamInfo`: This type is expected to be defined elsewhere in the codebase.
- `DocumentConverterResult`: This type is expected to be defined elsewhere in the codebase.
- `FileConversionException`: This exception is expected to be defined elsewhere in the codebase.
- `MissingDependencyException`: This exception is expected to be defined elsewhere in the codebase.

## Usage Example
```python
class MyDocumentConverter(DocumentConverter):
    def accepts(self, file_stream, stream_info, **kwargs):
        # Implementation of accepts method
        pass

    def convert(self, file_stream, stream_info, **kwargs):
        # Implementation of convert method
        pass

# Example of using MyDocumentConverter
converter = MyDocumentConverter()
file_stream = open('example.docx', 'rb')
stream_info = StreamInfo(mimetype='application/vnd.openxmlformats-officedocument.wordprocessingml.document', extension='docx')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.title)
    print(result.content)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
