# packages/markitdown/src/markitdown/converters/_bing_serp_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_bing_serp_converter.py",
  "file_hash": "09c51026d231c3a38a8baf2c9a7947715329fc3359defb38b16d01e93b7784a1",
  "last_updated": "2025-12-23T15:48:52.752896+00:00",
  "functions": {
    "BingSerpConverter": {
      "hash": "ddc0ffd8dde79beef3d6d0c85b80867544838774bcb35bf726a51304bd1b9b28",
      "lines": "23-121",
      "last_updated": "2025-12-23T15:48:52.752807+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_bing_serp_converter.py` implements a class named `BingSerpConverter`, which is responsible for converting Bing search engine results pages (SERPs) into Markdown format. The converter specifically handles organic search results from Bing, ensuring that the input is valid HTML content from a Bing search URL. The class includes methods to accept and convert the content based on specific criteria.

The main functions within the `BingSerpConverter` class include `accepts` and `convert`. The `accepts` method checks if the provided file stream is from a Bing search results page by validating the URL, MIME type, and file extension. The `convert` method processes the HTML content, extracting search query parameters, cleaning up the HTML structure using BeautifulSoup, and converting the results into Markdown format. The conversion process includes rewriting redirect URLs that are base64 encoded and formatting the output to present the search results clearly.

The file imports several modules, including `re`, `base64`, `binascii`, `urlparse` from `urllib.parse`, and `BeautifulSoup` from `bs4`. It also imports `DocumentConverter` and `DocumentConverterResult` from a base converter module, as well as `StreamInfo` and `_CustomMarkdownify` from other parts of the package. The data structures manipulated in this file include `BinaryIO` for file streams, `StreamInfo` for metadata about the input stream, and the resulting Markdown text encapsulated in a `DocumentConverterResult` object. The code specifically defines accepted MIME types and file extensions for validating input content.

## Functions and Classes

## `BingSerpConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_bing_serp_converter.py:23`](/packages/markitdown/src/markitdown/converters/_bing_serp_converter.py#L23-L121)

# BingSerpConverter Documentation

## Overview
`BingSerpConverter` is a class that extends `DocumentConverter` and is designed to handle Bing search engine results pages (SERPs), specifically focusing on organic search results. The class provides functionality to determine if a given HTML content is from Bing and to convert that content into a markdown format.

## Method: accepts

### Description
The `accepts` method checks if the provided file stream and stream information correspond to HTML content from Bing.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the file content to be checked.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL of the content being processed.
  - `mimetype` (str): The MIME type of the content.
  - `extension` (str): The file extension of the content.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `bool`: Returns `True` if the content is from a Bing SERP and is of an accepted MIME type or file extension; otherwise, returns `False`.

## Method: convert

### Description
The `convert` method processes the provided file stream and converts the Bing SERP HTML content into a markdown format.

### Parameters
- `file_stream` (BinaryIO): A binary stream of the HTML content to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the stream, which must include:
  - `url` (str): The URL of the content being processed. This parameter is required and must not be `None`.
- `**kwargs` (Any): Additional options to pass to the converter.

### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): A string formatted in markdown that represents the search results.
  - `title` (str or None): The title of the page if available; otherwise, `None`.

## External Dependencies
- `re`: Used for regular expression operations.
- `base64`: Used for decoding base64 encoded URLs.
- `binascii`: Used for handling binary data.
- `urllib.parse`: Used for parsing URLs and query strings.
- `bs4 (BeautifulSoup)`: Used for parsing and manipulating HTML content.
- `_CustomMarkdownify`: A custom class presumably defined elsewhere, used for converting HTML to markdown.

## Usage Example
```python
converter = BingSerpConverter()
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
