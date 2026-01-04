# packages/markitdown/src/markitdown/converters/_wikipedia_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_wikipedia_converter.py",
  "file_hash": "9ea1b94f6304d1aed4b677b35338f932f9e29b4d712b138062c3227746209b38",
  "last_updated": "2026-01-04T17:22:36.480257+00:00",
  "functions": {
    "WikipediaConverter": {
      "hash": "e02ecadadacca422e20b83900bee6fe6de1d99f72f293cee25c6cbc5d9faa200",
      "lines": "20-88",
      "last_updated": "2026-01-04T17:22:36.480201+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_wikipedia_converter.py` implements a `WikipediaConverter` class that is responsible for converting Wikipedia HTML content into Markdown format. The class extends the `DocumentConverter` base class and provides specific methods to determine if the content is acceptable for conversion and to perform the conversion itself.

The `WikipediaConverter` class includes two primary methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream is from a Wikipedia URL and verifies that the MIME type or file extension is appropriate for HTML content. The `convert` method processes the HTML content by parsing it with BeautifulSoup, removing script and style elements, and extracting the main content and title. It then converts the main content into Markdown format using the `_CustomMarkdownify` class and returns a `DocumentConverterResult` containing the converted Markdown text and the title.

The code imports several modules, including `re` for regular expressions, `bs4` for HTML parsing, and types from the `typing` module such as `Any` and `BinaryIO`. It also imports `DocumentConverter` and `DocumentConverterResult` from a base converter module, `StreamInfo` for handling stream metadata, and `_CustomMarkdownify` for converting HTML to Markdown. The file manipulates data structures such as `StreamInfo` for metadata and uses `DocumentConverterResult` to encapsulate the conversion output. The file defines constants for accepted MIME type prefixes and file extensions to validate input content.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `WikipediaConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (14 unique functions)</summary>

- `BeautifulSoup`
- `DocumentConverterResult`
- `WikipediaConverter`
- `_CustomMarkdownify`
- `accepts`
- `convert`
- `convert_soup`
- `extract`
- `find`
- `isinstance`
- `lower`
- `search`
- `soup`
- `startswith`

</details>

</details>



## Functions and Classes

## `WikipediaConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_wikipedia_converter.py:20`](/packages/markitdown/src/markitdown/converters/_wikipedia_converter.py#L20-L88)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `BeautifulSoup`, `DocumentConverterResult`, `WikipediaConverter`, `_CustomMarkdownify`, `accepts`, `convert`, `convert_soup`, `extract`, `find`, `isinstance`, `lower`, `search`, `soup`, `startswith`  


# WikipediaConverter Documentation

## Overview
`WikipediaConverter` is a class that extends `DocumentConverter` to handle the conversion of Wikipedia pages, focusing specifically on the main document content. It verifies that the input is from a valid Wikipedia URL and processes the HTML content to extract and convert it into a markdown format.

## Method: `accepts`

### Description
The `accepts` method determines if the provided file stream and stream information correspond to a valid Wikipedia HTML document.

### Parameters
- `file_stream` (BinaryIO): The input stream containing the HTML content.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the document.
  - `mimetype` (str): The MIME type of the document.
  - `extension` (str): The file extension of the document.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `bool`: Returns `True` if the URL is a valid Wikipedia URL and the MIME type or file extension is accepted; otherwise, returns `False`.

## Method: `convert`

### Description
The `convert` method processes the provided file stream, extracts the main content from the Wikipedia page, and converts it into markdown format.

### Parameters
- `file_stream` (BinaryIO): The input stream containing the HTML content.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `charset` (str, optional): The character set of the document.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted markdown content of the main document.
  - `title` (str, optional): The title of the Wikipedia page, or `None` if not available.

## Dependencies
- `bs4`: The Beautiful Soup library is used for parsing HTML content.
- `_CustomMarkdownify`: A custom class or function used to convert HTML to markdown format.
- `DocumentConverterResult`: A class that encapsulates the result of the conversion process.

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
