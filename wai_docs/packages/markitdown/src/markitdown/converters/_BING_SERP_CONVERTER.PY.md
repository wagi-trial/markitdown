# packages/markitdown/src/markitdown/converters/_bing_serp_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_bing_serp_converter.py",
  "file_hash": "09c51026d231c3a38a8baf2c9a7947715329fc3359defb38b16d01e93b7784a1",
  "last_updated": "2026-01-04T17:19:15.619336+00:00",
  "functions": {
    "BingSerpConverter": {
      "hash": "ddc0ffd8dde79beef3d6d0c85b80867544838774bcb35bf726a51304bd1b9b28",
      "lines": "23-121",
      "last_updated": "2026-01-04T17:19:15.619279+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_bing_serp_converter.py` implements a class named `BingSerpConverter`, which is designed to handle the conversion of Bing search engine results pages (SERPs) into Markdown format. The class extends the `DocumentConverter` base class and includes two primary methods: `accepts` and `convert`. The `accepts` method verifies if the input stream corresponds to a Bing SERP by checking the URL, MIME type, and file extension. The `convert` method processes the HTML content of the Bing SERP, extracts search results, and converts them into a structured Markdown format.

The `BingSerpConverter` class relies on several imported modules, including `re`, `base64`, `binascii`, `urlparse` from `urllib.parse`, `Any`, `BinaryIO` from `typing`, and `BeautifulSoup` from `bs4`. It also imports `DocumentConverter` and `DocumentConverterResult` from its parent module, as well as `StreamInfo` and `_CustomMarkdownify` from sibling modules. The class manipulates data structures such as `BinaryIO` for file streams and `StreamInfo` for metadata about the input stream. The output of the conversion process is encapsulated in a `DocumentConverterResult` object, which contains the generated Markdown text and an optional title extracted from the HTML content. 

The implementation also defines constants for accepted MIME type prefixes and file extensions, which are used in the `accepts` method to determine the validity of the input stream. The `convert` method utilizes BeautifulSoup to parse the HTML content, clean up specific elements, and extract relevant search result data, which is then formatted into Markdown.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `BingSerpConverter`

**Nested Functions:**
- `accepts`
- `convert`

<details>
<summary><strong>Calls/Dependencies</strong> (25 unique functions)</summary>

- `BeautifulSoup`
- `BingSerpConverter`
- `DocumentConverterResult`
- `_CustomMarkdownify`
- `accepts`
- `append`
- `b64decode`
- `convert`
- `convert_soup`
- `decode`
- `extract`
- `find_all`
- `get`
- `hasattr`
- `join`
- `len`
- `list`
- `lower`
- `pages`
- `parse_qs`
- `search`
- `split`
- `startswith`
- `strip`
- `urlparse`

</details>

</details>



## Functions and Classes

## `BingSerpConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_bing_serp_converter.py:23`](/packages/markitdown/src/markitdown/converters/_bing_serp_converter.py#L23-L121)

**Nested Functions:** `accepts`, `convert`  
**Dependencies:** `BeautifulSoup`, `BingSerpConverter`, `DocumentConverterResult`, `_CustomMarkdownify`, `accepts`, `append`, `b64decode`, `convert`, `convert_soup`, `decode`, `extract`, `find_all`, `get`, `hasattr`, `join` *(+10 more)*  


# BingSerpConverter Documentation

## Overview
`BingSerpConverter` is a subclass of `DocumentConverter` designed to handle Bing search engine results pages (SERPs), specifically focusing on organic search results. The class provides methods to determine if a given file stream contains valid Bing SERP content and to convert that content into a markdown format.

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

#### Parameters
- `file_stream` (BinaryIO): A binary stream representing the content to be evaluated.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL associated with the content.
  - `mimetype` (str): The MIME type of the content.
  - `extension` (str): The file extension of the content.
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `bool`: Returns `True` if the content is from a valid Bing SERP URL and is of an accepted file type or MIME type; otherwise, returns `False`.

### convert

```python
def convert(
    self,
    file_stream: BinaryIO,
    stream_info: StreamInfo,
    **kwargs: Any,
) -> DocumentConverterResult
```

#### Parameters
- `file_stream` (BinaryIO): A binary stream containing the HTML content of the Bing SERP.
- `stream_info` (StreamInfo): An object containing metadata about the stream, including:
  - `url` (str): The URL associated with the content.
  - `charset` (str): The character set of the content (optional).
- `**kwargs` (Any): Additional options that can be passed to the converter.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): A markdown representation of the parsed search results.
  - `title` (str or None): The title of the page, or `None` if no title is found.

## Dependencies
- `re`: Used for regular expression operations.
- `base64`: Used for decoding base64 encoded URLs.
- `binascii`: Used for handling binary data.
- `urlparse` and `parse_qs`: Functions from the `urllib.parse` module, used for parsing URLs and query strings.
- `BeautifulSoup`: A library for parsing HTML and XML documents.
- `_CustomMarkdownify`: A custom markdown conversion class that is instantiated within the `convert` method.

## Usage Example
```python
converter = BingSerpConverter()
file_stream = open('bing_results.html', 'rb')  # Example HTML file containing Bing SERP
stream_info = StreamInfo(url='https://www.bing.com/search?q=example', mimetype='text/html', extension='html')

if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
