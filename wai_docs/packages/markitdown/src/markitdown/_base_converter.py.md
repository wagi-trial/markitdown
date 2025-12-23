# packages/markitdown/src/markitdown/_base_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/_base_converter.py",
  "file_hash": "22e88190ef1cdc1a8af6f03aff9cc06a7015d342b4a6f0dd3b91d4a9536567e7",
  "last_updated": "2025-12-23T15:45:55.691623+00:00",
  "functions": {
    "DocumentConverterResult": {
      "hash": "05cf8805cba6d30c91267191ade807a23dd23982aea3f9bee17b896c1791f3a9",
      "lines": "5-41",
      "last_updated": "2025-12-23T15:45:49.746523+00:00"
    },
    "DocumentConverter": {
      "hash": "8a735c8657e5b5186b9c8ee302f5f5582c83fef26cf84995bcf3621b1a3d0a03",
      "lines": "42-106",
      "last_updated": "2025-12-23T15:45:55.691524+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/_base_converter.py` implements functionality for converting documents to Markdown format. It defines two primary classes: `DocumentConverterResult` and `DocumentConverter`. The `DocumentConverterResult` class encapsulates the result of a document conversion, storing the converted Markdown text and an optional title. It provides a string representation method and a soft-deprecated property for accessing the Markdown text.

The `DocumentConverter` class serves as an abstract base class for all document converters. It defines two methods: `accepts()` and `convert()`. The `accepts()` method is intended to determine if a specific document can be processed by the converter based on the provided `file_stream` and `stream_info`. It includes a note on the necessity of resetting the file stream position after reading for determination purposes. The `convert()` method is designed to perform the actual conversion of the document to Markdown and returns a `DocumentConverterResult`. Both methods raise `NotImplementedError`, indicating that subclasses must provide their specific implementations.

The code imports the `Any`, `BinaryIO`, and `Optional` types from the `typing` module, and it imports the `StreamInfo` class from the `_stream_info` module. The `DocumentConverterResult` class manipulates string data for the Markdown content and title, while the `DocumentConverter` class interacts with file-like objects that support `seek()`, `tell()`, and `read()` methods. The file also references exceptions such as `FileConversionException` and `MissingDependencyException`, which are raised during the conversion process under specific conditions.

## Functions and Classes

## `DocumentConverterResult`

**Location:** [`packages/markitdown/src/markitdown/_base_converter.py:5`](/packages/markitdown/src/markitdown/_base_converter.py#L5-L41)

# DocumentConverterResult Class Documentation

## Overview
The `DocumentConverterResult` class represents the result of converting a document to Markdown format. It encapsulates the converted Markdown text and an optional title.

## Constructor

### `__init__(self, markdown: str, *, title: Optional[str] = None)`

Initializes a new instance of the `DocumentConverterResult` class.

#### Parameters:
- `markdown` (str): The converted Markdown text. This parameter is required.
- `title` (Optional[str]): An optional title for the document. This parameter defaults to `None`.

## Properties

### `text_content`
- **Type**: str
- **Description**: A soft-deprecated alias for the `markdown` property. It retrieves the Markdown text. New code should use the `markdown` property or the `__str__` method instead.
- **Setter**: Allows setting the Markdown text using this alias. New code should migrate to using the `markdown` property or the `__str__` method.

## Methods

### `__str__(self) -> str`
- **Return Type**: str
- **Description**: Returns the converted Markdown text. This method allows the object to be represented as a string, returning the value of the `markdown` attribute.

## Dependencies
The class does not have any dependencies on external modules, APIs, or services.

## Usage Example
```python
result = DocumentConverterResult(markdown="# Sample Document", title="Sample Title")
print(result)  # Output: # Sample Document
print(result.text_content)  # Output: # Sample Document
result.text_content = "## Updated Document"
print(result.markdown)  # Output: ## Updated Document
```

---
## `DocumentConverter`

**Location:** [`packages/markitdown/src/markitdown/_base_converter.py:42`](/packages/markitdown/src/markitdown/_base_converter.py#L42-L106)

# DocumentConverter Class Documentation

## Overview
The `DocumentConverter` class serves as an abstract superclass for all document converters. It defines two methods: `accepts` and `convert`, which must be implemented by subclasses.

## Method: accepts

### Description
The `accepts` method determines if the converter can handle a specific document based on the provided `file_stream` and `stream_info`. It primarily evaluates the `stream_info` attributes, such as `mimetype`, `extension`, and potentially `url` or `filename`. This method is designed to match the signature of the `convert` method, ensuring compatibility.

### Parameters
- `file_stream` (BinaryIO): A file-like object that must support `seek()`, `tell()`, and `read()` methods. This object represents the document to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including attributes like `mimetype`, `extension`, and `charset`.
- `**kwargs` (Any): Additional keyword arguments that can be passed to the converter.

### Returns
- `bool`: Returns `True` if the converter can handle the document, `False` otherwise.

### Notes
- The method may require reading from `file_stream` to make a final determination. If this occurs, the position of `file_stream` must be reset to its original position before returning.
- If the method returns `True`, it is expected that the `convert` method will also be able to process the document.

## Method: convert

### Description
The `convert` method is responsible for converting a document to Markdown text. This method must be implemented by subclasses.

### Parameters
- `file_stream` (BinaryIO): A file-like object that must support `seek()`, `tell()`, and `read()` methods. This object represents the document to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including attributes like `mimetype`, `extension`, and `charset`.
- `**kwargs` (Any): Additional keyword arguments that can be passed to the converter.

### Returns
- `DocumentConverterResult`: The result of the conversion, which includes the title and markdown content.

### Raises
- `FileConversionException`: Raised if the mimetype is recognized, but the conversion fails for another reason.
- `MissingDependencyException`: Raised if the converter requires a dependency that is not installed.

## Dependencies
The implementation relies on the following external components:
- `BinaryIO`: Type hint indicating that the `file_stream` must be a binary file-like object.
- `StreamInfo`: A class that encapsulates metadata about the file.
- `DocumentConverterResult`: A class representing the result of the conversion.
- `FileConversionException`: An exception raised during conversion failures.
- `MissingDependencyException`: An exception raised when required dependencies are missing.

## Usage Example
```python
class MyDocumentConverter(DocumentConverter):
    def accepts(self, file_stream, stream_info, **kwargs):
        # Implementation of accepts method
        pass

    def convert(self, file_stream, stream_info, **kwargs):
        # Implementation of convert method
        pass

# Example of invoking the methods
converter = MyDocumentConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
