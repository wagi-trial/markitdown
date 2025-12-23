# packages/markitdown/src/markitdown/converters/_wikipedia_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_wikipedia_converter.py",
  "file_hash": "9ea1b94f6304d1aed4b677b35338f932f9e29b4d712b138062c3227746209b38",
  "last_updated": "2025-12-23T15:52:33.726845+00:00",
  "functions": {
    "WikipediaConverter": {
      "hash": "e02ecadadacca422e20b83900bee6fe6de1d99f72f293cee25c6cbc5d9faa200",
      "lines": "20-88",
      "last_updated": "2025-12-23T15:52:33.726774+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_wikipedia_converter.py` implements a class named `WikipediaConverter`, which is a specific type of `DocumentConverter`. This class is designed to handle the conversion of Wikipedia page content from HTML to Markdown format. The main operations include checking if a given file stream is from a Wikipedia page and converting the main content of that page into Markdown while excluding unnecessary elements such as JavaScript and CSS.

The `WikipediaConverter` class contains two primary methods: `accepts` and `convert`. The `accepts` method verifies if the provided file stream is from a Wikipedia URL and checks the MIME type and file extension to ensure they are acceptable for processing. The `convert` method parses the HTML content using BeautifulSoup, extracts the main content from the Wikipedia page, and converts it into Markdown format using the `_CustomMarkdownify` class. The method returns a `DocumentConverterResult` containing the converted Markdown text and the title of the page.

The file imports several modules, including `re` for regular expression operations, `bs4` for HTML parsing, and typing constructs such as `Any` and `BinaryIO`. It also imports `DocumentConverter` and `DocumentConverterResult` from a base converter module, as well as `StreamInfo` for handling stream metadata. The data structures manipulated in this file include strings for URLs and titles, and BeautifulSoup objects for HTML content, specifically targeting elements like `div` and `span` tags to extract relevant information. The file defines constants for accepted MIME types and file extensions, which are used in the `accepts` method to validate input.

## Functions and Classes

## `WikipediaConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_wikipedia_converter.py:20`](/packages/markitdown/src/markitdown/converters/_wikipedia_converter.py#L20-L88)

# WikipediaConverter Documentation

## Overview
The `WikipediaConverter` class is a subclass of `DocumentConverter` that processes HTML content specifically from Wikipedia pages. It focuses on extracting the main document content while removing unnecessary elements such as scripts and styles.

## Method: accepts

### Description
The `accepts` method determines whether the provided file stream and stream information are suitable for conversion by checking if the URL belongs to Wikipedia and if the content type is acceptable.

### Parameters
- `file_stream` (BinaryIO): A binary stream representing the content to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the content.
  - `mimetype` (str): The MIME type of the content.
  - `extension` (str): The file extension of the content.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `bool`: Returns `True` if the URL is a Wikipedia URL and the MIME type or file extension is acceptable; otherwise, returns `False`.

## Method: convert

### Description
The `convert` method processes the provided file stream and converts the main content of a Wikipedia page into Markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream containing the HTML content to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `charset` (str): The character set of the content, defaults to "utf-8" if not provided.
- `**kwargs` (Any): Additional options that can be passed to the converter.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted Markdown content of the main document.
  - `title` (str or None): The title of the Wikipedia page, or `None` if the title is not available.

## Dependencies
- `bs4`: The Beautiful Soup library is used for parsing HTML content.
- `_CustomMarkdownify`: A custom class or function used to convert Beautiful Soup objects to Markdown format.
- `DocumentConverter`: The base class from which `WikipediaConverter` inherits.
- `DocumentConverterResult`: The class used to encapsulate the result of the conversion.

## Usage Example
```python
converter = WikipediaConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
    print(result.title)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
