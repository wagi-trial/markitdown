# packages/markitdown/tests/test_docintel_html.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_docintel_html.py",
  "file_hash": "92ba03e288cbbf5099138357503160b8a2e4137d91f0d1acde0276a9444e6bf7",
  "last_updated": "2025-12-23T15:54:38.013518+00:00",
  "functions": {
    "_make_converter": {
      "hash": "7e3828bcd4902a292d5935bc36818b005ab7c12b9a8b28d9c067ab62ad127954",
      "lines": "9-14",
      "last_updated": "2025-12-23T15:54:32.463474+00:00"
    },
    "test_docintel_accepts_html_extension": {
      "hash": "966fd681dc20290637ab8f17645023cc7cdabf3c3dc5c65a47ddba28a45a255d",
      "lines": "15-20",
      "last_updated": "2025-12-23T15:54:35.105644+00:00"
    },
    "test_docintel_accepts_html_mimetype": {
      "hash": "2a8a4c4cf2a7a1d4fc2d28903a3c6da341876c18d38cbe71a274e965f7a49ee1",
      "lines": "21-27",
      "last_updated": "2025-12-23T15:54:38.013420+00:00"
    }
  }
}
```

</details>



The Python file `test_docintel_html.py` implements unit tests for the `DocumentIntelligenceConverter` class from the `markitdown` package, specifically focusing on its ability to accept HTML file types based on file extensions and MIME types. The file contains functions that create a converter instance and validate its behavior with respect to HTML content.

The main functions defined in this file are `_make_converter`, `test_docintel_accepts_html_extension`, and `test_docintel_accepts_html_mimetype`. The `_make_converter` function initializes a `DocumentIntelligenceConverter` instance and sets its `_file_types` attribute to the provided list of file types. The `test_docintel_accepts_html_extension` function tests whether the converter accepts a stream with an HTML file extension, while the `test_docintel_accepts_html_mimetype` function tests acceptance based on different HTML-related MIME types, specifically `text/html` and `application/xhtml+xml`.

The code explicitly imports the `DocumentIntelligenceConverter` and `DocumentIntelligenceFileType` from the `markitdown.converters._doc_intel_converter` module, as well as `StreamInfo` from `markitdown._stream_info`. The `StreamInfo` class is utilized to create instances that encapsulate the MIME type and file extension for testing. The data structures manipulated in this file include instances of `StreamInfo` and the `_file_types` attribute of the `DocumentIntelligenceConverter`, which is expected to contain file type constants such as `DocumentIntelligenceFileType.HTML`.

## Functions and Classes

## `_make_converter`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:9`](/packages/markitdown/tests/test_docintel_html.py#L9-L14)

# Documentation for `_make_converter`

## Function Overview
The `_make_converter` function creates an instance of the `DocumentIntelligenceConverter` class and assigns a list of file types to its `_file_types` attribute. The function then returns this instance.

## Parameters

### `file_types`
- **Type**: Any
- **Constraints**: The function does not enforce any specific type or structure on `file_types`. It can be any object, but it is expected to be a collection of file types (e.g., a list or tuple).
- **Usage**: This parameter is assigned to the `_file_types` attribute of the `DocumentIntelligenceConverter` instance.

## Return Value
- **Type**: `DocumentIntelligenceConverter`
- **Content**: The function returns an instance of `DocumentIntelligenceConverter` with the `_file_types` attribute set to the value of the `file_types` parameter.

## Dependencies
- The function explicitly calls the `DocumentIntelligenceConverter` class, which must be defined in the same module or imported from another module for this function to work.

## Usage Example
```python
file_types = ['pdf', 'docx', 'txt']
converter = _make_converter(file_types)
``` 

In this example, the `_make_converter` function is called with a list of file types, and the returned `converter` is an instance of `DocumentIntelligenceConverter` with its `_file_types` attribute set to `['pdf', 'docx', 'txt']`.

---
## `test_docintel_accepts_html_extension`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:15`](/packages/markitdown/tests/test_docintel_html.py#L15-L20)

# Function Documentation: test_docintel_accepts_html_extension

## Description
The function `test_docintel_accepts_html_extension` tests whether a converter accepts a document with the HTML file extension. It creates a converter instance configured for HTML file types and checks if it can accept an empty byte stream with a specified stream information that includes an HTML extension.

## Parameters
The function does not take any parameters.

## Return Value
The function does not return a value. It performs an assertion to verify that the converter accepts the specified input. If the assertion fails, an `AssertionError` will be raised.

## Dependencies
The function relies on the following external components:
- `_make_converter`: A function that creates a converter instance configured for specific document types.
- `DocumentIntelligenceFileType`: An enumeration or class that defines supported document file types, specifically including `HTML`.
- `StreamInfo`: A class or data structure that holds information about the stream, including its MIME type and file extension.
- `io`: The standard Python I/O module, specifically used here to create a `BytesIO` object.

## Usage Example
To invoke the function, simply call it without any arguments:

```python
test_docintel_accepts_html_extension()
``` 

This will execute the test, and if the assertion is true, it will complete without error. If the assertion is false, it will raise an `AssertionError`.

---
## `test_docintel_accepts_html_mimetype`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:21`](/packages/markitdown/tests/test_docintel_html.py#L21-L27)

# Function Documentation: test_docintel_accepts_html_mimetype

## Description
The `test_docintel_accepts_html_mimetype` function tests whether a converter object accepts specific HTML MIME types. It creates a converter instance configured to handle HTML file types and verifies its acceptance of two different MIME types: "text/html" and "application/xhtml+xml". The function uses assertions to confirm that the converter correctly identifies these MIME types as acceptable.

## Parameters
The function does not take any parameters.

## Return Value
The function does not return a value. It performs assertions to validate the behavior of the converter.

## Dependencies
The function relies on the following external components:
- `_make_converter`: A function that creates a converter instance configured for specified document types.
- `DocumentIntelligenceFileType`: An enumeration or class that defines supported document file types, specifically including `HTML`.
- `StreamInfo`: A class or data structure that encapsulates information about a stream, including its MIME type and file extension.
- `io`: The standard Python I/O module, specifically used here for creating a `BytesIO` stream.

## Usage Example
```python
test_docintel_accepts_html_mimetype()
```
This example demonstrates how to invoke the function directly. It does not require any arguments and will execute the internal assertions to validate the acceptance of the specified HTML MIME types.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
