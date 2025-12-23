# packages/markitdown/src/markitdown/converters/_html_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_html_converter.py",
  "file_hash": "b59352974cb741b5525d5b150a708b3f9c3cf8f06591ed8c50acd393d678f44d",
  "last_updated": "2025-12-23T15:50:21.374751+00:00",
  "functions": {
    "HtmlConverter": {
      "hash": "8ede1f2ec915ab2f57ee09bf125ccdf7d920de5ff84d9d0c1f6d7877355b010f",
      "lines": "20-91",
      "last_updated": "2025-12-23T15:50:21.374666+00:00"
    }
  }
}
```

</details>



The Python file `_html_converter.py` implements an `HtmlConverter` class that is responsible for converting HTML content into Markdown format. The class inherits from `DocumentConverter` and provides methods to determine if a given file stream is acceptable for conversion based on its MIME type or file extension, as well as the actual conversion process itself. The conversion process involves parsing the HTML content using BeautifulSoup, removing script and style elements, and extracting the main content from the body of the HTML document.

The main functions and methods defined in this file include:
- `accepts`: This method checks if the provided file stream and associated stream information match accepted MIME types or file extensions for HTML content.
- `convert`: This method performs the conversion of an HTML file stream into Markdown format. It handles the parsing of the HTML, removal of non-content elements, and uses a custom markdownify function to convert the content into Markdown.
- `convert_string`: This convenience method allows for the conversion of an HTML string directly to Markdown by wrapping the `convert` method.

The file imports several modules, including `io` for handling byte streams, `Any`, `BinaryIO`, and `Optional` from the `typing` module for type hinting, and `BeautifulSoup` from the `bs4` library for HTML parsing. It also imports `DocumentConverter` and `DocumentConverterResult` from a base converter module, as well as `StreamInfo` and `_CustomMarkdownify` from other modules within the same package. The data structures manipulated in this file include `BinaryIO` for file streams, `StreamInfo` for metadata about the file being processed, and `DocumentConverterResult` for encapsulating the output of the conversion process. The code explicitly defines accepted MIME types and file extensions for HTML content as lists.

## Functions and Classes

## `HtmlConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_html_converter.py:20`](/packages/markitdown/src/markitdown/converters/_html_converter.py#L20-L91)

# HtmlConverter Documentation

## Overview
`HtmlConverter` is a class that extends `DocumentConverter` and is designed to handle content with the MIME type `text/html`. It provides functionality to accept HTML file streams, convert them to markdown format, and extract relevant content while removing unnecessary elements like JavaScript and CSS.

## Methods

### accepts

#### Definition
```python
def accepts(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> bool
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the file content. This parameter is not directly used in the method logic.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
  - `mimetype` (str): The MIME type of the content. This is checked against accepted MIME type prefixes.
  - `extension` (str): The file extension. This is checked against accepted file extensions.
- `**kwargs` (Any): Additional options that can be passed to the converter. These are not utilized in this method.

#### Returns
- `bool`: Returns `True` if the file stream is accepted based on its MIME type or file extension; otherwise, returns `False`.

### convert

#### Definition
```python
def convert(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the HTML content to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream.
  - `mimetype` (str): The MIME type of the content, expected to be `text/html`.
  - `extension` (str): The file extension, expected to be `.html`.
  - `charset` (str): The character set for decoding the stream. If not provided, defaults to `utf-8`.
- `**kwargs` (Any): Additional options that can be passed to the converter, specifically to `_CustomMarkdownify`.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted markdown text extracted from the HTML content.
  - `title` (Optional[str]): The title of the HTML document, extracted from the `<title>` tag, or `None` if not present.

### convert_string

#### Definition
```python
def convert_string(
    self, html_content: str, *, url: Optional[str] = None, **kwargs
) -> DocumentConverterResult
```

#### Parameters
- `html_content` (str): A string containing HTML content to be converted to markdown.
- `url` (Optional[str]): An optional URL associated with the HTML content. This is passed to the `StreamInfo` object.
- `**kwargs` (Any): Additional options that can be passed to the converter, specifically to `_CustomMarkdownify`.

#### Returns
- `DocumentConverterResult`: The result of converting the provided HTML string to markdown, similar to the `convert` method.

## Dependencies
- `BeautifulSoup`: Used for parsing HTML content.
- `_CustomMarkdownify`: A custom class or function used for converting parsed HTML elements to markdown.
- `DocumentConverterResult`: A class that encapsulates the result of the conversion, including markdown text and title.
- `StreamInfo`: A class that holds metadata about the stream, including MIME type, extension, and charset.

## Usage Example
```python
html_converter = HtmlConverter()
html_content = "<html><body><h1>Hello World</h1><script>alert('test');</script></body></html>"
result = html_converter.convert_string(html_content)
print(result.markdown)  # Outputs: "# Hello World"
print(result.title)     # Outputs: None
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
