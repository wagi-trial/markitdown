# packages/markitdown/tests/test_docintel_html.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/tests/test_docintel_html.py",
  "file_hash": "92ba03e288cbbf5099138357503160b8a2e4137d91f0d1acde0276a9444e6bf7",
  "last_updated": "2026-01-04T17:24:15.579436+00:00",
  "functions": {
    "_make_converter": {
      "hash": "7e3828bcd4902a292d5935bc36818b005ab7c12b9a8b28d9c067ab62ad127954",
      "lines": "9-14",
      "last_updated": "2026-01-04T17:24:10.253619+00:00"
    },
    "test_docintel_accepts_html_extension": {
      "hash": "966fd681dc20290637ab8f17645023cc7cdabf3c3dc5c65a47ddba28a45a255d",
      "lines": "15-20",
      "last_updated": "2026-01-04T17:24:12.638237+00:00"
    },
    "test_docintel_accepts_html_mimetype": {
      "hash": "2a8a4c4cf2a7a1d4fc2d28903a3c6da341876c18d38cbe71a274e965f7a49ee1",
      "lines": "21-27",
      "last_updated": "2026-01-04T17:24:15.579151+00:00"
    }
  }
}
```

</details>



The Python file `test_docintel_html.py` implements unit tests for the `DocumentIntelligenceConverter` class from the `markitdown` package, specifically focusing on its ability to accept HTML file types. The file contains three functions: `_make_converter`, `test_docintel_accepts_html_extension`, and `test_docintel_accepts_html_mimetype`. 

The `_make_converter` function creates an instance of `DocumentIntelligenceConverter` and sets its `_file_types` attribute to the provided list of file types. The `test_docintel_accepts_html_extension` function tests whether the converter accepts a stream with a `.html` extension by creating a `StreamInfo` object with the HTML extension and asserting that the converter accepts it. The `test_docintel_accepts_html_mimetype` function tests the converter's acceptance of streams with specific MIME types associated with HTML, namely `text/html` and `application/xhtml+xml`, using `StreamInfo` objects without an extension.

The code explicitly imports the `DocumentIntelligenceConverter` and `DocumentIntelligenceFileType` from the `markitdown.converters._doc_intel_converter` module, as well as `StreamInfo` from `markitdown._stream_info`. The file manipulates instances of the `StreamInfo` class, which encapsulates information about the MIME type and file extension of the data being processed. The tests utilize the `io.BytesIO` class to create in-memory byte streams for testing the converter's acceptance criteria.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `_make_converter`

<details>
<summary><strong>Calls/Dependencies</strong> (2 unique functions)</summary>

- `__new__`
- `_make_converter`

</details>

### `test_docintel_accepts_html_extension`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `BytesIO`
- `StreamInfo`
- `_make_converter`
- `accepts`
- `test_docintel_accepts_html_extension`

</details>

### `test_docintel_accepts_html_mimetype`

<details>
<summary><strong>Calls/Dependencies</strong> (5 unique functions)</summary>

- `BytesIO`
- `StreamInfo`
- `_make_converter`
- `accepts`
- `test_docintel_accepts_html_mimetype`

</details>

</details>



## Functions and Classes

## `_make_converter`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:9`](/packages/markitdown/tests/test_docintel_html.py#L9-L14)

**Dependencies:** `__new__`, `_make_converter`  


# Documentation for `_make_converter` Function

## Function Overview
The `_make_converter` function creates an instance of the `DocumentIntelligenceConverter` class and assigns a specified set of file types to it. The function does not call the constructor of the class but instead uses the `__new__` method to create a new instance.

## Parameters

### `file_types`
- **Type**: Any
- **Constraints**: None specified in the code.
- **Usage**: This parameter is assigned to the `_file_types` attribute of the newly created `DocumentIntelligenceConverter` instance.

## Return Value
- **Type**: `DocumentIntelligenceConverter`
- **Content**: The function returns an instance of `DocumentIntelligenceConverter` with the `_file_types` attribute set to the value of the `file_types` parameter.

## Dependencies
- The function explicitly depends on the `DocumentIntelligenceConverter` class, which must be defined in the same module or imported from another module.

## Usage Example
```python
file_types = ['pdf', 'docx', 'txt']
converter_instance = _make_converter(file_types)
```

---
## `test_docintel_accepts_html_extension`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:15`](/packages/markitdown/tests/test_docintel_html.py#L15-L20)

**Dependencies:** `BytesIO`, `StreamInfo`, `_make_converter`, `accepts`, `test_docintel_accepts_html_extension`  


# Function Documentation: test_docintel_accepts_html_extension

## Description
The function `test_docintel_accepts_html_extension` tests whether a converter accepts a document of the HTML file type. It creates a converter instance configured to handle HTML files and checks if it can accept an empty byte stream with a specified stream information that includes an HTML extension.

## Parameters
The function does not take any parameters.

## Return Value
The function does not return a value. It performs an assertion to verify that the converter accepts the specified input.

## Dependencies
The function relies on the following external components:
- `_make_converter`: A function that creates a converter instance configured to handle specific document types.
- `DocumentIntelligenceFileType`: An enumeration or class that defines file types, specifically the `HTML` type.
- `StreamInfo`: A class or structure that holds information about the stream, including `mimetype` and `extension`.
- `io`: The standard library module used to create an in-memory byte stream.

## Usage Example
To invoke the function, simply call it without any arguments:

```python
test_docintel_accepts_html_extension()
``` 

This will execute the test, and if the assertion fails, an AssertionError will be raised.

---
## `test_docintel_accepts_html_mimetype`

**Location:** [`packages/markitdown/tests/test_docintel_html.py:21`](/packages/markitdown/tests/test_docintel_html.py#L21-L27)

**Dependencies:** `BytesIO`, `StreamInfo`, `_make_converter`, `accepts`, `test_docintel_accepts_html_mimetype`  


# Function Documentation: test_docintel_accepts_html_mimetype

## Description
The function `test_docintel_accepts_html_mimetype` tests the ability of a converter to accept HTML MIME types. It creates a converter instance configured to handle HTML document types and verifies that the converter accepts two specific MIME types: `text/html` and `application/xhtml+xml`. The function uses assertions to confirm that the converter correctly identifies these MIME types as acceptable.

## Parameters
The function does not take any parameters.

## Return Value
The function does not return a value. It uses assertions to validate the behavior of the converter. If the assertions fail, an `AssertionError` will be raised.

## Dependencies
The function relies on the following external components:
- `_make_converter`: A function that creates a converter instance configured to handle specified document types.
- `DocumentIntelligenceFileType`: An enumeration or class that defines various document file types, specifically including `HTML`.
- `StreamInfo`: A class or data structure that encapsulates information about a stream, including its MIME type and extension.
- `io.BytesIO`: A class from the `io` module that provides a buffer for reading and writing bytes.

## Usage Example
To invoke the function, simply call it without any arguments:

```python
test_docintel_accepts_html_mimetype()
``` 

This will execute the tests defined within the function. If both assertions pass, the function will complete without error. If either assertion fails, an `AssertionError` will be raised, indicating that the converter did not accept the specified MIME type as expected.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
