# packages/markitdown/src/markitdown/converters/_rss_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_rss_converter.py",
  "file_hash": "00bf56c318de8dd5a39de90b845ac6771a0348a7efebe39dd8c2e5736ac45c8d",
  "last_updated": "2026-01-04T17:22:18.577956+00:00",
  "functions": {
    "RssConverter": {
      "hash": "60f98ccc3689deeabe0a65f9f0f57be2df84e5081b5f6ef535815470bc445405",
      "lines": "29-193",
      "last_updated": "2026-01-04T17:22:18.577896+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_rss_converter.py` implements the `RssConverter` class, which is responsible for converting RSS and Atom feeds into Markdown format. The class extends `DocumentConverter` and provides methods to determine if a given file stream is acceptable for conversion, parse the content of RSS or Atom feeds, and format the parsed data into Markdown. The conversion process involves checking the MIME type and file extension of the input stream, parsing the XML structure, and extracting relevant data such as titles, descriptions, and publication dates.

The `RssConverter` class includes several key methods: 
- `__init__`: Initializes the converter and sets up any necessary parameters.
- `accepts`: Determines if the converter can handle the provided file stream based on its MIME type and extension.
- `_check_xml`: Validates if the input stream contains well-formed XML.
- `_feed_type`: Identifies whether the XML document is an RSS or Atom feed.
- `convert`: Main method that processes the input stream and returns the converted Markdown.
- `_parse_atom_type` and `_parse_rss_type`: Handle the specific parsing logic for Atom and RSS feeds, respectively.
- `_parse_content`: Converts HTML content within feed items to Markdown using BeautifulSoup.
- `_get_data_by_tag_name`: Retrieves data from XML elements based on tag names.

The code explicitly imports several modules: `minidom` from `defusedxml` for XML parsing, `BeautifulSoup` from `bs4` for HTML content processing, and various types from `typing` for type hints. The file also defines constants for precise and candidate MIME types and file extensions used to identify acceptable input formats. The data structures manipulated include XML documents represented as `Document` objects, and the results of the conversion are returned as instances of `DocumentConverterResult`, which encapsulates the Markdown output and associated titles.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `RssConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `_check_xml`
- `_feed_type`
- `convert`
- `_parse_atom_type`
- `_parse_rss_type`
- `_parse_content`
- `_get_data_by_tag_name`

<details>
<summary><strong>Calls/Dependencies</strong> (23 unique functions)</summary>

- `BeautifulSoup`
- `DocumentConverterResult`
- `RssConverter`
- `ValueError`
- `_CustomMarkdownify`
- `__init__`
- `_check_xml`
- `_feed_type`
- `_get_data_by_tag_name`
- `_parse_atom_type`
- `_parse_content`
- `_parse_rss_type`
- `accepts`
- `convert`
- `convert_soup`
- `getElementsByTagName`
- `hasattr`
- `lower`
- `parse`
- `seek`
- `startswith`
- `super`
- `tell`

</details>

</details>



## Functions and Classes

## `RssConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_rss_converter.py:29`](/packages/markitdown/src/markitdown/converters/_rss_converter.py#L29-L193)

**Nested Functions:** `__init__`, `accepts`, `_check_xml`, `_feed_type`, `convert`, `_parse_atom_type`, `_parse_rss_type`, `_parse_content`, `_get_data_by_tag_name`  
**Dependencies:** `BeautifulSoup`, `DocumentConverterResult`, `RssConverter`, `ValueError`, `_CustomMarkdownify`, `__init__`, `_check_xml`, `_feed_type`, `_get_data_by_tag_name`, `_parse_atom_type`, `_parse_content`, `_parse_rss_type`, `accepts`, `convert`, `convert_soup` *(+8 more)*  


# RssConverter Documentation

## Overview
`RssConverter` is a class that extends `DocumentConverter` to convert RSS and Atom feeds into Markdown format. It determines the type of feed (RSS or Atom) and parses the content accordingly.

## Parameters

### `__init__(self)`
- **Description**: Initializes a new instance of `RssConverter`.
- **Usage**: Calls the superclass constructor and initializes an empty dictionary for `_kwargs`.

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the file to be checked.
  - `stream_info` (StreamInfo): An object containing metadata about the stream, including `mimetype` and `extension`.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns**: `bool` - Returns `True` if the file stream is accepted based on its MIME type or file extension; otherwise, returns `False`.

### `_check_xml(self, file_stream: BinaryIO) -> bool`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the file to be checked for XML content.
- **Returns**: `bool` - Returns `True` if the file stream contains valid XML that can be parsed; otherwise, returns `False`.

### `_feed_type(self, doc: Any) -> str | None`
- **Parameters**:
  - `doc` (Any): A parsed XML document.
- **Returns**: `str | None` - Returns "rss" if the document is an RSS feed, "atom" if it is an Atom feed, or `None` if neither.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **Parameters**:
  - `file_stream` (BinaryIO): A binary stream representing the file to be converted.
  - `stream_info` (StreamInfo): An object containing metadata about the stream.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns**: `DocumentConverterResult` - Contains the converted Markdown text and the title of the feed.

### `_parse_atom_type(self, doc: Document) -> DocumentConverterResult`
- **Parameters**:
  - `doc` (Document): A parsed XML document representing an Atom feed.
- **Returns**: `DocumentConverterResult` - Contains the converted Markdown text and the title of the Atom feed.

### `_parse_rss_type(self, doc: Document) -> DocumentConverterResult`
- **Parameters**:
  - `doc` (Document): A parsed XML document representing an RSS feed.
- **Returns**: `DocumentConverterResult` - Contains the converted Markdown text and the title of the RSS feed.

### `_parse_content(self, content: str) -> str`
- **Parameters**:
  - `content` (str): The content string to be parsed.
- **Returns**: `str` - Returns the parsed content as Markdown.

### `_get_data_by_tag_name(self, element: Element, tag_name: str) -> Union[str, None]`
- **Parameters**:
  - `element` (Element): An XML element to search within.
  - `tag_name` (str): The name of the tag to retrieve data from.
- **Returns**: `Union[str, None]` - Returns the text content of the first child element with the specified tag name, or `None` if not found.

## Return Value
- The `convert` method returns a `DocumentConverterResult` object containing:
  - `markdown`: A string of the converted Markdown text.
  - `title`: The title of the feed.

## Dependencies
- The class uses the following external modules:
  - `minidom` from `xml.dom` for XML parsing.
  - `BeautifulSoup` from `bs4` for HTML content parsing.
  - `_CustomMarkdownify` for converting HTML to Markdown.

## Usage Example
```python
from io import BytesIO

# Create an instance of RssConverter
converter = RssConverter()

# Example file stream and stream info
file_stream = BytesIO(b"<rss><channel><title>Example RSS</title></channel></rss>")
stream_info = StreamInfo(mimetype="application/rss+xml", extension=".rss")

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    # Convert the file stream to Markdown
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
