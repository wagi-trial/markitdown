# packages/markitdown/src/markitdown/converters/_html_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_html_converter.py",
  "file_hash": "b59352974cb741b5525d5b150a708b3f9c3cf8f06591ed8c50acd393d678f44d",
  "last_updated": "2026-01-04T17:20:32.251951+00:00",
  "functions": {
    "HtmlConverter": {
      "hash": "8ede1f2ec915ab2f57ee09bf125ccdf7d920de5ff84d9d0c1f6d7877355b010f",
      "lines": "20-91",
      "last_updated": "2026-01-04T17:20:32.251856+00:00"
    }
  }
}
```

</details>



The file `_html_converter.py` implements an `HtmlConverter` class that is responsible for converting HTML content into Markdown format. The class inherits from `DocumentConverter` and provides methods to determine if a given file stream can be accepted for conversion based on its MIME type or file extension. It also includes functionality to parse HTML content, remove unnecessary elements, and return the main content in Markdown format.

The `HtmlConverter` class includes the following methods:
- `accepts`: This method checks if the provided file stream's MIME type or extension matches the accepted types for HTML content. It returns a boolean indicating whether the converter can process the input.
- `convert`: This method takes a file stream and a `StreamInfo` object, parses the HTML using BeautifulSoup, removes `<script>` and `<style>` elements, and converts the remaining content into Markdown using a `_CustomMarkdownify` instance. It returns a `DocumentConverterResult` containing the converted Markdown text and the title of the HTML document.
- `convert_string`: This convenience method allows for the conversion of a string containing HTML directly to Markdown by wrapping the string in a `BytesIO` stream and calling the `convert` method.

The code explicitly imports the `io` module for handling byte streams, the `BeautifulSoup` class from the `bs4` library for parsing HTML, and several components from the parent package, including `DocumentConverter`, `DocumentConverterResult`, and `StreamInfo`. The file defines and manipulates types such as `BinaryIO`, `Any`, and `Optional` from the `typing` module, as well as the `StreamInfo` class for providing metadata about the input stream. The constants `ACCEPTED_MIME_TYPE_PREFIXES` and `ACCEPTED_FILE_EXTENSIONS` are defined as lists to specify valid MIME types and file extensions for HTML content.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `HtmlConverter`

**Nested Functions:**
- `accepts`
- `convert`
- `convert_string`

<details>
<summary><strong>Calls/Dependencies</strong> (18 unique functions)</summary>

- `BeautifulSoup`
- `BytesIO`
- `DocumentConverterResult`
- `HtmlConverter`
- `StreamInfo`
- `_CustomMarkdownify`
- `accepts`
- `convert`
- `convert_soup`
- `convert_string`
- `encode`
- `extract`
- `find`
- `isinstance`
- `lower`
- `soup`
- `startswith`
- `strip`

</details>

</details>



## Functions and Classes

## `HtmlConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_html_converter.py:20`](/packages/markitdown/src/markitdown/converters/_html_converter.py#L20-L91)

**Nested Functions:** `accepts`, `convert`, `convert_string`  
**Dependencies:** `BeautifulSoup`, `BytesIO`, `DocumentConverterResult`, `HtmlConverter`, `StreamInfo`, `_CustomMarkdownify`, `accepts`, `convert`, `convert_soup`, `convert_string`, `encode`, `extract`, `find`, `isinstance`, `lower` *(+3 more)*  


# HtmlConverter Class Documentation

## Overview
The `HtmlConverter` class is a subclass of `DocumentConverter` designed to handle content with the MIME type `text/html`. It provides methods to determine if a file can be accepted for conversion and to convert HTML content into Markdown format.

## Methods

### accepts

```python
def accepts(
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> bool
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the file content to be checked.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `bool`: Returns `True` if the file is accepted based on its MIME type or file extension, otherwise returns `False`.

#### Logic
The method checks if the file extension is in the predefined list `ACCEPTED_FILE_EXTENSIONS`. If not, it checks if the MIME type starts with any prefix in `ACCEPTED_MIME_TYPE_PREFIXES`.

### convert

```python
def convert(
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream containing the HTML content to convert.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted Markdown content.
  - `title` (Optional[str]): The title of the HTML document, or `None` if not available.

#### Logic
The method reads the HTML content from the `file_stream`, removes `<script>` and `<style>` elements, and extracts the main content from the `<body>` tag. If the `<body>` tag is not present, it processes the entire HTML. The content is converted to Markdown using `_CustomMarkdownify`, and leading and trailing whitespace is stripped from the result.

### convert_string

```python
def convert_string(
    html_content: str,
    *,
    url: Optional[str] = None,
    **kwargs
) -> DocumentConverterResult
```

#### Parameters
- `html_content` (str): A string containing HTML content to convert.
- `url` (Optional[str]): An optional URL associated with the HTML content.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `DocumentConverterResult`: An object containing the converted Markdown content and title.

#### Logic
This method converts a string of HTML to Markdown by creating a binary stream from the string and invoking the `convert` method with appropriate `StreamInfo`.

## Dependencies
- `BeautifulSoup`: Used for parsing HTML content.
- `_CustomMarkdownify`: A custom class or function used to convert parsed HTML to Markdown.
- `DocumentConverterResult`: A class used to encapsulate the conversion result.
- `StreamInfo`: A class that contains metadata about the stream.

## Usage Example
```python
html_converter = HtmlConverter()
html_content = "<html><body><h1>Title</h1><p>Content</p></body></html>"
result = html_converter.convert_string(html_content)
print(result.markdown)  # Outputs the Markdown representation of the HTML content
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
