# packages/markitdown/src/markitdown/converters/_pptx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_pptx_converter.py",
  "file_hash": "1b9aac4678cb4eb3b6cef6a92ae05d10af18c094d704fdc58963a4e4720c162e",
  "last_updated": "2026-01-04T17:22:03.328771+00:00",
  "functions": {
    "PptxConverter": {
      "hash": "274c6d231d9e1df2de50607bfc960dcfddb78d1e6f072d2025c57732dd638628",
      "lines": "34-265",
      "last_updated": "2026-01-04T17:22:03.328715+00:00"
    }
  }
}
```

</details>



The file `_pptx_converter.py` implements a class `PptxConverter` that is responsible for converting PPTX (PowerPoint) files into Markdown format. The conversion process includes handling various elements such as headings, tables, images with alt text, and slide notes. The class extends `DocumentConverter` and utilizes an instance of `HtmlConverter` for HTML-related conversions.

The `PptxConverter` class contains two main methods: `accepts` and `convert`. The `accepts` method checks if the provided file stream and its associated metadata (MIME type and file extension) are compatible with the converter, specifically looking for `.pptx` file extensions and MIME types starting with `application/vnd.openxmlformats-officedocument.presentationml`. The `convert` method performs the actual conversion by iterating through the slides of the presentation, extracting content from shapes (such as images, tables, charts, and text), and formatting it into Markdown. It also handles optional image captioning using a language model if provided.

The code has a concrete dependency on the `pptx` library, which is used to read and manipulate PowerPoint files. The class also references `HtmlConverter`, `llm_caption`, `DocumentConverter`, `DocumentConverterResult`, `StreamInfo`, and `MissingDependencyException` from its own package structure. The file manipulates data structures such as `BinaryIO` for file streams and `StreamInfo` for metadata about the files being processed. The Markdown content generated is returned as an instance of `DocumentConverterResult`.

## Function Relationships

<details>
<summary><strong>View Function Relationships</strong></summary>

This section documents nested functions and dependencies to provide clarity about the code structure and workflow.

### `PptxConverter`

**Nested Functions:**
- `__init__`
- `accepts`
- `convert`
- `get_shape_content`
- `_is_picture`
- `_is_table`
- `_convert_table_to_markdown`
- `_convert_chart_to_markdown`

<details>
<summary><strong>Calls/Dependencies</strong> (40 unique functions)</summary>

- `BytesIO`
- `DocumentConverterResult`
- `HtmlConverter`
- `MissingDependencyException`
- `PptxConverter`
- `Presentation`
- `StreamInfo`
- `__init__`
- `_convert_chart_to_markdown`
- `_convert_table_to_markdown`
- `_is_picture`
- `_is_table`
- `accepts`
- `append`
- `b64encode`
- `convert`
- `convert_string`
- `decode`
- `enumerate`
- `escape`
- `float`
- `format`
- `get`
- `get_shape_content`
- `hasattr`
- `join`
- `len`
- `llm_caption`
- `lower`
- `lstrip`
- `map`
- `sorted`
- `splitext`
- `startswith`
- `str`
- `strip`
- `sub`
- `super`
- `type`
- `with_traceback`

</details>

</details>



## Functions and Classes

## `PptxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_pptx_converter.py:34`](/packages/markitdown/src/markitdown/converters/_pptx_converter.py#L34-L265)

**Nested Functions:** `__init__`, `accepts`, `convert`, `get_shape_content`, `_is_picture`, `_is_table`, `_convert_table_to_markdown`, `_convert_chart_to_markdown`  
**Dependencies:** `BytesIO`, `DocumentConverterResult`, `HtmlConverter`, `MissingDependencyException`, `PptxConverter`, `Presentation`, `StreamInfo`, `__init__`, `_convert_chart_to_markdown`, `_convert_table_to_markdown`, `_is_picture`, `_is_table`, `accepts`, `append`, `b64encode` *(+25 more)*  


# PptxConverter Documentation

## Overview
The `PptxConverter` class is a subclass of `DocumentConverter` that converts PPTX files into Markdown format. It supports the conversion of headings, tables, and images with alt text.

## Parameters

### `__init__(self)`
- **Type**: Constructor
- **Usage**: Initializes an instance of `PptxConverter` and calls the constructor of the parent class `DocumentConverter`. It also initializes an instance of `HtmlConverter` as `_html_converter`.

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
- **Parameters**:
  - `file_stream`: `BinaryIO`
    - Represents the input stream of the PPTX file.
  - `stream_info`: `StreamInfo`
    - Contains metadata about the file, including `mimetype` and `extension`.
  - `**kwargs`: `Any`
    - Additional options to pass to the converter.
- **Return Type**: `bool`
- **Usage**: Checks if the converter can accept the provided file based on its extension or MIME type. Returns `True` if the file is acceptable, otherwise returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
- **Parameters**:
  - `file_stream`: `BinaryIO`
    - Represents the input stream of the PPTX file.
  - `stream_info`: `StreamInfo`
    - Contains metadata about the file.
  - `**kwargs`: `Any`
    - Additional options to pass to the converter, including `llm_client`, `llm_model`, `llm_prompt`, and `keep_data_uris`.
- **Return Type**: `DocumentConverterResult`
- **Usage**: Converts the PPTX file into Markdown format. It processes slides, shapes, tables, charts, and notes, and returns a `DocumentConverterResult` containing the generated Markdown content.

## Return Value
- The `convert` method returns an instance of `DocumentConverterResult` which contains:
  - `markdown`: A string representing the converted Markdown content from the PPTX file.

## Dependencies
- The class relies on the following external modules:
  - `pptx`: For handling PPTX files.
  - `HtmlConverter`: For converting HTML tables to Markdown.
  - `io`: For handling binary streams.
  - `os`: For file path manipulations.
  - `base64`: For encoding images in base64 format.
  - `re`: For regular expression operations.
- The method `convert` may call an external LLM (Language Model) service for generating image descriptions if `llm_client` and `llm_model` are provided in `kwargs`.

## Usage Example
```python
from io import BytesIO

# Assuming pptx_file_stream is a BinaryIO stream of a PPTX file
pptx_file_stream = BytesIO(open("example.pptx", "rb").read())
stream_info = StreamInfo(mimetype="application/vnd.openxmlformats-officedocument.presentationml.presentation", extension=".pptx")

converter = PptxConverter()
if converter.accepts(pptx_file_stream, stream_info):
    result = converter.convert(pptx_file_stream, stream_info)
    print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
