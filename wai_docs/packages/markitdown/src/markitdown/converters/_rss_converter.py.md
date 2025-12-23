# packages/markitdown/src/markitdown/converters/_rss_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_rss_converter.py",
  "file_hash": "00bf56c318de8dd5a39de90b845ac6771a0348a7efebe39dd8c2e5736ac45c8d",
  "last_updated": "2025-12-23T15:52:14.117399+00:00",
  "functions": {
    "RssConverter": {
      "hash": "60f98ccc3689deeabe0a65f9f0f57be2df84e5081b5f6ef535815470bc445405",
      "lines": "29-193",
      "last_updated": "2025-12-23T15:52:14.117321+00:00"
    }
  }
}
```

</details>



The Python file `packages/markitdown/src/markitdown/converters/_rss_converter.py` implements the `RssConverter` class, which is responsible for converting RSS and Atom feeds into Markdown format. The class inherits from `DocumentConverter` and provides methods to accept, check, and convert XML-based feeds. It utilizes the `minidom` module from the `defusedxml` package for parsing XML documents and the `BeautifulSoup` library from `bs4` for handling HTML content within feed items.

The main functions and methods within the `RssConverter` class include:
- `__init__`: Initializes the converter and its internal state.
- `accepts`: Determines if the converter can process a given file stream based on its MIME type and file extension.
- `_check_xml`: Validates if the provided file stream contains well-formed XML.
- `_feed_type`: Identifies whether the XML document is an RSS or Atom feed.
- `convert`: Parses the XML document and delegates the parsing to either `_parse_rss_type` or `_parse_atom_type` based on the identified feed type.
- `_parse_atom_type` and `_parse_rss_type`: Extract relevant data from Atom and RSS feeds, respectively, and format it into Markdown.
- `_parse_content`: Converts HTML content to Markdown using a custom markdownify function.
- `_get_data_by_tag_name`: Retrieves the text content of the first child element with a specified tag name.

The file explicitly imports the `minidom` and `BeautifulSoup` modules, as well as several classes and functions from other modules within the same package, such as `_CustomMarkdownify`, `StreamInfo`, and `DocumentConverterResult`. It defines and manipulates data structures such as `Document`, `Element`, and `DocumentConverterResult`, which encapsulate the results of the conversion process. The converter also uses type hints for various parameters and return types, indicating the expected types for function arguments and return values.

## Functions and Classes

## `RssConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_rss_converter.py:29`](/packages/markitdown/src/markitdown/converters/_rss_converter.py#L29-L193)

# RssConverter Class Documentation

## Overview
The `RssConverter` class is a subclass of `DocumentConverter` that converts RSS and Atom feeds into Markdown format. It implements methods to determine if a given file stream is acceptable for conversion, parse the feeds, and format the output as Markdown.

## Parameters
### `__init__(self)`
- Initializes an instance of the `RssConverter` class.
- No parameters are accepted.

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **Parameters:**
  - `file_stream` (BinaryIO): A binary stream representing the file to be checked.
  - `stream_info` (StreamInfo): An object containing metadata about the stream, including:
    - `mimetype` (str): The MIME type of the file.
    - `extension` (str): The file extension.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns:** `bool` - Returns `True` if the file stream is accepted for conversion based on its MIME type or file extension; otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **Parameters:**
  - `file_stream` (BinaryIO): A binary stream representing the file to be converted.
  - `stream_info` (StreamInfo): An object containing metadata about the stream.
  - `**kwargs` (Any): Additional options to pass to the converter.
- **Returns:** `DocumentConverterResult` - Contains the converted Markdown text and the title of the feed.

## Return Value Types
- The `convert` method returns a `DocumentConverterResult` object, which includes:
  - `markdown` (str): The Markdown representation of the feed.
  - `title` (str): The title of the feed.

## Dependencies
- The class uses the following external modules:
  - `minidom`: For parsing XML documents.
  - `BeautifulSoup`: From the `bs4` library for parsing HTML content within feed items.
  - `_CustomMarkdownify`: A custom class presumably defined elsewhere for converting HTML to Markdown.

## Usage Example
```python
from io import BytesIO

# Create an instance of RssConverter
converter = RssConverter()

# Example file stream and stream info
file_stream = BytesIO(b"<rss><channel><title>Example RSS</title></channel></rss>")
stream_info = StreamInfo(mimetype="application/rss+xml", extension="rss")

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    # Convert the file stream to Markdown
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)  # Outputs the Markdown representation of the RSS feed
```

## Internal Methods
- `_check_xml(self, file_stream: BinaryIO) -> bool`: Checks if the file stream contains valid XML and determines if it is an RSS or Atom feed.
- `_feed_type(self, doc: Any) -> str | None`: Identifies the type of feed (RSS or Atom) based on the XML document structure.
- `_parse_atom_type(self, doc: Document) -> DocumentConverterResult`: Parses an Atom feed and converts it to Markdown.
- `_parse_rss_type(self, doc: Document) -> DocumentConverterResult`: Parses an RSS feed and converts it to Markdown.
- `_parse_content(self, content: str) -> str`: Parses the content of an RSS feed item, converting HTML to Markdown.
- `_get_data_by_tag_name(self, element: Element, tag_name: str) -> Union[str, None]`: Retrieves the data from the first child element with the specified tag name. Returns `None` if not found.

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
