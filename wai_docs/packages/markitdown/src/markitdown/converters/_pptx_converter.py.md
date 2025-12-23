# packages/markitdown/src/markitdown/converters/_pptx_converter.py

**[← Back to Parent Directory](./README.md)**

---

<details>
<summary>📊 Documentation Metadata (click to expand)</summary>

```json
{
  "source_file": "packages/markitdown/src/markitdown/converters/_pptx_converter.py",
  "file_hash": "1b9aac4678cb4eb3b6cef6a92ae05d10af18c094d704fdc58963a4e4720c162e",
  "last_updated": "2025-12-23T15:51:58.557956+00:00",
  "functions": {
    "PptxConverter": {
      "hash": "274c6d231d9e1df2de50607bfc960dcfddb78d1e6f072d2025c57732dd638628",
      "lines": "34-265",
      "last_updated": "2025-12-23T15:51:58.557869+00:00"
    }
  }
}
```

</details>



The file `_pptx_converter.py` implements a class named `PptxConverter`, which is responsible for converting PPTX files into Markdown format. This conversion process includes handling various elements such as headings, tables, images with alt text, and notes from slides. The class extends the `DocumentConverter` base class and utilizes an instance of `HtmlConverter` for additional HTML-related functionalities.

The `PptxConverter` class includes two primary methods: `accepts` and `convert`. The `accepts` method determines if the provided file stream and stream information are compatible with the converter by checking the MIME type and file extension against predefined accepted values. The `convert` method performs the actual conversion, processing each slide in the PPTX presentation, extracting content from shapes (including images, tables, charts, and text), and generating the corresponding Markdown output. It also handles the generation of image descriptions using an external function `llm_caption` when applicable.

Concrete dependencies used in this file include the `pptx` library for handling PPTX files, the `HtmlConverter` for HTML conversion tasks, and the `llm_caption` function for generating image descriptions. The code also imports several standard libraries such as `sys`, `base64`, `os`, `io`, `re`, and `html`. The data structures manipulated include `BinaryIO` for file streams, `StreamInfo` for metadata about the streams, and `DocumentConverterResult` for encapsulating the conversion result. The code defines constants for accepted MIME types and file extensions, and it employs various types from the `pptx` library to interact with presentation elements.

## Functions and Classes

## `PptxConverter`

**Location:** [`packages/markitdown/src/markitdown/converters/_pptx_converter.py:34`](/packages/markitdown/src/markitdown/converters/_pptx_converter.py#L34-L265)

# PptxConverter Documentation

## Overview
`PptxConverter` is a class that extends `DocumentConverter` to convert PPTX files into Markdown format. It supports the conversion of headings, tables, and images with alt text.

## Constructor
### `__init__(self)`
Initializes an instance of the `PptxConverter` class. It calls the constructor of the parent class `DocumentConverter` and initializes an instance of `HtmlConverter`.

## Methods

### `accepts(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> bool`
Determines if the converter can accept the provided file stream based on its MIME type and file extension.

#### Parameters
- `file_stream` (BinaryIO): The input file stream of the PPTX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file, including:
  - `mimetype` (str): The MIME type of the file.
  - `extension` (str): The file extension.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `bool`: Returns `True` if the file extension or MIME type is accepted; otherwise, returns `False`.

### `convert(self, file_stream: BinaryIO, stream_info: StreamInfo, **kwargs: Any) -> DocumentConverterResult`
Converts the provided PPTX file stream into Markdown format.

#### Parameters
- `file_stream` (BinaryIO): The input file stream of the PPTX file to be converted.
- `stream_info` (StreamInfo): An object containing metadata about the file.
- `**kwargs` (Any): Additional options to pass to the converter, including:
  - `llm_client`: A client for generating image captions using a language model.
  - `llm_model`: The model to be used for generating image captions.
  - `llm_prompt`: The prompt for the language model.
  - `keep_data_uris`: A boolean indicating whether to keep images as data URIs.

#### Returns
- `DocumentConverterResult`: An object containing the converted Markdown content in the `markdown` attribute.

### `_is_picture(self, shape)`
Checks if the given shape is a picture or a placeholder containing an image.

#### Parameters
- `shape`: The shape object to check.

#### Returns
- `bool`: Returns `True` if the shape is a picture; otherwise, returns `False`.

### `_is_table(self, shape)`
Checks if the given shape is a table.

#### Parameters
- `shape`: The shape object to check.

#### Returns
- `bool`: Returns `True` if the shape is a table; otherwise, returns `False`.

### `_convert_table_to_markdown(self, table, **kwargs)`
Converts a table shape into Markdown format.

#### Parameters
- `table`: The table object to convert.
- `**kwargs` (Any): Additional options to pass to the converter.

#### Returns
- `str`: The Markdown representation of the table.

### `_convert_chart_to_markdown(self, chart)`
Converts a chart shape into Markdown format.

#### Parameters
- `chart`: The chart object to convert.

#### Returns
- `str`: The Markdown representation of the chart, or a message indicating an unsupported chart type.

## Dependencies
- `pptx`: The `python-pptx` library is required for handling PPTX files.
- `HtmlConverter`: An instance is created to convert HTML tables to Markdown.
- `llm_caption`: A function for generating image captions using a language model, if applicable.

## Usage Example
```python
converter = PptxConverter()
with open('presentation.pptx', 'rb') as file_stream:
    stream_info = StreamInfo(mimetype='application/vnd.openxmlformats-officedocument.presentationml.presentation', extension='pptx')
    if converter.accepts(file_stream, stream_info):
        result = converter.convert(file_stream, stream_info)
        print(result.markdown)
```

---


---
*This documentation was automatically generated by AI (Woden DocBot) and may contain errors. It is the responsibility of the user to validate the accuracy and completeness of this documentation.*
