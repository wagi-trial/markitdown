# packages/markitdown/src/markitdown/converters/_epub_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_epub_converter.py",
  "file_hash": "c79684e502e1195256a725afe5387f67602202d3e9115aeb1581cda9203b1873",
  "last_updated": "2025-12-23T15:49:57.153032+00:00",
  "functions": {
    "EpubConverter": {
      "hash": "7077160e323ef1cb63e5ecbb15f9c5186de51184e3b0b037829fea1c4e852282",
      "lines": "26-147",
      "last_updated": "2025-12-23T15:49:57.152959+00:00"
    }
  }
}
```

</details>



The file `packages/markitdown/src/markitdown/converters/_epub_converter.py` implements an `EpubConverter` class that converts EPUB files into Markdown format. The conversion process involves extracting metadata and content from the EPUB file, which is structured as a ZIP archive. The class inherits from `HtmlConverter` and utilizes methods from this parent class to handle the conversion of HTML content to Markdown, while preserving style information and tables where possible.

The main class defined in this file is `EpubConverter`, which includes several methods with specific responsibilities. The `__init__` method initializes the converter and creates an instance of `HtmlConverter`. The `accepts` method checks if a given file stream and its associated stream information are compatible with EPUB formats based on MIME type prefixes and file extensions. The `convert` method performs the core functionality of extracting metadata and content from the EPUB file, converting it to Markdown, and returning a `DocumentConverterResult` that contains the converted Markdown and the title of the document. Additionally, helper methods `_get_text_from_node` and `_get_all_texts_from_nodes` are defined to facilitate the extraction of text from XML nodes.

The code explicitly imports several modules, including `os`, `zipfile`, and `defusedxml.minidom`, as well as types from the `typing` module such as `BinaryIO`, `Any`, `Dict`, and `List`. It also uses `DocumentConverterResult` and `StreamInfo` from other parts of the package. The data structures manipulated in this file include dictionaries for storing metadata and manifest items, lists for spine order and converted content, and XML document objects for parsing the EPUB's content. The file defines constants for accepted MIME type prefixes and file extensions, as well as a mapping for MIME types to file extensions.

## Functions and Classes

## `EpubConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_epub_converter.py:26`](/packages/markitdown/src/markitdown/converters/_epub_converter.py#L26-L147)

# EpubConverter Documentation

## Overview
`EpubConverter` is a class that extends the `HtmlConverter` class to convert EPUB files into Markdown format. It preserves style information such as headings and tables when possible.

## Constructor
### `__init__(self)`
Initializes an instance of the `EpubConverter` class. It calls the constructor of the parent class `HtmlConverter` and initializes an instance of `HtmlConverter` as `_html_converter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type or file extension.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the EPUB file.
- `stream_info` (StreamInfo): An object containing metadata about the stream, specifically:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the file.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `bool`: Returns `True` if the file is accepted based on its MIME type or extension; otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided EPUB file stream into Markdown format.

#### Parameters
- `file_stream` (BinaryIO): The input stream of the EPUB file.
- `stream_info` (StreamInfo): An object containing metadata about the stream, specifically:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension of the file.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `DocumentConverterResult`: An object containing:
  - `markdown` (str): The converted Markdown content.
  - `title` (str): The title of the EPUB document extracted from its metadata.

### `_get_text_from_node(self, dom: Document, tag_name: str) -> str | None`
Extracts the text from the first occurrence of a specified tag in the provided DOM.

#### Parameters
- `dom` (Document): The DOM object to search within.
- `tag_name` (str): The name of the tag to extract text from.

#### Returns
- `str | None`: The text content of the first occurrence of the specified tag, or `None` if the tag is not found.

### `_get_all_texts_from_nodes(self, dom: Document, tag_name: str) -> List[str]`
Extracts the text from all occurrences of a specified tag in the provided DOM.

#### Parameters
- `dom` (Document): The DOM object to search within.
- `tag_name` (str): The name of the tag to extract text from.

#### Returns
- `List[str]`: A list of text contents from all occurrences of the specified tag.

## Dependencies
- `zipfile`: Used to read and extract files from the EPUB archive.
- `minidom`: Used to parse XML content from the EPUB's metadata files.
- `os`: Used for file path manipulations.
- `MIME_TYPE_MAPPING`: A mapping of file extensions to MIME types, used to determine the MIME type of files in the EPUB.
- `ACCEPTED_FILE_EXTENSIONS`: A list of file extensions that the converter accepts.
- `ACCEPTED_MIME_TYPE_PREFIXES`: A list of MIME type prefixes that the converter accepts.
- `DocumentConverterResult`: A class used to encapsulate the result of the conversion.

## Usage Example
```python
from io import BytesIO

# Create an instance of EpubConverter
converter = EpubConverter()

# Prepare a file stream and stream info for an EPUB file
file_stream = BytesIO(epub_file_content)  # Replace with actual EPUB file content
stream_info = StreamInfo(mimetype="application/epub+zip", extension=".epub")

# Check if the converter accepts the file
if converter.accepts(file_stream, stream_info):
    result = converter.convert(file_stream, stream_info)
    print(result.markdown)  # Output the converted Markdown content
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
